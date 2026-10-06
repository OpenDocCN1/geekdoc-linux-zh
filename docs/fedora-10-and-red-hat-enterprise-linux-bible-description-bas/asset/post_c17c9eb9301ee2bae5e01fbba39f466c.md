
[content]
# Changing to a shutdown run level

Shutting down the machine is simply a change in run level. With that in mind, other ways to change the run level include the reboot, halt, poweroff, and shutdown commands. The reboot command, which is a symbolic link to the halt command, executes a shutdown -now, terminating all processes and rebooting the machine. The halt command executes shutdown -h now, terminating all processes and leaving the machine in an idle state (but still powered on).

Similarly, the poweroff command, which is also a link to the halt command, executes a change to run level 0, if the machine BIOS supports Advanced Power Management (APM), it will switch off the machine.

> NOTE: A time must be given to the shutdown command, either as +m (representing the number of minutes to delay before shutting down) or as hh:mm (an absolute time value, where hh is the hour and mm is the minute that you would like to shutdown to). Alternatively, now is commonly used to initiate the shutdown immediately.

# Scheduling System Tasks

Frequently, you need to run a process at specific times, or at off-hours. The at facility is designed to run such jobs at specific times. Jobs you submit in the directory /var/spool/at/ awaiting execution by the daemon are executed using the current environment that was active when the job was submitted. Any output or error messages that haven't been redirected are e-mailed to the user who submitted the job. The following sections describe how to use at, batch, and cron facilities to schedule tasks to specific times and also include ways of viewing which tasks are scheduled and deleting tasks.

# Using at.allow and at.deny

There are two access control files to limit which users can use the facility. The file /etc/at.allow contains a list of users who are granted access, and the file /etc/at.deny contains those who may not submit. If neither file exists (as in the default configuration), all users are allowed to use it. If you use either at, you aren't required to use both.

# Specifying when jobs run

There are many different ways to specify the time at which a job should run (most of which look like commands). Table 12-6 has a few examples. These are not complete commands — they only provide an example of how to specify the time that a job should run.

## Table 12-6: Samples for Specifying Times in at

| Command Line | When the Command Is Run |
|---|---|
| at now | The job is run immediately. |
| at now + 2 minutes | The job will start two minutes from the current time. |
| at now + 1 hour | The job will start one hour from the current time. |
| at now + 5 days | The job will start five days from the current time. |
| at now + 4 weeks | The job will start four weeks from the current time. |
| at now next minute | The job will start in exactly 60 seconds. |
| at now next hour | The job will start in exactly 60 minutes. |
| at now next day | The job will start tomorrow. |
| at now next month | The job will start on the same day and time month. |
| at now next year | The job will start on the same date and time next year. |
| at now next fri | The job will start at next Friday. |
| at teatime | The job will run at 4 p.m. Keywords now and midnight also be used. |
| at 16:00 today | The job will run at 4 p.m. today. |
| at 16:00 tomorrow | The job will run at 4 p.m. tomorrow. |
| at 2:45pm | The job will run at 2:45 p.m. on the current day. |
| at 14:45 | The job will run at 2:45 p.m. on the current day. |
| at 5:00 Apr 14 2008 | The job will begin at 5 a.m. on April 14, 2008. |
| at 5:00 14/04/08 | The job will begin at 5 a.m. on April 14, 2008. |

# Submitting scheduled jobs

The facility offers a lot of flexibility in how you can submit scheduled jobs. There are three ways to submit a job to the facility:

- **Piped in from standard input** — For example, the following command will attempt to build the Perl distribution from source in the early morning hours when the machine is likely to be busy, assuming the perl sources are stored in /tmp/perl:

```bash
echo "cd /tmp/perl; make; ls -al" | at 2am tomorrow
```

An ancillary benefit to this procedure is that a full log of the compilation process will be e-mailed to the user who submitted the job.

- **Read standard input** — If no command is specified, at will prompt you to enter commands at the at> prompt, as shown in the following example. You must indicate the end of the commands by pressing Ctrl+D, which signals an End of Transmission (<EOF) to at.

```bash
$ at 23:40
at> cd /tmp/perl
at> make
at> ls -al
at> <Ctrl-d>
```

- **Read from file** — When the -f command-line option is followed by a valid filename, the contents of that file are used as the commands to be executed, as in the following example:

```bash
$ -f /root/bin/runme now + 5 hours
```

This runs commands stored in /root/bin/runme in five hours. The file can be either a list of commands or a script to run in its own shell (that is, the file begins with /bin/bash or the name of another shell).

# Viewing scheduled jobs

You can use the atq command (effectively the same as at -l) to view list of pending jobs in the queue, showing each job's number, the date and time when the job is scheduled to run, and the queue in which the job is being run.

The most common queue names are a (which represents at queue) and b (which represents batch). All other letters can be used to specify priority. Here is an example of the output:

```bash
$ atq
1   Mon Oct 23 02:00 2023 a user1
2   Mon Oct 23 04:30 2023 a user2
3   Tue Oct 24 12:00 2023 b user3
```
```

# Deleting scheduled jobs

If you decide to cancel a particular job, you can use the atm command (equivalent to -d). Here is an example of the output:

```bash
$ atm -d 1
job 1 removed.
```

If you want to remove all jobs, you can use atrm command (equivalent to -r):

```bash
$ atrm -r
all jobs removed.
```
