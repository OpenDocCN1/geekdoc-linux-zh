> **NOTE:** The Trivial File Transfer Protocol server (tftp-server package), which is distributed with Fedora and RHEL systems, can also be used to provide FTP service. The tftp daemon is used primarily to provide support for diskless devices, which gather the files they need to boot and run from a TFTP server. TFTP is not intended for general, public FTP service. Because TFTP is considered a security risk to use publicly, it is generally used only on private LANs that are not accessible to public networks. Another FTP server package now available from the Fedora software repository is ProFTPD (http://proftpd.org).

Red Hat, Inc. itself uses vsFTPd on its own FTP servers (*ftp.redhat.com*). Other organizations in the Linux/GNU world have also made the switch to vsFTPd, including Debian Linux (*ftp.debian.org*) and the GNU Project (*ftp.gnu.org*).

Besides security and scalability, vsFTPd was designed for simplicity. Therefore, fewer options exist for configuring vsFTPd than you find in WU-FTPD, an older FTP server package that is still commonly used, so you are expected to rely on standard Linux file and directory permissions to provide refined access to your server. Getting started with vsFTPd, or using it to replace WU-FTPD, is fairly straightforward.

> **NOTE:** Although vsFTPd is the recommended FTP server software in Fedora and RHEL, the WU-FTPD FTP server software, which was once part of Red Hat Linux, is still available on the Web. However, WU-FTPD is considered by most to be far less secure than vsFTPd and should, therefore, not be used in most cases.

# ### Quick-starting vsFTPd

By enabling the vsFTPd service, you can almost instantly have an FTP service running with the default values (set in the */etc/vsftpd/vsftpd.conf* file). The following is a quick procedure for getting your vsFTPd server up and running. In case you didn't install vsFTPd when you originally installed Fedora, install it now by typing:

```
# yum install vsftpd
```

Here's how to start and try out the vsFTPd service.

+   1. To use the vsFTPd server, you must make sure that the vsFTPd software package is installed.
+      ```
+      # rpm -q vsftpd
+      ```

+   2. Enable the vsFTPd server by typing the following line (as root user):
+      ```
+      # chkconfig vsftpd on
+      ```

+   3. Start the vsFTPd server as follows:
+      ```
+      # service vsftpd start
+      ```

+   4. Try to log in to the FTP server as anonymous (using any e-mail address as the password):