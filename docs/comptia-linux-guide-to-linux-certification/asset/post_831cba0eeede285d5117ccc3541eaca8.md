
Table 12-2 Common well-known ports

| Service | Port |
| :--- | :--- |
| FTP | TCP 20, 21 |
| Secure Shell (SSH) | TCP 22 |
| Telnet | TCP 23 |
| SMTP | TCP 25 |
| HTTP / HTTPS | TCP 80 / TCP 443 |
| rlogin | TCP 513 |
| DNS | TCP 53, UDP 53 |
| Trivial FTP (TFTP) | UDP 69 |
| POP3 / POP3S | TCP 110 / TCP 995 |
| NNTP / NNTPS | TCP 119 / TCP 563 |
| IMAP4 / IMAP4S | TCP 143 / TCP 993 |

![](img/c27875544958897d817484d558c208c8_580_0.png)

Most systems do not contain the inetd or xinetd daemons by default, but you can install xinetd from a software repository.

The inetd daemon is configured by editing the /etc/inetd.conf file. For example, if you install the telnet daemon, you can configure the following line within /etc/inetd.conf to ensure that it can be started by inetd:

```
[root@server1 ~]# grep telnet /etc/inetd.conf
	telnet stream tcp nowait root /usr/sbin/tcpd /usr/sbin/in.telnetd
[root@server1 ~]#
```

The preceding output displays the full path to the telnet daemon (/usr/sbin/in.telnetd).

The xinetd daemon is configured via entries within the /etc/xinetd.conf file. Normally, this file incorporates all of the files in the /etc/xinetd.d directory as well. Most daemons that are managed by xinetd are configured by files in the /etc/xinetd.d directory named after the daemons. For example, if you install the telnet daemon, you can configure it to be started by xinetd via the /etc/xinetd.d/telnet file, as shown in the following output:

```
[root@server1 ~]# cat /etc/xinetd.d/telnet
service telnet
{
    flags           = REUSE
    socket_type     = stream
    wait            = no
    user            = root
    server          = /usr/sbin/in.telnetd
    log_on_failure  += USERID
    disable         = no
}
[root@server1 ~]#
```

Large network daemons are rarely started by inetd or xinetd. Instead, they are stand-alone daemons that are started at boot time from rc scripts as part of the UNIX SysV or Systemd system initialization process.

Many stand-alone and inetd/xinetd-managed daemons also have configuration files that control how they operate and indicate the pathname to other important files used by the daemon. For simplicity, many of these daemons store all information in only one configuration file that contains comments that indicate the syntax and purpose of each line. As a result, these configuration files can be very large; the configuration file used by the Apache Web Server is often several hundred lines long. In addition to this, most stand-alone network daemons do not use the system log daemon (syslogd) or Systemd journal daemon (journald) to log information related to their operation. Instead, they log this information themselves to subdirectories of the same name underneath the /var/log directory. For example, log files for the Samba daemon are located in the /var/log/samba directory.

Table 12-3 lists the names and features of network services that are commonly found on Linux computers that participate in a network environment. You’ll learn how to configure many of these network services in this chapter as well as in Chapter 13.

Table 12-3 Common network services

| Network Service | Type | Port | Description |
| :--- | :--- | :--- | :--- |
| Apache Web Server (httpd) | Stand-alone | TCP 80<br>TCP 443 | Serves Web pages using HTTP/HTTPS to other computers on the network that have a Web browser<br>Configuration file: /etc/httpd/conf/httpd.conf or<br>/etc/apache2/apache2.conf |
| BIND / DNS Server (named) | Stand-alone | TCP 53<br>UDP 53 | Resolves fully qualified domain names to IP addresses for a certain namespace on the Internet<br>Configuration file: /etc/named.conf |
| DHCP Server (dhcpd) | Stand-alone | UDP 67<br>UDP 68 | Provides IP configuration for computers on a network<br>Configuration file: /etc/dhcp/dhcpd.conf |
| Washington University FTP Server (in.ftpd) | inetd/xinetd | TCP 20<br>TCP 21<br>UDP 69 | Transfers files to and accepts files from other computers on the network with an FTP utility<br>Configuration file: /etc/ftpaccess<br>Hosts denied FTP access: /etc/ftphosts<br>Users denied FTP access: /etc/ftpusers<br>FTP data conversions /etc/ftpconversions |
| Very Secure FTP Server (vsftpd) | Stand-alone | TCP 20<br>TCP 21<br>UDP 69 | Transfers files to and accepts files from other computers on the network with an FTP utility. Configuration file: /etc/vsftpd/vsftpd.conf<br>Users denied FTP access: /etc/vsftpd/ftpusers and /etc/vsftpd.user_list |
| Internetwork News Server (innd) | Stand-alone | TCP 119<br>TCP 563 | Accepts and manages newsgroup postings and transfers them to other news servers<br>Configuration file: /etc/news/innd.conf |
| NFS Server (rpc.nfsd) | Stand-alone | TCP 2049 | Shares files to other computers on the network that have an NFS client utility<br>Configuration file: /etc/exports |
| NIS Server (ypserv & ypbind) | Stand-alone | TCP 111 | Shares configuration information to NIS clients that are members of an NIS domain<br>Configuration file: /etc/ypserv.conf |
| POP3 Server (pop3d) | Stand-alone | TCP 110<br>TCP 995 | Allows users with an e-mail reader to obtain e-mail from the server using the Post Office Protocol version 3 |
| IMAP4 Server (imapd) | Stand-alone | TCP 143<br>TCP 993 | Allows users with an e-mail reader to obtain e-mail from the server using the Internet Message Access Protocol |
| Sendmail Email Server (sendmail) | Stand-alone | TCP 25 | Accepts and sends e-mail to users or other e-mail servers on the Internet using the Simple Mail Transfer Protocol (SMTP)<br>Configuration file: /etc/sendmail.cf |
| Postfix Email Server (postfix) | Stand-alone | TCP 25 | Accepts and sends e-mail to users or other e-mail servers on the Internet using the Simple Mail Transfer Protocol (SMTP).<br>Configuration file: /etc/postfix/main.cf |
| rlogin Daemon (in.rlogind) | inetd/xinetd | TCP 513 | Allows users who use the rlogin and rcp utilities the ability to copy files and obtain shells on other computers on the network |
| rsh Daemon (in.rshd) | inetd/xinetd | TCP 514 | Allows users who use the rsh utility the ability to run commands on other computers on the network |
| Samba Server (smbd & nmbd) | Stand-alone | TCP 137<br>TCP 138<br>TCP 139<br>TCP 445 | Allows Windows users to view shared files and printers on a Linux server<br>Configuration file: /etc/samba/smb.conf |
| Secure Shell Daemon (sshd) | Stand-alone | TCP 22 | Provides a secure alternative to the telnet, rlogin, and rsh utilities by using encrypted communication<br>Configuration file: /etc/ssh/sshd_config |
| Squid Proxy Server (squid) | Stand-alone | TCP 3128 | Allows computers on a network to share one connection to the Internet. It is also known as a proxy server<br>Configuration file: /etc/squid/squid.conf |
| telnet Daemon (in.telnetd) | inetd/xinetd | TCP 23 | Allows users who have a telnet utility the ability to log in to the system from across the network and obtain a shell |

## Remote Administration

As we discussed in Chapter 6, Linux servers are typically installed on a rackmount server system that is located on a rack in a server room and administered remotely. There are several ways to perform command-line and graphical administration of remote Linux servers, including telnet, remote commands, Secure Shell (SSH), and Virtual Network Computing (VNC).

### Telnet

The easiest way to perform administration on a remote Linux computer is via a command-line interface. The `telnet` command has traditionally been used to obtain a command-line shell on remote UNIX and Linux servers across the network that run a telnet server daemon. Nearly all Macintosh, Linux, and UNIX systems come with a `telnet` command. For Windows systems, you can download the free Putty program at `www.chiark.greenend.org.uk/~sgtatham/putty/` to start a telnet session to another computer.

The telnet server daemon is not installed by default on most modern Linux distributions, but it can easily be installed from a software repository. On systems that use the Systemd system initialization process, such as Fedora 20, the telnet server daemon is managed directly by Systemd as a stand-alone daemon. On other systems, such as Ubuntu Server 14.04, the telnet server daemon is managed by inetd or xinetd.

![](img/c27875544958897d817484d558c208c8_583_0.png)

> By default, you are prevented from logging in and obtaining a shell as the root user to certain network services such as telnet due to entries in the /etc/security file. Removing or renaming this file allows the root user to log in and receive a shell across the network using the telnet command.

Once the telnet daemon has been configured, you can connect to it from a remote computer. Simply specify the host name or IP address of the target computer to the `telnet` command and log in with the appropriate user name and password. A shell obtained during a telnet session runs on a pseudoterminal (a terminal that does not obtain input directly from the computer keyboard) rather than a local terminal, and it works much the same way a normal shell does: you can execute commands and use the `exit` command to kill the BASH shell and end the session. A sample telnet session is shown in the following output using a computer with a host name of `server1`:

```
[root@server1 ~]# telnet server1
Trying 192.168.1.105...
Connected to server1.
Escape character is '^]'.
Fedora release 20 (Heisenbug)
Kernel 3.11.10-301.fc20.x86_64 on an x86_64 (1)
server1 login: root
Password: lNXrocks!
Last login: Fri Oct 24 16:55:33 from 192.168.1.100
[root@server1 ~]# who
(unknown) :0 2015-10-24 16:15 (:0)
root tty2 2015-10-24 16:16
root pts/0 2015-10-24 16:55 (server1)
[root@server1 ~]# exit
```
