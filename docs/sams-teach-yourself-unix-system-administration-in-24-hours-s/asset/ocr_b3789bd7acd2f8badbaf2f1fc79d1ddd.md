```
# happen is that they will temporarily corrupt the database...
[ -f $LOCKFILE ] && exit 0
trap "rm -f $LOCKFILE" EXIT
touch $LOCKFILE
makewhatis -w
exit 0
```

As is typical with these administrative scripts, both of these examples are essentially a single line long each. The first, 0anacron, calls anacron -u cron.weekly, and the second makewhatis.cron rebuilds the whatis database (used by man -k) every week with makewhatis -w.

4. The daily scripts are more interesting, and there are more of 'em, so let's see if there's anything unusual or otherwise exemplary:

```
# wc -l *
691 00.logwatch
8 00webalizer
12 0anacron
3 logrotate
13 makewhatis.cron
4 rpm
3 slocate.cron
5 sysstat
7 tmpwatch
746 total
```

The logwatch script is remarkably long at 691 lines. Otherwise, you can see that the scripts are all quite short. A few offer interesting techniques:

```
# cat 00webalizer
#!/bin/bash
# update access statistics for the web site

if [ -s /var/log/httpd/access_log ] ; then
/usr/bin/webalizer
fi
```

This is a common construct for an admin script—if a specific data file exists, run the program that analyzes it. In this case, it's checking to see if the Web server (httpd) received any hits. If it did, webalizer will produce some rudimentary log file analysis.

```
# cat slocate.cron
#!/bin/sh
renice +19 -p $$ >/dev/null 2>&1
/usr/bin/updatedb -f "nfs,smbfs,ncpfs,proc,devpts" -e "/tmp,/var/tmp,/usr/tmp,/afs,/net"
```