Various ports in this range are used by Trojan hackers that a cracker will install on a compromised system. Do you really want the next DDoS attack that makes national news to be traced to your system?

My suggestion would be to start with

```
acl Safe_ports port 80 21 443 563 70 210
http_access deny !Safe_ports
```

and allows you to present a case for allowing any other ports. See the CD-ROM for a list of the most popular default cracker ports, as encoded in the ports program source.

# ## 3.10 The syslog Service

![](bbox=[0.148, 0.355, 0.952, 0.403])

The syslog facility is used by many of the daemons and the kernel to log error messages and advisory messages. It has a facility to accept messages from remote systems over UDP port 514. This is a convenient way to consolidate messages from multiple systems and then just scan and review one of log files. Recent versions of syslog require the -r flag to enable it to listen on UDP port 514 for messages from remote systems to be logged. This is a welcome security enhancement that allows the large majority of systems that do not make use of this feature to be immune from crackers sending to this port.

The remote logging feature can increase security by logging activity on a system remotely. Thus, if a system is compromised and all log files destroyed, you still have the data on the remote system, assuming that the remote system is not also compromised. By having a special "high-security" system with minimal services supported (to reduce the likelihood of compromise) the logging, the chance of all logs being destroyed is minimized. This is discussed in "Monitoring Your System" on page 343.

However, UDP packet spoofing is true. Fortunately, modern versions of syslog (l1.3, as noted as far back as Hat 6.0) do not monitor UDP port unless there have been some exploits that can cause a DoS by repeatedly sending packets to syslog and deny access to legitimate clients or to fill up space due to the volume of logged messages. Occasionally, a cracker will write fake log messages to various systems that have this port accessible from the Internet.

There may be ways to gain root access, though hopefully these have been fixed by the time you run this, assuming that you have the latest syslog. Certainly, some crackers will spoof their UDP source IP, which is trivial, and then send messages. These will be logged and certainly confuse you. They may falsely indicate a break-in by any text they may have placed in them.

The clear solution is to have your firewall block this port from access by sites outside the trusted network.