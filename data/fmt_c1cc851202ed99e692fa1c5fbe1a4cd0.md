
```c
3028 static_inline void tcp_ack_snd_check(struct sock *sk)
3029 {
3030     struct tcp_opt *tp = &(sk->tp_pinfo.a[f_]);
3031     if (tcp_ack_scheduled(tp)) {
3032         /* We sent a data segment already. */
3033         return;
3034     }
3035     _tcp_ack_snd_check(sk, 1);
3036 }
```

`cs 10.23`, `tcp_ack_snd_check()`.

如果 ACK 没有被调度，我们直接返回。否则，在决定是否应该发送 ACK 之前，我们需要进行更多检查。因此，我们调用了 `_tcp_ack_snd_check()` 并将第二个参数设为 1（`cs 10.23`）。该值表示我们不应该忽略接收到乱序段的可能性，在这种情况下，我们需要立即发送 ACK（详情见第 10.4.4 节）。

## 10.4.6 tcp_send_delayed_ack()

在此路径中，我们尝试调整 ACK 超时，取决于：

- 1. 当前超时时间，`tp->ack_ato`
- 2. 平滑 rtt
- 3. 是否处于 ping pong 模式（乒乓模式）

在 ping pong 模式开启的情况下，我们对最大允许超时时间保持一个下限（`HZ/5`），因为 pingable 用于交互式会话。如果没有没有得足够频繁，我们需要足够的时间来回 ACK。一旦我们平滑了超时值，我们就在第 1282 行根据 `jiffies`（机器启动的滴答数）计算超时时间。接下来，我们在第 1285 行检查延迟 ACK 计时器是否已经安装。由于：

- 1. 延迟 ACK 计时器触发，但在计时器过期时因为 socket 被其他线程使用而被阻塞（`tp->ack_blocked` 被设置）。详情见第 10.4.8 节。
- 2. 我们在已安装的超时过期之前收到了更多数据。

在后一种情况下，当距离计时器过期只剩极短时间时，我们立即发送 ACK。在前一种情况下，我们尽早处理延迟 ACK，因为由于 socket 被他人占用的原因，我们已经错过了延迟 ACK 计时器。如果上述任何条件为真，我们将在第 1290 行调用 `tcp_send_ack()` 立即发送 ACK 并返回（`cs 10.24`）。

如果两个条件都为假，我们需要为当前的当前的超时时间重置 ACK 计时器。如果上述计算出的超时时间大于当前超时时间（`tp->`

# 348

# TCP 计时器

`net/ipv4/tcp_output.c`

```c
1253 void tcp_send_delayed_ack(struct sock *sk)
1254
1255     struct tcp_opt *tp = &sk->tp->pinfo.af_tcp;
1256     int ato = tp->ack_ato;

1281
1282     /* Stay within the limit we were given * */
1283     timeout = jiffies + ato;
1284
1285     /* Use new timeout if there wasn't an older one. */
1286     if (tp->ack_pending&TCP_ACK_TIMER) {
1287         /* If delay timer was blocked or about to expire,
1288             * send ACK now.\
1289
1290         if ((tp->ack_blocked || time_before_eq(tp->ack_timeout,jiffies+(ato>>2))) {
1291             tcp_send_ack(sk);
1292             return;
1293         }
1294         if (time_before(timeout, tp->ack_timeout)) {
1295             timeout = tp->ack_timeout;
1296         }
1297         tp->ack_timeout |= TCP_ACK_SCHED|TCP_ACK_TIMER;
1298         tp->ack_timeout = timeout;
1299     }
1300     if (!mod_timeout(&delay_timer,timeout))
1301         sock_hold(sk)
```

`cs 10.24`. `tcp_send_delayed_ack()`.

`ack.timeout()`, 我们在第 1294-1295 行获取当前的延迟 ACK 超时。这样做是因为我们进入此处时计时器已经安装，因此将按照计划执行。我们在第 1297 行设置与 ACK 相关的 `TCP_ACK_SCHED` 和 `TCP_ACK_TIMER` 标志。我们无条件地设置这些标志，因为我们不知道进入此例函数时计时器是否已经安装。我们在第 1300 行通过调用 `sock_hold()` 持有 socket 引用，以防 `mod_timeout()` 返回 0。如果 `mod_timeout()` 返回 0，说明计时器尚未安装或已经过期。如果已经安装，则 socket 的引用由计时器持有。我们在延迟 ACK 计时器例函数中释放 socket 的引用。

## 10.4.7 tcp_delack_timer()

这是延迟 ACK 的回调函数。这是延迟 ACK 的回调函数。这是延迟 ACK 的回调函数。这是延迟 ACK 的回调函数。

## 10.4.8 reset_xmit_timer(timer)

这是一个用于重置 RTO、窗口探测和延迟 ACK 计时器的通用例程。

# 350

# TCP 定器 (TIMERS)
