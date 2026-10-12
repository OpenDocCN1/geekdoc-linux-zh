
Welcome to the anonymous ftp service on %L!

There are %N out of %M users logged in.

Current system time is %T

Please send email to %E if there are
any problems with this service.

Your current working directory is %C

Save this file as /var/ftp/welcome.msg. Verify that it works by connecting to the FTP server:

220 FTP server ready.
504 AUTH GSSAPI not supported.
504 AUTH KERBEROS_V4 not supported.
KERBEROS_V4 rejected as an authentication type
Name (shuttle:phudson): anonymous
331 Guest login ok, send your complete e-mail address as password.
Password:
230- Welcome to the anonymous ftp service on shuttle.home.org!
230-
230- There are 1 out of unlimited users logged in.
230-
230- Current system time is Mon Nov 3 10:57:06 2003
230-
230- Please send email to root@localhost if there are
230- any problems with this service.
230- Your current working directory is /

## Display Administrator's Email Address

This line sets the email address for the FTP administrator:

```
email <name>
```

This string is printed whenever the %E magic cookie is specified. This magic cookie is used in the messages line or in the shutdown file. You should display this string to users in the login banner message so that they know how to contact you (the administrator) in case of problems with the FTP server.

> **CAUTION**
> Do not use your live email address in the display banner; you want others to be able to access user emails as necessary. Instead, use an alias address that routes the messages to the appropriate IT department or other address.

## Notify User of Last Modification Date

The `readme` line tells the server if a notification should be displayed to the user when a specific file was last modified. Here's the command:

```
readme <path> [when <class>]
```

The `path` parameter is any valid path for the user. The optional `when` parameter is exactly as seen in the message line. `class` can be one or more classes as defined in the class file. The `path` is absolute for real users. For the anonymous user, the `path` is relative to the anonymous home directory, which is `/var/ftp` by default.

## Configure System Logging

Part of any system administration involves reviewing log files for what the server is doing, who accessed it, what files were transferred, and other pieces of important information. You can use a number of commands within `/etc/ftpaccess` to control your FTP server logging actions.

## Redirect Logging Records

This line allows the administrator to redirect where logging information from the FTP server will be recorded:

```
log <syslog>|<xferlog>
```

By default, the information for commands is stored in `/var/log/messages`, although the man pages packaged in some RPMs state that this information will be written to `/var/log/xferlog`. Check your server's settings for information regarding the location of your file transfer logs.

## Log All User-Issued Commands

This line enables logging for all commands issued by the user:

```
log commands [<typelist>]
```

`typelist` is a comma-separated list of `anonymous`, `guest`, and `real`. If no `typelist` is given, commands are logged for all users. Some `wu-ftpd` RPMs set the logging of all file transfers to `/var/log/xferlog` (see the next section). However, you can add the `log` command to `ftpaccess` with the `commands` keyword to capture user actions. Logging will then be turned on and user actions captured in `/var/log/messages`. Here is an example of a sample log file:

Oct 6 12:21:42 shuttle2 ftpd[5229]: USER anonymous
Oct 6 12:21:51 shuttle2 ftpd[5229]: PASS phdson@widget.com
Oct 6 12:21:51 shuttle2 ftpd[5229]: ANONYMOUS FTP LOGIN FROM 192.168.2.31
[192.168.2.31], phdson@widget.com
Oct 6 12:21:51 shuttle2 ftpd[5229]: SYST
Oct 6 12:21:54 shuttle2 ftpd[5229]: CWD pub
Oct 6 12:21:57 shuttle2 ftpd[5229]: PASV
Oct 6 12:21:57 shuttle2 ftpd[5229]: LIST
Oct 6 12:21:59 shuttle2 ftpd[5229]: QUIT
Oct 6 12:21:59 shuttle2 ftpd[5229]: FTP session closed

The example log shows the username and password entries for an anonymous login. The CWD entry shows that a cd command is used to navigate to the pub directory. Note that the commands shown do not necessarily reflect the syntax the user typed in, but instead list corresponding system calls the FTP server received. For example, the LIST entry is actually the ls command.

## Log Security Violations and File Transfers

Two other logging commands are useful in the `/etc/ftpaccess` configuration file. This line enables the logging of security violations:

```
log security [<typelist>]
```

Violations are logged for anonymous, guest, and real users, as specified in the typelist— the same as other log commands. If you do not specify a typelist, security violations for all users will be logged.

This line writes a log of all files transferred to and from the server:

```
log transfers [<typelist> [\"<directions>\"]]
```

`typelist` is the same as seen in `log commands` and `log security` lines. `directions` is a comma-separated list of the keywords `inbound` for uploaded files and `outbound` for downloaded files. If no directions are given, both uploaded and downloaded files will be logged. Inbound and outbound logging is turned on by default.

## Configure Permission Control

Controlling user activity is an important component of securing your system's server. The `ftpaccess` file includes a number of commands that enable you to determine what users can and cannot execute during an FTP session. You can use these permission controls to allow users to change file permissions, delete or overwrite files, rename files, and to create new files with default permissions. You learn how to use all these `ftpaccess` file command lines in the following sections.

> **NOTE**
>
> By default, all the `ftpaccess` file command lines prohibit anonymous users from executing actions and enable authorized users to do so.

## Allow Users to Change File Permissions

The `chmod` line determines if a user has the ability to change a file's permissions. Here is the command line:

```
chmod <yes|no> <typelist>
```

This command acts the same as the standard `chmod` command.

The `yes|no` parameter designates whether the command can be executed. `typelist` is a comma-delimited string of the keywords `anonymous`, `guest`, and `real`. If you do not specify a `typelist` string, the command will be applied to all users. An exhaustive description of its purpose and parameters can be found in the man page.

## Assign Users File-Delete Permission

The `delete` line determines whether the user can delete files with the `rm` command. Here's the command line:

```
delete <yes|no> <typelist>
```

The `yes|no` parameter is used to turn this permission on or off, and `typelist` is the same as the `chmod` command.

## Assign Users File-Overwrite Permission

This command line of the `ftpaccess` file allows or denies users the ability to overwrite an existing file. Here's the command line:

```
overwrite <yes|no> <typelist>
```

The FTP client determines whether users can overwrite files on their own local machines; this line specifically controls overwrite permissions for uploads to the server. The `yes|no` parameter toggles the permission on or off, and `typelist` is the same as seen in the `chmod` line.

## Allow Users to Rename Files

You can enable or prevent a user from renaming files using this command line:

```
rename <yes|no> <typelist>
```

The `yes|no` parameter toggles the permission on or off, and `typelist` is the same comma-delimited string as seen in `chmod`.

## Allow Users to Compress Files

This line determines whether the user will be able to use the `compress` command on files:

```
compress <yes|no> [ <classGlob> ]
```

The `yes|no` parameter toggles the permission on or off, and `classGlob` is a regular expression string that specifies one or more defined classes of users. The conversions that result from the use of this command are specified in the `ftpconversions` file, which contains directions on what compression or extraction command is to be used on a file with a specific extension, such as `.Z` for the `compress` command, `.gz` for the `gunzip` command, and so on. See the section “Configure FTP Server File-Conversion Actions” later in this chapter.

## Assign or Deny Permission to Use tar

This line determines whether the user will be able to use the `tar` (tape archive) command on files:

```
tar <yes|no> [<classglob> ...]
```

The `yes|no` parameter toggles the permission on or off, and `classglob` is a regular expression string that specifies one or more defined classes of users. Again, the conversions that result from the use of this command are specified in the `ftpconversions` file.

## Determine What Permissions Can Apply to User-Created Upload Files

This line is a bit different from the other commands in the permission control section. The `umask` command determines with what permissions a user can create new files; here it is.

```
umask <yes|no> <typelist>
```

The `yes|no` parameter toggles based on whether a user is allowed to create a file with his default permissions when uploading a file. Like the `overwrite` command you read about earlier in this section, this command line is specific to uploaded files because the client machine determines how new files are created from a download.

## Configure Commands Directed Toward the cdpath

This `alias` command allows the administrator to provide another name for a directory other than its standard name:

```
alias <string> <dir>
```

The `alias` line only applies to the `cd` command. This line is particularly useful if a popular directory is buried deep within the anonymous FTP user’s directory tree. A sample entry is the following:

```
alias linux-386 /pub/redhat/7.3/en/i386/
```

This line would allow the user to type `cd linux-386` and be automatically taken to the `/pub/redhat/7.3/en/i386` directory.

The `cdpath <dir>` line specifies in what order the `cd` command will look for a given string the user enters. The search path is done in the order in which the `cdpath` lines are entered in the `ftpaccess` file.

For example, if the following `cdpath` entries are in the `ftpaccess` file,

```
cdpath /pub/redhat/
cdpath /pub/linux/
```
