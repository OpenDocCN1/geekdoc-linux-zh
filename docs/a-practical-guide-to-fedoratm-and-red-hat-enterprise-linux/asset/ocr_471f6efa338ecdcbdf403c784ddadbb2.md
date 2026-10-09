# ## MOVING A Job FROM THE Foreground to THE Background

You can suspend a foreground job (stop it from running) by pressing the suspend key, usually CONTROL-z. The shell then stops the process and disconnects standard input from the keyboard. It does, however, still send standard output and standard error to the screen. You can put a suspended job in the background and restart it by using the `bg` command followed by the job number. You do not need to specify the job number when there is only one suspended job.

Redirect the output of a job you run in the background to keep it from interfering with whatever you are working on in the foreground (on the screen). Refer to “Control Operators: Separate and Group Commands” on page 341 for more detail about background tasks.

Only the foreground job can take input from the keyboard. To connect the keyboard to a program running in the background, you must bring the program to the foreground. To do so, type `fg` without any arguments when only one job is in the background. When more than one job is in the background, type `fg` or a percent sign (`%`), followed by the number of the job you want to bring to the foreground. The shell displays the command you used to start the job (**promptme** in the following example), and you can enter input the program requires to continue.

```
$ `fg` 1
  `promptme`

```

# ## KILL: ABORTING A BACKGROUND Job

The interrupt key (usually CONTROL-c) cannot abort a background process because the keyboard is not attached to the job; you must use `kill` (page 465) for this purpose. Follow `kill` on the command line with either the PID number of the process you want to abort or a percent sign (`%`) followed by the job number.

If you forget a PID number, you can use the `ps` (process status) utility (page 374) to display it. The following example runs a `find` command in the background, uses `ps` to display the PID number of the process, and aborts the job using `kill`:

```
$ `find / -name memo55 > mem.out &`
  `[1]` 18228
$ `ps` | `grep find`
  `18228 pts/10  00:00:01 find`
$ `kill` 18228
  `[1]+ Terminated      find / -name memo55 > mem.out`
$ 
```

If you forget a job number, you can use the `jobs` command to display a list of jobs that includes job numbers. The next example is similar to the previous one except it uses the job number instead of the PID number to identify the job to be killed. Sometimes the message saying the job is terminated does not appear until you press RETURN after the RETURN that executes the `kill` command.