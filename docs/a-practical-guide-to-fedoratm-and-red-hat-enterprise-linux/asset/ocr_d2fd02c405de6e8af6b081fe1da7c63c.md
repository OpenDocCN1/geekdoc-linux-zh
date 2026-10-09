script first tests to see if today's date is the same as the one held by the cron.daily file. If it is, anacron has already run today, so the script exits. Next the script tests to see if the system is running on AC power. If it is not, the script exits. Thus, if the cron.daily job has not been run today and if the system is running on AC power, the script executes anacron. The -s option causes anacron to run its jobs serially (not all at once).

+   /etc/anacrontab

When anacron is run, it reads the commands it is to execute from the /etc/anacrontab file. This file is where the files in the /etc/cron.daily, /etc/cron.weekly, and /etc/cron.monthly directories get executed on a system running anacron. The anacrontab file specifies how often anacron is to run one or more jobs, but has a different syntax from a crontab file. Within the anacrontab file, comments begin with a hashtag (#). Several variables that establish the environment a job runs in can appear within the anacrontab file: The SHELL and PATH environment variables are described on page 359; MAILTO determines which user receives output (via email) from jobs; RANDOM_DELAY delays the start of jobs by a random number of minutes up to the value of this variable; and START_HOURS_RANGE specifies the hours during which anacron can start a job.

A job entry in the anacrontab file has the following format:

```
period delay jobID command
```

where the period is the frequency in days (how often) that anacron executes the command, the delay is the number of minutes after anacron starts that it executes the command, and the jobID is the name of the file in /var/spool/anacron that anacron uses to keep track of when it last executed the command.

Following is the default anacrontab file. Based on the value of the variable named START_HOURS_RANGE, anacron can start jobs in this file between 3 AM and 10 PM (3-22).

```
$ cat /etc/anacrontab
# /etc/anacrontab: configuration file for anacron

# See anacron(8) and anacrontab(5) for details.

SHELL=/bin/sh
PATH=/sbin:/bin:/usr/sbin:/usr/bin
MAILTO=root
# the maximal random delay added to the base delay of the jobs
RANDOM_DELAY=45
# the jobs will be started during the following hours only
START_HOURS_RANGE=3-22

#period in days delay in minutes job-identifier  command
1    5    cron.daily    nice run-parts /etc/cron.daily
7    25    cron.weekly    nice run-parts /etc/cron.weekly
@monthly 45    cron.monthly    nice run-parts /etc/cron.monthly
```