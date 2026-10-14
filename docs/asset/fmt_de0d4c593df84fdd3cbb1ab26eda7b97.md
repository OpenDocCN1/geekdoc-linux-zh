
`include/net/tcp.h`

`317` `#define TCP_TIMEWAIT_LEN (60*HZ)`

`cs 10.33`。非循环模式（noncycle mode）下槽位的等待定时器频率。

以相等的时间间隔处理。如果我们获得第一个槽，意味着我们应该被放置在即将到期的当前调度槽的下一个槽。首先，我们计算循环模式的槽；如果该值超过了全局时间限制，我们就切换到非循环模式。循环定时器每隔 `$2^{TCP\_RECYCLE\_TICK}$` 个 tick 到期一次，并在循环模式下，每隔 `$2^{^{\_RECYCLE\_TICK}$` 个时钟滴答将最终值除以 `TCP_JICK`。因此，我们在第 529 行（`cs 10.34`）计算该模式的槽，并将该值向上取整为 `$2^{TCP\_RECYCLE\_TICK}$` 的倍数。我们在第 531 行持有全局等待锁 `tw_death_lock`，因为我们将管理全局时间链。我们首先检查 time-wait 桶是否已经调度。如果 time-wait 桶的 `prev_` 字段为 `NULL`，则我们已经链接到全局列表中。在这种情况下，我们从列表中移除该桶（第 534-539 行）。我们减少 `tcp_tw_count`，因为我们将对其进行重新调度，这会将计数器加 1。如果桶尚未调度，我们对该桶持有额外的额外的引用，我们应该在定时器到期之前销毁该 time-wait 桶。我们检查根据 recycle ticks 计算的槽是否超过了循环 time-wait 表持有的最大槽数 `TCP_TW_RECYCLE_SLOTS`。让我们看看循环和非循环 time-wait 定器是如何处理的。

### 10.7.4 非循环模式（除非另有说明，请见 cs 10.34）

当我们在循环模式下的超时值过高或处于非循环模式时可能会发生这种情况。在这种情况下，我们采用慢定时器。在慢定时器模式下，我们以固定的间隔——即 10.5 所示的 `TCP_TWKILL_PERIOD`——在连续的槽中到期。`TCP_TWKILL_PERIOD` 通过将时间长度（60秒）除以总槽数 `TCP_TWKILL_SLOTS` 计算。如果我们的这个 expire-wait 桶的超时值超过了 `TCP_TIMEWAIT_LEN`，则 time-wait 桶相对于第 546 行的当前调度槽 `tw_death_last_row` 占据最后一个槽。否则，我们在第 548 行将槽计算为向上取整的 `TCP_TWKILL_PERIOD` 除以 `TCP_TWKILL_PERIOD`。在任何情况下，槽都不应超过 `TCP_TWKILL_SLOTS`。接下来，我们在第 553 行相对于当前调度槽 `slot_tw_death_last_row` 计算槽。我们在第 554 行的 `tcp_tw_death_[]` 表中保留与上述计算出的槽对应的条目，`tcp_tw_timer` 是非循环模式操作的定时器。定时器在第一个 time-wait 桶到达时触发。一旦定时器被触发，它将以 `TCP_TWKILL_PERIOD` 个时钟滴答的相等间隔（`cs 10.35`）为每个槽继续触发，无论该槽是否有被调度的条目。它仅在任何槽中都没有条目且 `tcp_tw_count` 降为零时才会停止。更多细节请见第 10.7.6 节，该节讨论了 `tcp_tw_timer_timer`。

![](img/b3f231108facab5be0138b2cfd3f681a_383_0.png)

`net/ipv4/tcp_timer.c`

```c
void tcp_tw_schedule(struct tcp_tw_bucket *tw, int timeo) {
    struct tcp_tw_bucket **tpp;
    int slot;
    slot = (timeo + (1 << TCP_RECYCLE_TICK) - 1)) > TCP_RECYCLE_TICK;
    spin_lock(&tw->death_lock);
    /* 如果已调度，则取消链接 */
    if (tw->prev_death) {
        if (tw->next_death) {
            tw->next_death->prev_death = tw->prev_death;
            tw->prev_death = NULL;
            tw->tw_count--;
        }
    } else {
        atomic_inc(&tw->ref_count);
    }
    if (slot == TCP_RECYCLE_SLOTS) {
        /* 调度定时器 */
        if (timeo < TCP_TIMEWAIT_LEN) {
            slot = TCP_TWKILL_SLOTS - 1;
        } else {
            slot = (timeo + TCP_TWKILL_PERIOD - 1) / TCP_TWKILL_PERIOD;
            if (slot < TCP_TWKILL_SLOTS) {
                slot = TCP_TWKILL_SLOTS - 1;
            }
        }
        tw->tw_death = jiffies + timeo;
        slot = &tw->tw_death_row[slot] + (TCP_TW_SLOTS - 1);
        tpp = &tw->tw_death_row[slot];
    } else {
        if (tcp_tw_cal_hand < 0) {
            tcp_tw_cal_hand = jiffies;
            tcp_tw_timer.expires = jiffies;
        } else {
            tcp_tw_timer.expires = jiffies + (slot < TCP_RECYCLE_TICK);
            add_timer(&tcp_tw_timer);
        }
        if ((long)tcp_tw_timer.expires - jiffies) < (slot << TCP_RECYCLE_TICK)) {
            mod_timer(&tcp_tw_timer, jiffies + (slot < TCP_RECYCLE_TICK));
            slot = (tcp_tw_cal_hand + slot) & (TCP_RECYCLE_SLOTS - 1);
        }
        tpp = &tcp_tw_cal_row[slot];
    }
    if (tw->next_death != *tpp) {
        (*tpp)->prev_death = tw->next_death;
        tw->pp = tw;
        tw->prev_death = tpp;
    }
    if (atomic_dec_and_test(&tw->tw_count) == 0) {
        mod_timer(&tw->tw_timer, jiffies + TCP_TWKILL_PERIOD);
    }
    spin_unlock(&tw->death_lock);
}
```

## TIME-WAIT 定器

### 365

`tcp_tw_death_row`

![](img/b3f231108facab5be0138b2cfd3f681a_385_0.png)

图 10.5. 非循环模式的 time-wait 定器调度。

```c
include/net/tcp.h
352 #define TCP_TWKILL_SLOTS 8
353 #define TCP_TWKILL_PERIOD (TCP_TIMEWAIT_LEN/TCP_TWKILL_SLOTS)
```
