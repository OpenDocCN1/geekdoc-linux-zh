
## Figure 10.1

The files `/etc/at.allow` and `/etc/at.deny` are used to control each user's ability to schedule at jobs.

If the users on your system are allowed to schedule jobs using the `at` command, you will need to periodically track the load that is being put on your system. You can use the `atq` command to see who has scheduled jobs, when they will run, and what kind of load they might put on your system. You also can use the `atrm` command to delete users' jobs when indicated.

> **Key Concept**
> In order to evaluate the system resources being used by `at`, use `atq` or `at -l` to see what jobs are scheduled. Use `atrm` or `at @d` to remove any scheduled job.

## batch Command

The `batch` command is the same as the `at -b` command and schedules a job to run one time. Its syntax is

```
batch [options] [time]
```

You use the same options with *batch* as you use with *at* (see Table 10.1).

If a time is not specified with *batch*, the job will run as soon as the system load is low. If a time is specified, the job will run as soon as the system load falls after the specified time.

*batch* examines the /proc/loadavg to check the system load. It executes when the average load falls below 1.5.

Commands that are run using *batch* or *at -b* run with a lower priority than when run in the background. Unlike background tasks, which are killed when you log off the system, *batch* commands continue until the system is shut down. In addition, *batch* sends you a mail message when the job is completed or if any errors occur.

## crontab

Often you will have a job that needs to be run on a regular basis. The *at* command allows you to schedule a reminder or job only once. To schedule recurring events, you can use the *crontab* command. Your scheduled events are then saved in a personal file.

The syntax for the *crontab* command is

```
crontab [options] [file] [username]
```

To use *crontab*, you first create a text file (with any name other than *crontab*) containing six fields, with a space between each field. The first five fields are minute, hour, day of the month, month, and day of the week; the sixth field is the command to be run. Table 10.2 shows the allowable values for these fields.

**Table 10.2** Allowable Values for Fields When Creating a cron Job

| Field | Values |
| :--- | :--- |
| minute | 0–59 |
| hour | 0–23 |
| day of month | 0–31 |
| month | 0–12 (or names) |
| day of week | 0–7 (0 or 7 is Sun, or use names) |

You can use an asterisk (*) to indicate commands are to be run in every instance of that field. Also note that days of the week can be defined by a number—with 0 or 7 for Sunday—or by name. In addition, times are specified in a 24-hour format. If you wanted to create a file containing who is logged on to your system every day at 10 a.m., you would type:

```
00 10 * * * who >> userList
```

You can specify ranges instead of specific days and times by using a hyphen (-). To specify non-inclusive values, use commas (,) to separate each value. If you wanted to run the script called myscript every Tuesday and Thursday at 1 a.m., you would enter the following in your file:

```
00 1 * * 2,4 myscript
```

After creating the file, you would need to install it by using the *crontab* command. After a job has been scheduled, it is referred to as a *cron job*. The syntax for the *crontab* command is

```
crontab [options] [filename]
```

The options that can be used with the *crontab* command are listed in Table 10.3.

### Table 10.3 Options to Be Used with the crontab Command

| Option | Action |
| :--- | :--- |
| -e | Creates or edits user's *crontab* file |
| -l | Displays user's *crontab* file |
| -r | Deletes user's *crontab* file |
| -u *username* | Specifies which user's *crontab* file to act on; can be used only by root |

The *crontab* command will create and install the cron file and save a copy of the original under the user's name in /usr/lib/crontab.

If you want to modify your cron configuration, edit this copy of the original file, and then install it using the *crontab* command as before. If you want to remove the file, use *crontab -r*.

### Key Concept

> Scheduling a job to run periodically entails first creating a file containing the commands and then scheduling it with the *crontab* command. Use *crontab -e* to edit the cron job or *crontab -r* to delete it.

The *crond* daemon checks several files to see whether there are jobs to be run. The first of these files is the /etc/crontab file, which looks like the following:

```
SHELL=/bin/bash
PATH=/sbin:/bin:/usr/sbin:/usr/bin
MAILTO=root
```

## run-parts

```
01 * * * * root run-parts /etc/cron.hourly
02 4 * * * root run-parts /etc/cron.daily
22 4 * * * 0 root run-parts /etc/cron.weekly
```

These are directories containing jobs to be run on a regular basis. run-parts is a script that executes each script in the designated directory. Some of these are

```
# ls -l /etc/cron.daily
-rwxr-xr-x  1 root root  51 Jun 29  1998 logrotate
-rwxr-xr-x  1 root root 102 Oct 11  1998 tetex.cron
-rwxr-xr-x  1 root root  54 Sep 10  1998 tmpwatch
-rwxr-xr-x  1 root root 557 Jul 29  1998 updatedb.cron
```

Each of these files is a script that performs periodic routine tasks such as updating the locatedb file used by the locate command (refer to Chapter 6, “Maintaining the Filesystem”) and rotating system logs (see the section “Rotating Logs” later in this chapter).

Another cron job that runs is the one that specifies when atrun is executed. This is necessary for at jobs to run. By default, atrun is executed every five minutes. You can change this to run more or less frequently or not at all.

Next, crond looks for schedules for usernames in the /var/spool/cron directory.

The crond daemon is responsible for running system and user cron jobs. It starts when Linux boots and wakes up every minute to see whether any jobs need to be run.

When constructing your cron jobs, you can include comments by starting a line with a pound sign (#). Comments can’t be on the same line as a command. A sample comment might look like

```
# mail any output to ‘hadden’
```

Users can edit only their own cron jobs. Root can edit any user’s cron jobs by using the -u option.

![](img/8dd1e68596303df43cb8ccf3197e8e53_255_0.png)

### Key Concept

The crond daemon checks every minute to see whether there are any jobs that need to be run. First it checks the /etc/crontab file and then it checks for any user scheduled jobs in the /var/spool/cron directory.

## Managing cron Jobs

If you have many users running cron jobs, your system could get overloaded. Therefore, you need to decide if and when you will allow users to schedule jobs. You can control which users are allowed to run cron jobs through the use of the /etc/cron.allow and /etc/cron.deny files.

If the /etc/cron.allow file exists, only the users listed in this file are allowed to run cron jobs. If cron finds the user’s name in the /etc/cron.allow file, it does not examine the /etc/cron.deny file.

If the /etc/cron.allow file does not exist but the /etc/cron.deny file does, any user not listed in the /etc/cron.deny file will be allowed to run cron jobs. If neither of these files exists, any user can run cron jobs. Figure 10.2 shows how the crontab uses the /etc/cron.allow and /etc/cron.deny files to determine whether a user can schedule cron jobs.

![](img/8dd1e68596303df43cb8ccf3197e8e53_256_0.png)

## Figure 10.2

How crontab evaluates a user’s ability to schedule a cron job.

Any user can view or edit her own cron jobs by using crontab -e. Users can delete their own jobs by using the crontab -r command.

As root, you can list any user’s cron jobs by using the crontab command with the -u username option. You also can delete any user’s cron jobs by using crontab with the -r option.

## System Logs

System information is stored in a variety of logs. These logs might be specific to an application or messages from several sources might be written to a single log file. It is also possible to log messages based on their importance as well as their source.

syslogd is the daemon that is responsible for logging system activity. It is usually started as part of one of the rc files when the system boots. See Chapter 2 for more information on rc files and the boot process.
