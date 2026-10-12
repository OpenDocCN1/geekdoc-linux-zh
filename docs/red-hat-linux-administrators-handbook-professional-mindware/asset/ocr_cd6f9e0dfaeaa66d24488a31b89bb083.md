# ## Using a Trivial File Transfer Protocol Server

You may have installed a TFTP server already. It's called the tftpd server. It really isn't an FTP server, because it uses the Trivial File Transfer Protocol instead of the File Transfer Protocol. TFTP uses UDP over IP, an unreliable, packet-oriented transfer method. FTP uses TCP over IP, a reliable, stream-oriented transfer method. TFTP has no provisions for security. FTP has user-authentication provisions for security.

However, a TFTP server works pretty much the same way an FTP server works. The only big difference is that it is *not* meant for anything but an anonymous FTP-like file transfer where no authentication is used.

Many people use TFTP primarily in conjunction with the boot protocol to load diskless workstations, such as X Window System terminals. The TFTP service is disabled by default in the `/etc/inetd.conf` file. You can enable it by removing the \# (comment sign) from the following line:

```
```code
# tftp dgram udp wait root /usr/sbin/tcpd \
 in.tftpd /tftpboot
```
```

After you enable the preceding line, restart the inetd server so that the change will be effective. Note that `/tftpboot` is the directory that TFTP clients can access. Make sure this directory does not contain any files that you don't want to share with anyone. Remember that no authentication is required to access this file, so anyone who can access your server will have access to this directory. You might want to allow only read-only access to files in the directory, as well.