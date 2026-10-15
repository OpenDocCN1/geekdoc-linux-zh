server data directories, such as /var/www for the Apache Web server Web site files or /var/ftp for your FTP site files, as well as /var/named for the DNS server. The /tmp directory is simply a directory to hold any temporary files programs may need to perform a particular task.

The /var directories are designed to hold data that changes with the normal operation of the Linux system. For example, spool files for documents that you are printing are kept here. A spool file is created as a temporary printing file and is removed after printing. Other files, such as system log files, are changed constantly. Table 30-4 lists the subdirectories of the /var directory.

# The /proc File System

The /proc file system is a special file system that is generated in system memory. It does not exist on any disk. /proc contains files that provide important information about the state of your system. For example, /proc/cpuinfo holds information about your computer’s CPU

| Directory | Description |
|---|---|
| /var/account | Processes accounting logs. |
| /var/cache | Holds application cache data for Man pages, Web proxy data, fonts, or application-specific data. |
| /var/crash | Holds system crash dumps. |
| /var/games | Holds varying games data. |
| /var/lib | Holds state information for particular applications. |
| /var/local | Used for data that changes for programs installed in /usr/local. |
| /var/lock | Holds lock files that indicate when a particular program or file is in use. |
| /var/log | Holds log files such as /var/log/messages that contain all kernel and system program messages. |
| /var/mail | Holds user mailbox files. |
| /var/opt | Holds variable data for applications installed in /opt. |
| /var/run | Holds information about system’s running processes. |
| /var/spool | Holds application’s spool data such as that for mail, news, and printer queues, as well as cron and at jobs. |
| /var/tmp | Holds temporary files that should be preserved between system reboots. |
| /var/yp | Holds Network Information Service (NIS) data files. |
| /var/www | Holds Web server Web site files. |
| /var/ftp | Holds FTP server FTP files. |
| /var/named | Holds DNS server domain configuration files. |

TABLE 30-4 /var Subdirectories