# Chapter 20: Setting Up an FTP Server 831

4. Try to log in to the FTP server as anonymous (using any e-mail address as the password):

```
$ ftp localhost
Connected tohost (127.0.0.1)
220 (vsFTpd 2.0.7)
Name (localhost:chris): anonymous
331 Please specify the password.
Password: ******
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp
```

If you saw messages similar to the preceding, your vsFTpd server is up and running. Next, try to access the server from another computer on the network to be sure.

> NOTE: If your FTP server is not accessible to the outside world, you may need to ensure that your network is configured properly and your firewall allows access to port 21 and possibly port 20. The quick way is to use system-config-firewall and add FTP as a trusted service. Also, if SELinux is enabled, it may prevent access to your FTP server that you would normally expect it to work. To disable SELinux, type setenforce 0 as root. Or type manage ftp_selinux to learn how to use SELinux with vsFTpd. Refer to Appendix B for information on getting your network services working.

The next section explains the /etc/vsftpd/vsftpd.conf file.

# Configuring vsFTPd

Most of the configuration of vsFTpd is done in the /etc/vsftpd/vsftpd.conf file. Although many values are not explicitly in vsftpd.conf, you can override the defaults by setting option=value statements in this file. You can set such things as which users have access to your vsFTpd server, how logging is done, and how timeouts are set.

Read the following sections for more information about how vsFTpd is configured by default and how you can configure your vsFTpd server.

# User accounts

Users who can access your vsFTpd server are, by default, the anonymous user and any users with real user accounts on your system. (A guest is simply a real user account that is restricted to its one home directory.) The following lines set these user account features:

```
anonymous_enable=YES
local_enable=YES
```

The anonymous_enable line lets users log in either the anonymous or ftp user name. If you want to disable access by anonymous users, don't just comment out