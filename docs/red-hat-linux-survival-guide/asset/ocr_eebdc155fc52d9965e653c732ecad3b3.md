For example, to rotate the log files syslogd creates, or to remove old files from the /tmp directory, you can choose to run a process daily or weekly. The cron facility allows you to create a recurring task schedule. In fact, it was not so long ago that there was no atd daemon, and all at jobs were run via a program called atrun, which in turn was run via the cron facility.

The cron facility includes the crond daemon, which the init process launches. crond reads task schedules from /etc/crontab and from files in the /var/spool/cron directory. The latter directory stores schedule files (often called crontab, or cron table) for normal users allowed to run cron jobs. As a superuser, you can specify a list of users that are allowed to run cron jobs in an /etc/cron.allow file. Similarly, you can explicitly deny cron access to users by specifying their names in an /etc/cron.deny file. Both files use a simple, one username per line format. If you allow users to run cron jobs, they can use the crontab utility to create job schedules; for example, they can run crontab -e to create and edit their cron job entries. A cron job specification has the following format:

```
minute(s) hour(s) day(s) month weekday username command argument(s)
```

Table 9-8 describes the first five time-specification fields.

# Table 9-8 cron Time-Specification Fields

| Fields | Description | Range |
|---|---|---|
| Minutes(s) | One or more minutes in an hour. You can specify a comma-separated list of minutes. | 0-59 |
| Hour(s) | One or more hours in a day. You can specify a comma-separated list of hours. | 0-23, where 0 is midnight |
| Day(s) | One or more days in a month. You can specify a comma-separated list of days. | 1-31 |
| Month(s) | One or more months in a year. You can specify a comma-separated list of months. | 1-12 |
| Weekday(s) | One or more days in a week. You can specify a comma-separated list of days. | 1-7, where 1 is Monday |

For any of the fields in Table 9-8, you can use “*” as a wildcard. For example, the following command states that /some/script runs every first minute of every hour, every day, every month, and every weekday:

```
01 * * * * root /some/script
```