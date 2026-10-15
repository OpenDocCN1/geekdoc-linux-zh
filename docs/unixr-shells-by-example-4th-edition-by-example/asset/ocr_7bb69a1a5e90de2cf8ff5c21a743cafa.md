# 1.6 The Environment and Inheritance

The Bourne, Bash, and Korn shells allow you to handle signals coming into your program, (see "Trapping Signals" on page 716 for programming in the Bourne shell; "Trapping Signals" on page 935 for programming in the Korn shell; and "Trapping Signals" on page 935 for programming in the Bash shell) either by ignoring the signal, by specifying some action to be taken when a specified signal arrives, or by resetting the signal back to its default action. The C and TC shells are limited to handling ^C (Ctrl-C), the interrupt character.

Table 1.2 lists the standard signals that a process can use.

# Table 1.2 Standard Signals

| Number | Name   | Description                                      | Action          |
|--------|--------|--------------------------------------------------|-----------------|
| 0      | EXIT   | Shell exits                                      | Termination     |
| 1      | SIGHUP | Terminal has disconnected                        | Termination     |
| 2      | SIGINT | User presses Ctrl-C                              | Termination     |
| 3      | SIGQUIT| User presses Ctrl-\                               | Termination     |
| 4      | SIGILL | Illegal hardware instruction                     | Program error   |
| 5      | SIGTRAP| Produced by debugger                             | Program error   |
| 8      | SIGFPE | Arithmetic error; e.g., division by zero        | Program error   |
| 9      | SIGKILL| Cannot be caught or ignored                      | Termination     |
| 10     | SIGUSR1| Application-defined signal for user              | Termination     |
| 11     | SIGSEGV| Invalid memory references                        | Program error   |
| 12     | SIGUSR2| Application-defined signal for user              | Termination     |
| 13     | SIGPIPE| Broken pipe connection                           | Operator error  |
| 14     | SIGALRM| Timeout                                          | Alarm sent      |
| 15     | SIGTERM| Termination of a program                         | Termination     |
| 17     | SIGCHLD| Child process has stopped or died                | Ignored         |
| 18     | SIGCONT| Starts a stopped job; can't be handled or ignored| Continue if stopped |
| 19     | SIGSTOP| Stops a job; can't be handled or ignored         | Stops the process |
| 20     | SIGTSTP| Interactive stop; user presses Ctrl-Z            | Stops the process |
| 21     | SIGTTIN| Background job is trying to read from the controlling terminal | Stops the process |
| 22     | SIGTTOU| Background job is trying to write to the controlling terminal | Stops the process |

> a. See your specific system manual. For a complete list of UNIX signals and their meanings, also go to www.cyber-magic.co.uk/technet/unixsignals.htm. For Linux signals, go to os/comptechdoc.com/linuxprogramming/linux_posix.html.