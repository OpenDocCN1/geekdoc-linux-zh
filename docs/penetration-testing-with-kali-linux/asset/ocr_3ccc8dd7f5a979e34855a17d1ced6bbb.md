# OffSec

```
total 60K
drwx-xr-x 2 root root 4.0K Aug 18 09:05
drwx-xr-x 12 root root 12K Aug 18 12:37 ..
-rwx-r--r- 1 root root 102 Oct 11 2019 .placeholder
-rwx-xr-x 1 root root 311 May 19 2019 Anacron
drwx-xr-x 1 root root 359 Aug 8 2020 apache
drwx-xr-x 1 root root 1.5K Dec 7 2020 apt-comp
drwx-xr-x 1 root root 355 Dec 29 2017 bsdminutils
drwx-xr-x 1 root root 384 Dec 31 2018 cracklib-runtime
drwx-xr-x 1 root root 1.2K Apr 18 2019 dpkg
drwx-xr-x 1 root root 2.2K Feb 28 2019 logostrate
drwx-xr-x 1 root root 1.1K Feb 10 2019 man-db
drwx-xr-x 1 root root 249 Sep 27 2017 password
```

```
/etc/cron.hourly:
total 28K
drwx-xr-x 2 root root 4.0K Aug 16 04:17
drwx-xr-x 12 root root 12K Aug 18 12:37 ..
-rwx-r--r- 1 root root 102 Oct 11 2019 .placeholder
drwx-xr-x 1 root root 311 May 19 2019 Anacron
```

```
/etc/cron.weekly:
total 28K
drwx-xr-x 2 root root 4.0K Aug 16 04:26
drwx-xr-x 12 root root 12K Aug 18 12:37 ..
-rwx-r--r- 1 root root 102 Oct 11 2019 .placeholder
drwx-xr-x 1 root root 312 May 19 2019 Anacron
drwx-xr-x 1 root root 813 Feb 10 2019 man-db
```

```
joe@debian-privesc:- $
```

Listing the directory entries, we notice several tasks scheduled to run daily.

It is worth noting that system administrators add their own scheduled tasks in the /etc/crontab file. These tasks should be inspected carefully for file permissions, since tasks in this particular file run as root. To view the current scheduled jobs, we can run crontab followed by the -l parameter.

```
joe@debian-privesc:- crontab -l
# Edit file to introduce tasks to run by cron.
#
# Each task to run has to be defined by a single line
# indicating with different fields when the task will be run
# and what command to run for the task
#
# To define the time you can provide concrete values
# minute (m), hour (h), day of month (dom), month (mon), year (year)
# and day of week (dow) or use '*' in these fields (for 'any').
#
```