shells-‐h ave built-in commands that emulate the kill command. As an alternative to using the PID list, you can use the option `%job> 'list.`

Although processes can choose to ignore commands, the kill command is the one command that must be obeyed. Try using signal 9 when the default signal 15 doesn't work. When the signal type 0 is used, the command specifies that all processes associated with the currently logged-in username should be killed. If that user is a root user, your current session is toast and you must reboot your system. Use kill –KILL 0 to forcibly terminate all processes for your user session.

> **WARNING** The command `kill –s 9 0` or `kill –9 0` terminates all current processes for a user. When root issues this command, the system will shut down.

Table 15.2 includes a short list of signal numbers. You can access a more complete listing at /usr/include/sys/signal.h or by issuing the `kill –l` command. There are 45 signal types listed.

**TABLE 15.2: SIGNAL DESCRIPTIONS**
| Number | Name | Description |
|:---|:---|:---|
| 0 | N/A | Exit command. (Not a signal, but used in program traps.) |
| 1 | SIGHUP | Hang up or disconnect line. |
| 2 | SIGINT | Terminal interrupt. You can perform the same action by pressing the interrupt keystroke (Ctrl+C). |
| 3 | SIGQUIT | Quit. You can perform the same action by using the quit keystroke (Ctrl+Shift+\) or Ctrl+Shift+\). |
| 4 | SIGILL | Illegal instruction. |
| 5 | SIGTRAP | Used for program tracing. |
| 6 | SIGABRT | Abort. |
| 7 | SIGEMT | Emulation trap. |
| 8 | SIGFPE | Provides an arithmetic exception. |
| 9 | SIGKILL | Kill. The `kill –9` command terminates a process. |
| 10 | SIGBUS | Signals a bus error. |
| 11 | SIGSEGV | Segmentation fault. |
| 12 | SIGSYS | Bad system call. |
| 13 | SIGPIPE | Broken pipe. |
| 14 | SIGALRM | Alarm clock. |
| 15 | SIGTERM | Software termination. This is the default kill signal. |
| 24 | SIGTSTP | Stop. The job control stop key is the equivalent of the Ctrl+Z keystroke. |