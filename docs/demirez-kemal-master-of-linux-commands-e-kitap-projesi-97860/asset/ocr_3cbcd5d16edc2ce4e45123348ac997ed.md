# 270 | Master Linux Commands

# Cron-Crontab

On the Linux operating system, it is possible to edit some of the work you want to do in specific time range. Means, you can delete some log files on time you scheduled, and you can schedule any processyou want. It is possible to schedule every job with cron service.

You can use service cron status command to get information about the status of your cron service.

```
root@kemal:~# service cron status
● cron.service - Regular background program processing daemon
 Loaded: loaded (/usr/lib/system/cron.service; enabled)
 Active: active (running) since Tue 2015-11-22 18:23:24 EET; 2h18min ago
 Docs: mancron(8)
 Main PID: 520 (cron)
 Cgroup: L520 /usr/sbin/cron -f
```

Crontab command is used to edit the scheduled jobs. So crontab files can be edited with the crontab command. Cron application configuration file is /etc/crontab file.

```
root@kemal:~# cat /etc/crontab
# /etc/crontab: system-wide crontab
# Unlike any other crontab you don't have to run the 'crontab'
# command to install the new version when you edit this file
# and files in /etc/cron.d. These files also have username fields,
# and none of the other crontabs do.
SHELL=/bin/sh
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin
# hour mon dom user command
17 + * * * root
25 6 * * * root test -x /usr/sbin/anacomll || ( cd /66 run-parts --repor
t /etc/cron.daily
47 6 * * * root test -x /usr/sbin/anacomll || ( cd /66 run-parts --repor
52 6 * * * root test -x /usr/sbin/anacomll || ( cd /66 run-parts --repor
t /etc/cron.monthly
#nroot@kemal:~#
```

After this brief introduction we will know how to use the crontab command to make arrangements and regulations. Some distributions open cron file using vim. (So, it opens the cron file based on the user who gives the cron command) and after the changes made and quit

![](bbox=[0.493, 0.915, 0.506, 0.933])