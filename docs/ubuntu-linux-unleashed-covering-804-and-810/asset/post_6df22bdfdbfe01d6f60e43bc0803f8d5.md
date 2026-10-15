
Stopping internet superserver inetd: [ OK ]
Starting internet superserver inetd: [ OK ]

Once restarted, the FTP server is accessible to all incoming requests.

## Using Commands for Server Administration

wu-ftpd provides a few commands to aid in server administration. Those commands are:

- ftpwho—Displays information about current FTP server users
- ftpcount—Displays information about current server users by class
- ftpshut—Provides automated server shutdown and user notification
- ftprestart—Provides automated server restart and shutdown message removal

Each of these commands must be executed with superuser privileges because they reference the ftpaccess configuration file to obtain information about the FTP server.

## Display Information About Connected Users

The ftpwho command provides information about who are users currently connected to the FTP server. Here’s the command line:

```
/usr/bin/ftpwho
```

Table 18.3 shows the format of the output ftpwho displays.

TABLE 18.3 ftpwho Fields
| Name | Description |
|---|---|
| Process ID | The process ID of the FTP server process. |
| TTY | The terminal ID of the process. This is always a ? because the FTP daemon is not an interactive login. |
| Status | The status of the FTP process. The values are
S: Sleeping
Z: Zombie, indicating a crash
R: Running
N: Normal process |
| Time | The elapsed processor time the process has used in minutes and seconds. |
| Details | Tells from what host the process is connecting, the user who connected, and the currently executing command. |

Listing 18.4 shows a typical output of this command. It lists the process ID for the ftp daemon handling requests, the class to which the particular user belongs, the total time connected, the connected username, and the status of the session.

In addition to the information given about each connected user, ftpwho also displays the total number of users connected out of any maximum that might have been set in the ftpaccess file. This information can be used to monitor the use of your FTP server.

You can pass one parameter to ftpwho. (You can find the parameter by using the ftpwho -help command.) The single parameter you can pass to ftpwho is -v. This parameter prints out version and licensing information for wu-ftpd, as shown here:

```
# ftpwho
Service class all:
10447 ?    SN      0:00 ftpd: localhost: anonymous/winky IDLE
1 users (no maximum)
```

The output of ftpwho, using the -v option, which shows version information, is shown in Listing 18.4.

### LISTING 18.4 ftpwho -V Command Output

```
Copyright © 1999,2000,2001 WU-FTPD Development Group.
All rights reserved.

Portions Copyright © 1980, 1985, 1988, 1989, 1990, 1991, 1993, 1994
The Regents of the University of California.
Portions Copyright © 1993, 1994 Washington University in Saint Louis.
Portions Copyright © 1996, 1998 Berkeley Software Design, Inc.
Portions Copyright © 1989 Massachusetts Institute of Technology.
Portions Copyright © 1998 Sendmail, Inc.
Portions Copyright © 1983, 1995, 1996, 1997 Eric P. Allman.
Portions Copyright © 1997 by Stan Barber.
Portions Copyright © 1997 by Kent Landfield.
Portions Copyright © 1991, 1992, 1993, 1994, 1995, 1996, 1997
Free Software Foundation, Inc.

Use and distribution of this software and its source code are governed
by the terms and conditions of the WU-FTPD Software License ("LICENSE").

If you did not receive a copy of the license, it may be obtained online
at http://www.wu-ftpd.org/license.html.
Version wu-2.6.2-8
```

## Count the Number of Connections

/usr/bin/ftpcount counts the number of connected users to the FTP server and the maximum number of users allowed. This same information is found at the end of the output for the ftpwho command. This command takes only one parameter, -v, which displays the same output as the previous ftpwho example.

# ftp count

Service class all - 4 users (no maximum)

## Use /usr/sbin/ftpshut to Schedule FTP Server Downtime

As with any public server administration, it is always good practice to let users of the FTP server know about upcoming outages, when the server will be updated, and other relevant site information. The ftpshut command allows the administrator to let the FTP server do much of this automatically.

The ftpshut command enables the administrator to take down the FTP server at a specific time, based on some parameters passed to it. The format of the command is as follows and is documented in the ftpshut man page:

```
ftpshut [ -V ] [ -l min ] [ -d min ] time [ warning-message ... ]
```

The -V parameter displays the version information of the command. The time parameter is the time when the ftpshut command will stop the FTP servers. This parameter takes either a + number for the number of minutes from the current time, or a specific hour and minute in 24-hour clock format with the syntax of HH:MM.

The -l parameter enables the FTP server administrator to specify how long, in minutes, before shutdown the server will disable new connections. The default for this is 10 minutes. If the time given to shut down the servers is less than 10 minutes, new connections will be disabled immediately.

The -d parameter is similar to the -l parameter, but controls when the FTP server terminates the current connections. By default, this occurs five minutes before the server shuts down. If the shutdown time is less than five minutes, the server terminates the current connections immediately.

When you execute this command, the FTP server creates a file containing the shutdown information in the location specified under the shutdown section in the ftpaccess file. The default configuration for this file is /etc/shutmsg. If you execute the ftpshut command with warning messages, the messages are displayed when the user logs in to the server.

```
Name (pheniox:tdc): anonymous
331 Guest login ok, send your complete e-mail address as password.
Password:
230-0 system doing down at Mon Sep 3 06:23:00 2001
230-0 users of unlimited on pheniox.
230 Guest login ok, access restrictions apply.
Remote system type is UNIX.
Using binary mode to transfer files.
```
