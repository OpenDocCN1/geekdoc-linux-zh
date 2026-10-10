# # /var/log/messages

This file contains informational messages logged by syslogd. To enable logging to this file, a line similar to the following must be present in /etc/syslog.conf:

```
   .info;mail.none;authpriv.none;cron.none	/var/log/messages

```

# # /var/log/secure

Processes that authenticate via username and password or other such mechanisms usually log to this file. Make sure this file is readable only by root. A line similar to the following must exist in /etc/syslog.conf:

```
   authpriv.*	/var/log/secure

```

# # /var/log/wtmp

This log file contains information about all the logins that have occurred on the host. It is not an ASCII file and therefore must be viewed using provided tools such as last. The following example shows the five most recent login or logout attempts:

```
(bash)$ last | head -5
       nit  pts/0   gateway   Fri Apr 11 10:12   still logged in
      anita  pts/1   nest      Thu Apr 10 21:14   still logged in
       ozzy   pts/1  gateway    Thu Apr 10 21:06 - 21:08 (00:01)
       kelly   pts/1  ftpserver  Thu Apr 10 20:01 - 20:02 (00:00)
       sharon pts/0  wireless   Thu Apr 10 16:34 - 21:26 (04:52)

```

# # /var/run/utmp

This file contains information about users that are currently logged on to the host. It is not an ASCII file and therefore must be viewed using tools such as w or who.

```
(bash)$ who
deepthi  pts/0     Apr 14 10:12 (intranet)
yash     pts/1     Apr 13 21:14 (egmoreftp)
natasha  pts/1     Apr 13 20:10 (punehttp)

```

# ## Log Rotation

Log files have the propensity to grow very fast and consume large amounts of disk space. For some environments, it makes sense to delete old log contents. To enable log rotations, most distributions use tools