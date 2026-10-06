# Mail 517

```
#imap stream tcp nowait root /usr/sbin/tcpd imapd
```

To properly configure inetd, simply locate each of these lines, remove the hash mark (#) at the beginning of the line, and save the revised file. Then restart inetd by issuing the command

```
killall -HUP inetd
```

# Administration of sendmail

The server administration script for sendmail is /etc/rc.d/init.d/sendmail. By invoking this script with the proper argument, you can control the operation of the server.

# Starting and Restarting the Service

To start sendmail, issue the command

```
/etc/rc.d/init.d/sendmail start
```

To restart sendmail, issue the command

```
/etc/rc.d/init.d/sendmail restart
```

# Stopping the Service

To stop sendmail, issue the command

```
/etc/rc.d/init.d/sendmail stop
```

# Checking Service Status

To check the status of sendmail, issue the command

```
/etc/rc.d/init.d/sendmail status
```

# Logs

In addition to log entries posted to the system log (/var/log/messages), sendmail keeps its own log file, /var/log/maillog. If mail service is not operating properly, check both log files for clues to find the source of the problem.