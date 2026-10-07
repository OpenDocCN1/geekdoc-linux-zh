# Notify User of Last Modification Date

The readme line tells the server if a notification should be displayed to the user when a
specific file was last modified. Here’s the command:

The path is any valid path for the user. The optional parameter is exactly
as seen in the message line. class can be one or more classes defined in the class file.
The path is absolute for anonymous, for real users. the path is relative to the
anonymous home directory, which is /var/ftp by default.

# Configure System Logging

Part of any system administration involves reviewing log files for what the server is doing,
who accessed, what files were transferred, and other pieces of important information.
You can use a number of commands within /etc/ftpassconf to control your FTP server
logging actions.

# Redirect Logging Records

This line allows the administrator to redirect where logging information from the FTP
server will be recorded:

```
log <syslog><+xferlog>
```

By default, the information for commands is stored in /var/log/messages, although the
man pages packaged in the Red Hat RPM state that this information will be written to
/var/log/xferlog. Information regarding what files were transferred and received are
witten to /var/xferlog.

# Log All User-Issued Commands

This line enables logging for all commands issued by the user.

```
log commands <typelist>
```

typelist is a comma-separated list of anonymous, guest, and real. If no typylist is given,
commands are logged for all users. The wu-ftpd RPM, packaged with Red Hat, sets the
logging of all file transfers to /var/log/xferlog (see the next section). However, you can
add the log command to ftpasswd with the commands keyword to capture user actions.
Logging will be turned on and user actions captured in /var/log/messages. Here is
an example of a sample log file:

+   Oct 6 12:21:42 shuffle 2 ftppd[5229]: USER anonymous
Oct 6 12:21:51 shuffle 2 ftppd[5229]: PASS bball@widget.com
Oct 6 12:21:51 shuffle 2 ftppd[5229]: ANONYMOUS FTP LOGIN FROM 192.168.2.31
--[192.168.2.31], bball@widget.com
Oct 6 12:21:51 shuffle 2 ftppd[5229]: SYST