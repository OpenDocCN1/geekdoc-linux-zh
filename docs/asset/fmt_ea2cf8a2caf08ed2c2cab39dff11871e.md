
我们想要隐藏在每个数据包前添加序列号和时间戳的事实。实现此点的最简单方法是使用 `writev`，我们的头部（`hdr` 结构）紧随调用者的数据，作为一个单一的 UDP 数据报。回想 `writev` 在 `datagram` 模式下的输出是一个单一数据报。我们的用法比强制调用者为单个 `sendto` 在缓冲区中分配空间（那由我们来分配）要简单得多。但由于我们使用 UDP 且必须指定目标地址，我们必须使用 `sendmsg` 和 `recvmsg` 的 `iovec` 功能，而不是 `sendto` 和 `recvfrom`。回顾 13.5 节，某些系统具有带有辅助数据的新 `msghdr` 结构，而旧系统仍使用旧结构，以避免使用 `#ifdef` 增加代码复杂度。为了处理这些初始化，我们将 `msghdr` 结构声明为 `static`，强制 C 将其初始化为全零，然后只需忽略结构末尾未使用的成员。

# 第一次调用时初始化

当我们第一次被调用时，会调用 `rtt_init` 函数。

# 填充 msghdr 结构

我们填充用于输出和输入的两个 `msghdr` 结构。我们增加此数据包的发送序列号，但在设置数据包之前不设置发送时间戳（它可能会重传，每次重传都需要当前时间戳）。

函数的后半部分以及 `sig_alarm` 信号处理程序如图 20.9（第 548 页）所示。

# 20.5 节 为 UDP 应用添加可靠性

```
#include <unprtt.h>
#include <setjmp.h>

#define RTT_DEBUG
static struct rtt_info rttinfo;
static int rtt_init = 0;
static struct msghdr msgsend, msgrcv; /* 假设初始化为 0 */
static struct hdr {
    uint32_t seq;      /* 序列号 */
    uint32_t ts;       /* 发送时间戳 */
} send_ts, recvhdr;

static void sigalrm(int signo);
static jmp_buf jmpbuf;

ssize_t
dg_recvv(int fd, const void *outbuf, size_t outbytes,
         void *inbuf, size_t inbytes,
         const SA *destaddr, socklen_t destlen);

ssize_t
dg_sendv;
struct iovec iovend(2), iovrecv(2);

if (rtt_init == 0) {
    rtt_init(&rttinfo);    /* 第一次被调用 */
    rtt_init = 1;
    rtt_d_flag = 1;
}

sendsend.msg_name = destaddr;
sendsend.msg_namelen = destlen;
sendsend.msg_iov = iovend;
sendsend.msg_iov_len = 2;
iovend(0).iov_base = &sendhdr;
iovend(0).iov_len = sizeof(struct hdr);
iovend(1).iov_base = outbuf;
iovend(1).iov_len = outbytes;

msgrcv.msg_name = NULL;
msgrcv.msg_namelen = 0;
msgrcv.msg_iov = iovrecv;
msgrcv.msg_iov_len = 2;
iovrecv(0).iov_base = &recvhdr;
iovrecv(0).iov_len = sizeof(struct hdr);
iovrecv(1).iov_base = inbuf;
iovrecv(1).iov_len = inbytes;
```

图 20.8 `dg_send_recvv` 函数：前半部分。

# 高级 UDP 套接字

```
Signal(SIGALRM, sig_alarm);                               /* rtt/dg_send_recv.c */
rtt_newpack(rttinfo);                                    /* 初始化此数据包 */
again:
sendhdr.ts = rtt_ts(&rttinfo);
sendmsg(fd, &msgsend, 0);
alarm(rtt_start(&rttinfo));                             /* 计算超时并启动计时器 */
if (sigsetjmp(jmpbuf, 1) == 0) {
    if (rtt_timeout(&rttinfo) < 0) {
        perror("dg_send_recv: no response, giving up");
        rtt_init = 0;                               /* 以防再次被调用时重新初始化 */
        return -ETIMOUT;
    }
    return (-1);
}
goto again;
do {
    n = recvmsg(fd, &msgrcv, 0);
} while (n < sizeof(struct hdr) || recvhdr.ts != sendhdr.ts);

alarm(0);                               /* 停止 RTT 计时器 */
/* 计算并存储新的 RTT 值 */
rtt_stop(&rttinfo, rtt_ts(&rttinfo) - recvhdr.ts);
return (n - sizeof(struct hdr));                     /* 返回接收数据包的大小 */
static void
sig_alarm(int signo) {
    siglongjmp(jmpbuf, 1);
}
```

图 20.9 `dg_send_recv` 函数。

# 信号处理程序

为 `SIGALRM` 信号处理程序，`rtt_newpack` 将重传计数设置为 0。

# 发送数据报

通过 `rtt_ts` 获取当前时间戳并存储在数据包结构中。单一 UDP 数据报通过 `sendmsg` 发送，`rtt_start` 返回超时的秒数，并通过 `alarm` 调度 `SIGALRM`。

# 跳转缓冲区

我们使用 `sigsetjmp` 为信号处理程序建立跳转缓冲区。通过 `recvmsg` 等待下一个数据报（讨论见 18.9 节中关于 `SIGALRM` 的 `sigsetjmp` 和 `siglongjmp`）。如果计时器过期，`sigsetjmp` 返回 1。

# 处理超时

发生超时时，`rtt_timeout` 计算 RTO（指数退避），如果应该放弃则返回 -1，应该重传则返回 0。如果放弃，我们将 `errno` 设置为 `TIMEDOUT` 并返回给调用者。

# 调用 recvmsg，比较序列号

通过 `recvmsg` 等待数据报到达。当它返回时，数据包长度至少等于我们的 `hdr` 结构，且序列号必须等于发送的。

# 关闭计时器并更新 RTT 估计值

当收到预期回复时，关闭挂起的计时器，`rtt_stop` 更新 RTT 估计值。`rtt_ts` 返回当前时间戳，减去接收数据包的时间戳得到 RTT。

# SIGALRM 处理程序

我们现在查看由 `dg_send_recv` 调各种 RTT 函数。图 20.10 显示了 `unprtt.h`。
