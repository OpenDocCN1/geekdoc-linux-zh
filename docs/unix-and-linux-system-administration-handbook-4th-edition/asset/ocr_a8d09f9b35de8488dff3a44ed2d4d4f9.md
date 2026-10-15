# Vendor specifics

Vendors seem to have hidden log files all over the disk. Careful detective work with your daemons' config files and your syslog configuration file will find many of them. This section details some of the more obscure nooks and crannies in which log files have been hidden.

![](bbox=[0.22, 0.3, 0.26, 0.35])

Linux distributions win the grand prize for simplified log management. Logs are clearly named and consistently stored in /var/log. All our example distributions also include a superior tool, logrotate, for rotating, truncating, and managing them. New software packages can drop a config file into the /etc/logrotate.d directory to set up a management strategy for their logs. (logrotate is covered in detail later in this chapter; see page 356.)

![](bbox=[0.15, 0.47, 0.22, 0.52])

By contrast, Solaris has the most disorganized collection of log files ever. With a directory called /var/log it shouldn't be so hard. A few pointers:

+   - /var/log/*
+   - /var/cron/log
+   - /var/lp/logs/*
+   - /var/saf/_log
+   - /var/saf/zsmon/log
+   - /var/svc/log
+   - /var/adm/*

You can run the vendor-supplied /usr/lib/newsyslog script out of cron to rotate the main log files, /var/adm/messages and /var/log/syslog.

![](bbox=[0.2, 0.8, 0.25, 0.85])

HP-UX log files are in /var/adm. A lot of odd little mystery files live in this directory, many of which are not logs, so be careful what you touch. nettl.LOG000 is a network control and statistics file; see man nettl for details. By default, log entries submitted through syslog go into the /var/adm/syslog directory.

# 11.2 SYSLOG: THE SYSTEM EVENT LOGGER

Syslog, originally written by Eric Allman, is a comprehensive logging system. It has two important functions: to liberate programmers from the tedious mechanics of writing log files, and to put administrators in control of logging. Before syslog, every program was free to make up its own logging policy. System administrators had no control over what information was kept or where it was stored.

Syslog is flexible. It lets you sort messages by their source and importance ("severity level") and route them to a variety of destinations: log files, users' terminals, or even other machines. Syslog's ability to centralize the logging for a network is one of its most valuable features.

![](bbox=[0.22, 0.94, 0.26, 1.0])

Syslog was long ago adopted by every major variant of UNIX and Linux with the exception of AIX. Even AIX includes the syslog daemon and library routines, but it supplies no default syslog configuration and uses its own proprietary daemon