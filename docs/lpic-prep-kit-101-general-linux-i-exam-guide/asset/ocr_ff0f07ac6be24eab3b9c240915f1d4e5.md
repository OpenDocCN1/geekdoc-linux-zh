Upon startup, the syslogd daemon reads the /etc/syslog.conf file that specifies the options to be used when logging system information.

Another configuration file can be specified instead of the /etc/syslog.conf file by using the -f option. The options that can be used with syslogd are listed in Table 10.4.

**Table 10.4 Options to Use with syslogd**

| Option | Action |
| :--- | :--- |
| -f *filename* | Specifies a configuration file other than /etc/syslog.conf |
| -h | Causes syslogd to forward messages received from remote hosts |
| -l *hostnames* | Causes hostname to be logged with simple hostname and not fully qualified domain name; separate multiple names with a colon (:) |
| -m *interval* | Time between two marked lines; default is 20 minutes |
| -r | Allows receipt of network messages |

# Key Concept

How and when system messages are written to a log file are controlled by the syslogd daemon. The configuration information usually is stored in the /etc/syslog.conf file, although another file containing configuration information can be used.

You can manage syslogd through the use of signals, too. A signal is a message that is sent to a process. Most often, this is used to tell a process to terminate. See Chapter 5 for additional information on processes and sending signals.

The use of signals enables you to stop and start syslogd, as well as update the /etc/syslog.conf file and have those changes processed by syslogd. The syntax for sending signals to syslogd is

```
kill -SIGNAL `cat /var/run/syslogd.pid`
```

The file /var/run/syslogd.pid contains the PID of the syslogd process. By enclosing the cat command in back quotes ( ), the actual contents of the file syslogd.pid—the PID of syslogd—is passed to the kill command. The signals that can be sent to syslogd are shown in Table 10.5.