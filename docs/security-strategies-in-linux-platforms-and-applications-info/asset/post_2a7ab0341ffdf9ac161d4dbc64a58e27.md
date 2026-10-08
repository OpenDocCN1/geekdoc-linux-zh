
## CHAPTER 2 | Basic Components of Linux Security

## More Boot Process Issues

The Transmission Control Protocol/Internet Protocol (TCP/IP) suite includes default port numbers for hundreds of services, such as 22 for SSH and 23 for Telnet. Some security professionals prefer to use nonstandard port numbers for key services. That obscurity can slow the efforts of black-hat hackers who want to break into a system.

Some services require network access during the boot process. For example, if you keep servers synchronized with the Network Time Protocol (NTP), those servers access external NTP servers during the boot process. The standard NTP port is 123. If you want to lock that port after the boot process is complete, you need to make sure the associated firewall isn't run until the NTP client is synchronized.

## Virtual Physical Security

Virtual machines add another dimension to the challenges of physical security. Standard Linux and group options add security to virtual machines. However, anyone who gains access to a virtual machine can more easily change virtual physical components. For example: a black-hat hacker who adds a CD file to a virtual CD drive would arouse less suspicion than a black-hat hacker who unlocks a CD/DVD drive on an actual physical system.

> NOTE
It's easier to modify virtual physical hardware. Although it takes time to look out or remove CD/DVD drives from physical systems, it's relatively easy to remove a CD/DVD drive from a virtual system. Although it is easier to install Linux from a CD/DVD drive, there is little need for that after installation is complete.

![](img/c0608a8c8a0777903dfec4ff61fdffa1_60_0.png)

## Linux Security Issues Beyond the Basic Operating System

While Linux distributions include a substantial number of applications and services, the essence of the Linux operating system is the kernel. Many security risks exist in applications and services beyond the kernel.

One of the main advantages of Linux is its structure as a multi-user operating system. When properly configured, Linux runs a black-hat hacker into one service, that user may gain access to the corresponding privileged account. However, that user won't have access to other accounts.

A GUI is also beyond the Linux operating system. If included, a GUI introduces a whole raft of additional security risks, discussed shortly.

## Service Process Security

For the purposes of this chapter, the boot process ends when the Linux kernel is loaded. The startup process then begins automatically, loading and starting a series of services configured in the default runlevel. A runlevel defines the services to be run. The default runlevel defines the services to be run after a system is booted. You'll read about runlevel and service management in Chapter 6.

## 36 PART 1 | Is Linux Really Secure?

| TABLE 2-2 - Typical default active services |
| SERVICE | DESCRIPTION |
| :--- | :--- |
| cups | Common UNIX Printing System (CUPS) service |
| isdn | Integrated Services Digital Network (ISDN) services |
| microcode_ctl | Microcode utility for Intel 32-bit processors |
| ntpd | Network Time Protocol (NTP) daemon |
| pcscd | PC smart card daemon |
| portmap | Remote procedure call (RPC) port-number mapper |
| sshd | Secure Shell (SSH) service |
| syslog | System log message service |
| xinetd | The extended internet server server |

Hat Enterprise Linux includes a number of services that are active by default. Most users do not need many of these services. Table 2-2 lists services that were active after installation of a fairly minimal 64-bit server system. The services in Table 2-2 are listed in lowercase because that's how they appear in the /etc/init.d/ directory. If any service is not maintained, related security flaws may not get fixed. And yes, black-hat hackers monitor security bulletins. If they learn about a security problem before you do, they'll have the advantage. If you're not paying attention to a security issue, a black-hat hacker can use information from security bulletins to break into your system. In Chapter 6, you'll learn about the risks associated with these services, along with how to keep these services to a minimum. This process can help you create bastion hosts where you need them.

The extended internet server server may be especially troublesome. First, for the editors in the audience, the term "internet" is lowercase because it refers to a group of interconnected networks, not the Internet. Second, it governs a number of network services configured in separate files in the /etc/xinetd.d/ directory.

> The very secure FTP server is a GPL version 2-licensed File Transfer Protocol (FTP) server for UNIX and Linux. You'll learn about it in depth in Chapter 9.

Other services that may be active on default Linux installations include the Apache Web server, the Samba file server, the Network File System service, the sendmail e-mail server, and the very secure FTP server. Because security issues of some services are relatively common, administrators should disable these services if they're not being used.

## CHAPTER 2 | Basic Components of Linux Security

## 37

## Security Issues with the GUI

Applications that require a GUI are common security risks. Although malware written for Windows applications may not affect Linux applications, similar risks do. Furthermore, the GUI itself is a security risk. On Linux, the GUI is a networked client-server system. Users can also run log into GUI clients over a network. In fact, administrators can configure a system to display GUI clients on a remote terminal. So malware on one Linux application can spread across a network to other GUI systems.

> NOTE
Linux server access control program, xhost, supports clear-text authentication. Telnet xhost makes it easy for black-hat hackers to read any information sent over that connection, including usernames and passwords. The SSH service can solve both problems, as it encrypted logins as well as networking of individual GUI clients.

![](img/c0608a8c8a0777903dfec4ff61fdffa1_62_0.png)

For these reasons, Linux security experts encourage administrators to installing the GUI unless absolutely. In the Linux world, a system without a GUI is no handicap. Linux administrators are accustomed to configure services from the command-line interface. As strange as it sounds, you don't even need a GUI to test the operation of a "graphical" services such as Apache and sendmail.

## User Authentication Databases

There are four major user authentication databases for Linux. The local Linux authentication databases is known as the shadow password suite. The files of the shadow password suite are /etc/passwd, /etc/group, /etc/shadow, and /etc/gshadow. These files include encrypted passwords, user and group accounts, home directories, and login shells. As you'll see in Chapter 4. these files also include specials configured for services and administrators.

The other three user authentication databases are designed as a central authentication databases on a network. When properly configured, a user can log into any configured workstation. Workstation checks login credentials from central database. Two of these databases are native to Linux: the Network Information Service (NIS) and the Lightweight Directory Access Protocol (LDAP). With the help of the Winbind service, Linux can also serve as the domain controller repository for some databases commonly used by Microsoft-based networks.

> NOTE
Incidentally, you can configure Windows NT-style authentication databases on Linux servers.
When Samba version 4 is released-expected in 2010—you'll be able to configure Linux as a domain controller for Microsoft networks instead of a Windows 2003/2008 server.

In all cases, the user and the group get both a user ID and a group ID. With those IDs, each user (and group) can own files on the local Linux system. Each networked user can be configured as a member of special groups with administrative privileges, just like other Linux user.
