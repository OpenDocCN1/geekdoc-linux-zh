
Processes Processes themselves can request the kernel to send signals to processes, even themselves. This is not so strange; an alarm clock is a way for you to send a signal to yourself in the future; you set the alarm and wait for it to signal you. Similarly, a process can ask the kernel to send a wake-up call to itself at some future time. A process can also ask the kernel to send a signal to other processes to which it has permission to send signals. For ordinary user processes, these include any processes with the same real or effective user-id.

## 5.3.3 Signal Types

UNIX systems define signals in the header file `<signal.h>`. More accurately, the header file `<signal.h>` includes the header file that contains the signal definitions. Different UNIX systems store this file in different places. In Linux, the file `<bits/signum.h>` is where the signals are defined. The kernel includes this header file, but user level programs are supposed to include `<signal.h>`. The idea is to keep separate headers for the kernel and the user-level programs.

The exact set of signals varies from one system to another, but some of them are standard across all systems. Signal names are just names for small integers such as `SIGINT`, `SIGKILL`, `SIGHUP`, and `SIGCHLD`. All names begin with the prefix `SIG`. `SIGHUP` is the *hang-up* signal. It is sent to a process when its control terminal has been disconnected. `SIGCHLD` is the signal sent to a parent by the kernel when it detects that one of its child processes has terminated. There are typically about 30 to 35 different signals defined in any UNIX system. The list of signals has changed over the years. The first 30 signals listed below are found in Linux and Solaris 9; the last 4 only in Solaris 9. The constant `NSIG` is the total number of signals defined. Since the signal numbers are allocated consecutively, `NSIG` is also one greater than the largest defined signal number.

| Name | Value | Default | Event | Note | Category |
|---|---|---|---|---|---|
| SIGHUP | 1 | Exit | Hangup |  | Termination |
| SIGINT | 2 | Exit | Interrupt |  | Termination |
| SIGQUIT | 3 | Core | Quit |  | Termination |
| SIGILL | 4 | Core | Illegal Instruction |  | Program Error |
| SIGTRAP | 5 | Core | Trace or Breakpoint Trap |  | Program Error |
| SIGABRT | 6 | Core | Abort |  | Program Error |
| SIGEMT | 7 | Core | Emulation Trap |  | Program Error |
| SIGFPE | 8 | Core | Arithmetic Exception |  | Program Error |
| SIGKILL | 9 | Exit | Killed |  | Termination |
| SIGBUS | 10 | Core | Bus Error | 1 | Program Error |
| SIGSEGV | 11 | Core | Segmentation Fault |  | Program Error |
| SIGSYS | 12 | Core | Bad System Call | 1 | Program Error |
| SIGPIPE | 13 | Exit | Broken Pipe |  | Operation Error |
| SIGALRM | 14 | Exit | Alarm Clock |  | Alarm |
| SIGTERM | 15 | Exit | Terminated |  | Termination |
| SIGUSR1 | 16 | Exit | User Signal 1 | 1 | Miscellaneous |
| SIGUSR2 | 17 | Exit | User Signal 2 | 1 | Miscellaneous |
| SIGCHLD | 18 | Ignore | Child Status Changed | 1 | Job Control |
| SIGPWR | 19 | Ignore | Power Fail or Restart |  | Hardware |
| SIGURG | 21 | Ignore | Urgent Socket Condition |  | Asynchronous I/O |
| SIGPOLL | 22 | Exit | Pollable Event |  | Asynchronous I/O |
| SIGSTOP | 23 | Stop | Stopped (signal) | 1 | Job Control |
| SIGTSTP | 24 | Stop | Stopped (user) | 1 | Job Control |
| SIGCONT | 25 | Ignore | Continued | 1 | Job Control |
| SIGTTIN | 26 | Stop | Stopped (tty input) | 1 | Job Control |
| SIGTTOU | 27 | Stop | Stopped (tty output) | 1 | Job Control |
| SIGVTALRM | 28 | Exit | Virtual Timer Expired | 1 | Alarm |
| SIGPROF | 29 | Exit | Profiling Timer Expired | 1 | Alarm |
| SIGXCPU | 30 | Core | CPU time limit exceeded | 1 | Operation Error |
| SIGXFSZ | 31 | Core | File size limit exceeded | 1 | Operation Error |
| SIGWINCH | 20 | Ignore | Window Size Change | 2 | Miscellaneous |
| SIGWAITING | 32 | Ignore | Concurrency signal | 3 | Miscellaneous |
| SIGLWP | 33 | Ignore | Inter-LWP signal | 3 | Miscellaneous |
| SIGFREEZE | 34 | Ignore | Check point Freeze | 3 | Miscellaneous |
| SIGTHAW | 35 | Ignore | Check point Thaw | 3 | Miscellaneous |

## Notes

- 1. In Linux the numerical value of the signal is architecture-dependent.
- 2. This is only found in Sun OS and BSD.
- 3. These are in Solaris 9.

The above list has four columns. The first is the mnemonic name for the signal, i.e., the name that can be used in a program. The second is the integer value, which you do not need to know. The third is the default action that happens to a process. For example, SIGCHLD is ignored by default,
