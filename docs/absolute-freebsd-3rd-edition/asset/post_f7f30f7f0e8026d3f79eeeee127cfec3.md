
/etc/crontab. Global cron entries can also be placed in /etc/cron.d and will be run as if they were part of /etc/crontab.

## User Crontabs vs. /etc/crontab

The purpose of /etc/crontab is different from that of individual users' crontabs. With /etc/crontab, root may specify which user will run a particular command. For example, in /etc/crontab, the sysadmin can say, “Run this job at 10 PM Tuesdays as root, and run this other job at 7 AM as www.” Other users can run jobs only as themselves. Of course, root can also edit a user's crontab.

Also, any system user can view /etc/crontab. If you have a scheduled job that you don't want users to know about, place it in a user crontab. For example, if you have an unprivileged user for your database, use that unprivileged user's crontab to run database maintenance jobs.

/etc/crontab is considered a FreeBSD system file. Don't overwrite it when you upgrade! One way to simplify upgrading /etc/crontab is to set your custom entries at the end of the file, marked off with a few lines of hash marks (#). The /etc/crontab file must end with a new line, or the last line won't get parsed and run. That's fine if your last entry is a comment, but not so good if it's a command.

Finally, while you edit /etc/crontab with a text editor, edit a user crontab with `crontab -e`.

## cron and Environment

Crontabs run in a shell, and programs might require environment variables to run correctly. You can also specify environment variables on the command line for each command you run from cron. cron doesn't inherit any environment variables from anywhere; any environment variables a program needs must be specified in the crontab. For example, here's the environment from /etc/crontab on a FreeBSD 12 system:

```
SHELL=/bin/sh
PATH=/etc:/bin:/sbin:/usr/bin:/usr/sbin
```

Yes, this is extremely minimal! Feel free to add environment variables as needed to user crontabs, but be conservative when changing /etc/crontab. If you need a custom environment variable, it’s safest to use a user crontab rather than /etc/crontab because many of the commands in /etc/crontab are for core system maintenance.

## Crontab Format

Beneath the environment statements, a user crontab is divided into six columns. The first five columns represent the time the command should run, as minute, hour, day of the month, month of the year, and day of the week, in that order. An asterisk (*) in any column means *every one*, while a number means *at this exact time*. Minutes, hours, and days of the week begin with 0, and days of the month and months begin with 1. Also, thanks to an ancient disagreement between AT&T and BSD, Sunday can be represented by either 7 or 0. After the time, list the command to be run at that time.

The /etc/crontab file, and files under /etc/cron.d, have one extra column: the user under which to run the command. It goes between the time specification and the command itself. Check out the many examples in /etc/crontab if you like.

## Sample Crontabs

Assume that we’re editing the crontab of an unprivileged user to schedule maintenance of a program. As /etc/crontab has column headings at the top, we’ll demonstrate user crontabs here. (To use these examples in /etc/crontab, just add the user before the command.) Here, we want to run the program /usr/local/bin/maintenance.sh at 55 minutes after each hour, every single hour:

```
55    *    *    *    *    /usr/local/bin/maintenance.sh
```

Asterisks tell cron to run this job every hour, on every day of the month, every month, and on every weekday. The 55 tells cron to run this job only at minute 55.

To run the same job at 1:55 PM every day, use the following:

```
55 13 * * * /usr/local/bin/maintenance.sh
```

Here, 13 represents 1:00 PM on the 24-hour clock, and 55 is the number of minutes past that hour.

One common mistake people make when using cron is specifying a large unit of time but missing the small one. For example, suppose you want to run the job every day at 8 AM:

```
* 8 * * * /usr/local/bin/maintenance.sh
```

This is wrong. Yes, the job will run at 8:00 AM. It will also run at 8:01, 8:02, 8:03, and so on, until 9 AM. If your job takes more than one minute to run, you’ll quickly bring your system to its knees. The correct way to specify 8:00 AM, and only 8:00 AM, is this:

```
0 8 * * * /usr/local/bin/maintenance.sh
```

To specify ranges of time, such as running the program once an hour, every hour, between 8 AM and 6 PM, Monday through Friday, use something like this:

```
55 8-18 * * 1-5 /usr/local/bin/maintenance.sh
```

To specify multiple exact times, separate them with commas:

```
55 8,10,12,14,16 * * * /usr/local/bin/maintenance.sh
```

More interestingly, you can specify fractions of time, or *steps*. For example, to run a program every 5 minutes, use:

```
*/5 * * * * /usr/local/bin/maintenance.sh
```

You can combine ranges with steps. To run the program every 5 minutes, but 1 minute after the previous example, use this:

```
1-56/5 * * * * /usr/local/bin/maintenance.sh
```

Control the day a job runs with two fields: the day of the month and the day of the week. If you specify both, the job will run whenever *either* condition is met. For example, tell cron to run a job on the 1st and the 15th of every month, plus every Monday, as follows:

```
55     13      *   1,15    1   /usr/local/bin/maintenance.sh
```

If your job has a nonstandard environment, set the environment on the command line just as you would in the shell. For example, if your program requires a `LD_LIBRARY_PATH` environment variable, you can set it thus:

```
55     *      *      *      *     LD_LIBRARY_PATH=/usr/local/mylibs ; /usr/local/bin/maintenance.sh
```

cron also supports special scheduling, such as *annually* or *daily*, with the `@` symbol. Most of these terms are best not used, as they can be ambiguous. While the machine knows exactly what they mean, humans tend to misunderstand! One useful crontab entry is for *whenever the system boots*, which is `@reboot`. This lets an unprivileged user run jobs when the system boots. Use the `@reboot` label instead of the time fields:

```
@reboot      /usr/local/bin/maintenance.sh
```

Crontabs and cron(8) let you schedule your work any way you like, eliminating the human being from many routine maintenance tasks.

## periodic(8)

Some system maintenance jobs should be run only on particular systems, but the way they should be run is identical across all hosts. That’s where periodic(8) comes in.

The periodic(8) command runs system functions on schedule, as cron(8) determines. Periodic checks a directory for a set of scripts to run. FreeBSD includes several directories for periodic tasks: /etc/periodic/daily, /etc/periodic/weekly, /etc/periodic/monthly, and /etc/periodic/security. Depending on which packages you install, you might have corresponding directories in /usr/local/etc/periodic. When cron runs, say, periodic daily, periodic(8) checks each script in each periodic/daily directory to see whether it should be run.

When you have spare time, I recommend perusing the periodic(8) scripts. You might find disabled maintenance scripts useful for your environment.

Which scripts should be run? The default settings are listed in /etc/defaults/periodic.conf, but you can override them in /etc/periodic.conf.

Once periodic(8) runs, it mails the results of the scripts to root on the local machine. Forward root's mail to someone who will actually read it.

Why use periodic(8)? It's all for system maintenance. /etc/crontab is for configuring your own system administration jobs. Using separate scripts allows the system upgrade process to replace tasks and packages to add and remove them.

All periodic(8) jobs run as root, though. If you have scheduled jobs that should be run by less privileged users, run them from the user's crontab.

Now that you have a decent understanding of the common small services provided by FreeBSD, let's go on to performance.
