
graphical applications, it can also be used to display a Linux desktop on an MS Windows machine, using remote X. From a Cygwin Bash shell, type the command `/usr/X11R6/bin/Xwin.exe -query your_linux_machine_name_or_IP`

The connection is by default denied. You need to change the X Display Manager (XDM) configuration and possibly the X Font Server (XFS) configuration to enable this type of connection, where you get a login screen on the remote machine. Depending on your desktop manager (Gnome, KDE, other), you might have to change some configuration there, too.

If you do not need to display the entire desktop, you can use SSH in Cygwin, just like explained in Section 10.4.4, without all the fuss of editing configuration files.

## 10.5 Security

### 10.5.1 Introduction

As soon as a computer is connected to the network, all kinds of abuse become possible, be it a UNIX-based or any other system. Admittedly, mountains of papers have been spilled on this subject and it would lead us too far to discuss the subject of security in detail. There are, however, a couple of fairly logical things even a novice user can do to obtain a very secure system, because most break-ins are the result of ignorant or careless users.

Maybe you are asking yourself if this all applies to you, using your computer at home or working at your office on a desktop in a fairly protected environment. The questions you should be asking yourself, however, are more on the lines of:

- Do you want to be in control of your own system?
- Do you want to (unwittingly) participate in criminal activities?
- Do you want your equipment to be used by someone else?
- Do you want to take risks on losing your Internet connection?
- Do you want to rebuild your system every time it has been hacked?
- Do you want to risk personal or other data loss?

Presuming you don't, we will quickly list the steps you can take to secure your machine. Extended information can be found in the Linux Security HOWTO <http://www.tldp.org/HOWTO/Security-HOWTO.html>.

### 10.5.2 Services

The goal is to run as few services as possible. If the number of ports that are open for the outside world are kept to a minimum, this is all the better to keep an overview. If services can’t be turned off for the local network, try to at least disable them for outside connections.

A rule of thumb is that if you don’t recognize a particular service, you probably won’t need it anyway. Also keep in mind that some services are not really meant to be used over the Internet. Don’t rely on what *should* be running, check which services are listening on what TCP ports using the `netstat` command:

```
[elley@mars ~]$ netstat -l | grep tcp
tcp        0      0  ::32769                 *:*                    LISTEN
tcp        0      0  ::32771                 *:*                    LISTEN
tcp        0      0  * :printer              *:*                    LISTEN
tcp        0      0  * :kerberos_master      *:*                    LISTEN
tcp        0      0  * :sunrpc               *:*                    LISTEN
tcp        0      0  * :6001                  *:*                    LISTEN
tcp        0      0  * :785                  *:*                    LISTEN
tcp        0      0  localhost.localdomain:smtp  *:*              LISTEN
tcp        0      0  * :ftp                  *:*                    LISTEN
tcp        0      0  * :ssh                  *:*                    LISTEN
tcp        0      0  ::1:x11-ssh-offset      *:*                    LISTEN
```

Things to avoid:

- `exec`, `rlogin` and `rsh`, and `telnet` just to be on the safe side.
- X11 on server machines.
- No `lp` if no printer is physically attached.
- No MS Windows hosts in the network, no Samba required.
- Don’t allow `FTP` unless an `FTP` server is required.
- Don’t allow `NFS` and `NIS` over the Internet, disable all related services on a stand-alone installation.
- Don’t run an `MTA` if you’re not actually on a mail server.
- ...

Stop running services using the `chkconfig` command, the initscripts or by editing the (x)inetd configuration files.

### 10.5.3 Update regularly

Its ability to adapt quickly in an ever changing environment is what makes Linux thrive. But it also creates a possibility that security updates have been released even while you are installing a brand new version, so the first thing you should do (and this goes for about any OS you can think of) after installing is getting the updates as soon as possible. After that, update all the packages you use regularly.

Some updates may require new configuration files, and old files may be replaced. Check the documentation, and ensure that everything runs normal after updating.

Most Linux distributions provide mailing list services for security update announcements, and tools for applying updates to the system. General Linux only security issues are reported among others at Linuxsecurity.com <http://linuxsecurity.com/>.

Updating is an ongoing process, so it should be an almost daily habit.

### 10.5.4 Firewalls and access policies

#### 10.5.4.1 What is a firewall?

In the previous section we already mentioned firewall capabilities in Linux. While firewall administration is one of the tasks of your network admin, you should know a couple of things about firewalls.

Firewall is a vague term that can mean anything that acts as a protective barrier between us and the outside world, generally the Internet. A firewall can be a dedicated system or a specific application that provides this functionality. Or it can be a combination of components, including various combinations of hardware and software. Firewalls are built from “rules” that are used to define what is allowed to enter and/or exit a given system or network.

After disabling unnecessary services, we now want to restrict accepted services as to allow only the minimum required connections. A fine example is working from home: only the specific connection between your office and your home should be allowed, connections from other machines on the Internet should be blocked.

#### 10.5.4.2 Packet filters

The first line of defense is a packet filter, which can look inside IP packets and make decisions based on the content. Most common is the Netfilter package, providing the iptables command, a next generation packet filter for Linux.

One of the most noteworthy enhancements in the newer kernels is the stateful inspection feature, which not only tells what is inside a packet, but also detects if a packet belongs or is related to a new or existing connection.

The Shoreline Firewall or Shorewall for short is a front-end for the standard firewall functionality in Linux.

More information can be found at the Netfilter/iptables project page <http://www.netfilter.org/>.

#### 10.5.4.3 TCP wrappers

TCP wrapping provides much the same results as the packet filters, but works differently. The wrapper actually accepts the connection attempt, then examines configuration files and decides whether to accept or reject the connection request. It controls connections at the application level rather than at the network level.

TCP wrappers are typically used with `xinetd` to provide host name and IP-address-based access control. In addition, these tools include logging and utilization management capabilities that are easy to configure.

The advantages of TCP wrappers are that the connecting client is unaware that wrappers are used, and that they operate separately from the applications they protect.

The host based access is controlled in the `hosts.allow` and `hosts.deny` files. More information can be found in the TCP wrapper documentation files in `/usr/share/doc/tcp_wrappers[< version >/]` or `/usr/share/doc/tcp` and in the man pages for the host based access control files, which contain examples.

#### 10.5.4.4 Proxies

Proxies can perform various duties, not all of which have much to do with security. But the fact that they are an intermediary make proxies a good place to enforce access control policies, limit direct connections through a firewall, and control how the network behind the proxy looks to the Internet.

Usually in combination with a packet filter, but sometimes all by themselves, proxies provide an extra level of control. More information can be found in the Firewall HOWTO <http://www.tldp.org/HOWTO/Firewall-HOWTO.html> or on the Squid website.

#### 10.5.4.5 Access to individual applications

Some servers may have their own access control features. Common examples include Samba, X Window, Bind, Apache and CUPS. For every service you want to offer check which configuration files apply.

#### 10.5.4.6 Log files

If anything, the UNIX way of logging all kinds of activities into all kinds of files confirms that "it is doing something." Of course, log files should be checked regularly, manually or automatically. Firewalls and other means of access control tend to create huge amounts of log files, so the trick is to try and only log abnormal activities.
