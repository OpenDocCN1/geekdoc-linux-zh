
Notice that you **must** use the `nice` command **on the same line** as the command you are starting. The output from the `ps` command confirms that the `nice` value (column NI) has been set to `10`.

```
$ ps -p 16462 -o pid,ppid,ni,cmd
   PID   PPID  NI  CMD
 16462   1630  10 /bin/bash ./jobcontrol.sh
$ 
```

The `nice` command causes the script to run at a lower priority. However, if you try to increase the priority of one of your commands, you might be in for a surprise:

```
$ nice -n -5 ./jobcontrol.sh > jobcontrol.out &
[2] 16473
$ nice: cannot set niceness: Permission denied
```

```
$ ps -p 16473 -o pid,ppid,ni,cmd
   PID   PPID  NI  CMD
 16473   1630   0 /bin/bash ./jobcontrol.sh
$ 
```

The `nice` command prevents normal system users from increasing the priority of their commands. Notice that the job does run, even though the attempt to raise its priority with the `nice` command failed. Only the `root` user or users with `superuser` privileges can elevate a job's priority.

You don't have to use the `-n` option with the `nice` command. You can simply type the priority, preceded by a dash:

```
$ nice -10 ./jobcontrol.sh > jobcontrol.out &
[2] 16520
$ 
```

```
$ ps -p 16520 -o pid,ppid,ni,cmd
   PID   PPID  NI  CMD
 16520   1630  10 /bin/bash ./jobcontrol.sh
$ 
```

However, this can get confusing when the priority is a negative number, because a double-dash is required. It's best just to use the `-n` option to avoid confusion.

## Using the renice command

Sometimes, you'd like to change the priority of a command that's already running on the system. The `renice` command helps in this situation. It allows you to specify the PID of a running process to change its priority:

```
$ ./jobcontrol.sh > jobcontrol.out &
[2] 16642
$ 
```

```
$ ps -p 16642 -o pid,ppid,ni,cmd
   PID   PPID  NI  CMD
 16642   1630   0 /bin/bash ./jobcontrol.sh
$ 
```

```
$ renice -n 10 -p 16642
16642 (process ID) old priority 0, new priority 10
$
$ ps -p 16642 -o pid,ppid,ni,cmd
  PID  PPID  NI CMD
 16642  1630  10 /bin/bash ./jobcontrol.sh
$
```

The `renice` command automatically updates the scheduling priority of the running process. As with the `nice` command, the `renice` command has some limitations for those without superuser privileges—you can only `renice` processes that you own, and only to a lower priority. However, the `root` user account and those users with superuser privileges can use the `renice` command to change any process to any priority.

## Running Like Clockwork

When you start working with scripts, you may want to run a script at some time in the future—usually at a time when you're not there. The Linux system provides ways to run a script at a preselected future time: the `at` command, the `cron` table, and `anacron`. Each method uses a different technique for scheduling when and how often to run scripts. The following sections describe each of these methods.

## Scheduling a job using the at command

The `at` command allows you to specify one future time when the Linux system will run a script. The `at` command submits a job to a queue with directions on when the shell should run the job.

The `at` daemon, `atd`, runs in the background and checks the job queue for jobs to run. Many Linux distributions start this daemon automatically at boot time, but some (such as Red Hat–based distributions) don't even have the package installed. If your distribution doesn't have it, and you'd like to install it (see Chapter 9, “Installing Software”), the package name is, as you might suppose, `at`.

The `atd` daemon checks a special directory on the system (usually `/var/spool/at` or `/var/spool/cron/at/jobs`) for jobs submitted using the `at` command. By default, the `atd` daemon checks this directory every 60 seconds. When a job is present, the `atd` daemon checks the time the job is set to be run. If the time matches the current time, the `atd` daemon runs the job.

The following sections describe how to use the `at` command to submit jobs to run and how to manage these jobs.

## Understanding the at command format

The basic `at` command format is pretty simple:

```
at [-f filename] time
```

By default, the `at` command submits input from *STDIN* to the queue. You can specify a filename used to read commands (your script file) using the `-f` parameter.

The `time` parameter specifies when you want the Linux system to run the job. If you specify a time that has already passed, the `at` command runs the job `at` that time on the next day.

You can get pretty creative with how you specify the time. The `at` command recognizes lots of different time formats:

- A standard hour and minute, such as `10:15`
- An a.m./p.m. indicator, such as `10:15PM`
- A specific named time, such as `now`, `noon`, `midnight`, or `teatime` (4 p.m.)

In addition to specifying the time to run the job, you can include a specific date using a few different date formats:

- A standard date format, such as `MMDDYY`, `MM/DD/YY`, or `DD.MM.YY`
- A text date, such as `Jul 4` or `Dec 25`, with or without the year
- A time increment:
    - `Now + 25 minutes`
    - `10:15PM tomorrow`
    - `10:15 + 7 days`

> **Tip**
> Several different date and time formats are available for use with the `at` command. All of them are conveniently described in the `/usr/share/doc/at/timespec` file.

When you use the `at` command, the job is submitted to a *job queue*. The job queue holds the jobs submitted by the `at` command for processing. There are 52 different job queues available for different priority levels. Job queues are referenced using lowercase letters, a through z, and uppercase letters A through Z, with A queue being a different queue than a queue.

The higher alphabetically the job queue letter, the lower the priority (higher *nice* value) the job will run under. By default, `at` jobs are submitted to the `at` job’s a queue. If you want to run a job at a lower priority, you can specify a different queue letter using the `-q` parameter. And if you want your jobs to consume as little CPU as possible compared to other current processes, you’ll want to put your job into the z (lowercase Z) queue.

## Retrieving job output

When an `at` job runs on the Linux system, there’s no monitor associated with the job. Instead, the Linux system uses the email address of the user who submitted the `at` job as *STDOUT* and *STDERR*. Any output destined to *STDOUT* or *STDERR* is mailed to the user via the mail system.

## Chapter 16: Script Control

Here's a simple example using the `at` command to schedule a job to run on a Rocky Linux distribution:

```
$ cat tryat.sh
#!/bin/bash
# Trying out the at command
#
echo "This script ran at $(date +"%B,%T")"
echo
echo "This script is using the $SHELL shell."
echo
sleep 5
echo "This is the script's end." 
# exit
$
$ at -f tryat.sh now
warning: commands will be executed using /bin/sh
job 9 at Mon Jul 14 16:19:00 2025
$ 
```

The `at` command displays the job number assigned to the job along with the time the job is scheduled to run. The `-f` option tells what script file to use, and the `now` time designation directs `at` to run the script immediately.

**Note**
Don't let that warning message from the `at` command cause you concern. Because this script has `#!/bin/bash` as its first line, the commands in this shell script will be executed by the Bash shell.

Using email for the `at` command's output is inconvenient at best. The `at` command sends email via the `sendmail` application. If your system does not use `sendmail`, you won't get any output! Therefore, it's best to redirect STDOUT and STDERR in your scripts (see Chapter 15) when using the `at` command, as the following example shows:

```
$ cat tryatout.sh
#!/bin/bash
# Trying out the at command redirecting output
#
Outfile=$HOME/scripts/tryat.out
#
echo "This script ran at $(date +"%B,%T")" > $outfile
echo >> $outfile
echo "This script is using the $SHELL shell." >> $outfile
echo >> $outfile
sleep 5 
```
