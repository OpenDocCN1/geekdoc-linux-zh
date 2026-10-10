Ports and their associated protocols are defined in the /etc/services file. To see to which port the telnet daemon listens, you can use the following command:

```
[root@server1 ~]# grep telnet /etc/services
telnet      23/tcp
telnet      23/udp
telnet      107/tcp     # Remote Telnet
rtelnet     107/udp
telnets     992/tcp
telnets     992/udp
skytelnet   1618/tcp    # skytelnet
skytelnet   1618/udp    # skytelnet
hp-3000-telnet      2564/tcp    # HP 3000 NS/VT block mode telnet
hp-3000-telnet      2564/udp    # HP 3000 NS/VT block mode telnet
tll1-telnet         3083/tcp    # TLL1-TELNET
tll1-telnet         3083/udp    # TLL1-TELNET
telnetcpd           3696/tcp    # Telnet Com Port Control
telnetcpd           3696/udp    # Telnet Com Port Control
scpi-telnet         5024/tcp    # SCPI-TELNET
scpi-telnet         5024/udp    # SCPI-TELNET
ktelnet             6623/tcp    # Kerberos VS Telnet
ktelnet             6623/udp    # Kerberos VS Telnet
[root@server1 ~]# _
```

The preceding output indicates that the telnet daemon listens on port 23 using both TCP/IP and UDP/IP.

![](bbox=[0.15, 0.55, 0.32, 0.62])

> The User Datagram Protocol/Internet Protocol (UDP/IP) is a faster and consequently less-reliable version of TCP/IP.

Ports range in number from 0 to 65534. The ports 0–1023 are called **well-known ports** because they represent commonly used services. Table 12-2 provides a list of common well-known ports.

![](bbox=[0.15, 0.71, 0.32, 0.78])

> Many protocols have a secure version that uses encrypted communication. For example, secure HTTP is called HTTPS and uses a different port number as a result.

Network utilities can connect to daemons that provide network services directly; these daemons are called stand-alone daemons. Alternatively, network utilities can connect to network services via the Internet Super Daemon (inetc) or Extended Internet Super Daemon (xinetd), which starts the appropriate daemon in order to provide the network service as needed. This structure is shown in Figure 12-8.

The inetc or xinetd daemons are typically used to start and manage connections for smaller network daemons such as telnet and rlogin. Ubuntu Server 14.04 installed the inetc daemon by default, but you can optionally install the xinetd daemon via a software repository. Fedora