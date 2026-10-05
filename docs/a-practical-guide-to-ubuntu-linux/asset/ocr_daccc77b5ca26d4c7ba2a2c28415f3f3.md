# SCHEDULING TASKS 607

```
# m h dom dow user command
17 * * * root cd //usr/run-parts --report /etc/cron.hourly
25 6 * * root test -x /usr/sbin/anacron // ( cd //usr/run-parts --report /etc/cron.daily )
47 6 * * root test -x /usr/sbin/anacron // ( cd //usr/run-parts --report /etc/cron.weekly )
52 1 * * root test -x /usr/sbin/anacron // ( cd //usr/run-parts --report /etc/cron.monthly )

run-parts The run-parts utility runs all executable files in the directory named as its argument. The --report option affects commands that produce output. It sends the name of the command to standard output or error—whichever command sends its first output.
```

The daemon runs the line that begins with 17 at 17 minutes past every hour. First the command runs in (). The AND Boolean operator (&&) then executes run-parts, which executes all files in the /etc/cron.hourly directory.

The next lines first test whether the /usr/sbin/anacron is executable. If the file is executable, the OR boolean (||) causes the shell to ignore the rest of the line. Then, if anacron is installed and executable, this file executes only the files in the line, then in the cron.hourly directory. If anacron is not installed or is not executable, each of these three lines cds to /root and executes the files in the specified directory.

/etc/cron.d/anacron In addition to the /etc/crontab file, cron reads the files in /etc/cron.d for commands to execute. The following cases cron run the anacron script once a day at 7:30 AM. This script runs anacron if the system is up and not running batteries:

```
$ /etc/cron.d/anacron
# /etc/anacontab: crontab entries for the package anacron
SHELL=/bin/sh
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/bin:/usr/bin
# 30 7 * * root test -x /etc/init/anacron && /usr/sbin/invoke-rc.d anacron start >/dev/null
30 7 * * root start -q anacron //
```

The line that runs SysInit script is commented out and replaced with a line that runs the anacron daemon in /etc/init/anacron, which is triggered by the Upstart daemon ancron (page 432).

/etc/anacontab When anacron runs, it reads the commands it to execute from the /etc/anacontab file. The anacron utility keeps track of the last time each of its jobs was when it is called, it can tell which jobs to run. This file is where files in the cron.daily, cron.weekly, and cron.monthly /usr/sbin directories are executed on a system running anacron.

```
$ /etc/anacontab
# /etc/anacontab: configuration file for anacron
```

# See anacron(8) and anacontab(5) for details.
SHELL=/bin/sh
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin

```
# These replace cron's entries
1 5 cron.daily nice run-parts --report /etc/cron.daily
7 10 cron.weekly nice run-parts --report /etc/cron.weekly
@monthly 15 cron.monthly nice run-parts --report /etc/cron.monthly
```