# # SCHEDULING TASKS IN LINUX

A multitasking operating system only fulfils its full purpose when it is engaged in processing jobs other than those being used interactively by users. That is, multitasking operating systems generally process background jobs which users do not see or interact with while users continue their interactive tasks.

While some of these background tasks will consist of server processes to handle FTP, HTTP, and other network requests, others will be tasks which launch and run automatically on a schedule to handle routine maintenance tasks, perform regular backups, or carry out any other periodic jobs.

Unix systems, from their early days, have been designed to operate all the time, shutting down only when maintenance tasks require it. On these types of systems, routine administrative tasks are generally scheduled to run late at night when the least numbers of users can be expected to be using the system. Linux is no exception: Any Linux server or workstation will likely need to be configured to handle some routine tasks during times of low usage, which are generally at night.

# # USING THE crond DAEMON

The crond daemon is the daemon responsible for running scheduled tasks. In Chapter 8, “Linux Process Management and Daemons,” we discuss daemons in detail. Generally, daemons are processes that answer network requests from clients or wake up periodically to perform a specific task. For example, the server processes that answer HTTP requests from Web browsers or handle delivery of emails are daemons.

crond is actually a simple application: It reads configuration files containing lists of commands and the times at which to run them. The configuration file also specify the user identifier (UID) under which to run these commands. crond then launches the specified commands at the specified times as the specified user. Any application or script you can execute by hand can be scheduled with crond.

At system boot up, crond is started from a script in the /etc/rc.d directory. When crond starts, it scans the /var/spool/cron/crontabs directory (this directory is /var/spool/cron/ on some Linux systems, including Red Hat 6.2) for crontab files. On Red Hat Linux 6.2 the /etc/crontab file is also scanned. This file schedules execution of /etc/cron.hourly, /etc/cron.daily, /etc/cron.weekly, and /etc/cron.monthly scripts. crontab files are organized by username and list all scheduled tasks for a particular user. Each individual crontab file is named after the login name of the user it is associated with.

In addition, in Linux, crond also looks at the /etc/cron.d directory for scheduled tasks. This directory is used to store tasks scheduled by the system. All crontab files are read and loaded into memory. crond then wakes up every minute and checks if it has any jobs to run, and if so, runs them. In addition, on Linux systems crond checks the modified time of the /var/spool/cron/crontabs directory when it wakes up every minute. If it detects an updated time stamp,