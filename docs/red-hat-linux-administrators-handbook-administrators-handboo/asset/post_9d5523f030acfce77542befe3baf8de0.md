
## Table A-2 Continued

| Options | Description |
|---|---|
| W | Show output in wide format. Normally, output is truncated if it cannot fit in a line. Using this option, you can prevent truncation. |
| Txx | Show processes that are associated with xx tty device. |
| X | Show processes without controlling tty. |

A few examples of using ps options are provided next.

To see all the processes you are running at any time, run the following:

```
ps u
```

An example of the output of the preceding command is shown here:

```
USER PID %CPU %MEM SIZE RSS TTY STAT START TIME COMMAND
kabir 18 0.0 0.8 1596 1040 p5 S 08:41 0:00 -tcsh
kabir 135 0.0 0.8 1560 1040 p7 S 09:03 0:00 -tcsh
kabir 852 53.8 0.6 1604 788 p8 R 09:33 0:04 perl ./eatcpu.pl
kabir 855 0.0 0.3 848 848 p7 R 09:34 0:00 ps u
```

This shows all the processes that are running for a user called kabir. Notice that ps itself is listed in the output. The first two lines show that kabir is running two tcsh shell sessions. The third line is very interesting, because it shows that a Perl script called eatcpu.pl is utilizing approximately 53.8 percent of the CPU. The STAT flags indicate that the Perl script and the ps utility are the only running (or runnable) processes here. By looking at the TTY field, you can tell which process is attached to which tty.

In the next example, ps is told to display all the processes (excluding the one not associated with any controlling tty):

```
ps au
```

To find out what processes are owned by a particular user, run

```
ps au | grep username
```

where *username* is the name of the actual user.

For example, ps au | grep sheila will show all the interactive processes (processes associated with a tty) being run by a user called sheila. Typically, normal users are not allowed to run daemon processes or processes that are not associated with a tty. However, if you just want to find out whether any such processes exist for any user, run

```
ps aux
```

The x option tells ps to list processes that are detached from terminals. You can identify these processes by looking at the TTY field, which displays a ? character instead of a shortened name of a tty device such as p7 (/dev/ttyp7).

To find the PID of a process's parent, you can run

```
ps l PID
```

where *PID* is the PID of the process.

For example, if you want to find the parent of a process with PID 123, run ps l 123, and the parent's PID will be listed in the PPID field of the report.

To determine what initial environment variables are available to processes, run

```
ps e
```

The environment information is appended to the COMMAND field.

## top

Using top, you can monitor process activity in real time. The top screen is automatically updated to provide a fresh look at the running state of the system. Here are the descriptions for the first five header lines displayed by top.

- Line 1. The uptime line, which shows the current time of the system, how long the system has been up since the last reboot, how many users are currently on the system, and three load average numbers. The load averages are the average numbers of processes ready to run during the last 1, 5, and 15 minutes.
- Line 2. The process statistics line that shows the total number of processes running at the time of the last top screen update. This line also shows the number of sleeping, running, zombie, and stopped processes.
- Line 3. Displays CPU statistics, which include percentage of CPU time used by the user, system, niced, and idle processes.
- Line 4. Provides memory statistics, which include total available memory, free memory, used memory, shared memory, and memory used for buffers.
- Line 5. Provides virtual memory or swap statistics, which include total available swap space, used swap space, free swap space, and cached swap space. The rest of the lines are similar to a ps-generated report.

Using top, you can identify which processes are using most of your resources, simply by looking at the few entries in the ps-like output. The process that consumes the second-most resources is the top utility itself! When you run top to monitor other processes, top takes some resources to run, but you still get a good idea about which process is consuming how much resources. To exit top, type 'q' at any time.

## Task Automation Commands

The commands discussed in this section show you how to run unattended tasks.

### at

The at utility allows you to queue a command for execution at a later time. For example, to run the disk usage summary generator utility called du at 8:40 p.m., you can run at as follows:

```
at 20:40
```

The at command displays a prompt such as at>, where you can enter the du command as follows:

```
at> du -a > /tmp/du.out
```

Here, the output of du is directed to a file. After you enter the command (the du command, in this example), at displays the prompt again. You can press Ctrl+D to exit. You will see a message similar to the one here:

```
at> <EOT>
warning: commands will be executed using /bin/sh
job 1 at 1999-12-06 20:40
```

This means that at has scheduled the du -a > /tmp/du.out job to be run by the at daemon (atd) at 8:40 p.m., 12/06/1999. You can use a wide variety of time formats to specify the time of execution. For example, instead of saying at 20:40, you can say at 8:40pm, as well. You can also specify the date along with the time. For example, 8:40pm feb 23, 10am + 5 days, 12:30pm tomorrow, midnight, and noon are all valid time specifications.

The scheduled job is run via the atd daemon process, which is started by init for run level 3 (multiuser mode). If you want to restrict use of the at facility, you can create an /etc/at.allow file and list all the users who are allowed to run it. Remember to enter a single username per line. Any user not listed in the allow file is refused access to the at facility. On the other hand, if you want to deny only a few users but allow the rest, you can create a similar file called /etc/at.deny. All usernames listed in this file are denied at access.

### atq

This command is used to verify that your at job is in the job queue. When you run this command it shows the currently scheduled jobs in the queue. All the scheduled jobs are stored in the /var/spool/at directory.

### atrm

To stop a scheduled at job, you can run the atrm command to remove a job. You need to know the job sequence number to remove a job with atrm. To find out what jobs you have scheduled, run the atq command. To delete any job, use atrm job#. For example, to remove job #1, run atrm 1.

### crontab

The crontab command is used to create and modify cron job settings. For example, if a user is allowed to run cron jobs, he can run crontab -e to create and edit cron job entries. A cron job specification has the following format:

```
minute(s) hour(s) day(s) month weekday username command argument(s) .
```

The first five time specification fields are discussed in Table A-3.

## Table A-3 Cron Time Specification Fields

| Fields | Description | Range |
|---|---|---|
| Minute(s) | One or more minutes in an hour. You can specify a comma-separated list of minutes. | 0-59 |
| Hour(s) | One or more hours in a day. You can specify a comma-separated list of hours. | 0-23, where 0 is midnight |
| Day(s) | One or more days in a month. You can specify a comma-separated list of days. | 1-31 |
| Month | One or more months in a year. You can specify a comma-separated list of months. | 1-12 |
| Weekday | One or more days in a week. You can specify a comma-separated list of days. | 1-7, where 1 is Monday |

For any of the fields shown in Table A-3, you can use * as a wildcard. The following is an example cron job specification:

```
01 * * * root /some/script
```

This states that /some/script is to be run every first minute of every hour, every day, every month, and every weekday. The script will be run as the root user. To run this script every ten minutes, a cron job such as the following can be defined:
