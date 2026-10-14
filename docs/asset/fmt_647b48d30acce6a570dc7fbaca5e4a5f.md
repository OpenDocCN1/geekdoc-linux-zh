
# TCP 定器 (TCP TIMERS)

`tcp_twacal_row`

![](img/b3f231108facab5be0138b2cfd3f681a_388_0.png)

图 10.7. 回收模式下的 time-wait 定器槽。

`tcp_twacal_row`

![](img/b3f231108facab5be0138b2cfd3f681a_388_1.png)

图 10.8. 新 time-wait 定器相对于槽 0 被添加到槽 16。

## TIME_WAIT 定器 (TIME_WAIT TIMER)

`net/ipv4/tcp_minisocks.c`

```
432 static void SMP_TIMER_NAME(tcp_twkill(unsigned long dummy))
```

... (省略)

> cs 10.37. `tcp_twkill`.

我们之所以来到这里是因为 time-wait 桶是空的。但我们不知道当前处理的槽是否有任何待处理的条目。我们启动一个循环来处理由 `tcp_tw_death_row[tcp_tw_death_row_slot]` 指向的槽中的条目。使用 `tcp_tw_bucket` 对象的 `next_death` 字段在冲突链中访问条目。一旦从链中获取了要处理的节点，并在每次访问节点时释放锁 `tw_death_lock`，我们就可以让 `tcp_tw_schedule()` 在槽被处理期间继续执行其工作，因为任何 time-wait 表哈希表都有单一锁。接下来，我们通过调用 `time_wait_kill()` 从 time-wait 哈希表 `tcp_eshash` 以及绑定哈希桶 `tcp_bhash` 获取 time-wait 套接。在 `timewait_kill()` 中将其从不同的 time-wait 哈希表取消时，我们释放了 time-wait 桶的额外引用。当套接在 `tcp_time_wait()` 中通过 `_tcp_tw_hashdance()` 链接到这些哈希表时，time-wait 套接上放置了额外引用。我们在第 454 行再次释放 time-wait 桶的一个引用。该引用是在我们到 `tcp_tw_schedule()` 并将 time-wait 套接链接到 time-wait 表槽时添加到套接上的。计数器每次都会递增，以跟踪从槽中被杀掉的数量。这将帮助我们在后续的执行中做出停止定时器的决定。

一旦我们处理了该槽中的 time-wait 槽，我们会在第 460–461 行计算下一个要处理的槽，`tcp_tw_death_row_slot` 移动到

![](img/b3f231108facab5be0138b2cfd3f681a_390_0.png)

如图 10.9 所示，顺时针一个方向的时钟上。当槽达到最大值 7 后，它将循环。接下来，我们在第 463 行检查 time-wait 表中是否还有更多待处理的条目。我们通过从 `tcp_tw_count` 中减去 `killed` 计数器来实现这一点。如果条目存在，则重新调度 `tcp_tw_timer` 在 `TCP_TWKILL_PERIOD` 个时钟刻度后过期。在槽空的情况下，我们不调用并调度定时器来处理由 `tcp_tw_death_row_slot` 指向的下一个槽。这样保持了处理的简单性。

```
432 static void SMP_TIMER_NAME(tcp_twkill(unsigned long dummy))
433 {
434     struct tcp_tw_bucket *tw;
435     int killed = 0;
436     ...
437     spin_lock(&tw_death_lock);
438
439     if (tcp_tw_count == 0)
440         goto out;
441
442     while ((tw = tw_death_row[tcp_tw_death_row_slot]) != NULL) {
443         tw_death_row[tcp_tw_death_row_slot] = tw->next_death;
444         tw->pprev_death = NULL;
445         spin_unlock(&tw_death_lock);
446
447         time_wait_kill(tw);
448         tcp_tw_put(tw);
449
450         killed++;
451         spin_lock(&tw_death_lock);
452     }
453     tcp_tw_death_row_slot =
454         (tcp_tw_death_row_slot + 1) & (TWKILL_SLOTS - 1);
455
456     if ((tcp_tw_count == 0) {
457         mod_timer(&tw->timer, jiffies+TWKILL_PERIOD);
458         net_statistics(snp_processor_id(tw),TimeWaited += killed;
459     out:
460     spin_unlock(&tw_death_lock);
461 }
```
