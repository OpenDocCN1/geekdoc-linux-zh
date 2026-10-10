![](bbox=[0.18, 0.08, 0.65, 0.37])

Figure 5.11 The new set of user restrictions.

# SSH: Network Access Controls

Installing an SSH management server adds tremendous flexibility and security to any network environment. The use of SOCKS and Chroot helps further streamline and secure management access to sensitive servers and devices. Another method to help secure the SSH management server is the use of TCP wrappers on Unix SSH servers and connection filters on Windows SSH servers.

# SSH TCP wrappers

TCP Wrappers is a Unix utility that permits or denies network access to a particular port to a specified set of IP addresses. TCP wrappers functions by replacing the network service with the TCP wrapper service before the communication can be completed. The IP addresses for TCP wrappers are located in the hosts.allow and hosts.deny. For example, before any IP address can connect to a particular service/port on a system using TCP wrappers, the TCP wrappers utility first checks to see if the requesting IP address is approved to access the service/port. If TCP wrappers denies that the IP address is allowed, by checking the hosts.allow and hosts.deny files, the requesting IP address is allowed to continue to access the service and port. Note that even though the IP address is allowed to access the service/port, the IP address will still need to carry out any authentication requirements for the service. Figure 5.12 shows the TCP-wrappers process.