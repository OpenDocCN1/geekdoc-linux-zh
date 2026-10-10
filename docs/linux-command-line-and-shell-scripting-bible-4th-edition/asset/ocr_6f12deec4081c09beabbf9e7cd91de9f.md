# # Exploring Parent and Child Shell Relationships

The default interactive shell (login shell) that starts when a user logs into a virtual console terminal or starts a terminal emulator in the GUI is a *parent shell*. As you have read so far in this book, a parent shell process provides a CLI prompt and waits for commands to be entered. When the `bash` command (or other shell program name) is entered at the CLI prompt, a new shell program is created. This is a *child shell*. A child shell also has a CLI prompt and waits for commands to be entered.

Because you do not see any relevant messages when you type `bash` and spawn a child shell, another command can help bring clarity. The `ps` command was covered in *Chapter 4*, “More Bash Shell Commands.” Using this with the -f option before and after entering a child shell is useful:

```
$ `ps` -f
UID     PID  PPID  C STIME TTY          TIME CMD
christi+ 6160  6156  0 11:01 pts/1    00:00:00 -bash
christi+ 7141  6160  0 12:51 pts/1    00:00:00 ps -f
$
$ `bash`
$
$ `ps` -f
UID     PID  PPID  C STIME TTY          TIME CMD
christi+ 6160  6156  0 11:01 pts/1    00:00:00 -bash
christi+ 7142  6160  0 12:52 pts/1    00:00:00 bash
christi+ 7164  7142  0 12:52 pts/1    00:00:00 ps -f
$
```

The first use of `ps` -f shows two processes. One process has a process ID of 6160 (second column) and is running the Bash shell program (last column). The second process (process ID 7141) is the actual `ps` -f command running.

> **NOTE**
> 
> A process is a running program. The Bash shell is a