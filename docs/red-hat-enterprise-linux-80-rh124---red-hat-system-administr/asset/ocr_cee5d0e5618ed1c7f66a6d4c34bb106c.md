# REVIEWING SYSLOG FILES

After completing this section, you should be able to interpret events in relevant syslog files to troubleshoot problems or recover system status.

# LOGGING EVENTS TO THE SYSTEM

Many programs use the syslog protocol to log events to the system. Each log message is categorized by a facility (the type of message) and a priority (the severity of the message). Available facilities are documented in the syslog.conf(5) page.

The following table lists the eight syslog priorities from highest to lowest.

| CODE | PRIORITY | SEVERITY |
|---|---|---|
| 0 | emerg | System is unusable |
| 1 | alert | Action must be taken immediately |
| 2 | crit | Critical condition |
| 3 | err | Non-critical error condition |
| 4 | warning | Warning condition |
| 5 | notice | Normal but significant event |
| 6 | info | Informational event |
| 7 | debug | Debugging-level message |

The syslog service uses the facility and priority of log messages to determine how to handle them. This is configured by rules in the /etc/syslog.conf file and in the /etc/syslog.d directory that has a file extension of .conf. Software packages can easily add rules by installing an appropriate file in the /etc/syslog.d directory.

Each rule controls how to sort messages is a line in one of the configuration files. The left side of each line indicates the facility and severity of the syslog message rule matches. The right side of each line indicates what to save the log message (or where to deliver the message). An asterisk (*) is a wildcard that matches all values.

For example, the following line would record messages sent to the authpriv facility at any priority to the file /var/log/secure:

```
authpriv.*                /var/log/secure
```