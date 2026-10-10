```
```
6   Fri Jun 19 16:53:00 2020 a  christine
7   Thu Jun 18 20:30:00 2020 a  christine
8   Thu Jun 18 17:54:00 2020 a  christine
$ 
```
```

The job listing from the atq command shows the job number, the date and time the system will run the job, and the job queue in which the job is stored.

# ## Removing jobs

After you know the information about what jobs are pending in the job queues, you can use the atrm command to remove a pending job. Just specify the job number you want to remove:

```
```
$ atq
1   Thu Jun 18 16:11:00 2020 a  christine
5   Fri Jun 19 16:00:00 2020 a  christine
6   Fri Jun 19 16:53:00 2020 a  christine
7   Thu Jun 18 20:30:00 2020 a  christine
8   Thu Jun 18 17:54:00 2020 a  christine
$ atrm 5
$ atq
1   Thu Jun 18 16:11:00 2020 a  christine
6   Fri Jun 19 16:53:00 2020 a  christine
7   Thu Jun 18 20:30:00 2020 a  christine
8   Thu Jun 18 17:54:00 2020 a  christine
$ 
```
```

You can only remove jobs that you submit for execution. Jobs submitted by others to at are off-limits for removal by you.

# ## Scheduling regular scripts

Using the at command to schedule a script to run at a future preset time is great, but what if you need that script to run at the same time every day or once a week or once a month? Instead of having to continually submit at jobs, you can use another feature of the Linux system.

The Linux system uses the cron program to allow you to schedule jobs that need to run on a regular basis. The cron program runs in the