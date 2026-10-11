the expiration schedule. If you’re not familiar with cron, check the relevant Unix manual pages using these commands:

```
$ man cron
$ man crontab
```

You might need to use another command to read about the crontab file format:

```
$ man 5 crontab
```

Suppose that you want to rotate a general query log named qlog by using the rotate_fixed_logs.sh script; that this script is installed in /home/mysql/bin, and that the log files are located in the /var/mysql/data directory. Log in as mysql, and then edit the mysql user’s crontab file using this command:

```
$ crontab -e
```

This command enables you to edit a copy of your current crontab file (which might be empty if no cron jobs have yet been set up). Add a line to the file that looks like this:

```
30 4 * * * /home/mysql/bin/rotate_fixed_logs.sh /var/mysql/data/qlog
```

This entry tells cron to run the script at 04:30 each day. You can vary the time or scheduling as desired; check the crontab manual page for the format of the entries. You’ll probably want to rotate the logs more frequently for a busy server that generates lots of log information than for one that is less active.

To make sure that the logs are flushed regularly (for example, to generate the next numbered binary log), you can schedule a mysqladmin flush-logs command to execute periodically by adding another crontab entry. You might need to list the full pathname to mysqladmin to make sure that cron can find it.

Automatic log file expiration is more problematic on Windows before MySQL 5.0.17/5.1.3, because you cannot rename the general query log or slow-query log file while the server has it open (see Section 12.5.7.1, “Rotating Fixed-Name Log Files”). This means that you cannot rotate any current log file without stopping and restarting the server, and there might be no time of day when you can guarantee that the server will not be in use.

# 12.5.7.4 Expiring or Rotating Log Tables

If the server is writing the general query log or slow-query log to tables in the mysql database, you can either truncate the tables or use a form of table rotation.

To truncate the tables, use these statements:

```
USE mysql;
TRUNCATE TABLE general_log;
TRUNCATE TABLE slow_log;
```

To rotate a log table, first create an empty copy. Then perform an atomic rename that “swaps out” the current table and replaces it with the empty one in a single statement:

```
USE mysql;
```