# jobs

Syntax:

```
jobs
```

This is a built-in shell command that is found in popular shells. jobs enables you to view the list of processes running in the background or currently suspended.

# Kill -signal PID

This command is used to send a signal to a process. Kill can be a built-in shell command for many popular shells, such as csh and tcsh. However, there is also an external kill program, which typically is found in the /bin directory. Both versions work the same way. To find out what signals you can send to processes via kill, you can run the following:

```
kill -l
```

You should see a list similar to the following:

```
1) SIGHUP  2) SIGINT  3) SIGQUIT  4) SIGILL
5) SIGTRAP  6) SIGIOT  7) SIGBUS  8) SIGFPE
9) SIGKILL  10) SIGUSR1  11) SIGSEGV  12) SIGUSR2
13) SIGPIPE  14) SIGALRM  15) SIGTERM  17) SIGCHLD
18) SIGCONT  19) SIGSTOP  20) SIGTSTP  21) SIGTTIN
22) SIGTTOU  23) SIGURG  24) SIGXCPU  25) SIGXFSZ
26) SIGVTALRM  27) SIGPROF  28) SIGWINCH  29) SIGIO
30) SIGPWR
```

The preceding output is produced by the built-in kill command in the GNU Bourne-Again Shell (/bin/bash). Other shells or the /bin/kill command might print the output a bit differently. For example, /bin/kill -l produces the following output:

```
HUP INT QUIT ILL TRAP IOT UNUSED FPE KILL USR1 SEGV USR2
PIPE ALRM TERM STKFLT CHLD CONT STOP TSTP TTIN TTOU IO
XCPU XFSZ VTALRM PROF WINCH
```