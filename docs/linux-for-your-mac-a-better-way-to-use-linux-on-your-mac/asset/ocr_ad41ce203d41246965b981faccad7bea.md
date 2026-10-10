![](bbox=[0.18, 0.08, 0.82, 0.37])

Figure 10.13  KDE includes a number of system and network monitoring tools, such as the ksysguard client and daemon.

![](bbox=[0.18, 0.42, 0.82, 0.66])

Figure 10.14  KDE’s kwuftpd client is a graphical interface, which administers FTP access for your system if you use the wuftpd FTP server.

/etc/inetd.conf. By default, LinuxPPC 2000 Q4 does not use wuftpd, but instead uses proftpd, like this:

```
```
... # These are standard services. 

#  ftp  stream tcp nowait  root  /usr/sbin/tcpd in.profFTPd
... 
```
```

To change your FTP server, change the example line to read:

```
```
ftp  stream tcp nowait root /usr/sbin/tcpd  in.wuftpd
```
```