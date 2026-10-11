
## Review Questions

- 1. What is the most common LAN protocol used today?
  - a. DLC
  - b. AppleTalk
  - c. IPX/SPX
  - d. TCP/IP

- 2. What is the subnet mask for a Class C IP address?
  - a. 0.0.0.0
  - b. 255.0.0.0
  - c. 255.255.0.0
  - d. 255.255.255.0

- 3. Which of the following is a popular, high-speed connection technology used in North America?
  - a. modems
  - b. DSL
  - c. ISDN
  - d. PPP

- 4. Which ftp command is used to change the directory on the remote computer?
  - a. lcd
  - b. rcd
  - c. cd
  - d. remcd

- 5. The most common mail user agent used in Red Hat Fedora Linux is _____________.
  - a. Mozilla
  - b. Exchange
  - c. POP
  - d. Simple Mail Transfer Protocol

- 6. True or false? ANDing is a mathematical operation that compares two binary digits and gives a result of 1 or 0.

- 7. True or false? The IP address 255.255.255.255 refers to all networks.

- 8. True or false? All routers are dedicated hardware devices.

- 9. True or false? All NIC cards are detected during Linux installation.

- 10. True or false? **PPP** is the standard protocol used today to connect to remote networks over serial lines.

- 11. Two or more computers that are connected with media that can exchange information are called a(n) \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_.

- 12. To participate on a TCP/IP network, your computer must have a valid Internet Protocol (IP) address and \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ mask.

- 13. The \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ command sends a small TCP/IP packet to another IP address and awaits a response.

- 14. The simplest method for mapping host names to IP addresses is by placing entries into the \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ file.

- 15. The traditional utility used to obtain a BASH shell from a remote Linux computer on the network is \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_.

## Chapter 15

### Configuring Network Services and Security

After completing this chapter, you will be able to:

- Identify and configure common network services
- Configure routing and firewalls
- Describe the different facets of Linux security
- Increase the security of a Linux computer
- Outline measures that can be used to detect a Linux security breach

In the previous chapter, you examined the configuration of a network interface and the usage of network utilities to interact with network services on the network. In this chapter, you examine the configuration of common network services, routing, and firewalls. Following this, you examine local and network security concepts, good security practices, and the utilities that you can use to secure your Linux computer and detect intruders.

### Network Services

Recall from Chapter 1, “Introduction to Linux,” that Linux provides a wide variety of services that are available to users across a network. Before you are able to organize the appropriate network services to meet your organization’s needs, you must first identify the types and features of network services. Following this, you can configure these network services as required, as well as configure additional network-related services, such as routing and firewalls.

#### Identifying Network Services

Network services are processes that run on your computer and provide some type of valuable service for client computers on the network. They are often represented by a series of daemon processes that listen for certain requests on the network. Daemons identify to which packets they should respond by listening only for packets that have a certain number. This number is called a port and uniquely identifies a particular service. A port number is like an apartment number for the delivery of mail. The network ID of the IP address ensures that the packet is delivered to the correct street (network); the host ID ensures that the packet is delivered to the correct building (host); and the transport layer protocol and port number ensure that the packet is delivered to the proper apartment (service).

Ports and their associated protocol are defined in the `/etc/services` file. To see to which port the telnet daemon listens, you can use the following command:

```bash
[root@server1 root]# grep telnet /etc/services
    telnet          23/tcp
    telnet          23/udp
    rttelnet      107/tcp             # Remote Telnet
    rttelnet      107/udp
    telnets        992/tcp
    telnets        992/udp
[root@server1 root]#
```

The preceding output indicates that the telnet daemon listens on port 23 using both TCP/IP and UDP/IP.

Ports range in number from 0 to 65534. The ports 0–1023 are called **well-known ports** because they represent commonly used services. Table 15–1 provides a list of common well-known ports.

**NOTE**

The **User Datagram Protocol/Internet Protocol (UDP/IP)** is a faster and consequently less-reliable version of TCP/IP.

**Table 15–1 Common well-known ports**

| Service | Port |
|---|---|
| FTP | TCP 20, 21 |
| Telnet | TCP 23 |
| SMTP | TCP 25 |
| HTTP | TCP 80 |
| DNS | TCP 53, UDP 53 |
| Trivial FTP (TFTP) | UDP 69 |
| POP3 | TCP 110 |
| NNTP | TCP 119 |
| IMAP | TCP 143 |
| Secure HTTP | TCP 443 |

In addition, network utilities, such as those seen in the previous chapter, can connect to daemons that provide network services directly, or they can connect to network daemons via the **Internet Super Daemon (xinetd)**, as shown in Figure 15–1.

![](img/09bf13b782f71165e17bb3839040c96a_584_0.png)

Server computer

Client computer

**FIGURE 15–1** *Interacting with network services*

The Internet Super Daemon is typically used to start and manage connections for smaller network daemons such as the telnet, rlogin, and FTP daemons. It is started automatically at boot time and uses the configuration file `/etc/xinetd.conf`. Normally, this file incorporates all of the files in the `/etc/xinetd.d` directory as well. Most daemons that are managed by the Internet Super Daemon are configured by files in the `/etc/xinetd.d` directory named after the daemons.
For example, the telnet daemon is configured by the Internet Super Daemon via the `/etc/xinetd.d/telnet` file, as shown in the following output:

```bash
[root@server1 root]# cat /etc/xinetd.d/telnet
# default: on
# description: The telnet server serves telnet sessions; it uses \
# unencrypted username/password pairs for authentication.

service telnet
{
    flags         = REUSE
    socket_type   = stream
    wait          = no
    user          = root
    server        = /usr/sbin/in.telnetd
    log_on_failure += USERID
    disable       = yes
}

[root@server1 root]#
```

The preceding output displays the full path to the telnet daemon (`/usr/sbin/in.telnetd`). In addition, the `disable = yes` line in the `/etc/xinetd.d/telnet` file indicates that the telnet daemon is currently disabled.

> **NOTE**
>
> After a Red Hat Fedora Core 2 Linux installation, most files in the `/etc/xinetd.d` directory have the line `disable = yes` in them to prevent them from being used.
>
> Older Linux systems use a version of the Internet Super Daemon called `inetd`, which uses the configuration file `/etc/inetd.conf`.

Large network daemons are rarely started by the Internet Super Daemon and are hence called **stand-alone daemons**. Stand-alone daemons are typically started at boot time from files in the `/etc/rc/rc*.d` directories; the `ntsysv` utility discussed in Chapter 9, “System Initialization and X Windows,” can be used to configure most stand-alone daemons to start in various runlevels. In addition, most stand-alone daemons can be started manually from files in the `/etc/init.d` or `/etc/rc.d/init.d` directories.

### NETWORK SERVICES

Many stand-alone and xinetd managed daemons also have configuration files that control how they operate and indicate the pathname to other important files used by the daemon. For simplicity, many of these daemons store all information in only one configuration file that contains comments which indicate the syntax and purpose of each line. As a result, these configuration files can be very large; the configuration file used by the Apache Web Server is over 1000 lines long. In addition to this, most stand-alone network daemons do not use the syslog daemon to log information related to their operation. Instead, they log this information themselves to subdirectories of the same name underneath the `/var/log` directory. For example, log files for the Samba daemon are located in the `/var/log/samba` directory.

> **NOTE**
> The location of configuration and log files for network daemons can vary between different Linux distributions; the locations discussed in this chapter are for Red Hat Fedora Core 2 only.

### Configuring Common Network Services

To configure most network services on a Linux system, you must first identify the features of the network service, including its purpose, configuration files, port number(s), and whether the service is a stand-alone service or managed by the Internet Super Daemon. Table 15-2 lists the names and features of network services that are commonly found on Linux computers that participate in a network environment.

**Table 15-2 Common network services**

| Network Service | Type | Port | Description |
|---|---|---|---|
| Apache Web Server (httpd) | Standalone | 80, 443 | Serves Web pages using HTTP to other computers on the network that have a Web browser.<br>Configuration file: `/etc/httpd/conf/httpd.conf` |
| BIND / DNS Server (named) | Standalone | 53 | Resolves fully qualified domain names to IP addresses for a certain namespace on the Internet.<br>Configuration file: `/etc/named.conf` |
| DHCP Server (dhcpd) | Standalone | NA | Provides IP configuration for computers on a network. |
