# Listing 13-2 Continued

```
/usr/bin/rdist -p /usr/sbin/rdistd -oremove,nochkgroup,nochkmode,nochkowner,quiet -f /usr/local/rdist/rdist_distfile

# Remove the lock file
rm -f /tmp/rdist.lck

# Write the time and date in the log file
echo `date` > /tmp/rdist.log

# Exit the script
exit 0
```

This script is smart enough to detect in progress the redistribute.sh process by using a lock file, which can tell when a previous rdistribute.sh is already in progress and continuing. This can happen when numerous files are being updated over multiple servers. The script also accepts an argument called boot that can be used to clean up the lock file and the log file it creates during the boot process. The script should be called from /etc/rc.d/rc.local as follows:

```
/usr/local/rdistribute.sh boot
```

This script can be scheduled to run by a cron entry in /etc/crontab. For example, to run this script every hour, the following cron entry can be added in /etc/crontab:

```
01 * * * * updater /usr/local/rdistribute.sh > /dev/null
```

The cron daemon will run the script as updater. Alternatively, you can create a link to rdistribute.sh from /etc/cron.hourly (or /etc/cron.daily, /etc/cron.monthly, or what have you) as you see fit.