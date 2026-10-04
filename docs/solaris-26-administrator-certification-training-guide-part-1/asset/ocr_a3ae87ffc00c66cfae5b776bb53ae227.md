The following sample crontab command entry displays a reminder in the user's console window at 5 p.m. on the 1st and 15th of every month.

```
0 17 1,15 * * echo Handing Timesheet > /dev/console
```

crontab files are found in the /var/spool/cron/crontabs directory. Several crontab files besides root are provided during SunOS software installation and are also located in this directory. Other crontab files are named after the user accounts in which they are created, such as bill, glenda, miguel, or nicole. They are also located in the /var/spool/cron/crontabs directory. For example, a crontab file named root is supplied during software installation. Its contents include these command lines:

```
10 3 * * 0,4 /etc/cron.d/logchecker
10 3 * * 0 /usr/lib/newsyslog
15 3 * * /usr/lib/fs/nfs/nfssfind
1 2 * * * [ -x /usr/sbin/rtc ] && /usr/sbin/rtc -c > /dev/null 2>&1
```

The first command line instructs the system to run logchecker at 3:10 on Sunday and Thursday nights. The second command line schedules the system to run newsyslog at 3:10 every Sunday morning. The third command line orders the system to execute nfssfind daily at 3:15 in the morning. The fourth command line instructs the system to check for daylight savings time and makes corrections if necessary. If there is no RTC time zone or no /etc/rtc_config file, this entry will do nothing.

The cron daemon handles the automatic scheduling of crontab commands. Its function is to check the /var/spool/cron/crontab directory every 15 minutes for the presence of crontab files. It checks for new crontab files or changes to existing ones, reads the execution times listed within the files, and submits the commands for execution at the proper times.

# How to Create or Edit a crontab File

Creating an entry in the crontab file is as easy as editing a text file using your favorite editor. The procedure is as follows:

+   1. (Optional) To create or edit a crontab file belonging to root or another user, become superuser.
2. Create a new crontab file, or edit an existing one, by typing
   `crontab -e`
3. Add command lines to the file, following the syntax described in Table 10-7.
4. Save the changes and exit the file. The crontab file is placed in /var/spool/cron/crontabs.
5. Verify the crontab file by typing
   `crontab -l`

The system responds by listing the contents of the crontab file.