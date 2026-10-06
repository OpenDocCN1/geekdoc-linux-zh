# One-Time Scheduling with at

When you want to schedule a command to execute once sometime in the future, whether it is 5 minutes or 6 months from now, at is the command you should use. at has a very simple and flexible syntax, allowing you to run multiple commands and specify the scheduled date and time in plain English. For example, to kill process ID 19072 at 5:30 p.m., you could type

```
# at 5:30 pm
at> kill -9 19072
at> <EOT>
commands will be executed using /bin/sh
job 1017441000.a at Fri Mar 29 17:30:00 2002
```

![](bbox=[0.198, 0.287, 0.802, 0.395])

> Mark the end of your command list by pressing CTRL-D. This will produce the <EOT> in the previous output, which means "End Transmission".

If you specify has already occurred, at schedules the command for the next day at the same time. You can also use relative times.

+   # date
Thu Mar 28 21:00:39 EST 2002
# at now + 1 hour
at> reboot
at> <EOT>
commands will be executed using /bin/sh
job 1017370846.a at Thu Mar 28 22:00:46 2002

![](bbox=[0.198, 0.574, 0.802, 0.682])

> The commands run from at under the current shell of the calling user. You can use -c (csh), -k (ksh), or -s (sh) to at to use a different shell.

After you submit an job, it joins the at queue for future execution. You have several options for manipulating the jobs in the queue. You can use the at -l command to list the at jobs submitted by the current user; root user can list jobs of other users by appending the username to the command. at -r job-id removes a pending job, where job-id as the identifier you submit a job (atm job-id does the same thing on Red Hat Linux).
Only root can remove jobs owned by others.

# Periodic Scheduling with cron

Although at can run a command once at a scheduled time, cron executes periodically according to schedules that you set in the crontab. A crontab is a file that stores scheduled cron jobs; crontab -e launches an editor to edit your crontab for the current user, and root can edit any user's crontab by appending -u username