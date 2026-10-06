# CHAPTER 8 Core System Services

entries to gain an accurate picture of what's going on. You could equate this system of logging facilities to the Event Viewer functionality in Windows.
rsyslog can send its output to various destinations: straight text files (usually stored in /var/log directory), Structured Query Language (SQL) databases, hosts, and more. Each log entry consists of a single line containing the date, time, hostname, process name, PID, and the message from that process. A system-wide function in the standard C library provides an easy mechanism for generating log messages. If you don't feel like writing code but want to generate entries in the logs, you have the option of using the logger command.

# Invoking rsyslog

If you find no need to either start rsyslog manually or modify the script that starts up at boot, you'll need to be aware of rsyslog's command-line parameters, shown in Table 8-4.

| Parameter | Description |
| --- | --- |
| -d | Debug mode. Normally, at startup, rsyslog detaches itself from the current terminal and starts running in the background. With the -d option, rsyslog retains control of the terminal and prints debugging information as messages are logged. It's extremely unlikely that you'll need this option. |
| -f config | Specifies a configuration file as an alternative to the default /etc/syslog.conf. |
| -h | By default, rsyslog does not forward messages to it that were for another host. This option will allow the daemon to forward logs remotely to other forwarding hosts that have been configured. |
| -l hostlist | This option lists the hosts for which only the simple hostname should be logged and not the fully qualified domain name (FQDN). You can list multiple hosts, as long as they are separated by a comma, like: -1 ubuntu-server:serverB |
| -m interval | By default, rsyslog generates a log entry every 20 minutes as “just so you know I'm running” message. This is for systems that might not be. (If you're watching the system log and don't see a single message in more than 20 minutes, you'll know for a fact something has gone wrong.) By specifying a numeric value for interval, you can indicate the number of minutes rsyslog should wait before generating another message. Setting a value of zero for this option turns it off completely. |

Table 8-4 rsyslog Command-Line Parameters