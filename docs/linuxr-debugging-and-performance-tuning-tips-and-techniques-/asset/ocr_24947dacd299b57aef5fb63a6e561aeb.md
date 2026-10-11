TABLE 9.3
The 4.2 and 4.3 BSD union wait

| POSIX macro | Union member | Usage | Meaning |
|---|---|---|---|
| WIFEXITED() | w_terminsig | w.w_terminsig = 0 | True if normal exit. |
| WEXITSTATUS() | w_retcode | code = w.w_retcode | Exit status if not by signal. |
| WIFSIGNALED() | w_terminsig | w.w_terminsig != 0 | True if death by signal. |
| WTERMSIG() | w_terminsig | sig = w.w_terminsig | Signal that caused termination. |
| WIFSTOPPED() | w_stopval | w.w_stopval == STOPPED | True if stopped. |
| WSTOPSIG() | w_stopsig | sig = w.w_stopsig | Signal that caused stopping. |
| WCOREDUMP() | w_coredump | w.w_coredump != 0 | True if child dumped core. |

# 9.2 Process Groups

A process group is a group of related processes that should be treated together for job control purposes. Processes with the same process group ID are members of the process group, and the process whose PID is the same as the process group ID is the process group leader. New processes inherit the process group ID of their parent process.

We have already seen that waitpid() allows you to wait for any process in a given process group. In Section 10.6.7, “Sending Signals: kill() and killpg(),” page 376, we’ll also see that you can send a signal to all the processes in a particular process group as well. (Permission checking always applies; you can’t send a signal to a process you don’t own.)

# 9.2.1 Job Control Overview

Job control is an involved topic, one that we’ve chosen not to delve into for this volume. However, here’s a quick conceptual overview.

The terminal device (physical or otherwise) with a user working at it is called the controlling terminal.

A session is a collection of process groups associated with the controlling terminal. There is only one session per terminal, with multiple process groups in the session. One