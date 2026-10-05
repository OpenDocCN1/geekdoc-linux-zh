
网络层（如路由器）将使用 IP 地址信息将数据包路由到主机。随后，主机必须处理数据包，并最终将携带的数据路由到适当的软件进程。正如帆船需要同时知道目的国家和卸货港一样，端口被用于识别数据的目的地。端口是传输层的信息。在 TCP/IP 协议族中，端口号是 16 位的数值。

许多主机提供了一系列服务器软件进程，例如 Web 服务器。这些服务器在所谓的“已知端口”上监听潜在的数据包或连接。服务名称与端口号之间的映射存储在 `/etc/services` 文件中。如图 7.1 所示。每行由一个服务名称（如 ftp）、一个端口号和一个协议组成。

图 7.1 `/etc/services` 文件的示例。

| service | port | description |
| :--- | :--- | :--- |
| tcpmux | 1/tcp | # TCP端口服务复用器 |
| echo | 7/tcp | |
| echo | 7/udp | |
| discard | 9/tcp | sink null |
| discard | 9/udp | sink null |
| systat | 11/tcp | users |
| daytime | 13/tcp | |
| daytime | 13/udp | |
| netstat | 15/tcp | |
| qqtd | 17/tcp | # 信息发送协议 |
| msp | 18/tcp | # 信息发送协议 |
| msp | 18/udp | |
| charger | 19/tcp | tttyst source |
| charger | 19/udp | tttyst source |
| ftp-data | 20/tcp | |
| ftp | 21/tcp | |
| fspd | 21/udp | fspd |
| sbb | 22/tcp | # SSH远程登录协议 |
| sbb | 22/udp | # SSH远程登录协议 |
| telnet | 23/tcp | |

### 7.3.3 UDP 数据报头部结构分析

UDP 数据报包含一个 8 字节的头部，并封装在 IP 数据报中。当携带 UDP 数据时，IP 协议字段被设置为 17。UDP 头部如图 7.1a 所示。

图 7.1a UDP 头部。

| 0 | 7 8 | 15 16 | 23 24 | 31 |
|---|---|---|---|---|
| 源 | 目的 | | | |
| 端口 | 端口 | | | |
| 长度 | 校验和 | | | |
| | | | | |
| 数据字节 ... | | | | |

图 7.2 连接结构与函数 (i)。

```
922 struct proto_ops inet_stream_ops = {
923     family: PF_INET,
924 
925     release: inet_release,
926     bind: inet_bind,
927     connect: inet_stream_connect,
928     socketpair: sock_no_socketpair,
929     accept: inet_accept,
930     getname: inet_getname,
931     poll: tcp_poll,
932     ioctl: inet_ioctl,
933     listen: inet_listen,
934     shutdown: inet_shutdown,
935     setsockopt: inet_setsockopt,
936     getsockopt: inet_getsockopt,
937     sendmsg: inet_sendmsg,
938     recvmsg: inet_recvmsg,
939     mmap: sock_no_mmap,
940     sendpage: tcp_sendpage
941 };
942 struct proto_ops inet_dgram_ops = {
```

UDP 在 IP 数据报层之上提供的传输层功能是多路复用和用于初步错误检查的校验和。

虽然 UDP 具有传输不可靠的缺点，但它还无法适应网络状况。如果网络负载过高导致无法进行通信，UDP 连接将会很差，并且对网络上的其他流量产生不利影响。本章后面描述的 TCP 传输提供了这些额外功能。

### 7.3.4 传输层连接

本节描述了将传输层连接到下方网络层的函数。

Socket 到传输层

Socket 的生命周期包括创建、操作和关闭。本节描述了用户空间调用如何通过内核传递。Socket 状态维护在多个结构中：

- struct socket，这是一个与协议无关的结构。
- struct sock，包含传输层信息。

主 socket 代码位于 net/socket.c。该文件中的函数被编码为调用与创建的 socket 类型特定的函数。当创建 socket（`socket` 调用）时，会调用 `sys_socket`，它分配 socket 并将 socket 映射到文件描述符。该描述符被传回用户进程以供后续操作。

`net_families` 数组允许我们看到此结构和其他结构是如何初始化的。`net_families` 数组在内核启动时在 ipv4/inet.c 中初始化。该函数是启动代码的一部分。其中一个函数是将 socket 族注册到哈希表中。

总结上述，协议族 (PF_INET) 已注册。创建的每个 socket 拥有一套 socket 操作。每个 socket 创建的拥有一套 socket 协议（TCP 或 UDP）。这套协议函数通过 socket 描述符被找到。在 socket 描述符处，通过将 socket 映射到 socket 结构。在整个代码中，会调用这些函数。这 7.3 连接结构与函数 (ii)。

```
struct proto udp_prot = {
name:           "UDP",
close:          udp_close,
connect:        udp_connect,
disconnect:      udp_disconnect,
ioctl:          udp_ioctl,
setsockopt:     ip_setsockopt,
getsockopt:     ip_getsockopt,
sendmsg:        udp_sendmsg,
recvmsg:        udp_recvmsg,
backlog_rcv:    udp_queue_rcv,
hash:           udp_v4_hash,
unhash:         udp_v4_unhash,
get_port:       udp_v4_get_port,
};
```

```
struct proto tcp_prot = {
name:           "TCP",
close:          tcp_close,
connect:        tcp_v4_connect,
disconnect:      tcp_disconnect,
accept:         tcp_accept,
ioctl:          tcp_ioctl,
init:           tcp_v4_init_sock,
destroy:         tcp_v4_destroy_sock,
shutdown:       tcp_shutdown,
setsockopt:     tcp_setsockopt,
getsockopt:     tcp_getsockopt,
sendmsg:        tcp_sendmsg,
recvmsg:        tcp_recvmsg,
backlog_rcv:    tcp_v4_do_rcv,
hash:           tcp_v4_hash,
unhash:         tcp_v4_unhash,
get_port:       tcp_v4_get_port,
};
```

```
struct tcp_func_ipv4_specific = {
  ip_u32
  tcp_v4_send_check,
  tcp_v4_rebuild_header,
  tcp_v4_conn_request,
  tcp_v4_syn_recv,
  tcp_v4_hash_connecting,
  tcp_v4_remember_stamp,
  sizeof(struct iphdr),
  
  ip_setsockopt,
  ip_getsockopt,
  v4_addr2sock,
  sizeof(struct sockaddr_in)
};
```

# IP 层连接

`af_specific` 结构包含了与网络层之间传递数据的函数。当 socket 初始化时，它被设置为 `ipv4_specific`。图 7.3。
