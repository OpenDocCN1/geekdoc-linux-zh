# Summary

In this chapter, you learned about system logging. The most important topics covered are:

**System Logging Processes** The system logging processes are sent to klog, the kernel logging process, and syslogd, the system logging process. By default, klog uses syslogd to handle its requests. The system logging configuration file is /etc/syslog.conf.

**Log Entry Contents** A log entry contains the following information:

+   * The date and time at which the message was received
* The name of the host that originated the message
* The name of the application that sent the message
* The process number of the application that sent the message
* The message contents

**Log Entry Types** Common log entry types include the following:

+   * Authorization failures
* Failed su commands
* Hardware errors, such as timeouts
* Logins via FTP, SSH, and TELNET
* Mail activity
* Startups and shutdowns of processes and services

**Log Rotation** Log rotation controls the amount of disk space consumed by log files. The configuration of the logrotate utility, which is stored in /etc/logrotate.conf, determines how long log files are retained and what action is taken when a log file reaches a specified age or size.

**The swatch Utility** The swatch utility can help you automate the regular review and analysis of system logs.