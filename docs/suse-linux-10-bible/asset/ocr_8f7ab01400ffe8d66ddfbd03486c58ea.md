The names of most of the entries in this directory indicate the contents of each log file or the program or type of program that created them. For example, mail refers to the Mail Transfer Agent (MTA) such as Postfix or sendmail that is running on your system. In much the same way, if you had Apache on your system, you would find an /var/log subdirectory that contains Apache-specific log files.

Most log files do not contain system or private user data so can be read by anybody on the system. Certain files do contain information that should be read only by the superuser on the system and refer to kernel messages, authentication messages, and mail messages. To find out what normal users are able to access the system, do a long listing on the /var/log directory (as we have done in Listing 7-1).

For more information on listing files, see Chapter 13.

# # Logging with syslog

The Standard logging facility is syslog. The syslog daemon intercepts messages logged to the system logging facility and then processes those messages based on the configuration specified in /etc/syslog.conf. The other side of syslog is the klog process, the kernel logging process processes kernel-specific messages such as kernel crashes or a failure in a component of the kernel (for example, a kernel module).

Not all processes use the syslog method of logging. You will see in this chapter that syslog has some limitations. To get around them, many applications provide their own logging facilities and use their own logging mechanisms. The way that such applications handle logging is therefore application-specific, and do not use the syslog process.

The configuration file for syslog is relatively simple to read, and you will see why it is limited in use by modern systems based on this.

When a process asks the kernel to log information, it passes a logging facility to the kernel system call. This logging facility tells the kernel and the user what type of log it is. In case of mail, the logging is MAIL. For FTP logging, it would be FTP. A total of 20 logging facilities are available to the system, 12 of which are used for specific purposes (see Table 7-1) and 8 for local use. (When we talk about local use, we mean that you can tell your application to use one of the local logging facilities to customize how those log entries are saved and interpreted).