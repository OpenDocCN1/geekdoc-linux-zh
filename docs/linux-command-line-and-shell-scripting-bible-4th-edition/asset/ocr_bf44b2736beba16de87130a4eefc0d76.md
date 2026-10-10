your cron table, use the -e parameter. When you do that, the crontab command starts a text editor (**Chapter 10**, “Working with Editors”) with the existing cron table (or an empty file if it doesn't yet exist).

# Viewing *cron* directories

When you create a script that has less precise execution time needs, it is easier to use one of the preconfigured *cron* script directories. There are four basic directories: hourly, daily, monthly, and weekly.

```
```
$ ls /etc/cron.*

1y
/etc/cron.daily:
@anacron apt-compat cracklib-runtime logrotate [...] 
appport bsdmainutils dpkg man-db [...]

/etc/cron.hourly:

/etc/cron.monthly:
@anacron

/etc/cron.weekly:
@anacron man-db update-notifier-common
$
```
```

Thus, if you have a script that needs to be run one time per day, just copy the script to the daily directory and *cron* executes it each day.

# Looking at the anacron program

The only problem with the *cron* program is that it assumes that your Linux system is operational 24 hours a day, 7 days a week. Unless you're running Linux in a server environment, this may not necessarily be true.

If the Linux system is turned off at the time a job is scheduled to run in the *cron* table, the job doesn't run. The *cron* program doesn't retroactively run missed jobs when the system is turned back on. To resolve this issue, many Linux distributions include the anacron program.

If anacron determines that a job has missed a scheduled running, it runs the job as soon as possible. This means that if your Linux system is turned off for a few days, when it starts back up any jobs scheduled