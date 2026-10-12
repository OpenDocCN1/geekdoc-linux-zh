+   - messages — Messages associated with many daemon processes are directed to the messages file.
+   - secure — Contains messages that may indicate security breaches. Connections from remote hosts are logged, as are attempts to log in to your system.
+   - xferlog — Shows which files have been transferred to and from your FTP server.
+   - XFree86.0.log — Contains detailed debugging messages about the startup of your graphical user interface (the X server). You will have multiple logs if multiple displays exist on your computer.

Besides these files, messages are also directed to several directories located in the `/var/log` directory. These directories include:

+   - cups — Messages from the Common UNIX Printing Service (CUPS).
+   - httpd — Messages from the Apache Web server are logged to files in this directory.
+   - news — Messages related to the Internet News service (INN).
+   - samba — Messages from the Samba service, for sharing files and printers with Windows systems.
+   - squid — Messages from the Squid proxy-server software.
+   - uucp — Messages from the UNIX-to-UNIX copy (uucp) facility are stored here.

# Using other administrative logins

You don’t hear much about other administrative logins (besides root) being used with Red Hat Linux. It was a fairly common practice in UNIX systems to have several different administrative logins that allowed administrative tasks to be split among several users. For example, a person sitting near a printer could have lp permissions to move print jobs to another printer if they knew a printer wasn’t working.

In any case, these administrative logins are available with Linux, so you may want to look into using them. At the very least, because individual software packages such as bind, squid, and amanda set up permissions for their log files and configuration files based on their administrative logins, maintaining those permissions can prevent someone who hacks into one of those services from gaining control of the whole computer.

> TIP: Because most Red Hat Linux administrative features are expected to be administered by the root user, e-mail for other administrative accounts is routed to the root user. If you want other administrative users to receive their own e-mail, delete the aliases for those users from the /etc/aliases file.

# Understanding administrative logins

Here are some of the administrative logins that are configured automatically for Linux systems. By tradition, these logins are assigned UID numbers under 100. These logins have no