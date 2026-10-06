# Understanding the Role of cron

The cron program is a daemon, it runs continuously, looking for events that cause it to spring into action. Unlike most daemons, which are network servers, cron responds to temporal events. Specifically, it "wakes up" once a minute, examines configuration files in the /var/spool/cron and /etc/cron.d directories and the /etc/crontab file, and executes commands specified by these configuration files if it matches the time listed in the files.

There are two types of cron jobs: system cron jobs and user cron jobs. System cron jobs run as root and perform system-wide maintenance tasks. By default, most Linux distributions include system cron jobs that clean out old log rotations (as described in "Rotating Log Files"), and so on. You can add to this repertoire, repeat, as described shortly. Ordinary users can create user cron jobs, which might run user program on a regular basis. You can also create a user cron job as root, which might be handy if you need to perform some task not supported by the system cron jobs, which are scheduled rather rigidly.

One of the critical points to remember about cron jobs is that they run unsupervised. Therefore, you shouldn't call any program in a cron job if that program requires user input. For instance, you not run a text editor in a cron job, but you might run a script that automatically manipulates text files, such as log files.

# Creating System Cron Jobs

The /etc/crontab file controls cron jobs. This file normally begins with several lines that set environment variables, such as PATH and MAILTO (the former sets the path, and the latter is the address to programs' output is mailed). The file contains several lines that resemble the:

```
0 4 * * * root-parts /etc/cron.daily
```

This line gives five fields that specify the time. The fields are, in the minute (0–59), the day of the month (1–31), the month (1–12), and the day of the week (0–7; both 0 and 7 correspond to Sunday). For the month and day-of-the-week values, you can use the first three letters of the name rather a number, if you like.

![](bbox=[0.147, 0.723, 0.235, 0.793])

> A useful mnemonic for the time fields is that the first four are ordered in increasing size. The day of the week doesn't fit neatly within this pattern and so is placed outside of—that, in the fifth field.

In all cases, you can specify multiple values in several ways:

+   * An asterisk (*) matches all possible values.
* A list separated by commas (such as 0,6,12,18) matches any of the specified values.
* Two values separated by a dash (--) indicate a range, inclusive of the end points. For instance, 9–17 in the hour field specifies a time from 9:00 a.m. to 5:00 p.m.