
execution of the command. As with the at facility, any output or error messages that haven’t been redirected elsewhere are e-mailed to the user that submitted the job.

Also like the at facility, cron includes two access control files designed to limit which users can use it. The file /etc/cron.allow contains a list of users that are granted access, and the file /etc/cron.deny contains a similar list of those who may not submit cron jobs. If neither file exists, all users are granted access to cron.

There are four places where a job can be submitted for execution by the cron daemon crond:

- The /var/spool/cron/username file. This method, where each individual user (indicated by username) controls his or her own separate file, is the method used on UNIX System V systems.
- The /etc/crontab file. This is referred to as the system crontab file, and was the original crontab file from BSD UNIX and its derivatives. Only root has permission to modify this file.
- The /etc/cron.d directory. Files placed in this directory have the same format as the /etc/crontab file. Only root is permitted to create or modify files in this directory.
- The /etc/cron.hourly, /etc/cron.daily, /etc/cron.weekly, and /etc/cron.monthly directories. Each file in these directories is a shell script that runs at the times specified in the /etc/crontab file (by default at one minute after the hour, at 4:02 a.m. every day, Sunday at 4:22 a.m., and 4:42 a.m. on the first day of the month, respectively). Only root is allowed to create or modify files in these directories.

The standard format of an entry in the /var/spool/cron/username file consists of five fields specifying when the command should run: minute, hour, day of the month, month, and day of the week. The sixth field is the actual command to be run.

The files in the /etc/cron.d directory and the /etc/crontab file use the same first five fields to determine when the command should run. However, the sixth field represents the name of the user submitting the job (because it cannot be inferred from the name of the file as in a /var/spool/cron/username directory), and the seventh field is the command to be run. Table 12-7 lists the valid values for each field common to both types of files.

### Table 12-7: Valid /etc/crontab Field Values

| Field Number | Field | Acceptable Values |
| :--- | :--- | :--- |
| 1 | minute | Any integer between 0 and 59 |
| 2 | hour | Any integer between 0 and 23 |
| 3 | day of the month | Any integer between 0 and 31 |
| 4 | month | Any integer between 0 and 12, or an abbreviation for the name of the month (Jan, Feb, Mar, Apr, May, Jun, Jul, Aug, Sep, Oct, Nov, Dec) |
| 5 | day of the week | Any integer between 0 and 7 (where both 0 and 7 can represent Sunday), or abbreviation for the day (Sun, Mon, Tue, Wed, Thu, Fri, Sat) |

An asterisk (*) in any field indicates all possible values for that field. For example, an asterisk in the second column is equivalent to 0,1,2 ... 22,23, and an asterisk in the fourth column means Jan,Feb,Mar ... Nov,Dec. In addition, lists of values, ranges of values, and increments can be used. For example, to specify the days Monday, Wednesday, and Friday, the fifth field could be represented as the list Mon,Wed,Fri. To represent the normal working hours in a day, the range 9-5 could be specified in the second field. Another option is to use an increment, as in specifying 0-31/3 in the third field to represent every third day of the month, or *5 in the first field to denote every five minutes.

Lines beginning with a # character in any of the crontab-format files are comments, which can be very helpful in explaining what task each command is designed to perform. It is also possible to specify environment variables (in Bourne shell syntax, e.g., NAME="value") within the crontab file. Any variable can be specified to fine-tune the environment in which the job will run, but one that may be particularly useful is MAILTO. The following line will send the results of the cron job to a user other than the one that submitted the job:

```
MAILTO=otheruser
```

If the following line appears in a crontab file, all output and error messages that haven't already been redirected will be discarded:

```
MAILTO=
```

## Modifying scheduled tasks with crontab

The files in /var/spool/cron should not be edited directly. They should only be accessed via the crontab command. To list the current contents of your own personal crontab file, type the following command:

```
$ crontab -l
```

All crontab entries can be removed with the following command:

```
$ crontab -r
```

Even if your personal crontab file doesn't exist, you can use the following command to begin editing it:

```
$ crontab -e
```

The file automatically opens in the text editor that is defined in your EDITOR or VISUAL environment variables, with vi as the default. When you're done, simply exit the editor. Provided there were no syntax errors, your crontab file will be installed. For example, if your user name is jsmith, you have just created the file /var/spool/cron/jsmith. If you add a line (with a descriptive comment, of course) to remove any old core files from your source code directories, that file may look similar to this:

```
# Find and remove core files from /home/jsmith/src
5 1 * * Sun,Wed find /home/jsmith/src -name core -exec rm {} \; > /dev/null 2>&1
```

The root user can access any user's individual crontab file by using the -u username option to the crontab command.

## Understanding cron files

There are separate cron directories set up to contain cron jobs that run hourly, daily, weekly, and monthly. These cron jobs are all set up to run from the /etc/crontab file. The default /etc/crontab file looks like this:

```
SHELL=/bin/bash
PATH=/sbin:/bin:/usr/sbin:/usr/bin
MAILTO=root
HOME=/

# run-parts
01 * * * * root run-parts /etc/cron.hourly
02 4 * * * root run-parts /etc/cron.daily
22 4 * * 0 root run-parts /etc/cron.weekly
42 4 1 * * root run-parts /etc/cron.monthly
```

The first four lines initialize the run-time environment for all subsequent jobs (the subshell in which jobs will run, the executable program search path, the recipient of output and error messages, and that user's home directory). The next five lines execute (as the user root) the run-parts program that controls programs that you may wish to run periodically.

run-parts is a shell script that takes a directory as a command-line argument. It then sequentially runs every program within that directory (shell scripts are most common, but binary executables and links are also evaluated). The default configuration executes programs in /etc/cron.hourly at one minute after every hour of every day; /etc/cron.daily at 4:02 a.m. every day; /etc/cron.weekly at 4:22 a.m. on Sundays; and /etc/cron.monthly at 4:42 a.m. on the first day of each month.

Here are examples of files that are installed in cron directories for different software packages:

- /etc/cron.daily/logrotate.cron — Automates rotating, compressing, and manipulating system logfiles.
- `/etc/cron.daily/makewhatis.cron` — Updates the whatis database (contains descriptions of man pages), which is used by the `man -k`, `apropos`, and `whatis` commands to find man pages related to a particular word.
- `/etc/cron.daily/slocate.cron` — Updates the `/var/lib/slocate/slocate.db` database (using the `updatedb` command), which contains a searchable list of files on the machine.
- `/etc/cron.daily/tmpwatch` — Removes files from `/tmp`, `/var/tmp`, and `/var/catman` that haven’t been accessed in ten days.
- `/etc/cron.hourly/diskcheck` — Checks available disk space on your hard drive each hour. Responds to low disk space based on settings in `/etc/diskcheck.conf`.

The `makewhatis.cron` script installed in `/etc/cron.weekly` is similar to the one in `/etc/cron.daily`, but it completely rebuilds the `whatis` database, rather than just updating the existing database.

Finally, in the `/etc/cron.d` directory are files that have the same format as `/etc/crontab` files.

## Summary

Shell scripts are an integral part of the Red Hat Linux system for configuring, booting, administering, and customizing Red Hat Linux. They are used to eliminate typing repetitive commands. They are frequently executed from the scheduling facilities within Red Hat Linux, allowing much flexibility in determining when and how often a process should run. And they control the start-up of most daemons and server processes at boot time.

The init daemon and its configuration file, `/etc/inittab`, also factor heavily in the initial start-up of your Red Hat Linux system. They implement the concept of run levels that is carried out by the shell scripts in `/etc/rc.d/init.d`, and they provide a means by which the machine can be shut down or rebooted in an orderly manner.

To have shell scripts configured to run on an ongoing basis, you can use the `cron` facility. Cron jobs can be added by editing `cron` files directly or by running commands such as `at` and `batch` to enter the commands to be run.
