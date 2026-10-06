# 670 Linux Administration: A Beginner's Guide

Here, filename is the name of the file that needs to be referenced, and servicename is the name of the service used to find the file. Multiple services can be listed, separated by spaces. Here are examples of some valid services:

+   - files Use the actual file on the host itself.
- yp Use NIS to perform the lookup.
- nis Use NIS to perform the lookup (nis is an alias of yp).
- dns Use DNS for the lookup (applies only to hosts).
- [NOTFOUND=return] Stop searching.
- nis+ Use NIS+. (Due to the experimental status of the NIS+ implementation under Linux as of this writing, avoid using this.)

+   Idap Use the Lightweight Directory Access Protocol (LDAP).

Here is an example in the /etc/nsswitch.conf file:

```
passwd nis
The /etc/passwd file should already exist and should contain most of the information needed. You might need to adjust the order in which certain service names are listed in the file.
```

Text and GUI Tools for Configuring NIS
Fedora, RHEL, and CentOS have various tools that can make it easy for you to configure a host as a NIS client. The first one is the nurses-based command-line tool, authconfig-tui. This is shown here:

![](bbox=[0.15, 0.68, 0.85, 0.94])