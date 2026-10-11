Cron is a time-based job scheduler in Unix-like operating systems. It enables users to schedule jobs (commands or shell scripts) to run periodically at fixed times, dates, or intervals.

# ### Cron Daemon

The cron daemon (`crond`) runs in the background and checks for scheduled tasks every minute. It reads the crontab files to determine which commands to execute.

# ### Crontab Files

Crontab (cron table) is a file containing the schedule of cron entries to be run at specified times. There are two types of crontab files:

+   1. **System-wide crontab:** Located at `/etc/crontab`
+   2. **User-specific crontabs:** Typically stored in `/var/spool/cron/`

# ### Crontab Syntax

A crontab file consists of lines of six fields:

```
```
 * * * * * command_to_execute
 | | | | |
 | | | | +---- Day of the week (0 - 7) (Sunday = 0 or 7)
 | | | +------ Month (1 - 12)
 | | +-------- Day of the month (1 - 31)
 | +---------- Hour (0 - 23)
 +------------ Minute (0 - 59)
```
```

Each field can contain: