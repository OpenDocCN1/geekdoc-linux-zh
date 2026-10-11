Although host names are easier to use when specifying computers on the network, TCP/IP cannot use them to identify computers. Thus, you must map host names to their associated IP addresses such that applications that contact other computers across the network can find the appropriate IP address for a host name.

The simplest method for mapping host names to IP addresses is by placing entries into the /etc/hosts file, as shown in the following example:

```
[root@server1 root]$ cat /etc/hosts
# Do not remove the following line, or various programs
# that require network functionality will fail.
127.0.0.1	server1 localhost.localdomain localhost
3.0.0.2	ftp.sampledomain.com fileserver
192.168.0.1	alpha
[root@server1 root]$ _
```

The entries in the preceding output identify the local computer, 127.0.0.1, by the host names server1, localhost.localdomain, and localhost. Similarly, you can use the host name ftp.sampledomain.com or fileserver to refer to the computer with the IP address of 3.0.0.2. Also, the computer with the IP address of 192.168.0.1 is mapped to the host name alpha.

![](bbox=[0.16, 0.48, 0.25, 0.51])

> You can use the Network Information Service (NIS) to share the /etc/hosts configuration file among several Linux computers on the network. NIS is discussed in Chapter 15, "Configuring Network Services and Security."

Because it would be cumbersome to list names for all hosts on the Internet in the /etc/hosts file, ISPs can list FQDNs in DNS servers on the Internet. Applications can then ask DNS servers for the IP address associated with a certain FQDN. To configure your system to resolve names to IP addresses by contacting a DNS server, simply specify the IP address of the DNS server in the /etc/resolv.conf file. This file can contain up to three DNS servers; if the first DNS server is unavailable, the system attempts to contact the second DNS server followed by the third DNS server listed in the file. An example /etc/resolv.conf file is shown in the following output:

```
[root@server1 root]$ cat /etc/resolv.conf
nameserver 209.121.197.2
nameserver 192.139.188.144
nameserver 6.0.4.211
[root@server1 root]$ _
```