Once a job has been successfully run, you will receive a status message similar to the following:

```
Commands will be executed using /usr/sbin/csh
Job 47180555.a at Fri Feb 23 10:13:43 2001
```

The following options may be used with the at command:

+   - -c option  Indicates that a command should run with csh
+   - -f <Filename> option  Tells at to use the file and not standard input as the job
+   - -k option  Indicates that a command should run with ksh
+   - -l option  Lists all scheduled jobs
+   - -m option  Notifies the user's mail when job completes
+   - -q option  Lets you specify a queue to put the job in
+   - -r id option  Removes a job with the ID specified by id
+   - -s option  Indicates that the job should run with sh
+   - time option  Runs the job at time specified

The following arguments can also be used with the at command options and are allowed by the C shell:

+   - atq argument  When used with the -c option, will list jobs according to queue order, creation date, and time. If used with the -n option, will display the number of jobs in the queue.
+   - atrm argument  Removes jobs already in queue. If used with option -a, will remove all jobs from queue. If used with option -f (force), will suppress all informational messages, and if used with -l, will interactively inquire about each job before it is removed.
+   - job id argument  Reports job IDs when jobs are originally scheduled by the at command.
+   - jobs argument  When used with option -l, lists the process IDs of each job.
+   - kill argument  Terminates a process or sends special signals to processes. If used with the -1 option, lists all signals. If stat has specified an exit status, the terminating signal will be displayed. If used with the -s signal option, specifies the signal to send to the process.
+   - nice argument  Runs a command with modified scheduling for better CPU usage. If used with the -n option, it sets priority to n, where n is 1 through 19; 1 is the highest priority, 19 the lowest, and the default is 10.