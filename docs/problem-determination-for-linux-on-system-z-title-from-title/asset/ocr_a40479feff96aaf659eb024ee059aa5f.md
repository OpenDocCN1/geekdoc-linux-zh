activities among all of the processors are also reported. 2 mpstat displays more in-depth CPU statistics than iostat.

# Automatic sampling via the cron

The sadc command collects system utilization data and writes it to a file for later analysis. By default, the data is written to files in the /var/log/sa/ directory. The files are named sa<dd>, where <dd> is the current day's two-digit date.

The command sadc is normally run by the sa1 script. This script is periodically invoked by cron via the file sysstat, which is located in /etc/cron.d. The sa1 script invokes sadc for a single one-second measuring interval. By default, cron runs sa1 every 10 minutes, adding the data collected during each interval to the current /var/log/sa/sa<dd> file.

The sar command produces system utilization reports based on the data collected by sadc. As configured in Red Hat Linux, sar is automatically run to process the files automatically collected by sadc. The report files are written to /var/log/sa/ and are named sar<dd>, where <dd> is the two-digit representation of the previous day's two-digit date. The command sar is normally run by the sa2 script. This script is periodically invoked by the cron via the file sysstat, which is located in /etc/cron.d. By default, the cron runs sa2 once a day at 23:53, allowing it to produce a report for the entire day's data.

To activate the cron daemon, run the following command:

```
service crond start
```

To start the service for the indicated level:

```
chkconfig --level 123456 crond on
```

To check the status:

```
service --status-all |grep cron
chkconfig --list |grep cron
```

As soon as the cron daemon and the service are started, they use the definitions in /etc/cron.d/sysstat, as shown in Example 3-6.

# Example 3-6 Automatic sampling via the cron

```
# run system activity accounting tool every 10 minutes
*/10 * * * * root /usr/lib64/sa/sa1 1 1
# generate a daily summary of process accounting at 23:53
53 23 * * * root /usr/lib64/sa/sa2 -A
```