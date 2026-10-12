| # | Name (Short Name) | Description |
| --- | --- | --- |
| 16 | SIGSTKFLT | Stack fault on coprocessor. |
| 17 | SIGCHLD (CHLD) | Child status has changed. |
| 18 | SIGCONT (CONT) | Continue after STOP signal. This signal cannot be blocked. |
| 19 | SIGSTOP (STOP) | Stop. This signal cannot be caught (i.e., handled in a process), blocked, or ignored. |
| 20 | SIGTSTP (TSTP) | Stop signal generated from keyboard, typically using Ctrl+Z. |
| 21 | SIGTTIN | Background read attempted from control terminal. |
| 22 | SIGTTOU | Background write attempted to control terminal. |
| 23 | SIGURG | Urgent condition present on socket. |
| 24 | SIGXCPU | CPU time limit exceeded. See man setrlimit(2). |
| 25 | SIGXFSZ | File size limit exceeded. See man setrlimit(2). |
| 26 | SIGVTALRM | Virtual time alarm. See man setitimer(2). |
| 27 | SIGPROF | Profiling timer alarm. See man setitimer(2). |
| 28 | SIGWINCH | Window size change. |
| 29 | SIGIO | I/O is possible on a descriptor. See man fcntl(2). |
| 30 | SIGPWR | Power failure. |
| 31 | UNUSED | Not used. |

After you have the `signal_demo.pl` script running, use another virtual console, login shell, or xterm (if you are on X Window) to send signals to the process. When you run the script, it displays the PID, so if you don't need to use ps to locate the PID of this process. Send any of the signals just listed to the process and view the message it displays. For example, if the PID of this process is 12345 and you run

```
kill -HUP 12345
```

it will display the following:

Caught a HUP signal.

Note that the script schedules an alarm event (using the alarm function) to occur after 10 seconds of execution that prints the following:

Caught a ALRM signal.