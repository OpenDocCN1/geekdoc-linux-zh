To move a background job into the foreground, use the fg builtin with a percent sign (%) followed by the job number as an argument. The following example moves job 2 into the foreground:

```
$ fg %2
```

You can also refer to a job by following the percent sign with a string that uniquely identifies the beginning of the command line to start the job. Instead of the preceding command, for example, you could have used fg %find or fg %f, because either one uniquely identifies job 2. If you follow the percent sign with a question mark and a string, the string matches itself over the command line. In the preceding example, %?ace also refers to job 2.

Often the job you wish to bring into the foreground is the only job running in the background or is the job that jobs lists with a plus (+). In these cases you can use fg without any arguments.

# bg: Sends a Job to the Background

To put the foreground job into the background, you must first suspend the job by pressing the suspend key (usually CONTROL-z). Pressing the suspend key stops the job immediately. Once the job is suspended, use the bg builtin to resume execution of the job, putting it in the background:

```
$ bg
```

If a background job attempts to read from the terminal, the shell stops it (puts it to sleep [pages 142 and 562]) and notifies you that the job has been stopped and is waiting for input. When this happens, you must move the job into the foreground so that it can read from the terminal. The shell displays the command line as it moves the job into the foreground:

```
$ sleep 5; cat > mytext &
[1] 1343
$ date
Sun Dec 7 11:58:20 PST 2003
[1]+ Stopped (tty input) ( sleep 5; cat >mytext )
$ fg
( sleep 5; cat >mytext
Remember to let the cat out!
CONTROL-D
```

In this example, the shell displays the job number and PID number of the background job as soon as it starts, followed by a prompt. This point user enters date, and its output appears on the screen. The shell waits until just it issues a prompt (after date has finished) to notify you that job 1 is waiting for input. The reason for this delay is so that the notice does not disrupt your work: the default