That’s when I wrote logit (Listing 7.1). logit is a simple shell script that “ages” any system accounting or log files by nightly renaming the current day’s file to add an extension (e.g., syslog would become syslog.1). At the same time, extensions from previously aged files are incremented (e.g., syslog.1 becomes syslog.2, syslog.2 becomes syslog.3, etc.).

After a log file becomes n days old, it is purged. Thus, any file specified in the variable LOGFILE will be aged until OLD, and then removed from the system. I keep log files around for a week (Figure 7.1). Each aged file is named with the .n extension displaying its current age. syslog.6 is the oldest syslog file and will be purged next.

# Listing 7.1 The logit shell script ages any system accounting on log files.

```
#!/bin/sh
#
# Move today's system log files to yesterday's,
# and yesterday's to the day before's, etc.
# Then, mail the contents of yesterday's.

for LOGFILE in /usr/adm/isdn.log /usr/adm/syslog
do
    OLD=6 # Logs older than current.
    while [ $OLD -gt 1 ]
    do
        NEW=`expr $OLD - 1`
        mv $LOGFILE.$NEW $LOGFILE.$OLD
        OLD=$NEW
    done
    mv $LOGFILE $LOGFILE.$OLD 2> /dev/null
    touch $LOGFILE 2> /dev/null
done

kill -HUP `cat /etc/syslog.pid` # Restart syslog.d

nohup /usr/bin/mailx -s "SYSLOG Status" root </usr/adm/syslog.1 &
nohup grep "Security Error" /usr/adm/isdn.log.1 \
| /usr/bin/mailx -s "ISDN Status" root &
```