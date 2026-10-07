# Profs — The Process File System

set during initialization and is reset on every pass through new_state(), marking the start time for a new state transition. The ms_acct[] array location that corresponds to the previous microstate is updated to reflect elapsed time in that state. Since the time values are summed, the current value in the ms_acct[] is added to the new elapsed time just calculated. Thus, the ms_acct[] array contains the elapsed time in the various microstates, updated dynamically when state changes occur. Lastly, the kernel thread's t_mstate is set to reflect the new microstate.

The calls into new_mstate() for the tracked microstates come from several areas in the kernel. Table 8-6 lists the kernel functions that call new_mstate() for specific state changes.

# Table 8-6 Microstate Change Calls into new_mstate ()

| New state | Called from |
| --- | --- |
| LMS_USER | System handler, on return from a system call. |
| LMS_SYSTEM | System handler, when a system call is entered. |
| LMS_TRAP | Trap handler, when a trap occurs (including floating points). |
| LMS_TFAULT | Trap handler (text page fault). |
| LMS_FAULT | Trap handler (data page fault). |
| LMS_KFAULT | Trap handler (kernel page fault). |
| LMS_USER_LOCK | LWP support code, when a mutex lock is acquired. |
| LMS_SLEEP | Turnstile code, when an LWP/kthread is about to block. |
| LMS_WAIT_CPU | Dispatcher code. Not updated in new_mstate(), but updated in restore_mstate() (see text below). |
| LMS_STOPPED | Signal code, when a job control signal is sent. |

The last function to discuss apropos of microstate accounting is restore_mstate(), which is called from a few places in the dispatcher code to restore the microstate of an LWP just for execution. restore_mstate() calculates the microstate time value spent in the previous state (typically a sleep) by using the same basic algorithm described for the new_mstate() function and the previous state is restored from the ms_prev field (lwp_state structure).

When LWP/kthreads terminate, the microstate accounting data in the ms_acct[] array, along with the resource usage counters, is added to the values in the corresponding locations in the proc structure. Again, the process level resource counters and microstate accounting data reflect all LWP/kthreads in the process.