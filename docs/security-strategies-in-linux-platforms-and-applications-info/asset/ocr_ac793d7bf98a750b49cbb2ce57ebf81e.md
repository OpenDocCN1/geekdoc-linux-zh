# CHAPTER 2 | Basic Components of Linux Security

# 37

# Security Issues with the GUI

Applications that require a GUI are common security risks. Although malware written for Windows applications may not affect Linux applications, similar risks do. Furthermore, the GUI itself is a security risk. On Linux, the GUI is a networked client-server system. Users can also run log into GUI clients over a network. In fact, administrators can configure a system to display GUI clients on a remote terminal. So malware on one Linux application can spread across a network to other GUI systems.

> NOTE
Linux server access control program, xhost, supports clear-text authentication. Telnet xhost makes it easy for black-hat hackers to read any information sent over that connection, including usernames and passwords. The SSH service can solve both problems, as it encrypted logins as well as networking of individual GUI clients.

![](bbox=[0.903, 0.235, 0.957, 0.335])

For these reasons, Linux security experts encourage administrators to installing the GUI unless absolutely. In the Linux world, a system without a GUI is no handicap. Linux administrators are accustomed to configure services from the command-line interface. As strange as it sounds, you don't even need a GUI to test the operation of a "graphical" services such as Apache and sendmail.

# The User Authentication Databases

There are four major user authentication databases for Linux. The local Linux authentication databases is known as the shadow password suite. The files of the shadow password suite are /etc/passwd, /etc/group, /etc/shadow, and /etc/gshadow. These files include encrypted passwords, user and group accounts, home directories, and login shells. As you'll see in Chapter 4. these files also include specials configured for services and administrators.

The other three user authentication databases are designed as a central authentication databases on a network. When properly configured, a user can log into any configured workstation. Workstation checks login credentials from central database. Two of these databases are native to Linux: the Network Information Service (NIS) and the Lightweight Directory Access Protocol (LDAP). With the help of the Winbind service, Linux can also serve as the domain controller repository for some authentication databases commonly used by Microsoft-based networks.

> NOTE
Incidentally, you can configure Windows NT-style authentication databases on Linux servers.
When Samba version 4 is released-expected in 2010—you'll be able to configure Linux as a domain controller for Microsoft networks instead of a Windows 2003/2008 server.

In all cases, the user and the group get both a user ID and a group ID. With those IDs, each user (and group) can own files on the local Linux system. Each networked user can be configured as a member of special groups with administrative privileges, just like other Linux user.