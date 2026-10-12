
This line limits the anonymous class to 10 concurrent connections on Monday through Friday, and on Saturday from midnight to 11:00 p.m. For example, if the number of concurrent connections is exceeded at 11:00 p.m. on Saturday, the users will see the contents of the file `/home/ftp/.message_limit_anon_class`.

Syntax for finer control over limiting user connections can be found in the `ftpaccess` man page.

## Limit the Number of Invalid Password Entries

This line allows control over how many times a user can enter an invalid password before the FTP server terminates the session:

```
loginfails <number>
```

The default for `loginfails` is set to 5. This command prevents users without valid passwords from experimenting until they get it right.

### Configure User Information

Providing users with information about the server and its use is a good practice for any administrator of a public FTP server. Adequate user information can help prevent user problems and eliminate tech support calls. You also can use this information to inform users of restrictions governing the use of your FTP server. User information gives you an excellent way to document how your FTP server should be used.

You can use the commands detailed in the following sections to display messages to users as they log in to the server and as they perform specific actions. The following commands enable messages to be displayed to users when logging in to the server and when an action is performed.

## Display a Prelogin Banner

This command is a reference to a file that is displayed before the user receives a login prompt from the FTP server:

```
banner <path>
```

This file generally contains information to identify the server. The path is an absolute pathname relative to the system root (/), not the base of the anonymous FTP user's home. The entry might look like this:

```
banner /etc/rh8ftp.banner
```

This example uses the file named `rh8ftp.banner` under the `/etc` directory. The file can contain one or more lines of text, such as

```
Welcome to Widget, Inc.'s Red Hat Linux FTP server.
This server is only for use of authorized users.
Third-party developers should use a mirror site.
```

When an FTP user attempts to log in, the banner is displayed like so:

```
S ftp shuttle2
Connected to shuttle2.home.org.
220-Widget, Inc.'s Red Hat Linux FTP server.
220-This server is only for use of authorized users.
220-Third-party developers should use a mirror site.
220-
220
220 shuttle2 FTP server (Version wu-2.6.2-8) ready.
504 AUTH GSSAPI not supported.
504 AUTH KERBEROS_V4 not supported.
KERBEROS_V4 rejected as an authentication type
Name (shuttle2:phudson):
```

**Note**

Note that the banner does not replace the greeting text that, by default, displays the hostname and server information, such as `220 shuttle2 FTP server (Version wu-2.6.2-8) ready.`

To hide version information, use the `greeting` command in `ftpaccess` with a keyword, such as `terse`, like so:

```
greeting terse
```

FTP users will then see a short message like this as part of the login text:

```
220 FTP server ready.
```

Also, not all FTP clients can handle multiline responses from the FTP server. The `banner <path>` command is how the banner line passes the file contents to the client. If a client cannot interrupt multiline responses, the FTP server is useless to them. You should also edit the default banner to remove identity and version information.

## Display a File

This line specifies a text file to be displayed to the user during login and when the user issues the `cd` command:

```
message <path> {<when> {<class> ...}}
```

The optional `when` clause can be `LOGIN` or `CWD=(dir)`, where `dir` is the name of a directory that is current. The optional `class` parameter enables messages to be shown to only a given class or classes of users.

Using messages is a good way to give information about where things are on your site as well as information that is system dependent, such as alternative sites, general policies regarding available data, server availability times, and so on.

You can use *magic cookies* to breathe life into your displayed messages. *Magic cookies* are symbolic constants that are replaced by system information. Table 24.1 lists the message command's valid magic cookies and their representations.

### Table 24.1 Magic Cookies and Their Descriptions

| Cookie | Description |
| :--- | :--- |
| $T | Local time (form Thu Nov 15 17:12:42 1990) |
| $F | Free space in partition of CWD (kilobytes) [Not supported on all systems] |
| $C | Current working directory |
| $E | Maintainer's email address as defined in `ftpaccess` |
| $P | Remote hostname |
| $N | Local hostname |
| $u | Username as determined via RFC931 authentication |
| $J | Username given at login time |
| $M | Maximum allowed number of users in this class |
| $Q | Current number of users in this class |
| $B | Absolute limit on disk blocks allocated |
| $b | Preferred limit on disk blocks |
| $0 | Current block count |
| $I | Maximum number of allocated inodes (+1) |
| $i | Preferred inode limit |
| $n | Current number of allocated inodes |
| $t | Time limit for excessive disk use |
| $N | Time limit for excessive files |
| $R | Uploaded bytes |
| $L | Downloaded bytes |
| $xR | Upload/download ratio (1:n) |
| %xR | Credit bytes |
| $X | Time limit (minutes) |
| $xE | Elapsed time since login (minutes) |
| %XL | Time left |
| $xu | Upload limit |
| $xO | Download limit |

To understand how this command works, imagine that you want to display a welcome message to everyone who logs in to the FTP server. An entry of

```
message /home/ftp/welcome.msg login
message /welcome.msg login
```

shows the contents of the `welcome.msg` file to all real users who log in to the server. The second entry shows the same message to the anonymous user.

The `welcome.msg` file is not created with the installation of the RPM, but you can create it using a text editor. Type the following:

```
Welcome to the anonymous ftp service on %L!

There are %N out of %M users logged in.

Current system time is %T

Please send email to %E if there are
any problems with this service.

Your current working directory is %C
```

Save this file as `/var/ftp/welcome.msg`. Verify that it works by connecting to the FTP server:

```
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
230-any problems with this service.
230-Your current working directory is /
```

## Display Administrator's Email Address

This line sets the email address for the FTP administrator:

```
email <name>
```

This string is printed whenever the `$E` magic cookie is specified. This magic cookie is used in the `message` line or in the `shutdown` file. You should display this string to users in the login banner message so that they know how to contact you (the administrator) in case of problems with the FTP server.

Do not use your live email address in the display banner; you want others to be able to access user emails as necessary. Instead, use an alias address that routes the messages to the appropriate IT department or other address.

## Notify User of Last Modification Date

The `readme` line tells the server if a notification should be displayed to the user when a specific file was last modified. Here’s the command:

```
readme <path> {<when {<class>}}}
```

The `path` parameter is any valid path for the user. The optional `when` parameter is exactly as seen in the `message` line. `class` can be one or more classes as defined in the `class` file. The path is absolute for real users. For the anonymous user, the path is relative to the anonymous home directory, which is `/var/ftp` by default.

## Configure System Logging

Part of system administration involves reviewing log files for what the server is doing, who accessed it, what files were transferred, and other pieces of important information. You can use a number of commands within `/etc/ftpaccess` to control your FTP server’s logging actions.

### Redirect Logging Records

This line allows the administrator to redirect where logging information from the FTP server is recorded:

```
log <syslog> {<xferlog>}
```

By default, the information for commands is stored in `/var/log/messages`, although the man pages packaged in some RPMs state that this information is written to `/var/log/xferlog`. Check your server’s settings for information regarding the location of your file transfer logs.

### Log All User-Issued Commands

This line enables logging for all commands issued by the user:

```
log commands [<typelist>]
```

`typelist` is a comma-separated list of `anonymous`, `guest`, and `real`. If no `typelist` is given, commands are logged for all users. Some wu-ftpd RPMs set the logging of all file transfers to `/var/log/xferlog` (see the next section). However, you can add the `log` command to `ftpaccess` with the `commands` keyword to capture user actions. Logging is then turned on and user actions are captured in `/var/log/messages`. Here is a sample log file:
