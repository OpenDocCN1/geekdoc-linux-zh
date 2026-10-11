The signal queue holds an indefinite number of queued signals. The semantics of *classic* signals are that follow-up signals are ignored—this is emulated in the signal code kernel/signal.c. *Generic* (or RT) signals can be queued arbitrarily—there are, however, reasonable limits to the length of the signal queue.

The signal is queued, and `current->signal` updated. Now comes the tricky part: the kernel returns to user-space. Return to user-space happens from `do_page_fault => page_fault` (entry.S), then the low-level exit code in entry.S is executed in the order detailed here:

```
```text
page_fault => (called do_page_fault) => error_code =>
ret_from_exception => (checks if return to userspace) =>
ret_with_reschedule => (sees that current->signal is nonzero) =>
calls do_signal().
```
```

Next, `do_signal()` unqueues the signal to be executed. In this case it’s SIGBUS. It then calls `handle_signal()` with the “unqueued” signal (which can potentially hold extra event information in case of real time signals or messages).

It then calls `setup_frame`, where all user-space registers are saved and the kernel stack frame return address is modified to point to the handler of the installed signal handler. A small sequence of jump code is put on the user stack (obviously, first the code makes sure the user stack is valid), which will return us to kernel space once the signal handler has finished:

```
```c
{
  err |= __put_user(frame->retcode, &frame->pretcode);
  /* This is popl %eax ; movl $,%eax ; int $0x80 */
  err |= __put_user(0xb858, (short *)(frame->retcode+0));
  err |= __put_user(__NR_sigreturn, (int *)(frame->retcode+2));
  err |= __put_user(0x80cd, (short *)(frame->retcode+6));
}
```
```

![](bbox=[0.14, 0.73, 0.21, 0.8])

> *This area is one of the least understood pieces of the Linux kernel. And for a good reason—it’s really tough code to read and follow.*

The `popl %eax ; movl $,%eax ; int $0x80` x86 assembly sequence calls `sys_sigret()`, which will, later on, restore the kernel stack frame return address to a point to the original (faulting) user-address.

What is all this magic good for? Well, first, the kernel has to guarantee that signal handlers get called properly and that the original state is restored. The kernel also has to deal with binary compatibility issues.