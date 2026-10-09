```
LogDir = /var/log
MailTo = root
Print = No
Range = yesterday
Detail = Low
```

These are highlighted in bold in the example. If we consult the man page for logwatch (run the command `man logwatch`), we can see that logwatch will check the log files in `/var/log`, looking for entries from the previous day, and e-mail a report containing a low level of detail to root.

If we've run our system for a few days and checked root mail, we'll have seen messages from logwatch, so how is this happening? Scheduling of unattended jobs on Red Hat Linux 9, and most other Unix flavors, is handled by the **cron daemon**. This daemon looks for files containing information about what to run and when to run it in the directories `/var/spool/cron` and `/etc/cron.d`, and in the file `/etc/crontab`. On Red Hat Linux 9, the `/etc/crontab` file is the one that is configured by default.

If we examine the contents of this file, we see that there are a few lines of environment information, and some other lines starting with numbers:

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

The numbers specify when cron should run the command described by the rest of the line. There are five fields which are, from left to right, minute, hour, day of month, month, and day of week. Where an asterisk is used, this means "I don't care". So the four scheduled jobs in the default Red Hat Linux 9 crontab are run at the following times:

| Scheduled Time | Interpretation |
| --- | --- |
| 01 * * * * | 01 minutes past each hour |
| 02 4 * * * | 04:02 every day |
| 22 4 * * 0 | 04:22 every Sunday (1=Monday, 2=Tuesday, etc., Sunday=0 or 7) |
| 42 4 1 * * | 04:42 on the 1st day of every month |