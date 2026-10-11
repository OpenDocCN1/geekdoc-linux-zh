# ## Bourne Built-Ins

Built-ins do not cause a shell to fork a new process when executed. The `trap` built-in catches a signal, which in turn reports to a process about a certain interrupt condition. Solaris uses signals to report an interrupt to the user or system. Interrupts may be caused by hitting the interrupt or Esc key or by a broken pipe line, illegal instructions, bad system calls, and other problems that periodically occur. By using `trap`, you can direct the actions a signal gives a script. There are six signals you can use in the Bourne shell when you work with scripts. (Signals were discussed in more detail in Chapter 15, “Memory and Process Management.”) Table 18.3 describes the `exit` command signal and the six system signals used in the Bourne shell.

**TABLE 18.3: SIGNALS USED IN THE BOURNE SHELL**
| Signal | No. | Description |
| :--- | :---: | :--- |
| No signal | 0 | Exit command given or end of program |
| SIGHUP | 1 | Indicates a hang up or disconnected line |
| SIGINT | 2 | Terminal interrupt, Ctrl+C |
| SIGQUIT | 3 | Quit, the quit key was pressed |
| SIGKILL | 9 | The kill command with the -9 option was given |
| SIGTERM | 15 | The default of the kill command |
| SIGSTP | 24 | Press the job-control stop key |

The numbers are the signals that `trap` catches. The command part is optional. The `trap` command resets the trap to its earlier condition, which is usually an `exit` command. When the commands part is present, the shell will execute the commands as it catches one of the signals. After it does so, the shell will resume executing from where it left off. If you use `trap` with a null or empty built-in, you can get `trap` to prevent a script from exiting and running any commands. An example of `trap` is `trap 9`. If `trap` is called without arguments, a list of commands will be displayed and an exit status of 1 will be given. The following example illustrates the `trap` built-in:

```
$ cat <trapper>
#!/bin/sh
trap 'echo PROGRAM INTERRUPt; exit 1' 2
while true
do
	echo 'Program up.'
```