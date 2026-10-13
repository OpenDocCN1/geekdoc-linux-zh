You can see that this script executes the updatedb command to build your system's locate database (see Hour 4, "Reading and Navigation Commands").

The cron command also searches the /var/spool/cron directory for personal crontab files with users' names. These files are created with the crontab command, found under the /usr/bin directory, and are used by your users to schedule their own regular tasks.

How do you tell cron when to run these scripts, and how do you know that that locatedb script is run at 5:50 a.m. each day? Read on to see the format of the cron commands.

# Managing User cron Scheduling

The /etc/crontab file is for scheduling regular, systemwide tasks. However, OpenLinux enables users to create their own cron schedules. As the root operator, if you want to enable your users to use the crontab command to create personal cron files under the /var/spool/cron directory, you first create two files: /etc/cron.allow and /etc/cron.deny. Under the /etc/cron.allow file, insert the root operator name, root, and the names of any users you want to enable access to the cron daemon. Because neither of these files exists in the default OpenLinux installation, all users have access to personal cron files. You can create files for your users with the crontab command, or users can create their own.

![](bbox=[0.07, 0.64, 0.18, 0.73])

> Always use the crontab command's -u command-line option. If you run crontab while running as root (after using the su command) and don't use this option, you receive a usage error message.

The next section shows you the format of the crontab file and the difference between the format of a cron entry for your Linux system and for individual users.

# Setting Schedules with the crontab Command

The format of crontab entries is detailed in the crontab manual page under section 5. To see the manual page, use the following:

```
# man 5 crontab
```

This page provides specifications for crontab entries. However, to make things simpler, I'll give you some examples and at the end of this hour, some samples you can use. In general, the fields of an entry are as follows:

```
minutes hour day of month month day of week command
```