The ftpshut command allows the administrator to take the FTP server down at a specific time based on some parameters passed to it. The format of the command is as follows and is documented on the ftpshut man page:

```
ftpshut [ -V ] [ -l min] [ -d min] time [ warning-message ... ]
```

The -V parameter displays the version information of the command. The time parameter is the time when the ftpshut command will stop the FTP servers. This parameter will take either a + number for the number of minutes from the current time, or a specific hour and minute in 24-hour clock format with the syntax of HH:MM.

The -l parameter allows the FTP server administrator to specify how long, in minutes, before shutdown the server will disable new connections. The default for this is 10 minutes. If the time given to shut down the servers is less than 10 minutes, new connections will be disabled immediately.

The -d parameter is similar to the -l parameter, but controls when the FTP server will terminate the current connections. By default this will occur five minutes before the server shuts down. If the shutdown time is less than five minutes, the server will terminate the connections immediately.

When you execute this command, the FTP server creates a file containing the shutdown information in the location specified in the ftpaccess file under the shutdown section. The default configuration for this file is /etc/shutmsg. If you execute the ftpshut command with warning messages, the messages are displayed when the user logs in to the server.

```
Name (pheniox:tdc): anonymous
331 Guest login ok, send your complete e-mail address as password.
Password:
230-system doing down at Mon Sep 3 06:23:00 2001
230-0 users of unlimited on pheniox.
230 Guest login ok, access restrictions apply.
Remote system type is UNIX.
Using binary mode to transfer files.
```

Here is a sample ftpshut command:

```
ftpshut -l 5 -d 5 +10 "system going down at %s %N users of %M on %R"
```

This command tells the FTP server to disconnect new connections in 5 minutes, drop all current connections in 5 minutes, shut down the server in 10 minutes, and display a warning message to the users at login. The message can be a mixture of text and magic cookies, defined in Table 23.4. It is important to keep in mind that the message can only be 75 characters in length. Additionally, it is not important to know how many characters the magic cookies will take because the system knows this information and will truncate the message at 75 characters.