# Part III: Administering Fedora and RHEL

Send the messages to another computer (loghost) instead of a file, simply replace the log filename with the @ character followed by the name of the loghost. For example, to redirect the output normally to the messages,secure, mailog log files, make these changes to the previous file:

```
# Log anything (except mail) of level info or higher.
# Don't log private authentication messages!
*.info@mail.none;news.none;authpriv.none;cron.none @loghost

# The authpriv file has restricted access.
authpriv.* @loghost

# Log all the mail messages in one place.
mail.* @loghost
```

The messages will be sent to rsyslog running on the computer named loghost. The name loghost was not an arbitrary choice. It is custom to create such a hostname and make an alias to the system acting as the loghost. That way, if you ever need to switch the loghost to a different machine, you only need to change the log alias; you do not need to re-edit the rsyslog.conf file on every computer.

# Understanding the messages logfile

Because of the many programs and services record information to the messages log file, it is important that you understand the format of this file. Examining this file gives you a early warning of problems developing on your system. Each line in the log is a single message recorded by some program or service. Here is a snippet of an messages log file:

```
Feb 25 11:04:32 toys network: Bringing up loopback interface: succeeded
Feb 25 11:04:35 toys network: Bringing up interface eth0: succeeded
Feb 25 13:01:14 toys vsftpd(pam_unix) [10565]: authentication failure;
name= uid=0 tty=root rhost=10.0.0.5 user-chris
Feb 25 14:44:24 toys su(pam_unix) [11439]: session opened for
user root by chris(uid=500)
```

This is really simple when you know what to look for. Each message is divided into five main parts. From left to right they are:

+   * The date and time that the message was logged
* The name of the computer that the message came from
* The program or service that the message pertains to
* The process number (enclosed in square brackets) of the program sending the message
* The actual text itself

Let's examine the previous file snippet. In the first two lines, you can see that I restarted the network. The next line shows that I tried to log in as the user named chris to get the FTP