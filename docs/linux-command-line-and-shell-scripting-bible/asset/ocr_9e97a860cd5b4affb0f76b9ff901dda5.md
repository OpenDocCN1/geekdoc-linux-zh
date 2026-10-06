# Part II Shell Scripting Basics

```
total 8
-rwxr--r--    1 rich      rich       219 Nov 2 11:27 test1*
 Loop #3
```

When you place the ampersand symbol after a command it separates the bash from the shell and runs it as a separate background process on the system. The first thing that displays is the line:

```
[1] 19555
```

The number in the square brackets is the job number assigned to the background process by the shell. The next number is the PID Linux system assigns to the process. Every process running on the Linux system must have a unique PID.

As soon the system displays these items, a new command line interface appears. You are returned back to the shell, and the command you executed runs safely in background mode.

At this point, you can enter new commands at the prompt (as shown in the example). However, while the background process is still running, it still uses your terminal monitor for STDOUT and STDERR messages. You'll notice from the example that the output from the test1 script appears in the output interleaved with other commands that run from the shell.

When the background process finishes, it displays a message on the terminal:

```
[1] Done                    /test1
```

This shows the job number and the status of the job (Done), along with the command used to start the job.

# Running multiple background jobs

You can start any number of background jobs at the same time from the command line prompt:

```
$ ./test1 &\n[1] 19582
$ This is test program
Loop #1
$ ./test1 &\n[2] 19597
$ This is test program
Loop #1
$ ./test1 &
[3] 19602
$ This is test program
Loop #1
Loop #2
Loop #2
```