
# Appendix B: Running Network Services

## Table B-1 (continued)

| Feature | Package Names | Startup Script(s) | Daemon | Configuration File(s) |
| --- | --- | --- | --- | --- |
| Login Servers | | | | |
| Telenet | telnet-server | /etc/init.d/xinetd (etc/xinetd.d/telnet) | /usr/sbin/xinetd | /etc/issue.net |
| Telenet with Kerberos Support (Krb5-telnet) | krb5-workstation | /etc/init.d/xinetd (etc/xinetd.d/krb5-telnet) | /usr/sbin/xinetd (/usr/kerberos/sbin/telnet) | /etc/krb5.conf |
| Open Secure Shell (Openssh) | openssh-server | /etc/init.d/sshd | /usr/sbin/sshd | /etc/ssh/* |
| Remote Login (Rlogin) | rsh-server | /etc/init.d/xinetd (etc/xinetd.d/rlogin) | /usr/sbin/xinetd (/usr/sbin/rlogin) | /etc/hosts.equiv $HOME/.hosts |
| Remote Login with Kerberos Support (Klogin) | krb5-workstation | /etc/init.d/xinetd (etc/xinetd.d/klogin) | /usr/sbin/xinetd (/usr/kerberos/sbin/klogin) | /etc/krb5.conf $HOME/.k5login $HOME/klogin |
| (Klogin) | krb5-workstation | /etc/init.d/xinetd (/usr/kerberos/sbin/klogin) | /etc/krb5.conf $HOME/.k5login $HOME/klogin |
| E-mail Servers | | | | |
| Remote Mail Access Servers (IMAP) | dovec | /etc/init.d/dovecot | /usr/sbin/dovecot | /etc/dovecot |
| (POP3) | | /etc/init.d/dovecot | /usr/sbin/dovecot | /etc/dovecot |
| E-mail Transfer Servers (Sendmail) | sendmail sendmail-cf | /etc/init.d/sendmail | /usr/sbin/sendmail | /etc/sendmail.cf /etc/mail.cf |
| (Postfix) | postfix | /etc/init.d/postfix | /usr/sbin/postfix | /etc/postfix/* |

## Table B-1 (continued)

| Feature | Package Names | Startup Script(s) | Daemon | Configuration File(s) |
| --- | --- | --- | --- | --- |
| News Server | | | | |
| Internet News (inn) | inn | /etc/init.d/innd | /usr/bin/innd | /etc/news/* |
| Print Server | | | | |
| Common Printing System | cups | /etc/init.d/cups | /usr/sbin/cups | /etc/cups/* |
| Printing System (CUPS) | cups-libs | | | |
| Network Administration Services | | | | |
| Network Time Server (NTP) | ntp | /etc/init.d/ntpd | /usr/sbin/ntpd | /etc/ntp.conf /etc/ntp/keys |
| Network Portmap (RPC) | portmap | /etc/init.d/portmap | /usr/sbin/portmap | /etc/rpc |
| Samba Administration (swat) | samba-swat | /etc/init.d/xinetd /etc/xinetd.d/swat | /usr/sbin/xinetd /usr/sbin/swat | /etc/smb.conf |
| Network Management (arpwatch) | arpwatch | /etc/init.d/arpwatch | /usr/sbin/arpwatch | /etc/sysconfig/arpwatch |
| Simple Network Management Protocol (SNMP) | net-snmp | /etc/init.d/snmpd /etc/init.d/snmpsd | /usr/sbin/snmp | /etc/snmp/snmp.conf |
| Information Servers | | | | |
| Network Information Server (Ypsbind) | ybind | /etc/init.d/ypbind | /usr/sbin/ypbind | /etc/yp.conf |
| (Ypasswdd) | ypserv | /etc/init.d/ypasswdd | /usr/sbin/yppasswd | /etc/passwd /etc/shadow |
| (Ypserver) | ypserv | /etc/init.d/ypserver | /usr/sbin/ypserver | /etc/ypserver.conf |

## Table B-1 (continued)

| Feature | Package Names | Startup Script(s) | Daemon | Configuration File(s) |
| --- | --- | --- | --- | --- |
| Information Servers (continued) | | | | |
| Dynamic Host Configuration Server (DHCP) | dhcp | /etc/init.d/dhcpd | /usr/sbin/dhcpd | /etc/dhcpd.conf |
| Lightweight Directory Access Protocol (LDAP) | openldap-servers | /etc/init.d/ldap | /usr/sbin/slapd /usr/sbin/slapsd | /etc/openldap/slapd.conf |
| Domain Name Server (DNS) | bind bind-utils bind-chroot | /etc/init.d/named | /usr/sbin/named | /etc/named.conf /var/named/* |
| Reverse Address Resolution Server (RARP) | rarpd | /etc/init.d/rarpd | /usr/sbin/rarpd | /etc/ethers |
| Database Services | | | | |
| MySQL Database | mysql mysql-server | /etc/init.d/mysqld | /usr/libexec/mysqld | /etc/my.cnf |
| Postgresql | postgresql-libs postgresql postgresql-server | /etc/init.d/postgresql | /usr/sbin/postmaster | /var/lib/postgresql/data |
| User Services | | | | |
| Remote Execution Servers (Rsh) | rsh-server | /etc/init.d/xinetd /etc/xinetd.d/rsh | /usr/sbin/xinetd /usr/sbin/in.rsh | /etc/hosts.equiv $HOME/.hosts |
| (Rexec) | rsh-server krb5-workstation | /etc/init.d/xinetd /etc/xinetd.d/rexec | /usr/sbin/xinetd /usr/sbin/in.rexec /usr/sbin/kerberos/sbin/krb5d | /etc/passwd /etc/krb5.conf |

## Table B-1 (continued)

| Feature | Package Names | Startup Script(s) | Daemon | Configuration File(s) |
| --- | --- | --- | --- | --- |
| User Services (continued) | | | | |
| Talk Server (intalkd) | talk-server | /etc/init.d/xinetd /etc/xinetd.d/intalkd | /usr/sbin/xinetd /usr/sbin/intalkd |
| (intalkd) | talk-server | /etc/init.d/xinetd /etc/xinetd.d/intalkd | /usr/sbin/xinetd /usr/sbin/intalkd |
| Finger Server (Finger) | finger-server | /etc/init.d/xinetd /etc/xinetd.d/finger | /usr/sbin/xinetd /usr/sbin/fingerd |
| Identify Users (Rusers) | rusers-server | /etc/init.d/xinetd /etc/xinetd.d/rusers | /usr/sbin/xinetd /usr/sbin/rusersd |
| Write All Users (Rwall) | rwall-server | /etc/init.d/xinetd /etc/xinetd.d/rwall | /usr/sbin/xinetd /usr/sbin/rwalld |
| Security Services | | | | |
| System Logging (rsyslog) | syslogd | /etc/init.d/rsyslog | /usr/sbin/rsyslog | /etc/rsyslog.conf |
| Caching Server (Squid) | squid | /etc/init.d/squid | /usr/sbin/squid | /etc/squid/squid.conf |

# Appendix C: Red Hat Enterprise Linux 5 Features

With its Red Hat Enterprise Linux (RHEL) commercial product line, Red Hat, Inc. is clearly positioning itself after customers looking to put Linux computing in place. So, when you look at the differences between Fedora distributions and RHEL products, many features RHEL products are geared toward deploying multiple desktop and server systems within a large organization.

Despite the fact that Red Hat is aimed primarily at customers who want to build large-scale Linux infrastructures, there are ways of starting with RHEL that require a much smaller investment. Later in this appendix, I describe how to get an evaluation copy of RHEL to turn out an affordable subscription program.

The current major release of Red Hat Enterprise Linux, RHEL 5, was released in March 2007 and is generally available. The latest point release is RHEL 5.2. Information about RHEL and related products is available from Red Hat site: http://www.redhat.com/rhel.

## What’s in RHEL 5?

Red Hat, Inc. released RHEL 5 in March 2007. Of Workstations, Desktops, and Application servers, there are two main categories: Servers and Clients.

- **RHEL 5 Servers**: Subsets of RHEL 5 server products include storage, cluster, and virtualization systems. The RHEL 5 Advanced Platform allows unlimited virtualization, GFS filesystem support, and improved clustering.
- **RHEL 5 Desktops**: For desktop systems, there are Workstation, Desktop, and virtualization systems.

While there are many new features in RHEL 5 compared to RHEL 4, here are some of the most striking features:

- **Virtualization**: RHEL 5 virtualization features are based on XenSource. XenServer is owned by Citrix Systems Inc. (http://www.citrixserver.com) through a recent acquisition. The concept of virtualization is to allow multiple operating systems to run on a single computer. For RHEL 5, this includes the ability to run multiple instances of RHEL 5 on one machine (in what is called parvirtualization). In most cases, specialized hardware is needed, such as Intel Virtualization Technology or AMD Virtualization processors.

Virtualization is seen as a critical feature for enterprise computing, where often a single machine is configured to run only a single application. With virtualization, a large enterprise can have multiple virtualized operating systems each running a single application and sharing the same hardware. As demand increases for a particular service, the entire virtual/OS can be moved to a different computer or duplicated to handle more load.

Virtualization also improves efficiency in other ways. For example, virtualization makes it easier to back up snapshots of the operating system, deploy systems in different ways, and enable virtual desktops and clients.

- **Security Enhanced Linux (SELinux)** continues to be one of the main features that Red Hat offers to distinguish itself from other Enterprise peers. With tools such as SELinux Troubleshooter and SELinux Management Tool, it becomes easier for systems administrators to lock down security on many of the most important services. We include Web service (httpd), name service (bind), network information services (ypbind), and DHCP (dhcp).

- **Software Package Management**: With RHEL 5, the yum facilities have become the backbone of the software installation and maintenance features. Improvements to anaconda allow RHEL 5 servers to install from multiple-enabled software repositories. Graphical tools such as PackageKit make it easy to get updates, search for packages, and add more software.

Other features of RHEL 5 desktop and server systems include (but not limited to):

- **Linux 2.6**: The 2.6 kernel is part of both the Fedora and RHEL distributions. Features in the 2.6 kernel make it particularly valuable in RHEL as is its ability to handle more processors, larger memory pools, more devices, larger file systems, and higher-bandwidth networks, than could the previous major kernel release (2.4).

- **GNOME and KDE desktops**: Like Fedora, RHEL 5 offers both GNOME and KDE desktop software, with GNOME installed by default. Aside from them, logos and backgrounds being different, you can follow most of the descriptions of Fedora desktop features in Chapter 3 to learn about how the RHEL 5 desktops work.
