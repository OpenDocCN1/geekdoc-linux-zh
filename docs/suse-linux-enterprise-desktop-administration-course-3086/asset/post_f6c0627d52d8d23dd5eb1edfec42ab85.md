
Table 10-19 shows some other commonly used commands and options for `at`.

| Command | Description |
|---|---|
| `atq` | Display defined jobs (including job numbers, which are needed to delete a job). |
| `atrm job_number` | Delete a job (using the job number). |

**Table 10-19**

![](img/9129877170834ca9d5fdac5319bf5f12_373_0.png)

## Exercise 10-4: Schedule Jobs with at and cron

In this exercise, schedule jobs with at and cron.

First, redirect the output of finger to `/var/log/messages` three minutes from the current time. Then, schedule the same job for tomorrow at noon. Then, schedule a program to run tomorrow at 2:00 p.m., and afterwards remove the job.

In the second part of the exercise, create a cron job as a normal user that logs the output of finger to `~/users/log` every minute.

## Detailed Steps to Complete This Exercise

- Part I: Schedule Jobs with at
- Part II: Schedule Jobs with cron

## Part I: Schedule Jobs with at

To schedule jobs with at, do the following:

1. From a terminal window on your GNOME desktop, switch to user root (`su -`, password `n0v3ll`).

2. Verify that the at service is running by entering
```
rcatd status
```

3. (Conditional) If the at service is not running, start the service by entering
```
rcatd start
```

4. Display the current date and time by entering
```
date
```

5. Three minutes from now, log to `/var/log/messages` who is logged in by entering
```
at hh:mm
/usr/bin/finger >> /var/log/messages
```

The above command redirects the output of finger to `/var/log/messages`. Make sure you have two `>` characters; if you have only one `>` character, existing entries in `/var/log/messages` will be removed.

6. Exit the `at` editor by pressing
`Ctrl+d`

7. View the scheduled `at` jobs by entering
`atq` (or `at -l`)

Notice the job number listed.

8. Wait for the 3 minutes to pass; then check the `/var/log/messages` file for the finger information by entering

```
tail /var/log/messages
```

Login information for geeko is listed at the end of the file.

9. Schedule the same job to run tomorrow at noon by entering
`at noon tomorrow`

At the at-prompt, enter

```
/usr/bin/finger >> /var/log/messages Ctrl+d
```

10. Schedule the date to be logged tomorrow at 2:00 p.m. to the `/var/log/messages` file by entering
`at 14:00 tomorrow`

At the at-prompt, enter

```
/bin/date >> /var/log/messages Ctrl+d
```

11. View the scheduled `at` jobs by entering
`atq` (or `at -l`)

Notice that the two jobs are listed, each with an individual job number.

12. Remove the job scheduled for tomorrow at 2:00 p.m. by entering
`atrm job number`

13. View the scheduled `at` jobs by entering
`atq` (or `at -l`)

Only the job scheduled for 12:00 p.m. is still listed.

## Part II: Schedule Jobs with cron

To schedule jobs with cron, do the following:

1. Open a terminal window.

2. Schedule a cron job as geeko by doing the following:
   a. Enter `crontab -e`.
   The vi editor is displayed for a cron table file (such as `/tmp/crontab.11743`).
   Press `i` to enter insert mode.

   b. Schedule a job to run every minute, using `finger` to record who is logged in currently. Have `finger` write its output to the `~/users.log` file by typing

   ```bash
   * * * * * /usr/bin/finger >> ~/users.log
   ```

   c. Press Esc.

   d. Save the file and exit the vi editor by entering

   ```bash
   :wq
   ```

   e. Watch the users.log file for a few minutes. To validate that it is being updated, enter

   ```bash
   tail -f ~/users.log
   ```

   f. When you finish watching the file update, press

   ```text
   Ctrl+c
   ```

3. View geeko’s crontab file by entering

```bash
crontab -l
```

4. Remove geeko’s crontab file by entering

```bash
crontab -r
```

5. Verify that the crontab file no longer exists by entering

```bash
crontab -l
```

6. Verify that the cron job you defined in Step 2 is no longer active by entering

```bash
tail -f ~/users.log
```

Notice that entries to users.log are no longer being added.

7. Press Ctrl+c.

## Summary

- To monitor the boot process, you can use YaST, view the output of the `dmesg` command, as well as view the contents of the `/var/log/boot.msg` file.

- Most hardware information is available within text files under the `/proc` directory. Alternatively, you can also use the `hwinfo`, `hwparm`, `fdisk`, `lspci`, and `sig` commands to view information regarding system hardware.

- General system information can be obtained using the `uptime`, `netstat`, and `uname` commands.

- The `df` command, `du` command, and GNOME System Monitor utility can be used to monitor disk usage.

- Most log files are stored in the `/var/log` directory and created by the Syslog daemon (syslog-ng) via entries in its configuration files. Text log files can be viewed using a text program such as `tail`.

- The `logrotate` program is run daily to archive log files using entries in the `/etc/logrotate.conf` file and application-specific information in the `/etc/logrotate.d` directory.

- You can monitor login activity using a variety of different command-line utilities, such as `who`, `w`, `finger`, `last`, and `lastlog`.

- Processes are programs that are executing on the system. User processes run in a terminal and are executed by users, whereas daemon processes are system services that do not run on a terminal.

- Every process has a PID, a PPID, and can possibly start an unlimited number of child processes.

- In addition to a PID, background processes have a job ID that you can use to control their execution. You can start any program in the background by appending the `&` character to the program command. This program can then be viewed using the `jobs` command or manipulated using the `fg` and `bg` commands.

- You can view processes within a desktop environment using the GNOME System Monitor, or at a command prompt by using the `ps`, `pstree`, and `top` commands.

- The GNOME System Monitor as well as the `kill`, `killall`, and `top` commands can be used to stop processes by sending them signals. Although there are many available signals, the default signal used by these commands is SIGTERM.

- You can affect the priority of a process by changing its nice value. All processes are started with a 0 nice value, which can be decreased to -20 (high priority) or increased to +19 (low priority). Only the root user can increase the priority of a process.

- To change the nice value of a program, you can use the `nice` command. To change the nice value of a process, you must use the `renice` command.

- Daemon process names typically end with d and contain a ? in the TTY column of ps command output. Signal-controlled daemons execute when a certain event occurs, whereas interval-controlled daemons run periodically on the system.

- You can start daemons by running the appropriate script in the `/etc/init.d` directory with the `start` argument, or by using the `rcdaemonname start` command.

- Commands can be scheduled to run at a later time using the `at` daemon.

- To schedule tasks to occur repetitively in the future, you must use the cron daemon and create a crontab (cron table). System tasks are scheduled to run using the `/etc/crontab` file. User tasks can be scheduled using the `crontab` command and are stored in the `/var/spool/cron/tabs` directory.

## Key Terms

- **&** — A special character used to start a program in the background.
- **/etc/at.allow** — A file that lists users who can use the at command.
- **/etc/at.deny** — A file that lists users who cannot use the at command.
- **/etc/cron.d** — A directory that contains additional system cron tables.
- **/etc/crontab** — The system cron table.
- **/etc/logrotate.conf** — The configuration file for the logrotate command. It typically uses parameters listed in the /etc/logrotate.d directory for each log file.
- **/etc/logrotate.d** — The directory that stores log file-specific information for use by the logrotate command.
- **/etc/sysconfig/cron** — A file that contains parameters for the cron daemon.
- **/etc/sysconfig/syslog** — A file that contains configuration parameters for the Syslog daemon.
- **/etc/syslog-ng/syslog-ng.conf** — The configuration file that defines how the Syslog daemon logs information about system processes.
- **/etc/syslog-ng/syslog-ng.conf.in** — A template used to create the /etc/syslog-ng/syslog-ng.conf file.
- **/proc** — A directory that contains hardware, software, and process information on a Linux system.
- **/var/log** — The directory that contains most log files on a Linux system.
- **/var/log/audit/audit.log** — The log file for AppArmor.
- **/var/log/boot.log** — A file that contains all messages written during the boot process.
- **/var/log/firewall** — The log file that stores firewall-related messages.
- **/var/log/messages** — The log file that contains most system messages.
- **/var/spool/cron/lastrun** — The directory used to store information about system cron jobs run in the past.
- **/var/spool/cron/tabs** — A directory that contains user cron tables.
- **at command** — A command that is used to schedule commands to run at a certain time in the future and manipulate at jobs.
- **atq command** — A command that is used to view scheduled at jobs.
- **atrm command** — A command that is used to remove a scheduled at job.
- **background process** — A process that runs unnoticed in your terminal and does not interfere with your command-line interface.
- **bg command** — A command that is used to start a process in the background.
- **child process** — A process that is started by another process.
- **cron** — The system service that executes commands repetitively in the future based on information in crontabs.
- **crontab (cron table)** — A file specifying the commands to be run by the cron daemon and the schedule to run them.
- **crontab command** — A command that is used to view and edit user cron tables.
- **daemon** — See daemon process.
- **daemon process** — A system process that is not associated with a terminal. It stands for Disk and Execution Monitor.
- **df command** — A command that displays disk usage by file system.
