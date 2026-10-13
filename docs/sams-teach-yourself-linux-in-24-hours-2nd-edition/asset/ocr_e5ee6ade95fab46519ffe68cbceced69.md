As you can see, this is why the at command depends on the cron command: the cron command runs the atrun command, found under the /usr/sbin directory, each minute your system is up. The atrun command, in turn, searches the /var/spool/atjobs directory to look for jobs to run. For example, if the root operator creates a job at 14:46 for that day (2:30 p.m.), you see the following:

```
# at 14:46
at> echo Hello
at> <EOT>
warning: commands will be executed using /bin/sh
job 11 at 1998-12-14 14:46
```

```
# ls -l /var/spool/atjobs
total 1
-rwx------ 1 root root 842 Dec 14 14:43 a000b00e85b62
```

To create an at command, use the word at, followed by a time. After you press Enter, the at > prompt appears. You can then enter a command and press Enter. To quit entering commands and save your job, press Ctrl+D. The at command then tells you the job number and the date and time the command executes. As you can see in the atjobs directory listing after entering the command, there is a job waiting for the root operator.

![](bbox=[0.22, 0.7, 0.3, 0.78])

> You can get more specific information about waiting at jobs with the atq command. If you're the root operator, you see all the jobs your users have scheduled, instead of just the ones you've scheduled.

# Controlling the batch and at Commands

Now that you know how the at facilities run, how do you control how at works, and for whom, on your system? One way to control how at works on your OpenLinux system is to use the atrun command's -l (load average) option. This option controls any jobs submitted by users using the batch command (discussed in Hour 18 with the at command). You can limit when batch jobs are run by specifying a number lower than 1.5 (the default), which tells atrun to run batch jobs only when the system load average is low. The load average is determined by a value in the /proc/loadavg file while the system is running.

You can see the current load average with the following:

```
# cat /proc/loadavg
0.20 0.11 0.03 2/50 1228
```