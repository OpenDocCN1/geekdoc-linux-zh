

# 156 第 8 章 点对点协议 (PPP)

## 8.3.3 初始化

当 PPP 模块 `ppp_generic_o` 加载时，`ppp_init` 首先注册一个主设备号为 108 的字符设备，这通常会将 `/dev/ppp` 嵌入到系统中。接下来，该模块使用 `ppp_async_init()` 为异步 PPP 驱动（`ppp_async.`）注册一个名为 'ppp' 的新 TTY 线路规范（见第 7.2.1 节）。该 TTY 线路规范是设备与底层设备以及 `ppp_async_c` 模块之间的中间层，便于对所有入站数据包进行访问。一旦 `/dev/tty` 设备和 PPP TTY 行规范注册完成，第一阶段初始化即告完成。

第二阶段通过调用 `ppp` 启动。在简短测试其版本号是否匹配内核驱动版本后，它打开设备 `/dev/ppp`。然后它会打开一个文件描述符，这是与通用 PPP 驱动通信所必需：但最初，PPP 设备的引用指针 `USAGE_COUNT` 会递增。

接着，用户需要建立物理连接（例如，`chat` 程序可以拨打拨号服务器的号码）。如果此操作成功，则 PPP 使用系统的 `ioctl(tty_fd, TIOCSREED, N_PPP)` 将 TTY 线路规范更改为 `N_PPP`。然后它使用 `ioctl(ppp_fd, PPPOCNEWUNIT)` 请求通用 PPP 驱动创建一个网络设备，然后使用 `ioctl(fd, PPPOCGCATATCH)` 将新网络设备绑定到底层 TTY 设备。

这些步骤完成了实际 PPP 连接的建立：现在 PPP 协议（如 LCP）可以开始验证用户身份并配置高层（见第 8.4 节）。

## 8.3.4 发送 IP 数据包

通用 PPP 驱动通过两条路由接收待传输的数据包：网络层通过匹配的网络设备 (`pppX`) 发送负载包，而 PPP 守护进程通过字符设备 `/dev/ppp` 控制数据包。

网络层发送到函数 `ppp_start_xmit()` 的每个数据包都包含在 `sk_buff` 缓冲区中（见第 4.1 节）。该函数在数据包开头添加一个 2 字节的 PPP 头（见图 8-2），并将数据包存储在传输队列 `ppp_xq` 中。同样的操作也发生在接收来自 ppp 数据包的函数 `ppp_write()` 中。

最后，在每种情况下都会调用函数 `ppp_xmit()`。它从传输队列中获取数据包并将其转发到函数 `ppp_send_frame()` 进行进一步处理。根据设置，数据包头可能会通过 Van-Jacobson 方法压缩，并可能使用 deflate 和 BSD-Compress 方法进行负载压缩。在转发到异步 PPP 驱动的函数 `ppp_send_async()`（或同步 PPP 驱动的相应函数）后，通用 PPP 驱动即完成了它的处理。

## 8.3.5 检测帧边界

帧同步（成帧）在异步 PPP 驱动（`drivers/net/ppp_async.c`）中作为 TTY 线路规范实现，并遵循 [Simp94b] 中指定的标准。基本上，这是一个易于修改且精简的 HDLC（高级数据链路控制；见 [ISO93]）。

第 7.1.1 节简要解释了为什么成帧是必要的：异步 TTY 设备（例如调制解调器连接）只能处理无结构的字节流和完整数据包，因此需要标记数据包的开始和结束。在 PPP 中，这是通过使用二进制表示为 01111110 的特殊字符 `PPP_FLAG` 来的。

当然，剩余的数据流不应意外地包含此类特殊字符。为了防止特殊字符的出现，我们使用字符转义（character stuffing）。这意味着所有由如 `PPP_FLAG` 等控制字符包围的负载字节都会以字符 `PPP_ESCAPE`（或 01111101）作为前缀。还有更多的控制字符；我们可以查看 `include/linux/ppp.defs` 获取完整列表。

成帧和字符转义在函数 `ppp_async_encode()` 中被正确实现。`async_struct` 结构体中 `xaccm` 字段的位向量用于检测应该有 `PPP_ESCAPE` 前缀的字符。该向量中 32 × 8 位中的每一位都对应 256 个可用位字符之一。以下来自 `drivers/net/ppp_async.c` 的程序转储显示了我们如何将负载转换为数据流：

```
#define PUT_BYTE(ap, buf, c, iscl) do {
    if ((iscl && c < 0x20) || (ap->xaccm[c] & (1 << (c & 0xf))))
        *buf = PPP_ESCAPE;
    *buf = c ^ 0x20;
} while (c);
```

在此代码中，`iscl` 是为特殊 LPC 命令设置的标志，即使位向量 `->xaccm` 尚未初始化或初始化错误，这些命令也必须工作。

为了防止传输错误，在 PPP 数据包的结束字符（`PPP_FLAG`）之前，会附加一个 2 字节的校验和（帧校验序列–FCS）。如果数据包已完全转换为数据流，则底层 TTY 设备的驱动（由 `tty->driver.write()` 调用）将承担剩余的工作。

## 8.3.6 接收 PPP 数据包

通过异步 PPP 驱动接收 PPP 数据包的工作与发送数据包非常，只是方向相反：入站数据首先发送到 TTY 驱动的 `ppp_async` 函数，然后由异步 PPP 驱动的 `ppp_async_input()` 处理。如果数据包已完全转换为数据流，则底层 TTY 设备的驱动由 `tty->driver.write()` 调用，假设了剩余的工作。在校验（见 8.3.5 节）正确后，最后，恢复的数据包被传递给通用 PPP 驱动的 `ppp_input()` 函数。基于 `sk_buff` 传输队列中的数据包标识（见图 8-2），通用 PPP 驱动已完成了它的处理。

## 8.4 实现 PPP 守护进程

如反复提到的，大部分实现工作发生在 PPP 守护进程 `ppad` 中。为了保持可扩展性，尽力使实现高度模块化，并为子规范定义了清晰的接口。

## 8.4.1 管理子规范

```
struct protocol pppd/pppd.h
```

子规范的核心是结构体，它定义在 `pppd.h` 文件中。它主要包含了 pppd 接收到数据包时调用的回调函数：

```
struct protocol {
    /* PPP 协议号 */
    /* 初始化程序 */
    void (*init)_P(int unit);
    /* 处理接收的数据包 */
    void (*input)_P(int unit, u_char *pkt, int len);
    /* 处理接收到的协议拒绝 */
    void (*protrej)_P(int unit);
    /* 底层已启动 */
    void (*lookup)_P(int unit);
    /* 底层掉线 */
    void (*lowdown)_P(int unit);
    /* 打开协议 */
    void (*open)_P(int unit);
    /* 关闭协议 */
    void (*close)_P(int unit, u_char *reason);
    /* 以可读形式打印数据包 */
    int (*printpkt)_P(u_char *pkt, int len,
        void (*printer)_P(void *, char *, ...),
        void *arg);
    /* 处理接收到的数据包 */
    void (*datainup)_P(int unit, u_char *pkt, int len);
};
```

`bool enabled_flag;` // 如果协议被禁用则为 0
`char *name;` // 协议的文本名称
`char *data_name;` // 对应数据协议的文本名称
`_t *options;` // 命令行选项列表
`/* 检查请求的选项，分配默认值 */`
`void (*check_options)_P(void);`
`/* 为需求拨号配置接口 */`
`int (*demand_conf)_P(int uint);`
`/* 根据此数据包决定是否建立链路 */
`int (*active_pkt)_P(u_char *pkt, int len);`

