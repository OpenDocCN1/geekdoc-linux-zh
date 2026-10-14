
```
pop3    stream  tcp    nowait  root    /usr/sbin/tcpd ipop3d
imap    stream  tcp    nowait  root    /usr/sbin/tcpd imapd
telnet  stream  tcp    nowait  root    /usr/sbin/tcpd in.telnetd
```

You only need to notice two of the fields on these lines from inetd.conf, the first and the last. The first field, on the far left, is the service name. This name must correspond to a service name in /etc/services. The service name tells inetd which port to listen to. The far-right item on each line defines the server program that inetd starts when a client request arrives on the corresponding port.

## TCP Wrappers

If you look back at the sample lines from inetd.conf, you will notice that the last part of each line, right before the name of the server to be started, contains the text "/usr/sbin/tcpd." This is a security mechanism. For nearly every service managed by inetd, the program that inetd actually starts is tcpd. tcpd is a security program known as TCP Wrappers that examines the incoming network connection and compares it to a configuration file to determine whether the connection is allowed. If so, the "real" program is started (such as in.ftpd or in.telnetd). If access is not allowed, the packet requesting a connection is simply dropped.

TCP Wrappers—tcpd—is an application-level access control program. It is not a firewall in the traditional sense, because it operates only for a specific application. In theory, TCP Wrappers is not as secure as a firewall because the packet in question is already being examined by the software running on your system. That said, TCP Wrappers provides a good way to add security to a system that is already protected with a firewall. You should use both whenever you have any concerns about who accesses your Linux system.

TCP Wrappers is configured by two files: /etc/hosts.allow and /etc/hosts.deny. The interaction of these two files in controlling access to network services is shown in Figure 15-17. Getting started with these files is easy, but be aware that you should test the configuration carefully before relying on it. This flexibility in configuration means that you may not be configuring exactly what you think you are configuring! The format is simple. You list a service, followed by the host name or IP address that should be allowed or denied access to that service. A few keywords are supported as well, such as ALL and EXCEPT. For example, suppose the hosts.deny file contains this line:

```
in.telnetd ALL
```

And the hosts.allow file contains this line:

```
in.telnetd 192.168.
```

![](img/43f64015de86d989e30eff5bb284fb96_751_0.png)

## Figure 15-17 Controlling access via hosts.allow and hosts.deny

complexity of the assignments you can create. The ALL and EXCEPT keywords (plus several others) can be used in the service name field as well to protect a number of fields at the same time. For example, the hosts.deny file can contain this line to block access to all services for all users:

```
ALL ALL
```

Whenever you make a change in the inetd.conf file, you must restart the inetd program using a system script with a command like this:

```
# /etc/rc.d/init.d/inetd restart
```

Note that the default action of tcpd is to allow access. The hosts.allow file is checked first, and if an entry matching a pending connection request is found, the connection is accepted. If no entry is found, hosts.deny is checked. If an entry is found there, the connection is denied;

otherwise, it is accepted. The safest configuration you can make for TCP Wrappers is therefore to block all services to all users, then in hosts.allow you specifically allow any service to which you want users to have access, with corresponding IP addresses, hosts, or even an ALL designation. To learn about these options, carefully review the hosts_access man page.

![](img/43f64015de86d989e30eff5bb284fb96_752_0.png)

Besides the man command, you can view both info and man pages using the pinfo command, which presents info or man pages in a color-coded format with hypertext links to other referenced documents. The program looks first for an info page, then for a man page for the utility you name on the command line. Other similar programs that provide a more attractive interface for viewing info or man pages include xman, xinfo, and tkman. Of these, only pinfo is included by default on Red Hat Linux and Fedora.

## TROUBLESHOOTING AND RECOVERY

Your success at troubleshooting problems in Linux is largely dependent on how well you understand the services and protocols involved in a problem, and how comfortable you are with the utilities described in this book (and others that you will learn about on your own). Still, having an appropriate methodology can make it much easier to locate and fix problems. Again, the success of any methodology depends in part on how well you understand system services and the utilities and configuration files that control them. Otherwise, you will not be able to answer the questions posed in any reasonable troubleshooting method.

A basic methodology for troubleshooting in Linux might present the following questions:

- Is this problem being caused by hardware failure, hardware configuration, internal errors, software configuration, or user error?
- What system or service is causing this problem?
- Can I eliminate other possible causes to limit the scope of the problem?

Starting with the least complex element, or lowest-common-denominator that might cause the problem, check the status of that item so you can eliminate it as a reason for the trouble. Then move to the next most complex item.

Walking through an example or two can illustrate this process. Suppose that when you turn on your Linux server, it doesn't appear to boot. You might go through the following series of inquiries to locate the trouble:

- 1. Did the system boot yesterday? It did, so you know the operating system has been correctly installed. If not, maybe an operating system has never been installed (or installed correctly) on this system.
- 2. Is the power cord attached to the system? Yes, you can hear a fan blowing when you turn it on. Other parts of the system could still have failed, so if nothing else is found as the cause, you would want to examine hardware components, such as the hard disk.
- 3. Is the power cord attached to the monitor? Yes, you see a light on the bottom of the monitor. Otherwise, the system may have started up normally, you just cannot see any evidence of that on screen.
- 4. Has the system been moved lately? No. Otherwise, a loose expansion card in the system could cause it to fail on startup.
- 5. Is the hard disk being accessed to find the boot manager for Linux? It appears not, because there is no on screen display of the boot manager.
- 6. Is a different device being used to boot the system instead of the hard disk? Yes, a floppy disk was inadvertently left in the disk drive, so the system is trying to boot from that disk. When you remove that disk and reboot, the system starts normally.

An experienced system administrator considers all of these questions without really thinking about them. Only less common problems, or problems involving systems you are unfamiliar with, require a more formal process of eliminating possible causes of a problem.

Consider another example: You are trying to use your Web browser, but cannot connect to your home page, www.yahoo.com. You might think of questions such as these:

- 1. Is the network cable correctly attached to my system?
- 2. Is the DNS server I use unavailable, so that my browser cannot resolve www.yahoo.com into an IP address?
- 3. Is my connection to the Internet unavailable?
- 4. Is my connection to this site being blocked by software on my local network?
- 5. Is my local network using a proxy or other service that I need to configure on my system before I can access the Internet?
- 6. Is the Yahoo! server down?

You can investigate all of these questions according to how likely each is, and how much effort it takes to check each one. As you gain experience, you will learn about the order to ask questions for different situations. For example, you may recall that you can test whether your DNS server is the problem by trying to establish a network connection using an IP address rather than a domain name (using either your Web browser or the ping command). Or, someone at your organization may have made changes in the network (such as adding a proxy server) of which you are unaware.
