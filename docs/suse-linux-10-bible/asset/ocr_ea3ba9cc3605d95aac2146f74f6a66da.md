# Chapter 7 + Logging 181

![](bbox=[0.137, 0.115, 0.203, 0.163])

evlog has been part of the SUSE system since version 9.3.

For information about the current state of the evlog project, see its home page at http://evlog.sourceforge.net. For an overview of the evlog project, its goals, and its approach to unifying enterprise logging, see the everwork documentation at http://evlog.sourceforge.net/linux@evlog.html.

# Managing Your Logs with logrotate

Having these logging technologies is great for accessing the information at your fingerprints, a time will come when you do not need the logs in their original form and would like to archive them off. This can be handled manually, but if you have a large number of logs, automation is the way to go.

Logs, left to their own devices, especially those on a large active system, can run riot your disk space. The logrotate application can automate the management of log files by copying and archiving them based on rules.

SUSE includes logrotate scripts for most active logging processes, and these are found in /etc/logrotate.d. The directory contains a logrotate configuration file for each process logrotate. The main configuration file for logrotate is /etc/logrotate.conf and contains archiving defaults as well as an entry to link all of the configuration files for logrotate-aware applications.

Any files located in /etc/logrotate.d will be opened and interpreted as logrotate directs when executed.

# Executing Processes Automatically on Linux Systems

The cron process automatically executes tasks at various times based on the contents of configuration files stored in user-specific subdirectories of the directory /var/spool/cron or in the system-wide configuration file /etc/crontab. This file runs processes in the directories /etc/cron.hourly, /etc/cron.daily, /etc/cron.weekly, and /etc/monthly on hourly, daily, weekly and monthly basis, respectively. These automatically scheduled and executed processes perform essential cleanup and maintenance tasks on most Linux systems. For more information about cron and the format of its configuration files, check the online reference information by executing the commands man cron and man 5 crontab on your SUSE system.

![](bbox=[0.137, 0.835, 0.862, 0.86])