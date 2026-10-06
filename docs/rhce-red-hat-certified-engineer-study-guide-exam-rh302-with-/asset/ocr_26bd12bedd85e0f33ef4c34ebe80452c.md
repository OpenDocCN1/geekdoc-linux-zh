sync:x:0:sync:/sbin/bin/sync
shutdown:x:6:0:shutdown:/sbin/sbin/shutdown
halt:x:7:0:halt:/sbin/sbin/halt
mail:x:8:12:mail:/var/spool/mail:
news:x:9:13:news:/var/spool/news
uucp:x:10:14:uucp:/var/spool/uuc
operator:x:11:0:operator:/root
games:x:12:100:games:/usr/games
gopher:x:13:30:gopher:/usr/lib/gopher-data
ftp:x:14:50:FTP:/home/ftp:
nbody:x:99:99:Nobody:/

In particular, the nobody account has no associated home directory or shell and, therefore, cannot log in to the system. The httpd process, and an intruder who compromises the nobody account can cause significant harm—for example, by killing processes—but far less harm than possible via a compromised root account.

# Network Security

If a computer is connected to a network, you should consider the following additional security measures in addition to those described in the preceding section.
as a start, you should not run telnet, rcp, rexec, rlogin, or rsh servers; instead, you should install an ssh server. Unlike ssh, the telnet, rcp, rexec, rlogin, and rsh servers send passwords over the network in clear. Unless you use ssh, someone running a packet sniffer can easily obtain important passwords and use them to compromise your system. For the same reason, unless you need it, you should not install an FTP server, particularly an anonymous FTP server. If you need the functions provided by FTP, but don't require FTP as such, you may be able to use scp, which is based on ssh.
You should remove unused services from /etc/rc.d and /etc/inetd.conf and configure TCP wrappers to protect services that remain in /etc/inetd.conf. By removing an unused service from /etc/inetd.conf, you eliminate the possibility that the unused service can be used to compromise your system. Generally, it is also a good idea to remove finger, netstat, and systat, which can provide a bad-intruder with potentially useful information about your system. On the other hand, you should run identd, which can help track an intruder by confirming the identity of the user account used to request a TCP service.