
In addition, to send five ping requests to the IP address configured earlier, you can use the following command:

```
[root@server1 root]# ping -c 5 3.4.5.6
PONG 3.4.5.6 (3.4.5.6) 56(84) bytes of data.
64 bytes from 3.4.5.6: icmp_seq=0 ttl=64 time=0.157 ms
64 bytes from 3.4.5.6: icmp_seq=1 ttl=64 time=0.113 ms
64 bytes from 3.4.5.6: icmp_seq=2 ttl=64 time=0.106 ms
64 bytes from 3.4.5.6: icmp_seq=3 ttl=64 time=0.107 ms
64 bytes from 3.4.5.6: icmp_seq=4 ttl=64 time=0.115 ms

--- 3.4.5.6 ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4000ms
rtt min/avg/max/mdev = 0.106/0.119/0.157/0.022 ms, pipe 2
[root@server1 root]# _
```

Next, you need to test whether the Linux computer can ping other computers on the same network; the following command can be used to send five ping requests to the computer that has the IP address 3.0.0.2 configured:

```
[root@server1 root]# ping -c 5 3.0.0.2
PONG 3.0.0.2 (3.0.0.2) 56(84) bytes of data.
64 bytes from 3.0.0.2: icmp_seq=0 ttl=128 time=0.448 ms
64 bytes from 3.0.0.2: icmp_seq=1 ttl=128 time=0.401 ms
64 bytes from 3.0.0.2: icmp_seq=2 ttl=128 time=0.403 ms
64 bytes from 3.0.0.2: icmp_seq=3 ttl=128 time=0.419 ms
64 bytes from 3.0.0.2: icmp_seq=4 ttl=128 time=0.439 ms

--- 3.0.0.2 ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4001ms
rtt min/avg/max/mdev = 0.401/0.422/0.448/0.018 ms, pipe 2
[root@server1 root]# _
```

## Configuring a PPP Interface

Instead of configuring TCP/IP to run on a NIC to gain network access, you can instead run TCP/IP over serial lines using a WAN protocol, such as SLIP or PPP. PPP is a newer technology than SLIP and incorporates all of SLIP’s features; thus, PPP is the standard protocol used today to connect to remote networks over serial lines.

Three common technologies use PPP today to connect computers to a network such as the Internet:

- Modems
- ISDN
- DSL

Modem (modulator-demodulator) devices use PPP to send TCP/IP information across normal telephone lines; they were the most common method for home users to gain Internet access in the last decade. Modem connections are considered slow today compared to most other technologies; most modems can only transmit data at 56KB/s. Modems are typically detected and configured during installation or by the kudzu program. Because modems transmit information on a serial port, the system typically makes a symbolic link called /dev/modem that points to the correct serial port device, such as /dev/ttyS0 for COM1.

Integrated Services Digital Network (ISDN) was originally intended to replace normal telephone lines and allows data to be transferred at 128KB/s. ISDN uses an ISDN modem device to connect to a different type of media than regular phone lines. Although ISDN is popular in Europe, it does not have a large presence in North America. Like modems, ISDN modems are typically detected and configured by kudzu or during installation.

One of the most popular connection technologies in North America is DSL. DSL has many variants such as Asynchronous DSL (ADSL), which is the most common DSL used in homes across North America, and High-bit-rate DSL (HDSL), which is common in business environments; for simplification, all variants of DSL are referred to as xDSL. You use an Ethernet NIC to connect to a DSL modem using TCP/IP and PPP; the DSL modem then transmits information across normal telephone lines at speeds that can exceed 8Mb/s. Because DSL modems are connected to a NIC via some type of media, they are not normally configured automatically during installation or by the kudzu program; instead, they are usually configured manually.

Configuring a PPP connection requires support for PPP compiled into the kernel or available as a module, the PPP daemon (pppd), and a series of supporting utilities such as the chat program, which is used to communicate with a modem. PPP configuration in the past was tedious at best; you needed to create a chat script that contained the necessary information to establish a PPP connection (user name, password, and so on), a connection script that contained device parameters used by the PPP daemon, as well as use a program such as minicom to initiate network communication. Because the TCP/IP configuration is typically assigned by the Internet service provider to which you connect, it rarely needs to be configured during the process.

Today, a wide variety of graphical programs can configure the necessary files and start the necessary utilities to allow PPP network communication. In Red Hat Fedora Linux, you simply navigate to the Red Hat button, System Settings, Network, as shown earlier in Figure 14-2, and click the New button and specify which type of device to add, as shown in Figure 14-4.

![](img/09bf13b782f71165e17bb3839040c96a_556_0.png)

**FIGURE 14-4** *Adding a network interface*

If you choose to configure a Modem connection or ISDN connection from Figure 14-4, you are first prompted for the device information shown in Figure 14-5 and Figure 14-6, respectively.

![](img/09bf13b782f71165e17bb3839040c96a_556_1.png)

**FIGURE 14-5** *Selecting modem hardware*

![](img/09bf13b782f71165e17bb3839040c96a_557_0.png)

**FIGURE 14-6** *Selecting ISDN hardware*

Regardless of whether you configure the hardware for a modem or ISDN connection, you are then prompted for the ISP and TCP/IP information, as shown in Figure 14-7 and Figure 14-8.

![](img/09bf13b782f71165e17bb3839040c96a_557_1.png)

**FIGURE 14-7** *Specifying ISP settings*

![](img/09bf13b782f71165e17bb3839040c96a_558_0.png)

**FIGURE 14-8** *Specifying TCP/IP settings*

Alternatively, if you chose to set up an xDSL connection from Figure 14-4, you are prompted to choose the Ethernet interface that is connected to the DSL modem as well as the ISP information, as depicted in Figure 14-9.

![](img/09bf13b782f71165e17bb3839040c96a_558_1.png)

**FIGURE 14-9** *Configuring an xDSL connection*

Like configuring a NIC, information about each PPP device is stored in files named ifcfg-InternetServiceProviderName underneath the /etc/sysconfig/network-scripts directory. For example, the information configured earlier for the xDSL connection is stored in the /etc/sysconfig/network-scripts/ifcfg-isp file, as shown in the following output:

```bash
[root@server1 root]# cat /etc/sysconfig/network-scripts/ifcfg-isp
# Please read /usr/share/doc/initscripts-*/sysconfig.txt
# for the documentation of these parameters.

IPV6INIT=no
ONBOOT=yes
USERCTL=yes
PEERDNS=yes
TYPE=xDSL
DEVICE=ppp0
BOOTPROTO=dialup
PIDFILE=/var/run/pppoe-ads1.pid
FIREWALL=NONE
PING=.
PPPOE_TIMEOUT=80
LCP_FAILURE=3
LCP_INTERVAL=20
CLAMPMS=1412
CONNECT_POLL=6
CONNECT_TIMEOUT=60
PERSIST=no
SYNCHRONOUS=no
DEFRROUTE=yes
USER=user1
ETH=eth0
PROVIDER=isp
DEMAND=no
[root@server1 root]# _
```

Other configurations used by the PPP daemon are stored in the /etc/ppp and /etc/isdn directories. It is good form to double-check the passwords used to connect to the ISP because incorrect passwords represent the most common problem with PPP connections. These passwords are stored in two files: /etc/ppp/pap-secrets (Password Authentication Protocol secrets) and /etc/ppp/chap-secrets (Challenge Handshake Authentication Protocol secrets). If the ISP accepts passwords sent across the network in text form, the /etc/ppp/pap-secrets file is consulted for the correct password; however, if the ISP requires a more secure method for validating the identity of a user, the passwords in the /etc/ppp/chap-secrets file are used. When you configure a PPP connection, this information is automatically added to both files, as shown in the following output:

```
[root@server1 root]# cat /etc/ppp/pap-secrets
# Secrets for authentication using PAP
# client      server    secret                  IP addresses
##### redhat-config-network will overwrite this part!!! (begin) #####
"user1"     "isp"      "secret"
##### redhat-config-network will overwrite this part!!! (end) #####

[root@server1 root]# cat /etc/ppp/chap-secrets
# Secrets for authentication using CHAP
# client      server    secret                  IP addresses
##### redhat-config-network will overwrite this part!!! (begin) #####
"user1"     "isp"      "secret"
##### redhat-config-network will overwrite this part!!! (end) #####
[root@server1 root]#
```

After a PPP device has been configured, that device must be activated by connecting (or by dialing) the ISP. You can do this by using the command `ifup InternetServiceProviderName` at a command prompt, or by navigating to the Red Hat button, System Settings, Network and clicking the Activate button for the appropriate line for your PPP connection, as shown in Figure 14-10.

![](img/09bf13b782f71165e17bb3839040c96a_560_0.png)

**FIGURE 14-10** *Activating a PPP connection*

After being activated, the `ifconfig` command indicates the interface using the appropriate names such as ppp0 (for the first modem or xDSL device) or ippp0 (for the first ISDN device).
