stream-oriented transfer method. TFTP has no provisions for security.
FTP has user-authentication provisions for security.

However, a TFTP server works pretty much the same way as an FTP server works. The only big difference is that it is not meant for anything but an anonymous FTP-like file transfer where no authentication is used.

Many people use TFTP primarily in conjunction with the bootp protocol to load diskless workstations, such as X Windows terminals. The TFTP service is disabled by default in the /etc/inetd.conf file. You can enable it by removing the # (comment sign) from the following line:

```
# tftp dgram udp wait root /usr/sbin/tcpd \
 in.tftpd /tftpboot
```

After you enable the preceding line, restart the inetd server so that the change will be effective. Note that /tftpboot is the directory that TFTP clients can access. Make sure this directory does not contain any files that you don't want to share with anyone. Remember that no authentication is required to access this file, so anyone who can access your server will have access to this directory. You might want to allow only read-only access to files in the directory, as well.