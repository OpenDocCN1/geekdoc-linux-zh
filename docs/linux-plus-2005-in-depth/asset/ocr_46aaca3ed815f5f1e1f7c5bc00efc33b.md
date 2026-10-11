**Table 15-2 Common network services (Continued)**

| Network Service | Type | Port | Description |
|---|---|---|---|
| Secure Shell Daemon (sshd) | Standalone | 22 | Provides a secure alternative to the telnet, rlogin, and rsh utilities by using encrypted communication. Configuration File: `/etc/ssh/sshd_config` |
| Sendmail Email Server (sendmail) | Standalone | 25 | Accepts and sends e-mail to users or other e-mail servers on the Internet using the Simple Mail Transfer Protocol (SMTP). Configuration file: `/etc/sendmail.cf` |
| Squid Proxy Server (squid) | Standalone | 3128 | Allows computers on a network the ability to share one connection to the Internet. It is also known as a proxy server. Configuration file: `/etc/squid/squid.conf` |
| telnet Daemon (in.telnetd) | xinetd | 23 | Allows users who have a telnet utility the ability to log in to the system from across the network and obtain a shell. |
| Very Secure FTP Server (vsftpd) | Standalone | 20 21 | Transfers files to and accepts files from other computers on the network with an FTP utility. Configuration file: `/etc/vsftpd/vsftpd.conf` Users denied FTP access: `/etc/vsftpd/ftpusers` and `/etc/vsftpd.user_list` |
| X Server | Stand-alone | 0 | Generates graphics that will be displayed on a computer on the network that has an X client using the DISPLAY variable on the X server. |

> > **NOTE**
> > By default, you are prevented from logging in and obtaining a shell as the root user to certain network services such as telnet due to entries in the `/etc/security` file. This file lists terminals that the root user is allowed to access. Removing or renaming this file allows the root user to log in and receive a shell across the network.

Some of the network services in Table 15–2 have become a vital component of many networks today; these include DNS, DHCP, Apache, Samba, NFS, FTP, NIS, and the Secure Shell Daemon.