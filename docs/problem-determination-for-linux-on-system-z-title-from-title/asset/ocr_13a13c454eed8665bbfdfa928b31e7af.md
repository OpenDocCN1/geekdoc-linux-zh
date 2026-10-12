```
Mar 10 12:56:32 linux SuSEfirewall2: Setting up rules from
/etc/sysconfig/SuSEfirewall2 ...
Mar 10 12:56:32 linux SuSEfirewall2: batch committing...
Mar 10 12:56:32 linux SuSEfirewall2: Firewall rules successfully set
Mar 10 12:57:40 linux SuSEfirewall2: Warning: iptables does not
support state matching. Extended IPv6 support disabled.
Mar 10 12:57:40 linux SuSEfirewall2: batch committing...
Mar 10 12:57:40 linux SuSEfirewall2: Firewall rules unloaded.
Mar 10 12:57:40 linux SuSEfirewall2: Warning: iptables does not
support state matching. Extended IPv6 support disabled.
Mar 10 12:57:40 linux SuSEfirewall2: Setting up rules from
/etc/sysconfig/SuSEfirewall2 ...
Mar 10 12:57:40 linux SuSEfirewall2: batch committing...
Mar 10 12:57:40 linux SuSEfirewall2: Firewall rules successfully set
Mar 10 12:59:07 linux syslog-ng[1733]: SIGHUP received, restarting
syslog-ng
Mar 10 12:59:08 lxorainst init: Re-reading inittab
Mar 10 12:59:08 lxorainst syslog-ng[1733]: new configuration
initialized
Mar 10 13:00:56 lxorainst idown:        eth0
Mar 10 13:00:56 lxorainst idown:        eth0        configuration:
qeth-bus-ccw-0.0.0650
Mar 10 13:00:56 lxinst init: Entering runlevel: 5
Mar 10 13:00:57 lxinst kernel: Kernel logging (proc) stopped.
Mar 10 13:00:57 lxinst kernel: Kernel log daemon terminating.
Mar 10 13:00:57 lxinst ifup:        lo
Mar 10 13:00:57 lxinst ifup:        lo
Mar 10 13:00:57 lxinst ifup: IP address: 127.0.0.1/8
Mar 10 13:00:57 lxinst ifup:        eth0
```

For a better understanding of this we discuss parts of /var/log/messages logs in the following sections.

# **Information regarding applications (for example, SuSEfirewall2)**

This part of the log shows information about the SuSEfirewall2 application. We can note that there is information about firewall rules status process, warnings, and so on. All information printed here is an execution result from the SuSEfirewall2 configuration file.

> *Example 9-5* SuSEfirewall2 logs on /var/log/messages

```
Mar 10 12:56:30 linux SuSEfirewall2: Warning: iptables does not
support state matching. Extended IPv6 support disabled.
```