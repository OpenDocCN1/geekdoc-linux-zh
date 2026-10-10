+   • /etc/sysconfig — Contains important system configuration files that are created and maintained by various system services (including iptables, samba, and most networking services).
+   
+   • /etc/uuconf — Contains configuration files used with Taylor UUCP (a nonstandard version of the uucp facility) that is used to create modem, direct line, and other serial connections with other computers.
+   
+   • /etc/vsftpd — Contains configuration files used to set up the vsftpd FTP server.
+   
+   • /etc/xinetd.d — Contains a set of files, each of which defines a network service that the xinetd daemon listens for on a particular port. When the xinetd daemon process receives a request for a service, it uses the information in these files to determine which daemon processes to start to handle the request.

# Administrative log files

One of the things that Linux does well is keep track of itself. This is a good thing, when you consider how much can go wrong with a complex operating system. Sometimes you are trying to get a new facility to work and it fails without giving you the foggiest reason why. Other times you want to monitor your system to see if people are trying to access your computer illegally. In any of those cases, you can use log files to help track down the problem.

The main utilities for logging error and debugging messages for Linux are the rsyslogd and klogd daemons. General system logging is done by rsyslogd. Logging that is specific to kernel activity is done by klogd, from the optional ksyslog package. Logging is done according to information in the /etc/rsyslog.conf file. Messages are typically directed to log files that are usually in the /var/log directory.

As root user, you can view log files with the less command or watch messages as they get logged using the tail command (tail -f /var/log/messages).

# Using other administrative logins

You don't hear much about other administrative logins (besides root) being used with Linux. It was a fairly common practice in UNIX systems to have several different administrative logins that allowed administrative tasks to be split among several users.

In any case, these administrative logins are available with Linux, so you may want to look into using them. At the very least, because individual software packages such as bind, squid, and amanda set up permissions for their log files and configuration files based on their administrative logins, maintaining those permissions can impede someone who hacks into one of those services from gaining control of the whole computer.

> TIP: Because most Fedora administrative features are expected to be administered by the root user, e-mail for other administrative accounts is routed to the root user. If you want other administrative users to receive their own e-mail, delete the aliases for those users from the /etc/aliases file.