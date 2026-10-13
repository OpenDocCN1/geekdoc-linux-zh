# Using the cron Daemon

The cron daemon, crond, is a program that starts after you boot Linux by the cron script in the /etc/rc.d/init.d directory on your system. This is done automatically, so you don't have to worry about starting the cron daemon every time you boot Linux. The crond program runs in the background and checks several files. The first is the crontab file in the /etc directory. A portion of this file reads as follows:

```
...
03 3 1 * * root [ -x /usr/sbin/cronloop ] && /usr/sbin/
->cronloop Monthly
04 4 * 6 root [ -x /usr/sbin/cronloop ] && /usr/sbin/
->cronloop Weekly
05 5 * * root [ -x /usr/sbin/cronloop ] && /usr/sbin/
->cronloop Daily
42 * * * * root [ -x /usr/sbin/cronloop ] && /usr/sbin/
->cronloop Hourly
...
```

As you can see, this is a list of commands that runs tasks hourly, daily, weekly, and monthly. The cronloop command is a shell script that looks in the /etc/cron.d directory and then runs assigned tasks (in the form of shell scripts) according to files found in the Monthly, Weekly, Daily, and Hourly directories under /etc/cron.d. The actual shell scripts are found in the lib directory under the /etc/cron.d directory.

For example, if you look at the contents of the Daily directory, you find a file called 50update-locatedb that is linked to a shell script called update-locatedb in the /etc/cron.d/lib directory. This shell script, according to the preceding Daily /etc/crontab entry, builds a new database for the locate command at 5:50 a.m. each day:

```
#!/bin/bash
# Make/update the file name database

. /etc/cron.d/lib/functions

TMPDIR=$(cronloop_mk_TMPDIR)
declare -rx TMPDIR

# remove TMPDIR on exit
trap cronloop_rm_TMPDIR EXIT

OMIT="/tmp /proc /mnt /var/tmp /var/spool /dev /net /auto /amd /NetWare"

/usr/bin/updatedb --prunepaths="$OMIT" --netuser=nobody 2> /dev/null
exit 0
```