# Notify User of Last Modification Date

The `readme` line tells the server if a notification should be displayed to the user when a specific file was last modified. Here's the command:

```
readme <path> [<-when {<class>}}
```

The `path` parameter is any valid path for the user. The optional `when` parameter is exactly as seen in the message line. `class` can be one or more classes as defined in the class file. The `path` is absolute for real users. For the anonymous user, the `path` is relative to the anonymous home directory, which is `/var/ftp` by default.

# Configure System Logging

Part of any system administration involves reviewing log files for what the server is doing, who accessed it, what files were transferred, and other pieces of important information. You can use a number of commands within `/etc/ftpadaccess` to control your FTP server logging actions.

# Redirect Logging Records

This line allows the administrator to redirect where logging information from the FTP server will be recorded:

```
log <syslog>{<xferlog>}
```

By default, the information for commands is stored in `/var/log/messages`, although the man pages packaged in some RPMs state that this information will be written to `/var/log/xferlog`. Check your server's settings for information regarding the location of your file transfer logs.

# Log All User-Issued Commands

This line enables logging for all commands issued by the user:

```
log commands [<typelist>]
```

`typelist` is a comma-separated list of `anonymous`, `guest`, and `real`. If no `typelist` is given, commands are logged for all users. Some `wu-ftpd` RPMs set the logging of all file transfers to `/var/log/xferlog` (see the next section). However, you can add the `log` command to `ftpadaccess` with the `commands` keyword to capture user actions. Logging will then be turned on and user actions captured in `/var/log/messages`. Here is an example of a sample log file:

```
```
Oct  6 12:21:42 shuttle2 ftpd[5229]: USER anonymous
Oct  6 12:21:51 shuttle2 ftpd[5229]: PASS phdson@widget.com
Oct  6 12:21:51 shuttle2 ftpd[5229]: ANONYMOUS FTP LOGIN FROM 192.168.2.31
[192.168.2.31], phdson@widget.com
Oct  6 12:21:51 shuttle2 ftpd[5229]: SYST
Oct  6 12:21:54 shuttle2 ftpd[5229]: CWD pub
```
```