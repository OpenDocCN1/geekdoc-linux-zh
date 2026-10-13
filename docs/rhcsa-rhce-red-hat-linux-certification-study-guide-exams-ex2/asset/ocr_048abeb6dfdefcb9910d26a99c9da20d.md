Produce and deliver reports on system utilization (processor, memory, disk, and network)

As this is not a network objective, there is no need to configure a firewall. There are no current SELinux-related system utilization options. However, as with other services, it's hard to see how you'd get credit for any configuration made for system utilization information reports unless such services are booted automatically.

# ## System Logging Server

Nominal ly, the standard RHEL 6 system logging service is a network server, like other network servers discussed in the second half of this book. But based on the way the RHCE objectives are written, system logging is an element of "System Configuration and Management." System logging information that's transmitted over a network should be configured on the client, to send logging information to a remote system, and the logging server should be configured to accept logging information from remote systems.

The system logging server normally uses TCP or UDP port 514. However, there are no current SELinux-related options. As system logging is the province of the root administrative user, there are no other real user limitations, unless you configure users in the /etc/sudoers file to administer the syslog service using the techniques discussed in Chapter 8. However, host limits are possible based on iptables-based firewalls.

# ## The Network Time Service

Finally, the last service covered in the RHCE objectives is based on NTP. The requirement suggests that you need to know how to take advantage of the cooperative nature of NTP servers:

+   - Synchronize time using other NTP peers

# # CERTIFICATION OBJECTIVE 17.01

# ## Basic Domain Service Organization

DNS is a service that translates human-readable domain names such as www.mheducation.com to IP addresses such as 12.163.148.101, and vice versa. DNS is a distributed database; each server has its own delegated zone of authority for one or more domains. The DNS service associated with RHEL is the Berkeley Internet Name Domain (BIND). As no individual DNS server is large enough to keep a