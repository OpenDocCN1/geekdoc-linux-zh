![](bbox=[0.27, 0.09, 0.91, 0.37])

*Figure 11-10: The syslog.conf file with the logging configuration settings.*

Some applications maintain their own log files and directories independent of the syslog.conf file. Each service has its own log storage file. Some of the frequently used log files are listed in the table.

| Log File | Description |
| :--- | :--- |
| /var/log/syslog | Stores the system log file, which contains information about the system. |
| /var/log/maillog | Stores mail messages. |
| /var/log/samba | Stores Samba messages. |
| /var/log/mrtg | Stores Multi Router Traffic Grapher (MRTG) messages. |
| /var/log/httpd | Stores Apache web server messages. |

# MRTG

MRTG is free software, licensed under GPL, that is used to monitor and measure the traffic load on network links. The traffic load on a network is represented in graphical form.