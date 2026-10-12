
## Table 1-6 (continued)

| Filename | Content |
| --- | --- |
| /proc/mounts | List of mounted file systems |
| /proc/net | Directory with many subdirectories that contain information about networking |
| /proc/partitions | List of partitions known to the Linux kernel |
| /proc/pci | Information about PCI devices found on the system |
| /proc/scsi | Directory with information about SCSI devices found on the system (present only if you have a SCSI device) |
| /proc/stat | Overall statistics about the system |
| /proc/swaps | Information about the swap space and how much is used |
| /proc/sys | Directory with information about the system; you can change kernel parameters by writing to files in this directory (using this method to tune system performance requires expertise to do properly) |
| /proc/uptime | Information about how long the system has been up |
| /proc/version | Kernel version number |

## Scheduling Jobs in Fedora Core

As a system administrator, you may have to run some programs automatically at regular intervals or execute one or more commands at a specified time in the future. Your Fedora Core system includes the facilities to schedule jobs to run at any future date or time you want. You can also set up the system to perform a task periodically or just once. Here are some typical tasks you can perform by scheduling jobs on your Linux system:

- Back up the files in the middle of the night.
- Download large files in the early morning when the system isn't busy.
- Send yourself messages as reminders of meetings.
- Analyze system logs periodically and look for any abnormal activities.

You can set up these jobs by using the `at` command or the `crontab` facility of Fedora Core. In the next few sections, I introduce these job-scheduling features of Fedora Core.

### Scheduling one-time jobs

If you want to run one or more commands at a later time, you can use the at command. The atd daemon — a program designed to process jobs submitted using at — runs your commands at the specified time and mails the output to you.

Before you try the at command, you need to know that the following configuration files control which users can schedule tasks using the at command:

- /etc/at.allow contains the names of the users who may submit jobs using the at command.
- /etc/at.deny contains the names of users not allowed to submit jobs using the at command.

If these files aren’t present, or if you find an empty /etc/at.deny file, any user can submit jobs by using the at command. The default in Fedora Core is an empty /etc/at.deny file; with this default in place, anyone can use the at command. If you don’t want some users to use at, simply list their user-names in the /etc/at.deny file.

To use at to schedule a one-time job for execution at a later time, follow these steps:

1. **Run the at command with the date or time when you want your commands executed.**

   When you press Enter, the at> prompt appears, as follows:

   ```
   at 21:30
   at>
   ```

   This method is the simplest way to indicate the time when you want to execute one or more commands — simply specify the time in a 24-hour format. In this case, you want to execute the commands at 9:30 p.m. tonight (or tomorrow, if it’s already past 9:30 p.m.). You can, however, specify the execution time in many different ways (see Table 1-7 for examples).

2. **At the at> prompt, type the commands you want to execute as if typing at the shell prompt; after each command, press Enter and continue with the next command. When you finish entering the commands you want to execute, press Ctrl+D to indicate the end.**

![](img/9f89727199836b0f871f1745838aa8b2_445_0.png)

Book VI Chapter 1 Performing Basic System Administration

420 Scheduling Jobs in Fedora Core

Here is an example showing how to execute the `ps` command at a future time:

```
at> ps
at> <EOT>
job 1 at 2004-02-29 21:30
```

After you press Ctrl+D, the `at` command responds with a job number and the date and time when the job will execute.

**Table 1-7: Formats for the Time of Execution with the at Command**

| Command | When the Job Will Run |
|---|---|
| `at now` | Immediately |
| `at now + 15 minutes` | 15 minutes from the current time |
| `at now + 4 hours` | 4 hours from the current time |
| `at now + 7 days` | 7 days from the current time |
| `at noon` | At noontime today (or tomorrow, if already past noon) |
| `at now next hour` | Exactly 60 minutes from now |
| `at now next day` | At the same time tomorrow |
| `at 17:00 tomorrow` | At 5:00 p.m. tomorrow |
| `at 4:45pm` | At 4:45 p.m. today (or tomorrow, if it’s already past 4:45 p.m.) |
| `at 3:00 Aug 16, 2004` | At 3:00 a.m. on August 16, 2004 |

After you enter one or more jobs, you can view the current list of scheduled jobs with the `atq` command:

```
atq
```

The output looks similar to the following:

```
4       2004-08-16 03:00 a root
5       2004-10-26 21:57 a root
6       2004-10-26 16:45 a root
```

The first field on each line shows the job number — the same number that the `at` command displays when you submit the job. The next field shows the year, month, day, and time of execution. The last field shows the jobs pending in the queue named a.

If you want to cancel a job, use the `atrm` command to remove that job from the queue. When removing a job with the `atrm` command, refer to the job by its number, as follows:

```
atrm 4
```

This command deletes job 4 scheduled for 3:00 a.m. August 16, 2004.

When a job executes, the output is mailed to you. Type **mail** at a terminal window to read your mail and to view the output from your jobs.

### Scheduling recurring jobs

Although at is good for running commands at a specific time, it’s not useful for running a program automatically at repeated intervals. You have to use `crontab` to schedule such recurring jobs — for example, if you want to back up your files to tape at midnight every day.

You schedule recurring jobs by placing job information in a file with a specific format and submitting this file with the `crontab` command. The `cron` daemon — `crond` — checks the job information every minute and executes the recurring jobs at the specified times. Because the `cron` daemon processes recurring jobs, such jobs are also referred to as `cron` jobs.

Any output from a `cron` job is mailed to the user who submits the job. (In the submitted job-information file, you can specify a different recipient for the mailed output.)

Two configuration files control who can schedule `cron` jobs using `crontab`:

- `/etc/cron.allow` contains the names of the users who may submit jobs using the `crontab` command.
- `/etc/cron.deny` contains the names of users not allowed to submit jobs using the `crontab` command.

If the `/etc/cron.allow` file exists, only users listed in this file can schedule `cron` jobs. If only the `/etc/cron.deny` file exists, users listed in this file cannot schedule `cron` jobs. If neither file exists, the default Fedora Core setup enables any user to submit `cron` jobs.

To submit a `cron` job, follow these steps:

1. Prepare a shell script (or an executable program in any programming language) that can perform the recurring task you want to perform. You can skip this step if you want to execute an existing program periodically.
2. Prepare a text file with information about the times when you want the shell script or program (from Step 1) to execute, and then submit this file by using `crontab`.

You can submit several recurring jobs with a single file. Each line with timing information about a job has a standard format with six fields — the first five specify when the job runs, and the sixth field constitutes the actual command that runs. For example, here is a line that executes the *myjob* shell script in a user’s home directory at five minutes past midnight each day:

```
5 0 * * * $HOME/myjob
```

Table 1-8 shows the meaning of the first five fields. **Note:** An asterisk (*) means all possible values for that field. Also, an entry in any of the first five fields can be a single number, a comma-separated list of numbers, a pair of numbers separated by a dash (indicating a range of numbers), or an asterisk.

3. Suppose the text file *jobinfo* (in the current directory) contains the job information. Submit this information to *crontab* with the following command:

```
crontab jobinfo
```

That’s it! You are set with the *cron* job. From now on, the *cron* job runs at regular intervals (as specified in the job information file), and you receive mail messages with the output from the job.

To verify that the job is indeed scheduled, type the following command:

```
crontab -l
```

The output of the *crontab -l* command shows the *cron* jobs currently installed in your name. To remove your *cron* jobs, type **crontab -r**.

**Table 1-8: Format for the Time of Execution in crontab Files**

| Field Number | Meaning of Field | Acceptable Range of Values* |
| :--- | :--- | :--- |
| 1 | Minute | 0–59 |
| 2 | Hour of the day | 0–23 |
| 3 | Day of the month | 0–31 |
| 4 | Month | 1–12 (1 means January, 2 means February, and so on) or the names of months using the first three letters (Jan, Feb, Mar, Apr, May, Jun, Jul, Aug, Sep, Oct, Nov, Dec) |
| 5 | Day of the week | 0–6 (0 means Sunday, 1 means Monday, and so on) or the three-letter abbreviations of weekdays (Sun, Mon, Tue, Wed, Thu, Fri, Sat) |

*An asterisk in a field means all possible values for that field. For example, if an asterisk is in the third field, the job is executed every day.*
