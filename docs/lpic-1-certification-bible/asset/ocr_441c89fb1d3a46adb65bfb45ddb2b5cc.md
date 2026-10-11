# Performing Security Administration Tasks

**1.13 Networking Services**

+   • **Configure and manage inetd and related services.** Configure which services are available through inetd, use tcpwrappers to allow or deny services on a host-by-host basis, manually start, stop, and restart internet services, configure basic network services including telnet and ftp. Includes managing inetd.conf, hosts.allow, and hosts.deny.

**1.14 Security**

+   • **Perform security admin tasks.** Configure and use TCP wrappers to lock down the system, list all files with SUID bit set, determine if any package (rpm or .deb) has been corrupted, verify new packages prior to install, use setgid on dirs to keep group ownership consistent, change a user’s password, set expiration dates on user’s passwords, obtain, install and configure ssh

An administrator can do several things to secure a newly installed system. These involve locking down some services with TCP wrappers and managing users and groups.

> Assigning and using passwords are topics covered in more detail in Chapter 10.

# Configuring TCP wrappers

The *tcpd* daemon, also known as the *TCP wrappers package*, can be used to limit what connections can be made to some network services. This way you can limit access to the services to only authorized users. It is easy to configure and integrate into a working system. No changes need to be made to the network daemons, only minor changes to the *inetd.conf* file. For example, if your *inetd.conf* file currently has the following entry for the FTP server:

```
ftp\t\tstream\ttcp\t\tnowait\troot\t\t/usr/sbin/in.ftpd\n\t\tin.ftpd -l -a
```