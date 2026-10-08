# STARTING COMMANDS AUTOMATICALLY 289

To execute every program Sunday, you can specify the entry shown in Listing 10.36. You can use either numbers or fully spelled names to represent months and days of the week. cron recognizes the three-character abbreviations of the English names of months days. If you use this notation, enumerations are no longer allowed.

```
0 ** sun clean_up
```

Listing 10.36 Executing a job once a week.

More information on cron and its possibilities can be found in the man page. LINUX generally uses the highly commendable Vicie cron by Paul Vieix which has several extensions with respect to the standard cron.

# 10.4.4 Cron and systems that run only part-time

The program cron expects the system to run all the time. If this is not the case, for example because the system is turned off overnight, cron jobs that should have been started during that time will be missed. For a system that runs most of the time this is not harmful, sometime next night, week or month the cleanup jobs will run. If a system is turned off every evening, this may be a big problem. A lot of jobs for system administration the pruning of log files, removing old cached data and so on are planned for night or at the weekend. These jobs will be missed and log files may grow until the disk is filled.
The program anacron will help in case the file /etc/ancrontab contains the jobs that should be started after a certain number of days. Jobs that need to be scheduled more often can be run by anacron. Besides, anacron cannot guarantee the execution of on a given day.
If the system is turned on and lots of jobs to be started, the system may be easily overloaded. In the second column of the file /etc/ancrontab you define the number of minutes that anacron waits until the job is started.
Listing 10.37 below shows an example that is used on the Debian distribution.

| These replace cron's entries |
| #day min | command |
| 1 | 5 | cron.daily nice run-parts --report /etc/cron.daily |
| 7 | 10 | cron.weekly nice run-parts --report /etc/cron.weekly |
| 30 | 15 | cron.monthly nice run-parts --report /etc/cron.monthly |

Listing 10.37 The file /etc/ancrontab.