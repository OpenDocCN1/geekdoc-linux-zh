

## 24.2 实现 TCP 协议

```c
u32 end_seq;
u32 when;
u8 flags;
/* SEQ + FIN + SYN datalen*/
/* used to compute rtt*/
/* TCP header flags*/
```

```c
#define TCPCB_FLAG_FIN 0x01
#define TCPCB_FLAG_SYN 0x02
#define TCPCB_FLAG_RST 0x04
#define TCPCB_FLAG_PSH 0x08
#define TCPCB_FLAG_ACK 0x10
#define TCPCB_FLAG_URG 0x20
#define TCPCB_FLAG_ECE 0x40
#define TCPCB_FLAG_CWR 0x80
```

u8 sacked;
/* State flags for SACK/FACK*/
#define TCPCB_SACKED_ACKED 0x01 /* SKB ACK'd by a SACK block*/


```c
#define TCPCB_SACKED_RETRANS 0x02 /* SKB retransmitted*/
u16 /* Valid w/URG flags is set*/
u32 ack_seq; /* Sequence number ACK'd*/
```

上述结构表示了数据包的控制块。这种结构包含在每个数据包中。

```c
struct tcphdr {
  // include <linux/tcp.h>
```

```c
struct tcphdr {
  u16 source;
  u16 dest;
  u32 seq;
  u32 ack_seq;
#if defined(_LITTLE_ENDIAN_BITFIELD)
  u16 res:4, doff:4, fin:1, syn:1, rst:1;
  psh:1, ack:1, urg:1, ece:1, cwr:1;
#elif defined(_BIG_ENDIAN_BITFIELD)
  u16 doff:4, res:1, cwr:1, ece:1, urg:1;
  ack:1, psh:1, rst:1, syn:1, fin:1;
#else
#error "Adjust your <asm/byteorder.h> defines"
#endif
  u16 window;
  u16 check;
  u16 urg_ptr;
};
```

第 24.1.2 节引入了协议头部。`tcphdr` 结构映射了该头部，取决于内存顺序。

## 24.3 连接管理

TCP 作为一种支持多种额外机制（如按正确顺序传输数据包或紧急数据）的面向连接的协议，极其复杂。图 24-5 所示的协议机特征共有十二种状态。这种复杂性要求对活动连接的当前状态进行广泛的管理。

### 24.3.1 TCP 状态机

TCP 连接的状态存储在关联的 `sock` 结构状态字段中。对接收数据包的响应取决于其当前状态，因此必须对每个传入的数据包进行状态轮询。这分为三个阶段：连接建立阶段、数据传输阶段和连接终止阶段。

![](img/5a25b942ec3329b8799f2b5f0de564f6_499_0.png)

图 24-5
TCP 状态自动机。

第 24.4 节详细描述了数据传输阶段的协议机制。本节将讨论连接建立阶段和连接终止阶段。

如第 24.2 节所示，`tcp_rcv_state_process()` (net/ipv4/tcp_input.c) 是连接管理中最重要的函数，只要连接尚未建立。处于 `TIME_WAIT` 状态的数据包是 `tcp_v4_rcv()` 函数中唯一处理的数据包。

```
tcp_rcv_state_process()                               net/ipv4/tcp_input.c
```

`tcp_rcv_state_process()` 函数主要处理状态转换和连接的管理工作。根据连接状态的不同，接收数据包时会有不同的操作：

- CLOSED: 数据包被丢弃。
- LISTEN: 如果接收到 SYN，连接进入 SYN_RECV。
- SYN_SENT: 如果接收到 ACK，连接进入 ESTABLISHED。
- SYN_RECV: 如果接收到 ACK，连接进入 ESTABLISHED。
- ESTABLISHED: 如果接收到 FIN，连接进入 FIN_WAIT1。
- FIN_WAIT1: 如果接收到 ACK，连接进入 FIN_WAIT2。
- FIN_WAIT2: 如果接收到 FIN，连接进入 CLOSE_WAIT。
- CLOSE_WAIT: 如果接收到 ACK，连接进入 LAST_ACK。
- LAST_ACK: 如果接收到 ACK，连接进入 TIME_WAIT。
- TIME_WAIT: 如果接收到 ACK，连接关闭。

### 24.3.2 建立连接

为了建立连接，客户端发送一个带有 SYN 标志的数据包，然后从 CLOSED 状态变为 SYN_SENT 状态。这发生在 `tcp_connect()` 方法中，该方法由 `tcp_v4_connect()` 调用（见图 24-6）。`tcp_v4_connect()` 在客户端应用程序于套接接口调用 `connect()` 时触发。

```
tcp_connect()                               net/ipv4/tcp_output.c
```

当服务器应用程序在套接接口激活 `listen()` 调用时，服务器 TCP 进入 LISTEN 状态。当监听 状态下的 TCP 接收到 SYN 字符时，它会变为 SYN_RECV 状态。这发生在 `tcp_create_openreq_child()` 函数中，执行 `newsk->state = TCP_SYN_RECV;`。

```
tcp_setsockopt()                           net/ipv4/tcp_core.c
```

