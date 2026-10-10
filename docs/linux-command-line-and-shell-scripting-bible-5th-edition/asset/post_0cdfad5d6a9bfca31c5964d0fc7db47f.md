
## Part II: Shell Scripting Basics

### Modifying and Removing Traps

After the signal **trap** is modified, the script manages the signal or signals differently. However, if a signal is received before the **trap** is modified, the script processes it per the original **trap** command:

```bash
$ ./trapmod.sh
Loop #1
^C Sorry...Ctrl-C is trapped.
Loop #2
Loop #3
Second Loop #1
Second Loop #2
^C I have modified the trap!
Second Loop #3
$ 
```

> **Tip**
> If you try out the **trap** command in your interactive shell session, you can view what signals are being trapped by issuing `trap -p`. If nothing displays, your shell session is handling signals in the default manner.

You can also remove a set **trap**. Add two dashes after the **trap** command and a list of the signals you want to return to default behavior:

```bash
$ cat trapremoval.sh
#!/bin/bash
#Removing a set trap
#
trap "echo ' Sorry...Ctrl-C is trapped.'" SIGINT
#
count=1
while [ $count -le 3 ]
do
	echo "Loop #$count"
	sleep 1
	count=$[ $count + 1 ]
done
#
trap -- SIGINT
echo "The trap is now removed."
#
count=1
while [ $count -le 3 ]
do
	echo "Second Loop #$count"
	sleep 1
	count=$[ $count + 1 ]
done
#
exit
$
```

> **Note**
> You can use a single dash instead of a double dash after the `trap` command to remove signals traps. Both the single and double dash work properly.

After the signal trap is removed, the script handles the SIGINT signal in its default manner, terminating the script. However, if a signal is received before the trap is removed, the script processes it per the original trap command:

```bash
$ ./trapremoval.sh
Loop #1
Loop #2
^C Sorry...Ctrl-C is trapped.
Loop #3
The trap is now removed.
Second Loop #1
Second Loop #2
^C
$
```

In this example, the first Ctrl+C key combination was used to attempt to terminate the script prematurely. Because the signal was received before the trap was removed, the script executed the command specified in the trap. After the script executed the trap removal, then Ctrl+C could prematurely terminate the script.

![](img/0798d50a0e5dbf1265fbda3832b3e015_410_0.png)

### Running Scripts in Background Mode

Sometimes, running a shell script directly from the command line is inconvenient. Some scripts can take a long time to process, and you may not want to tie up the command-line interface as it executes. While the script is running, you can't do anything else in your terminal session. Fortunately, there's a simple solution to that problem.

When you use the `ps -e` command, you see a whole bunch of different processes running on the Linux system:

```bash
$ ps -e
PID TTY TIME CMD
1 ? 00:00:02 systemd
2 ? 00:00:00 kthreadd
3 ? 00:00:00 rcu_gp
4 ? 00:00:00 rcu_par_gp
[...]
2585 pts/0 00:00:00 ps
$
```

Obviously, all these processes are not running on your terminal. In fact, many are not running on any terminal—they are running in the *background*. In background mode, a process runs without being associated with a `STDIN`, `STDOUT`, and `STDERR` on a terminal session (see Chapter 15, “Presenting Data”).

You can exploit this feature with your shell scripts as well, allowing them to run behind the scenes and not lock up your terminal session. The following sections describe how to run your scripts in background mode on your Linux system.

#### Running in the background

Running a shell script in background mode is a fairly easy thing to do. To run a shell script in background mode from the command-line interface, just place an ampersand symbol ( & ) after the command:

```bash
$ cat backgroundscript.sh
#!/bin/bash

#Test running in the background

while [ $count -le 5 ]
do
	sleep 1
	count=$[ $count + 1 ]
done

# exit

$ ./backgroundscript.sh &
[1] 2595
$
```

When you place the ampersand symbol after a command, it separates the command from the current shell and runs it as a separate background process on the system. The first thing that displays is the line:

```bash
[1]  2595
```

The number in the square brackets is the job number (1) assigned by the shell to the background process. The next number is the process ID (PID) the Linux system assigns to the process. Every process running on the Linux system must have a unique PID.

As soon as the system displays these items, a new command-line interface prompt appears. You are returned to the current shell, and the command you executed runs safely in background mode. At this point, you can enter new commands at the prompt.

When the background process finishes, it displays a message on the terminal:

```bash
[1]+  Done                ./backgroundscript.sh
```

This shows the job number and the status of the job (Done), along with the command used to start the job (minus the &).

Be aware that while the background process is running, it still uses your terminal monitor for STDOUT and STDERR messages:

```bash
$ cat backgroundoutput.sh
#!/bin/bash
#Test running in the background

echo "Starting the script..."
count=1
while [ $count -le 5 ]
do
        echo "Loop #$count"
        sleep 1
        count=$[ $count + 1 ]
done
#
echo "Script is completed."
exit
$

$ ./backgroundoutput.sh &
[1] 2615
$ Starting the script...
Loop #1
Loop #2
Loop #3
Loop #4
Loop #5
Script is completed.

[1]+  Done                ./backgroundoutput.sh
$
```

You'll notice from the example that the output from the `backgroundoutput.sh` script displays. The output intermixes with the shell prompt, which is why *Starting the script* appears next to the $ prompt.

You can still issue commands while this output is occurring:

```bash
$ ./backgroundoutput.sh &
[1] 2719
$ Starting the script...
Loop #1
Loop #2
Loop #3
pwd
/home/christine/scripts
$ Loop #4
Loop #5
Script is completed.

[1]+ Done        ./backgroundoutput.sh
$
```

While the `backgroundoutput.sh` script is running in the background, the `pwd` command was entered. The script's output, the typed command, and the command's output all intermixed with each other's output display. This can be confusing! It is a good idea to redirect `STDOUT` and `STDERR` (Chapter 15) for scripts you will be running in the background to avoid this messy display.

#### Running multiple background jobs

You can start any number of background jobs at the same time from the command-line prompt:

```bash
$ ./testAScript.sh &
[1] 2753
$ This is Test Script #1.

$ ./testBScript.sh &
[2] 2755
$ This is Test Script #2.

$ ./testCScript.sh &
[3] 2757
$ And... another Test script.

$ ./testDScript.sh &
[4] 2759
$ Then...there was one more Test script.
$
```

Each time you start a new job, the Linux system assigns it a new job number and PID. You can see that all the scripts are running using the `ps` command:

```bash
$ ps
PID TTY TIME CMD
1509 pts/0 00:00:00 bash
2753 pts/0 00:00:00 testAscript.sh
2754 pts/0 00:00:00 sleep
2755 pts/0 00:00:00 testBscript.sh
2756 pts/0 00:00:00 sleep
2757 pts/0 00:00:00 testCscript.sh
2758 pts/0 00:00:00 sleep
2759 pts/0 00:00:00 testDscript.sh
2760 pts/0 00:00:00 sleep
2761 pts/0 00:00:00 ps
```

You must be careful when using background processes from a terminal session. Notice in the output from the `ps` command that each of the background processes is tied to the terminal session (pts/0) terminal. If the terminal session exits, the background process also exits.

![](img/0798d50a0e5dbf1265fbda3832b3e015_415_0.png)

If you want your script to continue running in background mode after you have logged off the console, there’s something else you need to do. The next section discusses that process.

### Running Scripts Without a Hang-Up

Sometimes, you may want to start a shell script from a terminal session and let the script run in background mode until it finishes, even if you exit the terminal session. You can do this by using the `nohup` command.

The `nohup` command blocks any SIGHUP signals that are sent to the process it is protecting. This prevents the process from exiting when you exit your terminal session.

The format used for the `nohup` command is as follows:

```bash
nohup command
```

Here’s an example using a shell script launched into the background as the command:

```bash
$ nohup ./testAscript.sh &
[1] 1828
$ nohup: ignoring input and appending output to `nohup.out`
$
```
