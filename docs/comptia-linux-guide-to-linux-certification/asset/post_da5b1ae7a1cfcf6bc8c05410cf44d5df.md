
# Protecting Against Network Attacks

Recall from earlier in this chapter that network services listen for network traffic on a certain port number and interact with that traffic. As long as network services exist on a computer, there is always the possibility that hackers can manipulate the network service by interacting with it in unusual ways. One example of this type of network attack is a **buffer overrun**, which can replace program information used by the network service in memory with new program information, consequently altering how the network service operates.

**Network Security Essentials** The first step to securing your computer against network attacks such as buffer overruns is to minimize the number of network services running. If you run only the minimum number of network services necessary for your organization, you greatly reduce the chance of network attacks. To see what network services are running on your network, you can run the **`nmap`** (**network mapper**) command. The following output demonstrates how nmap can be used to determine the number of services running on the server1 computer:

```bash
[root@server1 ~]$ nmap -sT server1.class.com
Starting Nmap 6.45 (http://nmap.org) at 2015-11-01 15:14 EDT
Nmap scan report for server1.class.com (192.168.1.105)
Host is up (0.0019s latency) .

rDNS record for 192.168.1.105: server1.class.com
Not shown: 995 closed ports

PORT     STATE SERVICE
22/tcp   open  ssh
111/tcp  open  rpcbind
631/tcp  open  ipp
5903/tcp open  vnc-3
6003/tcp open  X11:3

Nmap done: 1 IP address (1 host up) scanned in 0.13 seconds
[root@server1 ~]# _
```

![](img/c27875544958897d817484d558c208c8_674_0.png)

The **`nmap`** command is not normally installed on a Linux distribution by default, but it can be added from a software repository.

From the preceding output, you can determine which services are running on your computer by viewing the service name or by searching the descriptions for the port numbers in the `/etc/services` file or on the Internet. For services that are not needed, ensure that they are not started automatically when entering your runlevel.

For services that must be used because they are essential to your organization, you can take certain steps to ensure that they are as secure as possible. You should ensure that network service daemons are not run as the root user on the system when possible. If a hacker gains access to your system via a network service daemon run as the root user, the hacker has root access as well. Many network daemons, such as Apache, set the user account by which they execute in their configuration files.

Similarly, for daemons such as Apache that run as a non-root user, you should ensure that the shell listed in /etc/passwd for the daemon is set to an invalid shell, such as /sbin/nologin. If a hacker attempted to remotely log into the system using a well-known daemon account, she would not be able to get a BASH shell. Instead, the /sbin/nologin simply prints the warning listed in the /etc/nologin.txt file to the screen and exits. If the /etc/nologin.txt file doesn't exist, the /sbin/nologin program prints a standard warning.

In addition, because network attacks are reported in the open source community, new versions of network services usually include fixes for known network attacks. As such, these new versions are more resilient to network attacks. Because of this, it is good form to periodically check for new versions of network services, install them, and check the associated documentation for new security-related parameters that can be set in the configuration file.

If you use network services that are started by inetd or xinetd, you can use TCP wrappers to provide extra security. A **TCP wrapper** is a program (/usr/sbin/tcpd) that can start a network daemon. To enable TCP wrappers, you must modify the /etc/inetd.conf file (for inetd) or the appropriate file in the /etc/xinetd.d directory (for xinetd) and start the network daemon as an argument to the TCP wrapper. For the telnet daemon started by xinetd, you modify the /etc/xinetd.d/telnet file, as shown in the following example:

```bash
[root@server1 ~]# cat /etc/xinetd.d/telnet
# default: on
# description: the telnet server serves telnet sessions; it uses \
#   unencrypted username/password pairs for authentication.
service telnet
{
    flags            = REUSE
    socket_type      = stream
    wait             = no
    user             = root
    server           = /usr/sbin/tcpd
    server_args      = /usr/sbin/in.telnetd
    log_on_failure   += USERID
    disable          = no
}
[root@server1 ~]# _
```

Now, the telnet daemon (/usr/sbin/in.telnetd) will be started by the TCP wrapper (/usr/sbin/tcpd). Before a TCP wrapper starts a network daemon, it first checks the /etc/hosts.allow and /etc/hosts.deny files. This allows you to restrict the network service such that it can only be accessed by certain hosts within your organization. The following /etc/hosts.allow and /etc/hosts.deny files only give the computers client1 and client2 the ability to use the telnet utility to connect to your telnet server.

```bash
[root@server1 ~]# cat /etc/hosts.deny
in.telnetd: ALL
[root@server1 ~]# cat /etc/hosts.allow
in:telnetd: client1, client2
[root@server1 ~]# _
```

Another important component of network security involves local file permissions. If everyone had read permission on the /etc/shadow file, any user could read the encrypted passwords for all user accounts, including the root user, and possibly decrypt the password using a decryption program. Fortunately, the default permissions on the /etc/shadow file allow read permission for the root user only to minimize this possibility. However, similar permission problems exist with many other important files, and hackers typically exploit these files as a result. Thus, you need to carefully examine the permissions on files and directories associated with system and network services.

Take, for example, the Apache Web server discussed in Chapter 13. Apache daemons are run as the user apache and the group apache by default. These daemons read HTML files from the document root directory such that they can give the information to client Web browsers. The following directory listing from a sample document root directory shows that the Apache daemons also have write permission because they own the index.html file:

```bash
[root@server1 ~]# ls -l /var/www/html
total 64
-rw-r--r-- 1 apache apache 61156 Sep 5 08:36 index.html
[root@server1 ~]# _
```

Thus, if a hacker were able to manipulate an Apache daemon, the hacker would have write access to the index.html file and would be able to modify it. It is secure practice to ensure that the index.html is owned by the Web developer (who needs to modify the file) and that the Apache daemons are given read access only through membership in the other category. If your Web developer logs into the system as the user account webma, you could perform the following commands to change the permissions on the Web content and verify the results:

```bash
[root@server1 ~]# chown webma /var/www/html/index.html
[root@server1 ~]# ls -l /var/www/html
total 64
-rw-r--r-- 1 webma apache 61156 Sep 5 08:36 index.html
[root@server1 ~]# _
```

# Configuring a Firewall

Another method that you can use to ensure that network services are as secure as possible is to configure a firewall on your Linux computer using a component of the Linux kernel called netfilter. Recall from Chapter 1 that firewalls can be used in your organization to block unwanted network traffic; as a result, firewalls are typically enabled on router interfaces.

Netfilter discards certain network packets according to chains of rules that are stored in your computer's memory. By default, you can specify firewall rules for three types of chains:

- INPUT chain, for network packets destined for your computer
- FORWARD chain, for network packets that must pass through your computer (if you are a router)
- OUTPUT chain, for network packets that originate from your computer

![](img/c27875544958897d817484d558c208c8_676_0.png)
