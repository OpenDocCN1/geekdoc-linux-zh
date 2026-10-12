# Table C-1 (continued)

| Feature | Package Names | Startup Script(s) | Daemon | Configuration File(s) |
| :--- | :--- | :--- | :--- | :--- |
| Security Services | | | | |
| System Logging (syslog) | syslogd | /etc/init.d/syslog | /sbin/syslogd | /etc/syslog.conf |
| Virtual Private Network Servers (CIPe) | cipe | /etc/cipe/ip-up /etc/cipe/ip-down | /usr/sbin/ciped-cb | /etc/sysconfig/network-scripts/ifdown-cipe<br>/etc/sysconfig/network-scripts/ifup-cipe |
| Caching Server (Squid) | squid | /etc/init.d/squid | /usr/sbin/squid | /etc/squid/squid.conf |