```
-rw-r--r-- 1 root root 1472087 Feb 6 04:02 /var/log/maillog.4
-rw-r--r-- 1 root root 171891 Feb 6 04:02 /var/log/messages.4
-rw-r-x--x-- 1 root root 0 Oct 12 08:41 /var/log/netconf.log.4
-rw-r-x--x-- 1 root root 23795 Jan 24 09:55 /var/log/samba/log.nmb.4
-rw-r--r-- 1 root root 2300 Feb 4 21:48 /var/log/secure.4
-rw-r--r-- 1 root root 0 Jan 30 04:02 /var/log/spooler.4
-rw-r--r-- 1 uucp uucp 0 Jan 30 04:02 /var/log/uucp/Debug.4
-rw-r-x--x-- 1 uucp uucp 0 Jan 30 04:02 /var/log/uucp/log.4
-rw-r-x--x-- 1 uucp uucp 0 Jan 30 04:02 /var/log/uucp/Stats.4
-rw-r--r-- 1 root root 130101 Jan 31 14:20 /var/log/xferlog.4
```

As you can see, some of these logs can get quite large in the course of a single month! If you don't need these files, you can safely delete them and free up disk space.

# Putting It Together with Automation

Linux comes with not only the tools you need to handle finding and deleting files, but also the software required to automate the process.

By using the cron daemon and your system's crontab table, you can set up Linux to automatically search for and delete unwanted files. Log in as root, and then use your favorite editor to open the /etc/crontab file. You might see something like this:

```
SHELL=/bin/bash

PATH=/sbin:/bin:/usr/sbin:/usr/bin

MAILTO=root
HOME=/

# run-parts

01 * * * * root run-parts /etc/cron.hourly

02 4 * * * root run-parts /etc/cron.daily

22 4 * * 0 root run-parts /etc/cron.weekly

42 4 1 * * root run-parts /etc/cron.monthly
```

The /etc/crontab file contains directions for the cron daemon, which is started when you boot Linux. This software, which runs in the background, looks to this file every minute for tasks to run.

In this example, the cron daemon looks into the /etc/cron.hourly directory every hour on the hour. Once a day at 4:02 a.m., it looks at /etc/cron.daily for tasks. Every Sunday at 4:22 a.m., it runs tasks in the /etc/cron.weekly directory. And on the first day of every month at 4:42 a.m., the daemon runs the tasks listed in /etc/cron.monthly.