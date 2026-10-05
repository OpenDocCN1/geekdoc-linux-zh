# RUNNING A COMMAND IN THE BACKGROUND

The [1] following the command line indicates that the shell has assigned job number 1 to this job. The 22092 is the PID of the first command in the job. When this background job completes execution, you see the message

```
[1]+ Done  ls -l | lpr
```

(In place ls -l, the shell may display similar to ls --color=always -l. This difference is due to the fact that ls is aliased [346] to ls --color=always.)

# MOVING A JOB FROM THE FOREGROUND TO THE BACKGROUND

You can suspend a foreground job (stop it from running) by pressing the suspend key, control-z. The shell then stops the process and disconnects standard input from the keyboard. You can put a suspended job in the background and restart it using the bg command followed by the job number. You do not need to specify the job number when there is only one stopped job.

Only the foreground job can take input from the keyboard. To connect the key board to a program running in the background, you must bring it to the foreground. Do so, type fg without any arguments when only one job is in the background. When more than one job is in the background, type fg, or a percent sign (%), followed by the number of the job you want to bring into the foreground. The shell displays the command you used to start the job (prompt in the following example), and you can enter any input the program requires to continue:

```
bash $ fg 1
promptme
```

Redirect the output of a job you run in the background to keep it from interfering with whatever you are working on in the foreground (on the screen). Refer to “Separating and Grouping Commands” on page 303 for more detail about background tasks.

# ABORTING A BACKGROUND JOB

The interrupt key (usually CONTROL-C) cannot abort a background process; you may use kill (page 455) for this purpose. Follow kill on the command line with either the PID of the process you want to abort or a percent sign (%) followed by the job number.

If you have a PID, you can use the ps (process status) utility (page 328) to display it. The following examples run tail -f outline command (the -f [follow] option allows you to tail outline and display new lines as they are written to the (file) as a background job, use ps to display the PID of the process, and aborts the job with:

```
$ tail -f outline &
[1] 18228
$ ps | grep tail
18228 pts/4    00:00:00
$ kill 18228
[1]+ Terminated
$ tail -f outline
```