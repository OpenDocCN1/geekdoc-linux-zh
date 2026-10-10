
## Part II: Shell Scripting Basics

### Linux Signals

| Signal | Value | Description |
| :--- | :--- | :--- |
| 1 | SIGHUP | Hangs up the process |
| 2 | SIGINT | Interrupts the process |
| 3 | SIGQUIT | Stops the process |
| 9 | SIGKILL | Unconditionally terminates the process |
| 15 | SIGTERM | Terminates the process if possible |
| 18 | SIGCONT | Continues a stopped process |
| 19 | SIGSTOP | Unconditionally stops, but doesn’t terminate, the process |
| 20 | SIGTSTP | Stops or pauses the process, but doesn’t terminate it |

By default, the Bash shell ignores any SIGQUIT (3) and SIGTERM (15) signals it receives (so an interactive shell cannot be accidentally terminated). However, the Bash shell does not ignore any received SIGHUP (1) and SIGINT (2) signals.

If the Bash shell receives a SIGHUP signal, such as when you leave an interactive shell, it exits. Before it exits, however, it passes the SIGHUP signal to any processes started by the shell, including any running shell scripts.

With a SIGINT signal, the shell is just interrupted. The Linux kernel stops giving the shell processing time on the CPU. When this happens, the shell passes the SIGINT signal to any processes started by the shell to notify them of the situation.

As you probably have noticed, the shell passes these signals on to your shell script program for processing. However, a shell script’s default behavior does not govern these signals, which may have an adverse effect on the script’s operation. To avoid this situation, you can program your script to recognize signals and perform commands to prepare the script for the consequences of the signal.

### Generating signals

The Bash shell allows you to generate two basic Linux signals using key combinations on the keyboard. This feature comes in handy if you need to stop or pause a runaway script.

### Interrupting a process

The Ctrl+C key combination generates a SIGINT signal and sends it to any processes currently running in the shell. You can test this by running a command that normally takes a long time to finish and pressing the Ctrl+C key combination:

```bash
$ sleep 60
^C
$
```

The `sleep` command pauses the shell's operation for the specified number of seconds and returns the shell prompt. The Ctrl+C key combination sends a `SIGINT` signal, which simply stops the current process running in the shell. By pressing the Ctrl+C key combination before the time passed (50 seconds), you can permanently terminate the `sleep` command.

### Pausing a process

Instead of terminating a process, you can pause it in the middle of whatever it’s doing. Sometimes, this can be a dangerous thing (for example, if a script has a file lock open on a crucial system file), but often it allows you to peek inside what a script is doing without actually terminating the process.

The Ctrl+Z key combination generates a `SIGTSTP` signal, stopping any processes running in the shell. Stopping a process is different than terminating the process. Stopping the process leaves the program in memory and able to continue running from where it left off. In the “Controlling the Job” section later in this chapter, you learn how to restart a process that’s been stopped.

When you use the Ctrl+Z key combination, the shell informs you that the process has been stopped:

```bash
$ sleep 60
^Z
[1]+  Stopped            sleep 60
$
```

The number in the square brackets is the *job number* assigned by the shell. The shell refers to each process running in the shell as a *job* and assigns each job a unique number within the current shell. It assigns the first started process job number 1, the second job number 2, and so on.

If you have a stopped job assigned to your shell session, Bash warns you the first time you try to exit the shell:

```bash
$ sleep 70
^Z
[2]+  Stopped            sleep 70
$
$ exit
logout
There are stopped jobs.
$
```

You can view the stopped jobs using the `ps` command:

```bash
$ ps -l
  F   UID     PID   PPID   %CPU      S      TTY    TIME    CMD
 0 S  1001   1509   1508   0.0  0 S  pts/0  00:00:00 bash
 0 T  1001   1532   1509   0.0  0 T  pts/0  00:00:00 sleep
 0 T  1001   1533   1509   0.0  0 T  pts/0  00:00:00 sleep
 0 R  1001   1534   1509   0.0  0 R  pts/0  00:00:00 ps
$
```

In the S column (process state), the `ps` command shows the stopped job's state as T. This indicates the command either is being traced or is stopped.

If you really want to exit the shell with a stopped job (or jobs) still active, just type the `exit` command again. The shell exits, terminating the stopped job.

Alternately, now that you know the PID of the stopped job(s), you can use the `kill` command to send a `SIGKILL` (9) signal to terminate it:

```bash
$ kill -9 1532
[1]- Killed                 sleep 60
$ kill -9 1533
[2]+ Killed                 sleep 70
$
```

Each time the shell produces a prompt, it also displays the status of any jobs that have changed states in the shell. After you kill a job, the shell displays a message showing that the job was killed while running and then provides the prompt.

> **Note**
> On some Linux systems, when you kill the job, you initially don't get any response. However, the next time you do something that produces a shell prompt (such as pressing the Enter key), you'll see a message indicating that the job was killed.

### Trapping signals

Instead of allowing your script to leave signals ungoverned, you can trap them when they appear and perform other commands. The `trap` command allows you to specify which Linux signals your shell script can watch for and intercept from the shell. If the script receives a signal listed in the `trap` command, it prevents it from being processed by the shell and instead handles it locally.

The format of the `trap` command is

```bash
trap commands signals
```

On the `trap` command line, you just list the commands you want the shell to execute, along with a space-separated list of signals you want to trap. You can specify the signals either by their numeric value or by their Linux signal name.

Here's a simple example of using the `trap` command to capture the `SIGINT` signal and govern the script's behavior when the signal is sent:

```bash
$ cat trapsignal.sh
#!/bin/bash
#Testing signal trapping
#
trap "echo ' Sorry! I have trapped Ctrl-C'" SIGINT
# echo This is a test script.
# count=1
while [ $count -le 5 ]
do
    echo "Loop #$count"
    sleep 1
    count=$(( $count + 1 ))
done
# echo "This is the end of test script."
exit
$
```

The **trap** command used in this example displays a simple text message each time it detects the SIGINT signal. Trapping this signal makes this script impervious to the user attempting to stop the program by using the Bash shell keyboard Ctrl+C command:

```bash
$ ./trapsignal.sh
This is a test script.
Loop #1
Loop #2
^C Sorry! I have trapped Ctrl+C
Loop #3
^C Sorry! I have trapped Ctrl+C
Loop #4
Loop #5
This is the end of test script.
$
```

Each time the Ctrl+C key combination was used, the script executed the **echo** statement specified in the **trap** command instead of not managing the signal and allowing the shell to stop the script.

> **WARNING**
>
> If a command in your script is interrupted by a signal, using **trap** with a specified command will not necessarily allow the interrupted command to continue where it left off. To keep critical operations flowing in your scripts, use **trap** with a null specification along with a list of the signals to trap, such as
>
> ```bash
> trap "" SIGINT
> ```
>
> Using **trap** in this way allows the script to completely ignore signal interruptions and continue its important work.

### Trapping a script exit

Besides trapping signals in your shell script, you can trap them when the shell script exits. This is a convenient way to perform commands just as the shell finishes its job.

To trap the shell script exiting, just add the `EXIT` signal to the `trap` command:

```bash
$ cat trapexit.sh
#!/bin/bash
#Testing exit trapping
#
trap "echo Goodbye..." EXIT
#
count=1
while [ $count -le 5 ]
do
    echo "Loop #$count"
    sleep 1
    count=$(( $count + 1 ))
done
#
exit
$
$ ./trapexit.sh
Loop #1
Loop #2
Loop #3
Loop #4
Loop #5
Goodbye...
$
```

When the script gets to the normal exit point, the trap is triggered, and the shell executes the command you specify on the `trap` command line. The `EXIT` trap also works if you prematurely exit the script:

```bash
$ ./trapexit.sh
Loop #1
Loop #2
Loop #3
^C Goodbye...
$
```

Because the `SIGINT` signal isn’t in the `trap` command list, when the Ctrl+C key combination is used to send that signal, the script exits. However, before the script exits, because the `EXIT` is trapped, the shell executes the `trap` command.

### Modifying or removing a trap

To handle traps differently in various sections of your shell script, you simply reissue the `trap` command with new options:

```bash
$ cat trapmod.sh
#!/bin/bash
#Modifying a set trap
#
```
