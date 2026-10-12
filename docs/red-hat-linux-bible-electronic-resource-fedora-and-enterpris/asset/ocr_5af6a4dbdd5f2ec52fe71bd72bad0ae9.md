execution of the command. As with the at facility, any output or error messages that haven’t been redirected elsewhere are e-mailed to the user that submitted the job.

Also like the at facility, cron includes two access control files designed to limit which users can use it. The file /etc/cron.allow contains a list of users that are granted access, and the file /etc/cron.deny contains a similar list of those who may not submit cron jobs. If neither file exists, all users are granted access to cron.

There are four places where a job can be submitted for execution by the cron daemon crond:

+   - The /var/spool/cron/username file. This method, where each individual user (indicated by username) controls his or her own separate file, is the method used on UNIX System V systems.
+   - The /etc/crontab file. This is referred to as the system crontab file, and was the original crontab file from BSD UNIX and its derivatives. Only root has permission to modify this file.
+   - The /etc/cron.d directory. Files placed in this directory have the same format as the /etc/crontab file. Only root is permitted to create or modify files in this directory.
+   - The /etc/cron.hourly, /etc/cron.daily, /etc/cron.weekly, and /etc/cron.monthly directories. Each file in these directories is a shell script that runs at the times specified in the /etc/crontab file (by default at one minute after the hour, at 4:02 a.m. every day, Sunday at 4:22 a.m., and 4:42 a.m. on the first day of the month, respectively). Only root is allowed to create or modify files in these directories.

The standard format of an entry in the /var/spool/cron/username file consists of five fields specifying when the command should run: minute, hour, day of the month, month, and day of the week. The sixth field is the actual command to be run.

The files in the /etc/cron.d directory and the /etc/crontab file use the same first five fields to determine when the command should run. However, the sixth field represents the name of the user submitting the job (because it cannot be inferred from the name of the file as in a /var/spool/cron/username directory), and the seventh field is the command to be run. Table 12-7 lists the valid values for each field common to both types of files.

# Table 12-7: Valid /etc/crontab Field Values

| Field Number | Field | Acceptable Values |
| :--- | :--- | :--- |
| 1 | minute | Any integer between 0 and 59 |
| 2 | hour | Any integer between 0 and 23 |
| 3 | day of the month | Any integer between 0 and 31 |
| 4 | month | Any integer between 0 and 12, or an abbreviation for the name of the month |