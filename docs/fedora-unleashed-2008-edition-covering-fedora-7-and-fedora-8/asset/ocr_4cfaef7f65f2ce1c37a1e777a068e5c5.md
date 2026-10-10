The `ftpshut` command enables the administrator to take down the FTP server at a specific time, based on some parameters passed to it. The format of the command is as follows and is documented in the `ftpsht` man page:

```
``` 
ftpsht [ -V ] [ -1 min ] [ -d min] time [ warning-message ... ]
```
```

The -V parameter displays the command's version information. The time parameter is the time when the `ftpshut` command will stop the FTP servers. This parameter takes either a + number for the number of minutes from the current time, or a specific hour and minute in 24-hour clock format with the syntax of HH:MM.

The -1 parameter enables the FTP server administrator to specify how long, in minutes, before shutdown the server disables new connections. The default is 10 minutes. If the time given to shut down the servers is less than 10 minutes, new connections are disallowed immediately.

The -d parameter is similar to the -1 parameter, but controls when the FTP server terminates the current connections. By default, this occurs five minutes before the server shuts down. If the shutdown time is less than five minutes, the server terminates the current connections immediately.

When you execute this command, the FTP server creates a file containing the shutdown information in the location specified under the shutdown section in the `ftpaccess` file. The default configuration for this file is /etc/ftpshtmsg. If you execute the `ftpshut` command with warning messages, the messages are displayed when the user logs in to the server.

```
``` 
Name (phenix:tdc): anonymous
331 Guest login ok, send your complete e-mail address as password.
Password:
230-system doing down at Mon Sep  3 06:23:00 2001
230-0 users of unlimited on phenix.
230 Guest login ok, access restrictions apply.
Remote system type is UNIX.
Using binary mode to transfer files.
```
```

Here is a sample `ftpshut` command:

```
``` 
ftpsht -1 5 -d 5 +10 "system doing down at %s \n users of %M on %R" 
```
```

This command tells the FTP server to disconnect new connections in 5 minutes, drop all current connections in 5 minutes, shut down the server in 10 minutes, and display a warning message to the users at login. The message can be a mixture of text and the magic cookies defined in Table 20.4. It is important to keep in mind that the message can be a maximum of 75 characters in length. Additionally, it is not important to know how many characters the magic cookies take because the system knows this information and truncates the message at 75 characters.