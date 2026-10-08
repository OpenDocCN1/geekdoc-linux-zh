
# 70

## at, batch

### tomorrow

The day following the current day.
If no date is given, today is assumed if the given time is greater than the current time, and tomorrow is assumed if it is less. If the given month is less than the current month (and no year is given), next year is assumed.

### increment

The optional increment is a number preceded by a sign (+) and suffixed by one of the following: minutes, hours, days, weeks, months, or years. (The singular forms are also accepted.) The keyword next is equivalent to an increment number of +1. For example, the following are equivalent commands:

- - at 2pm +1 week
- at 2pm next week

## Usage

The format of the command line shown here is guaranteed only for the C locale. Other locales are not supported for midnight, noon, non, mon, alex, day, abxday, today, tomorrow, minutes, hours, days, weeks, months, years, and next.

Because the commands run in a separate shell invocation, running in a process group with no controlling terminal results in the loss of open file descriptors, and priority inherited from the invoking environment.

## at Examples

The following two examples produce the same result. The first example uses the -t to specify the time to run the script tryit.

```
castle at -f /export/home/winsor/bin/tryit -t 08281215
commands will be executed using /bin/csh
job 90427700.a at Fri Aug 28 12:15:00 1998
castle$
```

> Note - It is a good idea to use the full path for scripts scheduled with the at. Otherwise, like cron, at may not find the script when the time comes to run it.

The next example uses the timespec operand to specify the time to run the named tryit.

```
castle at -f /export/home/winsor/bin/tryit 1230:60
commands will be executed using /bin/csh
job 904278600.a at Fri Aug 28 12:30:00 1998
castle$
```

The following example lists the at-job-id for the two scheduled jobs.

```
castle@ -1
904277700.a Fri Aug 28 12:15:00 1998
904278600.a Fri Aug 28 12:30:00 1998
castle * *
```

# 71 at, batch

You can also schedule multiple at jobs by typing a timespec and pressing Return. Put one command on each line and press Return. Then type Control-D when you have scheduled all of the jobs. The following example schedules only one job.

```
castle@ at 1230pm
at> tryit
at> Control-D <EOT>
commands will be executed using /bin/csh
job 904278601.a at Fri Aug 28 12:30:00 1998
castle@
```

By default, results of at-jobs are e-mailed to the person who scheduled the job. The following screen shows the in-box with the results of the previous examples.

| Mailbox Message | Subject | Date and Time | Size |
| :--- | :--- | :--- | :--- |
| winsor@castle | Output from "at" job | Fri Aug 28 12:15 | 479 |
| winsor@castle | Output from "at" job | Fri Aug 28 12:30 | 479 |
| winsor@castle | Output from "at" job | Fri Aug 28 12:30 | 548 |

You can use the following sequence from a terminal.

```
$ -m 0730 tomorrow
at> sort < file > outfile
at> Control-D <EOT>
commands will be executed using /bin/sh
job 904380100.a at Sat Aug 29 07:30:00 1998
$
```

The following sequence demonstrates redirecting standard error to a pipe. It is useful in a command procedure. Note that the output of redirection is significant.

```
$ now + 5 min
at> << !! file1 2>&1 > outfile | mailx mygroup!
at> Control-D <EOT>
commands will be executed using /bin/sh
job 904280212.a at Fri Aug 28 12:56:52 1998
$ -1
90437000.a Sat Aug 29 07:30:00 1998
904280100.a Fri Aug 28 12:55:00 1998
904280212.a Fri Aug 28 12:56:52 1998
$
```

You can have a job reschedule it by calling at from within the at-job. For example

```
$ my.daily runs every day at now tomorrow < my.daily daily-processing
```

# 72 at, batch

You have quite a bit of flexibility in the spacing of the three portions of the C locale timespec, as long as there are no ambiguities. Examples of various times and operand include:

- - at 0815am Jan 24
- at 8:15amjan24
- at now '+ day'
- at 5 pm FRIDAY
- at '17
- utc+
- 30minutes

### batch Examples 

You can use the following sequence at a terminal. Notice that batch uses the at prompt and that batch job ends with a .b suffix.

```
$ batch
at> sort <file> outfile
at> Control-D <EOT>
commands will be executed using /bin/sh
job 904280755.b Fri Aug 28 13:00:55 1998
$
```

The following sequence demonstrates redirecting standard error to a pipe. It is useful in a command procedure. Note that the sequence of output redirection is significant.

```
$ batch
at> <<!
at> diff file1 file2 2>&1 outfile | mailx mygroup
at> Control-D <EOT>
commands will be executed using /bin/sh
job 904280755.b Fri Aug 28 13:00:55
$
```

### Environment Variables

See environ(5) for descriptions of variables that affect the execution of:

- SHELL: Determine the name of interpreter to be used.
- TZ: Determine the time zone. If unset or null, it uses the default. If specified, it uses that value.

# 102 at, batch

You have quite a bit of flexibility in the spacing of the three portions of the C locale timespec, as long as there are no ambiguities. Examples of various times and operand include:

- - at 0815am Jan 24
- at 8:15amjan24
- at now '+ day'
- at 5 pm FRIDAY
- at '17
- utc+
- 30minutes

### batch Examples 

You can use the following sequence at a terminal. Notice that batch uses the at prompt and that batch job ends with a .b suffix.

```
$ batch
at> sort <file> outfile
at> Control-D <EOT>
commands will be executed using /bin/sh
job 904280755.b Fri Aug 28 13:00:55 1998
$
```

# 103 at, batch

## atplot — Graphics Filters for Various Plotters

### Synopsis

```
`usr/ucb/plot [-]`
```

### Description

See plot(1).

## atq — Display the Queued at Times

### Synopsis

```
`usr/bin/atq [-c] [-n] [username...] own```

### Description

The atq command enables users to execute commands at a later date. Use the atq command to display for the current user at-jobs that were created by the at(1) command. Starting in the Solaris 8 release, if invoked by a user with solaris.jobs.admin, atq displays all jobs in the queue.

If you use no options, jobs are displayed in chronological order.

When superuser uses the atq command without specifying username the entire queue is displayed; when you specify a user name, jobs belonging only to the named user are displayed.

### Options

- -c Display the queued jobs in the order they were created (that is, the time that the at command was given).
- -n Display the total number of jobs in the queue.

### Examples

The following example shows output from the atq command with no arguments. The list shows the jobs only for the current user, winsor.

```
castle% atq
Rank Execution Date Owner Queue Queue Name
1st Aug 28, 1998 17:00 winsor 90429800.a a tryit
2nd Aug 29, 1998 01:00 winsor 90423600.a a tryit
3rd Aug 29, 1998 07:30 winsor 90434700.a a stdin
4th Aug 30, 1998 15:00 winsor 90446000.a a tryit
```

For comparison, the following example shows the output from the at -1 command, which also lists at and batch jobs in the queue.

```
castle% at -1
90427800.a Sat Aug 29 07:30:00 1998
90427800.a * Fri Aug 28 17:00:00 1998
```
