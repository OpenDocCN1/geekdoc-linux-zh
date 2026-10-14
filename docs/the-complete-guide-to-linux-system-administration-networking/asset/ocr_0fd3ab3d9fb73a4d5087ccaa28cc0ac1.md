Another useful method to know about is sending a reconfigure signal to the logging daemons. Several Linux daemons store their process identifier (PID) in files for occasions when you need to send a signal to the process. The following command shows you the PID of syslogd:

```
# cat /var/run/syslogd.pid
```

The following command shows you the PID of klogd:

```
# cat /var/run/klogd.pid
```

Use the PID returned by these commands with kill to send a SIGHUP signal to each daemon. This signal tells the daemon to reread its configuration files. You can also use single backward quotation marks to execute the cat command and insert the resulting text as a parameter for the kill command. (Be sure to use single backward quotation marks rather than forward marks.) The following command causes syslogd to reread the syslog.conf configuration file:

```
# kill -HUP `cat /var/run/syslogd.pid`
```

Similarly, you can have klogd reread the configuration file using this command:

```
# kill -HUP `cat /var/run/klogd.pid`
```

Another acceptable method of sending the signal to the logging daemons is to use the killall command with the name of the daemon, as these two commands show:

```
# killall -HUP syslogd
# killall -HUP klogd
```

# Using the logger Utility

The logger utility lets you send a message to the syslog function, just as programs do. You can use the logger utility from a command line or from a script (as described in Chapter 14, “Writing Shell Scripts”). You can use the logger command with just a message. For example, suppose you created a script to compress files automatically. The script can include a simple logger command like this:

```
$ logger Compression utility started
```

This logs the message using a default selector of user.notice. The message is logged wherever the syslog.conf file has configured messages matching that selector (normally in /var/log/messages). Because no additional information is specified, the user name of the user running the script is included in the log file as the program name providing the log message. The resulting log entry looks something like this (the timestamp, machine name, and user name would differ on your system):

```
Oct 26 11:42:25 brighton rajw: Compression utility started
```

You can also specify other selectors with the logger command. For example, to log a message to the mail facility with a priority of info and the name of the compression script as part of the log file, use this command: