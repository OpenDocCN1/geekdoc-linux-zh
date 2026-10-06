

## 9.4 在 Linux 内核中的实现

PPPoE 实现被移动到 `pppoox.c` 文件中，未来应该支持其他网络上的 PPP 实现。

### PPPoE 驱动程序的函数和数据结构

在第一步中，PPPoE 驱动程序向内核注册 PPPoE 协议。可以通过以下源码片段看到这一点：

```
pppoe_init() drivers/net/pppoox.c
{
  使用来自 drivers/net/pppoox.c 的函数注册 PPPoE 协议：
  int err = register_pppoe_proto(PX_PROTOCOL_POE, &pppoe_proto);
  if (err==0) {
    dev_add_pack(&pppoes_type);
    /*为类型为 ETH_P_PPP_SES 
    （PPPoE 会话包）的入站数据包添加处理程序，它指向 pppoe_rcv */
    dev_add_pack(&pppoed_type);
    /*为类型为
    ETH_P_PPP_DISC（PPPoE 连接建立包）的入站数据包添加处理程序，它
    指向 pppoe_disc_rcv */
    register_netdevice_notifier(&pppoe_notifier);
    /*加入网络设备通知链 */
    proc_net_create("pppoe", 0, pppoe_proc_info);
    /*在 proc 目录下生成一个条目 */
  }
  return (err);
}
```

随后，PPPoE 协议功能提供了可以供 `pppd` 用以访问 PPPoE socket 的函数。`driver/net/pppoe.c` 中的 `proto_ops proto_pppoe_ops` 结构用于将 PPPoE socket的功能绑定到通用 socket 函数（例如 `connect()`、`sendmsg()`、`recvmsg()` 和 `bind()`）。第 26 节包含了关于如何在 Linux 内核中实现 socket 的更详细的描述。

```
pppoe_create() drivers/net/pppoe.c
```

每当打开一个新的 PPPoE socket 时，就会调用此函数。该函数是导出的，并公布了结构体 `pppoe_proto` 和函数 `register_pppoe_proto()`。

```
pppoe_connect() drivers/net/pppoe.c
```

此函数在 PPPoE socket 接口处调用 `connect()`。如果调用成功，则之前在指定的以太网上发送或接收的 PPPoE 数据包就可以在应用层通过 PPPoE socket 进行访问。

### pppoe_sendmsg()

`pppoe_sendmsg()` 函数用于将 `pppd` 发的数据封装成 PPPoE 数据包，并通过以太网发送。

### pppoe_rcvmsg()

此函数用于通过 PPPoE socket 接收 PPPoE 数据包。然而，只有属于 PPPoE 协议发现阶段的数据包会被处理；所有其他数据包都会被转发到通用 PPPoE 驱动程序。关于 PPPoE 协议处于发现阶段还是会话阶段的信息保存在 `sk->state` 中。

最后，一旦 PPPoE 发现阶段完成，入站数据包将转发到通用 PPPoE 驱动程序（此处不讨论 PPPoE 中继的情况）。可以使用多种函数来接收包：

### pppoe_rcv()

此函数在 `NET_RX` tasklet 中执行。它处理错误情况并将数据包传递给函数 `pppoe_rcv_core()` 进行进一步处理。

### pppoe_rcv_core()

此函数根据存储在 `sk->state` 中的 PPPoE 协议阶段确定依赖，这意味着入站数据包要么被转发到通用 PPP 驱动程序（通过函数 `大量_input()`），要么由函数 `sock_queue_rcv_skb()` 添加到 PPPoE socket 的队列中，在那里将由上述函数 `pppoe_rcvmsg()` 处理。

### pppoe_disc_rcv()

每当收到 PPPoE 发现阶段的数据包（ethertype 为 0x8863 或 `linux/if_ether.h` 中定义的 PPP DISC）时，就会调用此函数。然而，`pppoe_disc_rcv()` 函数仅用于接收 PADT 包；所有其他数据包都会被拒绝。如果入站数据包是 PADT 包，则 PPPoE 连接将断开，socket 将释放。

### pppoe_xmit()

此函数由通用 PPP 驱动程序调用。它作为函数 `__pppoe_xmit()` 的封装。

### _pppoe_xmit()

此函数用于将通用 PPP 驱动程序的传输数据封装成 PPPoE 帧，并通过指定的以太网网卡发送。

### 9.4.2 ppp 守护进程的任务

数据连接分几个阶段建立。PPPoE 发现阶段完全由 `ppp` 守护进程处理，避免了 pppo 驱动程序的参与。内核 2.4 版本包含了特殊数据包 socket（见第 26 节），可用于直接从网卡发送或接收 RFC 2516 中指定的数据包。如果发现成功，`ppp` 守护进程会在内核中设置一个 ppp 接口。`ppp` 守护进程通过打开 PPPoE socket 并将该 socket 绑定到 PPPoE 驱动程序来实现这一点。最后，`ppp` 守护进程使用 `ioctl()` 通过参数 `PPPOCCGAN`（在 `driver/net/ppp.c` 中实现）将字段 `sk->state` 设置为 `PPPOX_BOUND`。

如前节所述，这会导致 PPPoE 驱动程序将 PPPoE 数据包转发到 `ppp` 守护进程（此处未讨论 PPPoE 中继的情况），并对于 PADT 包通过函数 `pppoe_disc_recv()` 处理；`ppp` 守护进程可以使用 PPPoE socket 上的不同 `ioctl()` 调用来更改参数。ATM 数据路径始终指向通用 PPP 驱动程序，它接收包并发送到网卡。

### 9.4.3 配置

为了在内核 2.4 及更高版本中使用 PPPoE，必须在编译时激活 `PPPOverEthernet` 选项以及 Socket 支持。如果 PPPoE 支持是以模块形式编译的，我们还需要在 `/etc/modules` 中添加该行 `alias net-pf-24 pppoe`。该行用于为协议分配 `pppoe`。一个集 PPPoE 扩展的包对于 `pppd` 可用。我们只需要在 `/etc/ppp/options` 文件中添加 `plugin pppoe` 行，即可通过 `eth0` 启动 `pppd`。[Ostr01] 提供了更多安装说明。

## 第 10 章 异步传输模式—ATM

### 10.1 引言

最初，异步传输模式（ATM）的引入是为了为语音和数据的传输提供统一的协议，并为所需的 QoS（服务质量）提供保证 [McSp95]。与预期和预测不同，ATM 网络技术并未建立在端系统中，但在核心网络中被广泛使用：ATM 为网络提供了统一的 QoS（服务质量）支持。

该网络技术是面向连接的，这意味着在传输之前必须建立连接。在永久虚拟连接（PVC）中，整个网络连接由网络管理建立：网络管理站扩展两个端点之间的转发节点的转发表，以便 ATM 单元被转发到另一个端点。另一种 ATM 连接类型是信号虚拟连接（SVC）；这种连接由通信系统建立，它们发送连接请求并响应此类请求。

在 ATM 中，数据包被称为单元。与 IP 协议数据单元不同，ATM 单元的大小固定为 53 字节：5 字节的包头，48 字节的负载。

