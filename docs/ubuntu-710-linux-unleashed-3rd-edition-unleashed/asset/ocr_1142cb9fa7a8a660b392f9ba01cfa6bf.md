# Display Administrator's Email Address

This line sets the email address for the FTP administrator:

```
email <name>
```

This string is printed whenever the %E magic cookie is specified. This magic cookie is used in the messages line or in the shutdown file. You should display this string to users in the login banner message so that they know how to contact you (the administrator) in case of problems with the FTP server.

CAUTION
Do not use your live email address in the display banner; you want others to be able to access user emails as necessary. Instead, use an alias address that routes the messages to the appropriate IT department or other address.

# Notify User of Last Modification Date

The readme line tells the server whether a notification should be displayed to the user when a specific file was last modified. Here's the command:

```
readme <path> {<when {<class>}>}
```

The path parameter is any valid path for the user. The optional when parameter is exactly as seen in the message line. class can be one or more classes as defined in the class file. The path is absolute for real users. For the anonymous user, the path is relative to the anonymous home directory, which is /var/ftp by default.

# Configure System Logging

Part of system administration involves reviewing log files for what the server is doing, who accessed it, what files were transferred, and other pieces of important information. You can use a number of commands within /etc/ftpaccess to control your FTP server logging actions.

# Redirect Logging Records

This line allows the administrator to redirect where logging information from the FTP server is recorded:

```
log <syslog|{<xferlog>}>
```

By default, the information for commands is stored in /var/log/messages, although the man pages packaged in some packages state that this information is written to /var/log/xferlog. Check your server's settings for information regarding the location of your file transfer logs.