There are two problems with this scheme. First, its implementation depends on how the system administrator configures the system. Second, owing to the sheer size of the Internet and its current rate of growth, the static file can be extremely large.

You can use the ifconfig command to view and set network interface parameters, including the IP address, localhost, netmask, broadcast address, and maximum transmission unit (MTU). The netmask, also known as the subnetmask, is a bit mask used by TCP/IP to identify whether a host is on a remote network or on a local subnet. A broadcast address is used by the IP layer in a host to send a datagram to all the hosts on a subnet or to a remote network. The Ethernet broadcast address is all 1s. The MTU in a TCP/IP network is the maximum size of an IP datagram (packet) and is dependent on the technology used at the data link layer for connection to other hosts. The following is an example run of the command on Solaris. The command output shows that you are logged on to a host that has localhost and network interfaces each for IPv4 and IPv6 addresses. For IPv4, localhost is 127.0.0.1, with MTU 8232 bytes and netmask ff000000; network IP address is 202.147.169.197 with MTU 1500 bytes and netmask ffffffe0; and broadcast IP address is 202.147.169.223. For IPv6, localhost is ::1 with MTU 8252 bytes and IP address for external traffic is fe80::dad3:85ff:fe7b:21fe with MTU 1500 bytes. The system administrator can enable or disable these interfaces or any of its parameters. Further discussion on the output of the command and its various options for viewing and setting various network parameters is beyond the scope of this book.

```
$ ifconfig -a
lo0: flags=2001000849<UP,LOOPBACK,RUNNING,MULTICAST,IPv4,VIRTUAL>
mtu 8232 index 1 inet 127.0.0.1 netmask ff000000
net0: flags=10001000843<UP,BROADCAST,RUNNING,MULTICAST,IPv4,PHYSR
UNNING> mtu 1500 index 2 inet 202.147.169.197 netmask ffffffe0
broadcast 202.147.169.223
lo0: flags=2002000849<UP,LOOPBACK,RUNNING,MULTICAST,IPv6,VIRTUAL>
mtu 8252 index 1 inet6 ::1/128
net0: flags=120002004841<UP,RUNNING,MULTICAST,DHCP,IPv6,PHYSRUNN
ING> mtu 1500 index 2 inet6 fe80::dad3:85ff:fe7b:21fe/10
$
```

The ifconfig command is normally located in the /sbin directory on PC-BSD and the /usr/bin directory on Solaris. If you get an error message such as ifconfig: Command not found, you should include the relevant directories in your search path and re-execute the command. You can run the cat/etc/hosts command to display the domain names and IP addresses of the hosts on your network.

You can use the host command to do the DNS lookup for a host whose domain name is passed as a command line argument to it. The command allows you to display IP address(es) for a domain name or vice versa. In the following session, we use the host command to display the IP addresses of the hosts iastate.edu, berkeley.edu, and facebook.com, and the domain names corresponding to two IPv6 addresses. The output of