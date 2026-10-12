You can identify users and groups by either numbers or names. If you use numbers, those numbers must be preceded by a percent sign (%). Here are some examples:

```
deny-gid      %-110
deny-uid      %-110
allow-uid     uucp news
```

In these examples, all administrative logins and other users up to user id 110 and group id 110 are denied access to your FTP service. The `allow-uid` line, however, overrides the denial of service for the `uucp` and `news` logins.

# Starting and shutting down the WU-FTPD service

Once you have configured your FTP server, you are ready to start it up. WU-FTPD is enabled or disabled based on information in the `/etc/xinetd.d/wu-ftpd` directory. To shut down the WU-FTPD service temporarily, you can use the `ftpsut` command.

# Starting WU-FTPD

To enable WU-FTPD, which is disabled by default, you have to change the `disable = yes` entry in the `/etc/xinetd.d/wu-ftpd` file. Open the file as root user, using any text editor, and change the line to read as follows:

```
disable = no
```

Next, you need to restart the `xinetd` daemon so that the new changes are picked up. You can do that by typing the following as root user:

```
# /etc/init.d/xinetd restart
Stopping xinetd:        [   OK   ]
Starting xinetd:        [   OK   ]
```

Now try using the `ftp` command or other FTP client to connect to your WU-FTPD server.

# Shutting down WU-FTPD

The `ftpsut` command shuts down the FTP service. Any users who are currently connected to the FTP service are disconnected. When they type FTP commands, they will see a message such as “FTP server shut down -- please try again later” or simply “Not connected.”

With the `ftpsut` command, you can either shut down the server immediately or set it to shut down in the future. To shut down the service immediately, type the following:

```
# ftpsut now
```

You can set the server to shut down at a specific time by either adding the number of minutes from now that you want the server to shut down or by entering a particular time in the future. Here are some examples: