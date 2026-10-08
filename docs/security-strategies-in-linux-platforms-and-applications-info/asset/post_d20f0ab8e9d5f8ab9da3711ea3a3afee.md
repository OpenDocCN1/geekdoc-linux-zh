
## PART 1 Is Linux Really Secure?

The advantage of NIS is that it can start with the files of the shadow password suite. NIS has two disadvantages, however: it is relatively insecure and does not support authentication of Microsoft users or groups. In contrast, LDAP is a more complex authentication scheme, it supports authentication of both Linux/UNIX and Microsoft users and groups.

In a Linux authentication database, a user is typically configured as a member of a group with the same name. For example, if a Linux system has a user name mike, that user is a member of a group named mike. That Linux user mike may be a member of other groups. For example, one group may have print-administration privileges; another group may have access to telephone modem.

To manage this variety of authentication databases, Linux uses the /etc/n.conf file, also known as the name switch file. That file lists databases associated with a number of configuration files in the /etc/ directory, in specific order. That order determines where the local system looks first to verify a username and password. Red Hat includes a descriptive configuration for all databases and, shown in Figure 2-2.

Linux supplements authentication databases with a system known as pluggable authentication modules (PAM). The rules associated with PAM files in the /etc/pam.d/ directory can further specify local access limits for different administrative tools and commands.

Some Linux appliances, such as home routers, include default usernames and password. It is important to configure such appliances with nonempty usernames and strong passwords. One recently detected botnet, named for Chuck Norris, can infect and take over such Linux appliances if their administrators retain standard or weak usernames and passwords. The botnet was detected by Masaryk University researchers in the Czech Republic with the help of a honeypot, which tempts black hackers with seemingly valuable data.

FIGURE 2-2
Red Hat's Authentication Configuration tool.

![](img/c0608a8c8a0777903dfec4ff61fdffa1_63_0.png)

## CHAPTER 2 | Basic Components of Linux Security

# 39

## So Many Access Controls

In Linux, there are several systems known as access controls. Even if you've studied them in other Linux books, it may be difficult to keep them straight. Here's a short primer of various access controls in Linux.

Discretionary access controls are read, write, and execute permissions that can be given to users and groups. Linux includes two types of discretionary access controls: standard octal read, write, and execute permissions; and access control lists (ACLs).

ACLs provide a second layer of discretionary access control. Specifically, they support read, write, and execute permissions that may supersede discretionary access controls. But ACL require additional configuration, as described in Chapter 5.

Mandatory access controls are like SELinux and AppArmor. You'll have to choose one or the other, as these systems are not compatible. While SELinux is the default for Red Hat distributions, AppArmor is the default for many other Linux distributions, including Ubuntu and SUSE.

When used together, discretionary and mandatory access controls provide multiple layers of protection. These controls are usually also coupled with the firewall protection associated with the iptables command. Most iptables rules control access to systems and protocols, making them another layer of access control.

## File Ownership, Permissions, and Access Controls

Everything on Linux is represented by a file. A directory is a special kind of file, which should be executable for users who are allowed to list files on that directory. Other kind of files include devices, commonly used to represent and communicate with certain hardware components, character devices as sound cards, block devices as drives and partitions, and soft links, which can connect across different partitions or volumes.

Every file and directory on a Linux system is owned by a specific user and group. With discretionary access controls, the user owner can set different read, write, and executable permissions for the user owner, the group owner, and all other users.

While a lot can be done with, write, and execute permissions for a file, such permissions may not provide enough control. For an additional layer of permissions, Linux can work with access control lists. To make that happen, the target filesystem must be configured and mounted with the access control list option. Once mounted, you can configure access control masks that supersede regular file permissions. For more details on access control lists and standard file permissions, see Chapter 5.

![](img/c0608a8c8a0777903dfec4ff61fdffa1_64_0.png)

# 40 PART 1 Is Linux Really Secure?

Current Linux distributions include one or two levels of administrative access control. The standard configuration file for custom administrative permissions is /etc/sudoers. Later distributions support fine-grained access to hardware components through the PolicyKit.

## Firewalls and Mandatory Access Controls

Firewalls and mandatory access controls may seem to be unrelated. However, it's common to use them together in a layered defense for Linux systems. The layers go deeper, Several layers of firewalls are available on modern Linux systems. Since the advent of kernel version 2.6, the foundation of the Linux firewall has been the iptables command. Other firewalls are available for services that depend on the Transmission Control Protocol (TCP) Wrappers, like libwrap.so. It's common practice on Linux to supplement these firewalls with mandatory access control systems such as SELinux and AppArmor. SELinux has quite a bit of acclaim because it was developed by and still receives code contributions from the U.S. National Security Agency (NSA). But the configuration of SELinux is somewhat challenging.

Because firewalls and mandatory access controls can be configured differently on every system, you can set up different levels of protection in a trusted network and in areas such as demilitarized zone (DMZ).

## Firewall Options

Of course, you can create a firewall with the iptables command. But that command can be tricky. Some Linux distributions make it easier to configure a firewall with tools like ufw.

![](img/c0608a8c8a0777903dfec4ff61fdffa1_65_0.png)

## CHAPTER 2 | Basic Components of Linux Security

Custom firewalls can include dozens of iptables commands. You can configure a second layer of firewalls for services that use TCP Wrapper libraries. Specifically, if you use a service that depends on libwrap, you can protect that service with directives in /etc/hosts.allow and /etc/hosts.deny. You can block access by address.

Some services allow you to configure a third layer of firewalls. For example, the Samba service can limit access to users on specific networks. The SSH service can be set to accept connections only on nonstandard TCP/IP ports. The Apache service can limit access to certain users and prohibit connections from groups of IP addresses. For more on these services, firewalls for individual services are described in Chapter 9.

You can configure a fourth layer of firewalls for services associated with the /etc/xinetd.conf configuration file, also known as the extended internet service. Those services have configuration files in the /etc/xinetd.d/ directory. For more on protecting these services, see Chapter 6.

## Mandatory Access Control Support

To paraphrase a famous philosopher, networks cannot be protected by firewalls alone. The mandatory access controls associated with SELinux and AppArmor provide another layer of security. When properly configured, these can check access to services and commands to make sure they're run only by intended users, in properly labeled directories.

Proper mandatory access controls make a system more robust. Compromised users, even service users with some level of administrative privileges, can use other services.

However, the configuration of a mandatory access control system requires discipline. For example, you can't just add a new directory to organize FTP server files. With a mandatory access control system like SELinux, you must make sure those directories labeled and configured for their intended purposes.

It's normally best to administer a system from the command-line interface. However, some of these tools are tricky. Some GUI tools can help less-familiar administrators understand more about the service. To that end, Red Hat's SELinux Administration tool, shown in Figure 2-4, is excellent.

> TIP You can't use both SELinux and AppArmor on the system.
