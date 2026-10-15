are pressed or if something exceptional happens.⁶ The trap command tells the shell to terminate the command currently in execution upon the receipt of a signal. If the trap command is followed by commands within quotes, the command string will be executed upon receipt of a specified signal. The shell reads the command string twice, once when the trap is set, and again when the signal arrives. If the command string is surrounded by double quotes, all variable and command substitution will be performed when the trap is set the first time. If single quotes enclose the command string, variable and command substitution do not take place until the signal is detected and the trap is executed.
Use the command kill -l or trap -l to get a list of all signals. Table 14.6 provides a list of signal numbers and their corresponding names. The most commonly used signals for trap are 1) SIGHUP (hangup), 2) SIGINT (interrupt), 3) SIGQUIT (quit), and 4) SIGTERM (exit).

# FORMAT

```
trap 'command; command' signal-number
trap 'command; command' signal-name
```

# EXAMPLE 14.61

```
trap 'rm tmp*; exit 1' 0 1 2 15
trap 'rm tmp*; exit 1' EXIT HUP INT TERM
```

# EXPLANATION

When any of the signals 1 (hangup), 2 (interrupt), or 15 (software termination) arrives, remove all the tmp files and exit.

# Table 14.6 Signal Numbers and Signalsᵃ

| 1) SIGHUP | 9) SIGKILL | 17) SIGCHLD | 25) SIGXFSZ |
| 2) SIGINT | 10) SIGUSR1 | 18) SIGCONT | 26) SIGVTALRM |
| 3) SIGQUIT | 11) SIGSEGV | 19) SIGSTOP | 27) SIGPROF |
| 4) SIGILL | 12) SIGUSR2 | 20) SIGTSTP | 28) SIGWINCH |
| 5) SIGTRAP | 13) SIGPIPE | 21) SIGTTIN | 29) SIGIO |
| 6) SIGABRT | 14) SIGALRM | 22) SIGTTOU | 30) SIGPWR |
| 7) SIGBUS | 15) SIGTERM | 23) SIGURG | |
| 8) SIGFPE | 16) SIGSTKFLT | 24) SIGXCPU | |

a. For a complete list of UNIX signals and their meanings, go to www.cybermagician.co.uk/technet/unixsignals.htm. For Linux signals, go to www.comptedoc.org/os/11unix/programming/linux_pgsignals.html.