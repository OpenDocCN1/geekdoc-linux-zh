
## RECEIVE MEMORY MANAGEMENT

在每次循环中，保留 socket 内存池中的剩余字节数（第 347 行）。如果存在内存压力且全局 TCP 内存池分配的总内存小于分配下限（`sysctl_tcp_mem[0]`），我们在第 348-350 行释放内存压力。

### 9.1.12 `wait_for_tcp_memory()`

当我们需要等待发送缓冲区内存压力可用时调用此例。我们在两种情况下调用此例：

- socket 发送缓冲区满（`sk->wmem_queued >= sk->sndbuf`）。
- 内存压力且我们尚未耗尽发送配额。

看看它是如何工作的。我们检查调用此例是因为内存压力无法为 socket 分配配额。发送配额未耗尽这一事实位于第 695 行。如果是如此，我们需要在第 696 行设置一个新的超时，以便等待系统内存可用。循环直到发生以下事件之一：

- socket 遇到错误或 socket 发端关闭（第 704 行）（cs 9.17）。
- 超时（第 706 行）。在第一次迭代中我们可以退出阻塞循环。
- 我们获得了信号。我们通过在第 708 行调用 `signal_pending()` 来检查。我们从睡眠唤醒是因为是因为信号。
- 我们获得了 socket 的发送配额且不再等待更多内存（第 711 行）。如果我们是因为发送缓冲区耗尽而调用的，且现在 `tcp_memory_free()` 返回 TRUE，则意味着发送缓冲区配额现在可用。在这种情况下，我们不应该等待。在系统内存不可用但存在缓冲区配额的情况下，我们应该等待直到 VM超时发生，以便现在系统内存被释放。VM超时在第 696 行计算。

`net/ipv4/tcp.c`

```c
static int wait_for_tcp_memory(struct sock *sk, long *timeout)
{
    int err = 0;
    long vm_wait = 0;
    long current_time = *timeout;
    DECLARE_WAITQUEUE(wait, current);
    if (tcp_memory_free(sk))
        current_time = vm_wait = (HZ/2);
    add_wait_queue(sk->sleep, &wait);
    for (;;) {
        set_bit(SOCK_ASYNC_NOSOSPACE, &sk->flags);
        set_current_state(TASK_INTERRUPIBLE);
        if (sk->err || (sk->shutdown & SEND_SHUTDOWN))
            goto do_error;
        if (signal_pending(current))
            goto do_interrupted;
do_nonblock:
        clear_bit(SOCK_ASYNC_NOSOSPACE, &sk->flags);
        if (tcp_memory_free(sk) || vm_wait)
            break;
        set_bit(SOCK_NOSOSPACE, &sk->flags);
        if (sk->tp_pinfo.of_tcp.write_pending++)
            release_sock(sk);
        if (!tcp_memory_free(sk) || vm_wait)
            current_time = schedule_timeout(current_time);
            lock_sock(sk);
            sk->tp_pinfo.of_tcp.write_pending--;
            if (vm_wait) {
                vm_wait = current_time;
                current_time = *timeout;
                if (current_time != MAX_SCHEDULE_TIMEOUT &&
                    (current_time -= vm_wait) < 0)
                    vm_wait = current_time;
            }
    }
out:
    set_task(TASK_RUNNING);
    remove_wait_queue(sk->sleep, &wait);
    return err;
do_error:
    err = -EPIPE;
    goto out;
do_interrupted:
    err = -EAGAIN;
    goto out;
do_nonblock:
    err = -EINTR;
    goto out;
}
```

```
708         set_bit(SOCK_NOSOSPACE, &sk->flags);

709         if (sk->tp_pinfo.of_tcp.write_pending++)

710             release_sock(sk);

711         if (!tcp_memory_free(sk) || vm_wait)

712             current_time = schedule_timeout(current_time);

713             lock_sock(sk);

714             sk->tp_pinfo.of_tcp.write_pending--;

715             if (vm_wait) {

716                 vm_wait = current_time;

717                 current_time = *timeout;

718                 if (current_time != MAX_SCHEDULE_TIMEOUT &&

719                     (current_time -= vm_wait) < 0)

720                     vm_wait = current_time;

721             }

722     }

723 out:

724     set_task(TASK_RUNNING);

725     remove_wait_queue(sk->sleep, &wait);

726     return err;

727 do_error:

728     err = -EPIPE;

729     goto out;

730 do_interrupted:

731     err = -EAGAIN;

732     goto out;

733 do_nonblock:

734     err = -EINTR;

735     goto out;

736 }
```
