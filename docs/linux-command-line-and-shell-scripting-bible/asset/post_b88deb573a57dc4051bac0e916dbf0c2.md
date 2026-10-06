# Part II Shell Scripting Basics

If you really want to exit the shell with the stopped job still active, just type the exit command again. The shell will exit, terminating the stopped job. Alternately, now that you know the PID of the stopped job, you can use the kill command to send a SIGKILL signal to terminate it:

```
$ kill -9 20065
$
[1]+ Killed      sleep 100
$
```

When you kill the job, initially you won't get any response. However, the next time you do something that produces a shell prompt, you'll see a message indicating that the job was killed. Each time the shell produces a prompt, it also displays the status of any jobs that have changed states in the shell. After you kill a job, the next time you force the shell to produce a prompt, it displays a message showing that the job was killed while running.

# Trapping signals

Instead of using your script to ignore signals, you can trap them when they appear and perform other commands. The trap command allows you to specify which Linux signals your shell script can watch for and intercept from the shell. If the script receives a signal listed in the trap command, it prevents it from being processed by the shell, and handles it locally.

The format of the trap command is:

```
trap commands signals
```

That's simple enough. On the trap command line, you just list the commands you want the shell to execute, along with a space-separated list of signals you want to trap. You can specify the signals either by their numeric value or by their Linux signal name.

Here's a simple example of using the trap command to ignore SIGINT and SIGTERM signals:

```
$ cat test1
#!/bin/bash
# testing output in a background job

trap "echo Haha" SIGINT SIGTERM
echo "This is a test program"
count=1
while [ $count -le 10 ]
do
    echo "Loop #$count"
    sleep 10
    count=$((count + 1))
done
echo "This is the end of the test program"
$
```

The trap command used in this example displays a simple text message each time it detects either the SIGINT or SIGTERM signal. Trapping these signals makes this script impervious to the user attempting to stop the program by using the bash keyboard Ctrl-C command:

```
$ ./test1
This is a test program
Loop #1
Haha
Loop #2
Loop #3
Haha
Loop #4
Loop #5
Loop #6
Loop #7
Haha
Loop #8
Loop #9
Loop #10
This is the end of the test program
$
```

Each time the Ctrl-C key combination was used, the script executed the echo statement specified in the trap command instead of ignoring the signal and allowing the shell to stop the script.

# Trapping a script exit

Besides trapping signals in your shell script, you can trap them when the shell script exits. It is a convenient way to perform commands just as the shell finishes its job.

To trap the shell script exit, just add the EXIT signal to the trap command:

```
$ cat test2
#!/bin/bash
# trapping the script exit

trap "echo byebye" EXIT

count=1
while [ $count -le 5 ]
do
    echo "Loop $count"
    sleep 3
    count=$(( count + 1 ))
done
$ ./test2
Loop #1
Loop #2
Loop #3
Loop #4
Loop #5
byebye
$
```

When the script gets to the normal exit point, the trap is triggered, and the shell executes the command you specify on the trap command line. The EXIT trap also works if you prematurely exit the script:

```
$ ./test2
Loop #1
Loop #2
byebye
$
```

When the Ctrl-C key combination is used to send a SIGINT signal, the script exits (since that signal is not listed in the trap list), but before the script exits, the shell executes the trap command.

# Removing a trap

You can remove a set trap by using a dash as the command and a list of the signals you want to return to normal behavior:

```
$ cat test3
#!/bin/bash
# removing a set trap

trap "echo byebye" EXIT

count=1
while [ $count -le 5 ]
do
    echo "Loop #$count"
    sleep 3
    count=$(( count + 1 ))
done
trap - EXIT
echo "I just removed the trap"
$ ./test3
Loop #1
Loop #2
Loop #3
Loop #4
Loop #5
I just removed the trap
```

Once the signal trap is removed, the script ignores the signals. However, if a signal is received before the trap is removed, the script processes it per the trap command:

```
$ ./test3
Loop #1
Loop #2
byebye
```

In this example Ctrl-C key combination was used to terminate the script prematurely. Since the script was terminated before the trap was removed, the script executed the command specified in the trap.

# Running Scripts in Background Mode

There are times when running a shell script directly from the command line interface is inconvenient. Some scripts can take a long time to process, and you may not want to tie up the command interface waiting. While the script is running, you can't do anything else in your terminal session. Fortunately, there's a simple solution to that problem.

When you use the ps command, you see a bunch of different processes running on the Linux system. Obviously, all of these processes aren't running on your terminal monitor. This is called running in the background. In background mode, a process runs without being associated with STDIN, STDOUT, and STDERR on your terminal (see Chapter 12). You can exploit this feature with your shell scripts as well, allowing them to run behind the scenes.

# Running in the background

Running a shell script in background is a fairly easy thing to do. To run a shell script in background mode from the command line, just place an ampersand symbol after the command:

```
$ ./test1 &
[1] 19555
$ This is test program
Loop #1
Loop #2
ls -l
total 8
-rwxr-r-- 1 rich Nov 2 11:27 test1* Loop #3
```

When you place the ampersand symbol after a command it separates from the shell and runs it as a separate background process. The first thing that displays is the line:

```
[1] 19555
```

The number in square brackets is the job number assigned to the background process by the shell. The next number is the PID. Every process running on the Linux system must have a unique PID. As soon as the system displays these items, a new command line appears. You are returned back to the shell, and the command executes safely in background mode. At this point, you can enter new commands at the prompt (as shown in the example). However, while the background process is still running, it uses your terminal monitor for STDOUT and STDERR. You'll notice from the example that the output from test1 appears in the output interleaved with other commands run from the shell. When the background process finishes, it displays a message on the terminal:

```
[1] Done                    test1
```

This shows the job number and the status of the job (Done), along with the command used to start the job.

# Running background jobs

You can start any number of background jobs at the same time from the command line prompt:

```
$ ./test1 &
[1] 19582
$ This is test program
Loop #1
$ ./test1 &
[2] 19597
$ This is test program
Loop #1
$ ./test1 &
[3] 19602
$ This is test program
Loop #1
Loop #2
```

Each time you start a new job, the Linux system assigns a new job number and PID. You can see that all of the scripts are running under the ps command:

```
$ ps au
USER PID %CPU %MEM VSZ RSS TTY STAT TIME COMMAND
rich 19498 0.0 9.276 1628 1628 pts/0 S 11:38 0:00 -bash
rich 19582 0.0 9.276 1180 1180 pts/0 S 11:55 0:00 /bin/bash .test1
rich 19597 0.1 0.227 1180 1180 pts/0 S 11:55 0:00 /bin/bash .test1
rich 19612 0.1 0.927 1180 1180 pts/0 S 11:55 0:00 /bin/bash .test1
rich 19639 0.0 0.4 1564 552 pts/0 S 11:56 0:00 sleep 10
rich 19640 0.0 0.4 1564 552 pts/0 S 11:56 0:00 sleep 10
rich 19641 0.0 0.4 1564 552 pts/0 S 11:56 0:00 sleep 10
rich 19642 0.0 0.4 2558 744 pts/0 R 11:56 0:00 ps au
```

Each of the background processes starts appears in the ps command output of running processes. If all of the processes display output in your terminal session, things can get pretty messy pretty quickly. Fortunately, there's a simple way to solve that problem. we'll discuss this in the next section.

# Exiting the terminal

You must be careful when using background processes from a terminal session. Notice in the output from the ps command that each of the background processes is tied to the terminal session (pts/0) terminal. If the terminal session exits, the background process also exits.

Some terminal emulators warn if you have any running background processes associated with the terminal, while others don't. If you want your script to continue running in background mode after you've logged off the console, there's something you need to do. The next section discusses that.

# Running Scripts without a Console

There will be times when you want to start a shell script from a terminal session, then let the script run in background mode until it finishes, even if you exit the terminal session. You can do this by using the nohup command.

The nohup runs another command blocking any SIGHUP signals that are sent to the process. This prevents the process from exiting when you exit your terminal session.

The format used for the nohup command is:

```
$ nohup ./test1 &
[1] 19831
$ nohup: appending output to `nohup.out`
```
