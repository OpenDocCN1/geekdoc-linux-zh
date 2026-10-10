then turned on and user actions are captured in /var/log/messages. Here is a sample log file:

```
Oct  6 12:21:42 shuttle2 ftpd[5229]: USER anonymous
Oct  6 12:21:51 shuttle2 ftpd[5229]: PASS phudson@widget.com
Oct  6 12:21:51 shuttle2 ftpd[5229]: ANONYMOUS FTP LOGIN FROM 192.168.2.31
[192.168.2.31], phudson@widget.com
Oct  6 12:21:51 shuttle2 ftpd[5229]: SYST
Oct  6 12:21:54 shuttle2 ftpd[5229]: CWD pub
Oct  6 12:21:57 shuttle2 ftpd[5229]: PASV
Oct  6 12:21:57 shuttle2 ftpd[5229]: LIST
Oct  6 12:21:59 shuttle2 ftpd[5229]: QUIT
Oct  6 12:21:59 shuttle2 ftpd[5229]: FTP session closed
```

The sample log shows the user name and password entries for an anonymous login. The CWD entry shows that a cd command is used to navigate to the pub directory. Note that the commands shown do not necessarily reflect the syntax the user typed, but instead list corresponding system calls the FTP server received. For example, the LIST entry is actually the ls command.

# **Log Security Violations and File Transfers**

Two other logging commands are useful in the /etc/ftpacess configuration file. This line enables the logging of security violations:

```
log security [<type list>]
```

Violations are logged for anonymous, guest, and real users, as specified in the typelist—the same as other log commands. If you do not specify a typelist, security violations for all users are logged.

This line writes a log of all files transferred to and from the server:

```
log transfers [<type list> [<directions>]]
```

typelist is the same as in log commands and log security lines. directions is a comma-separated list of the keywords inbound for uploaded files and outbound for downloaded files. If no directions list is given, both uploaded and downloaded files are logged. Inbound and outbound logging is turned on by default.

# **Configure Permission Control**

Controlling user activity is an important component of securing your system's server. The ftpacess file includes a number of commands that enable you to determine what users can and cannot execute during an FTP session. You can use these permission controls to allow users to change file permissions, delete and overwrite files, rename files, and create new files with default permissions. You learn how to use all these ftpacess file command lines in the following sections.