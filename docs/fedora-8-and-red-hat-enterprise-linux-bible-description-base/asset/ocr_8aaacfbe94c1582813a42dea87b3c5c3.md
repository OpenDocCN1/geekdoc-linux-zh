+   - `/etc/skel` — Any files contained in this directory are automatically copied to a user's home directory when that user is added to the system. By default, most of these files are dot (.) files, such as `.kde` (a directory for setting KDE desktop defaults) and `.bashrc` (for setting default values used with the bash shell).
+   - `/etc/squid` — Contains configuration files for the Squid proxy caching server.
+   - `/etc/sysconfig` — Contains important system configuration files that are created and maintained by various system services (including `iptables`, `samba`, and most `networking services`).
+   - `/etc/ucp` — Contains configuration files used by Taylor UUCP (a nonstandard version of the uucp facility that is used to create modem, direct line, and other serial connections with other computers).
+   - `/etc/vsftpd` — Contains configuration files used to set up the vsftpd FTP server.
+   - `/etc/xinetd.d` — Contains a set of files, each of which defines a network service that the xinetd daemon listens for on a particular port. When the xinetd daemon process receives a request for a service, it uses the information in these files to determine which daemon processes to start to handle the request.

# Administrative log files

One of the things that Linux does well is keep track of itself. This is a good thing, when you consider how much can go wrong with a complex operating system. Sometimes you are trying to get a new facility to work and it fails without giving you the foggiest reason why. Other times you want to monitor your system to see if people are trying to access your computer illegally. In any of those cases, you can use log files to help track down the problem.

The main utilities for logging error and debugging messages for Linux are the syslog and klogd daemons. General system logging is done by syslogd. Logging that is specific to kernel activity is done by klogd. Logging is done according to information in the /etc/syslog.conf file. Messages are typically directed to log files that are usually in the /var/log directory.

As root user, you can view log files with a text editor (such as gedit or vi) or watch messages as they enter log file using the tail command (tail -f /var/log/messages).

# Using other administrative logins

You don't hear much about other administrative logins (besides root) being used with Linux. It was a fairly common practice in UNIX systems to have several different administrative logins that allowed administrative tasks to be split among several users.

In any case, these administrative logins are available with Linux, so you may want to look into using them. At the very least, because individual software packages such as bind, squid, and amanda set up permissions for their log files and configuration files based on their