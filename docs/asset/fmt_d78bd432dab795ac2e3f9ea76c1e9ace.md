
```
siglongjmp(jmpbuf, 1);
```
}

当收到回复但序列号不是预期的，我们会再次调用 `recvfrom`，但不会重传请求，也不会重启正在运行的重传计时器。注意图 22.5 最右侧的示例，重传请求的最终回复将在客户端下次发送新请求时位于套接缓冲区中。这是没问题的，因为客户端会读取它，发现序列号不是预期的，丢弃回复并再次调用 `recvfrom`。

我们调用 `sigsetjmp` 和 `siglongjmp` 来避免与我们在第 20.5 节中描述的 `SIGARM` 信号产生竞态条件。

图 22.8 显示了我们 `dg_send_recv` 函数的第一部分。（注：图 22.8 的 OCR 是交错/不可读的）。

### I-5
图 22.10 中包含一个新头文件 `unprt.h`，它定义了维护客户端 RTT 信息的 `rtt_info` 结构。我们定义了这些结构以及其他变量。

### 6-10
我们想向调用者隐藏我们在每个数据包前面添加序列号和时间戳的事实。实现此点的最简单方法是使用 `write()`，将我们的头部（`hdr` 结构）紧随数据作为一个单一 UDP 数据报文写入。这比强制调用者在它的缓冲区前端分配空间进行写入要简单，也比将我们的头部和调用者的数据拷贝到单个缓冲区（我们必须分配该缓冲区）中进行单个 `sendto` 要快。但我们使用的是 UDP，并且具有 `sendmsg` 和 `recvmsg` 的 `iovec` 能力，而不是 `sendto` 和 `recvfrom`。回想第 14.5 节，系统仍然拥有我们所需的结构访问权限。为了避免使用 `#ifdef` 处理这些差异导致代码复杂，我们将两个 `msghdr` 结构声明为 `static`，强制 C 将其初始化为零，然后我们忽略结构末尾未使用的成员。

### 在第一次被调用时初始化
20-24 第一次被调用时，我们调用 `rtt_init` 函数。

填充 `msghdr` 结构

25-41 我们填充了用于输出和输入的 `msghdr` 结构。我们增加了此数据包的序列号，但在发送数据包之前不设置发送戳（它可能会被重传，每次重传都需要当前的时间戳）。

函数的后半部分以及 `sig_alarm` 信号如图 22.9 所示。（注：图 22.8 和 22.9 的 OCR 文本是交错/不可读的，但周围文本已处理。）

```c
#define RTT_RXTMAX 60

/* * 重传超时，单位为秒 */
#define RTT_MAXNREXMT 3 /* * 重传次数 */
```

```c
/* / 函数原型声明 */
void rtt_debug(struct rtt_info *);
void rtt_init(struct rtt_info);
void rtt_newpack(struct rtt_info *);
int rtt_start(struct rtt_info *);
void rtt_stop(struct rtt_info *, uint32_t);
int rtt_timeout(struct rtt_info *);
uint32_t rtt_ts(struct rtt_info *);
```

```c
extern rtt_d_flag; /* / 可以置为非零以获取额外信息 */
```

```c
#endif /* / __unpp_rtt_h */
```

# `rtt_info` 结构

4-11 该结构体包含了客户端和服务器之间数据包计时所需的变量。前四个变量来自本节开头附近的公式。

12-14 这些常量定义了最小和最大重传超时，以及我们的最大重传次数。

图 22.11 显示了宏以及我们的前两个 Rtt 函数。

# 图 22.11 RTT_RTOCALC 宏和 `rtt_minmax` 以及 `rtt_init` 函数。

`lib/rtt`

```c
#include "unprtt.h"
int rtt_d_flag = 0; /* / 调试标志；可以由调用者设置 */
/*
* 根据当前估算值计算 RTO 值：
* 平滑 RTT 加上四倍标准差
*/
#define RTT_RTOCALC(ptr) ((ptr)->rtt_srt + (4.0 * (ptr)->rtt_rttvar))
static float;
rtt_minmax(float rto)
{
if (rto < RTT_RXMIN)
rto = RTT_RXMIN;
else if (rto > RTT_RXMAX)
rto = RTT_RXMAX;
return (rto);
}
```

```c
void
rtt_init(struct rtt_info *ptr)
{
struct timeval tv;
```

```c
Gettimeofday(&tv, NULL); /* / 开始自 1970/1/1 以来的秒数 */
ptr->rtt_base = tv.tv_sec;
```

```c
ptr->rtt_rtt = ;
ptr->rtt_srtt = ;
ptr->rtt_rtvar = 0.75;
ptr->rtt_rto = rtt_minmax(RTT_RTOCALC(ptr));
/* 第一次 RTO 在 (srtt + (4 * rttvar)) 处，为 3 秒 */
}
```

3-7 `RTTROCALC` 根据 RTT 估算值和四倍平均标准差估算值计算 RTO。

8-16 `rtt_minmax` 确保 RTO 介于 `unprtt.` 头文件中定义的上限和下限之间。

17-28 `rtt_init` 在 `dg_send_recv` 发送第一个包时被调用。`gettimeofday` 返回 `timeval` 结构体中的当前时间和日期，之前我们在 `select`（第 6.3 节）中见过该结构。我们只保存自 Unix Epoch（即 UTC 1970 年 1 月 1 日 00:00:00）的秒数。测得的 RTT 设置为 0，RTT 和平均标准差估算值分别设置为 0 和 0.75，产生 3 秒的初始 RTO。

图 22.12 显示了接下来的三个 RTT 函数。

# 图 22.12 `rtt_ts`, `rtt_newpack` 和 `rtt_start` 函数。

`lib/rtt`

```c
uint32_t
rtt_ts(struct rtt_info *ptr)
{
    uint32_t ts;
    struct timeval tv;
    Gettimeofday(&tv, NULL);
    ts = ((tv.tv_sec - ptr->rtt_base) * 1000) + (tv.tv_usec / 1000);
    return (ts);
}
```

```c
void
rtt_newpack(struct rtt_info *ptr)
{
    ptr->rtt_nrexmt = 0;
}
```

```c
int
rtt_start(struct rtt_info *ptr)
{
    return (int)ptr->rto;
    /* 返回值可以作为 alarm 使用 */
}
```
