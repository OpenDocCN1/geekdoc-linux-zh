
## 530 Part III: Administering Fedora RHEL

There are four places where a job can be submitted for execution by the cron daemon crond:

- The /var/spool/cron/username file — This method, where each individual user (indicated by username) controls his own separate file, the method used on UNIX System V.
- The /etc/crontab file — This is referred to the system crontab file, and was the original crontab file from BSD UNIX and its derivatives. Only root has permission to modify this file.
- The /etc/cron.d directory — Files placed in this directory have the same format as the /etc/crontab file. Only root is permitted to create or modify files in this directory.
- The /etc/cron.hourly, /etc/cron.daily, /etc/cron.weekly, and /etc/cron.monthly directories — Each file in these directories is a script that runs at the times specified in the /etc/crontab file (by default, one minute after the hour every hour; at 4:02 a.m. every Sunday; at 4:22 a.m.; and 4:42 a.m. every Monday). Only root is allowed to create or modify files in these directories.

The standard format of an entry in the /var/spool/cron/username file consists of five fields specifying when the command should run: minute, hour, day of the month, month, and day of the week. The sixth field is the actual command to run.

The files in the /etc/cron.d directory and the /etc/crontab file use the first five fields to determine when the command should run. However, the sixth field represents the name of the user submitting the job (because it cannot be inferred by the name of the file as in /var/spool/cron/username directory), and the seventh field is the command to be run.
Table 12-7 lists the values for each field to both types of file.

### Table 12-7: Valid /etc/crontab Field Values

| Field Number | Field | Acceptable Values |
|---|---|---|
| 1 | minute | Any integer between 0 and 59 |
| 2 | hour | Any integer between 0 and 23 |
| 3 | day of the month | Any integer between 0 and 31 |
| 4 | month | Any integer between 0 and 12, or an abbreviation for the name of the month (Jan, Feb, Apr, May, Jun, Jul, Aug, Sep, Oct, Nov, Dec) |
| 5 | day of the week | Any integer between 0 and 7 (where 0 can represent Sunday, 1 is Monday, 2 is Tuesday, and so on), or abbreviation for the day (Sun, Mon, Tue, Wed, Thu, Fri, Sat) |

## Chapter 12: Automating System Tasks 531

The latest version of cron (cronie and crontabs packages) includes the ability to indicate that a cron job be at boot time. Refer to the cron page (type **man 5 cron**) for information on using the reboot option to have a command run once at startup.

> NOTE: The cronie package replaces the older vix-cron.

An asterisk (*) in any field indicates all possible values for that field. For example, an asterisk in the second column is equivalent to 0,1,2 .. 22,23, and an asterisk in the fourth column Jan,Feb,Mar ... Nov,Dec. In addition, lists of values, ranges of values, and increments can be used. To specify the days Monday, Wednesday, Friday, the fifth field could be represented as the list Mon,Wed,Fri. To represent the normal working hours in a day, the range 9–17 could be specified in the second field. Another option is to use an increment, as in specifying 0–31 in the third field to represent every day of the month, or */5 in the first field to denote every five minutes.

Lines beginning with a # character in any of the crontab-format files are comments, which can be very helpful in explaining what task each command is designed to perform. It is also possible to specify environment variables (in Bourne syntax, for example NAME="value") within the crontab file. Any variable can be specified to fine-tune the environment in which the job runs, but one that may be particularly useful is MAILTO. The following line sends the results of the cron job to a user other than the one who submitted the job:

```
MAILTO=otheruser
```

If the following line appears in a crontab file, all output and error messages that haven’t already redirected will be discarded:

```
MAILTO=
```

## Scheduling scheduled tasks with crontab

The files in /var/spool/cron should not be edited directly. They should only be accessed via the crontab command. To list the current contents of your personal crontab file, type the following command:

```
$ crontab -l
```

All crontab entries can be removed with the following command:

```
$ crontab -r
```

Even if your personal crontab file doesn’t exist, you can use the following command to begin editing it:

```
$ crontab -e
```

## Part III: Administering Fedora and RHEL

The file automatically opens in the text editor that is defined in your EDITOR or VISUAL environment, vi as the default. When you're done, simply exit the editor. Provided there were no syntax errors, your crontab will be installed.

```
SHELL=/bin/bash
PATH=/usr/bin:/usr/sbin:/bin:/sbin
MAILTO=root
01 * * * * cron-hourly
02 * * * * cron-daily
22 * * * * cron-weekly
42 * * * * cron-monthly
```

Any variable can be specified to fine-tune the environment in which the job runs, but one that may be particularly useful is MAILTO. The following line sends the results of the cron job to a user other than the one who submitted the job:

```
MAILTO=otheruser
```

If the following line appears in a crontab file, all output and error messages that haven’t already redirected will be discarded:

```
MAILTO=
```

The files in /var/spool/cron should not be edited directly. They should only be accessed via the crontab command. To list the current contents of your personal crontab file, type the following command:

```
$ crontab -l
```

All crontab entries can be removed with the following command:

```
$ crontab -r
```

Even if your personal crontab file doesn’t exist, you can use the following command to begin editing it:

```
$ crontab -e
```

The file automatically opens in the text editor that is defined in your EDITOR or VISUAL environment, vi as the default. When you're done, simply exit the editor. Provided there were no syntax errors, your crontab will be installed.

```
SHELL=/bin/bash
PATH=/usr/bin:/usr/sbin:/bin:/sbin
MAILTO=root
01 * * * * cron-hourly
02 * * * * cron-daily
22 * * * * cron-weekly
42 * * * * cron-monthly
```

The directories /etc/cron.hourly, /etc/cron.daily, /etc/cron.weekly, and /etc/cron.monthly — Each file in these directories is a script that runs at the times specified in the /etc/crontab file (by default, one minute after the hour every hour; at 4:02 a.m. every Sunday; at 4:22 a.m.; and 4:42 a.m. every Monday). Only root is allowed to create or modify files in these directories.

The files in the /etc/cron.d directory and the /etc/crontab file use the first five fields to determine when the command should run. However, the sixth field represents the name of the user submitting the job (because it cannot be inferred by the name of the file as in /var/spool/cron/username directory), and the seventh field is the command to be run.
Table 12-7 lists the values for each field to both types of file.

## Chapter 12: Automating System Tasks 533

Here are examples of files that are installed in cron directories for different packages:

- /etc/cron.daily/logrotate.cron — Automates rotating, compressing, and manipulating system logs.
- /etc/cron.daily/whatis.cron — Updates the whatis database (contains man pages), which is used by the man -k, apropos, and whatis commands to find pages related to a particular word.
- /etc/cron.daily/slocate.cron — Updates the /var/lib/locate.db database (using updateddb command), which contains a search list of files on the machine.
- /etc/cron.daily/tmpwatch — Removes files from /tmp, /tmp, and /var/tmp that haven't been accessed in ten days.

The whatis.cron script installed in /etc/cron.weekly is similar to the one in /etc/cron.daily, but it completely rebuilds the whatis database, rather than just updating it.

Finally, in the /etc/cron.d directory are files that have the same format as /etc/crontab files.

> NOTE: If you are not comfortable working with cron from the command line, there is a KCron Scheduler window that comes in the kdeadmin package for managing cron tasks. To launch KCron, use kcron from a Terminal window.
