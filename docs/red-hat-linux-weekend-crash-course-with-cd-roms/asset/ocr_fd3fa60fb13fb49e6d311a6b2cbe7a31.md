The first field on each line shows the job number — the same number that the at command displays when you submit the job. The next field displays the year, month, day, and time of execution. The last field shows that the jobs are pending in the a queue.

# Canceling one-time jobs and receiving the output

If you want to cancel a job, use the atrm command to remove that job from the queue. When removing a job with the atrm command, refer to the job by its number as follows:

```
atrm 3
```

This deletes job number 3 scheduled for 3:00 a.m. August 16, 2000.

When a job executes, the output is mailed to you. Type mail to read your mail and view the output from your jobs.

# Scheduling Recurring Jobs

While the at command is good for running commands at a specific time, it’s not useful for running a program automatically at repeated intervals. You have to use crontab to schedule such recurring jobs. You need to do this, for example, if you want to back up your files to tape at midnight every day.

You schedule recurring jobs by placing job information in a file with a specific format and submitting this file with the crontab command. The cron daemon — crond — checks the job information every minute and executes the recurring jobs at the specified times. Because the cron daemon processes recurring jobs, such jobs are also referred to as cron jobs.

Any output from the job is mailed to the user who submits the job. (In the submitted job information file, you may specify a different recipient for the mailed output.)

As with the at command, two files control who can schedule cron jobs using crontab:

+   - `/etc/cron.allow` contains the names of the users who may submit jobs using the crontab command.
+   - `/etc/cron.deny` contains the names of users who are not allowed to submit jobs using the crontab command.

![](bbox=[0.03, 0.47, 0.12, 0.62])