> (table continued from previous page)

| Signal | Description | Default Action |
|---|---|---|
| SIGPWR | System detected a power failure (System V) | Ignore |
| SIGQUIT | User generated a keyboard quit (POSIX) | Process terminates and dumps core |
| SIGSEGV | Process attempted to reference inaccessible memory (POSIX) | Process terminates and dumps core |
| SIGSTKFLT | Process generated a stack fault (“blew the stack”) | Process terminates |
| SIGSTOP | Stop signal (POSIX) | Stop, cannot catch or ignore |
| SIGSYS | Bad argument to routine | Process terminates and dumps core |
| SIGTERM | Process received a termination signal (POSIX) | Process terminates |
| SIGTRAP | Process hit a trace or breakpoint trap (usually during debugging) (POSIX) | Process terminates and dumps core |
| SIGTSTP | User generated a stop from the keyboard (POSIX) | Stop |
| SIGTTIN | Process attempted to read from stdin while running in the background (POSIX) | Stop |
| SIGTTOU | Process attempted to write to stdout while running in the background (POSIX) | Stop |
| SIGUNUSED | Unused signal | Process terminates |
| SIGURG | Urgent condition on socket (4.2 BSD) | Ignore |
| SIGUSR1 | User-defined signal 1 (POSIX) | Process terminates |
| SIGUSR2 | User-defined signal 2 (POSIX) | Process terminates |
| SIGVTALRM | Interval alarm clock expired (4.2 BSD) | Process terminates |
| SIGWINCH | The size of a terminal window changed (4.3 BSD, Sun) | Ignore |
| SIGXCPU | Process exceeded the amount of CPU time it can use (4.2 BSD) | Process terminates and dumps core |

continues