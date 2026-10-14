
# /etc/crun

`dumpfile = /dev/ksys, memelist outfile = stdout`

*callout*

```
Function ARGUMENT TIME ID
politime 000000008df260 000000006a491 7fffffe61f0
realtimepire 000000009d8e90 000000006adf39 7ffffff79890
setrun 00000000a1b2c0 0000000069d97 7ffffff25a31
schedpaging 00000000000000 0000000069d0f 7ffffff7c18
mi_timer_fire 0000000036280 0000000069d2e 7ffffff7c528
signal2proc 00000000974ac0 0000000069be19 7ffffff7c648
ts_update 00000000000000 000000008b4c5 7ffffff7b58
seg_paginate 00000000000000 0000000069139 7ffffff7cb88
kmem_update 00000000000000 0000000069139 7fffffffb3069
```

请注意，`crash(1)` 中 `callout` 函数的示例输出并不是完整的列表。同样请注意，输出是一个 64 位的 Solaris 7 系统，这就是为什么 `ARGUMENT`、`TIME` 和 `ID` 列是 8 字节（64 位）数据类型。在 32 位内核上，它们是 32 位数据类型。

你将在调用输出表上持续使用的一些内核函数包括：

- `politime` — 一种实时调用输出。由 `poll(2)` 系统调用设置并基于 `poll` 间隔。`politime()` 唤醒等待 `poll` 事件的线程。
- `realexpire` — 一种实时调用输出。当设置定时器时用于实时间隔。调用输出滴答源自定时器值。`realtimeexpire()` 生成 `SIGALRM`。
- `setrun` — 一种实时调用输出。由 `sleep/wakeup` 代码（变量）在调用输出队列上调用，用于定时器过期时强制唤醒线程；例如，`aiowait(2)` 可以为 I/O 完成指定最大超时时间。带有超时变量的 `aiowait(2)` 将 `setrun()` 事件放置在调用输出队列上，以便在 I/O 完成之前强制唤醒线程。
- `scheduled` — 一种普通调用输出。虚拟内存中调用输出子系统的一部分，用于管理页速率。
- `mi_timer_fire` — 一种普通调用输出。STREAMS-TCP/IP 支持的一部分。`mi_timer_fire()` 通过 STREAMS 队列生成常规消息处理。
- `sigalarm2` — 一种普通调用输出。`alarm(2)` 闹钟。
- `ts_update` — 一种普通调用输出。
- `seg_paginate` — 一种普通调用输出。
- `kmem_update` — 一种普通调用输出。

通过对比 `t_bolt` 和 `lbolt` 对线程进行 tick（时钟滴）处理是必要的。

```
if (lbolt - t_lbolt) = 0

    no need to do tick processing

else

    set t_pctcpu

    t_bolt = lbolt

    call clock_tick(current thread)
```
