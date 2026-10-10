220 (vsFTpd 2.0.7)
Name (localhost:timothy): anonymous
331 Please specify the password.
Password: *****
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp>

If you saw messages similar to the preceding, your vsFTpd server is now up and running. Next, try to access the server from another computer on the network to be sure that it is accessible.

**NOTE** If your FTP server is not accessible to the outside world, you may need to ensure that your network is configured properly and that your firewall allows access to port 21 and possibly port 20. The quick way is to run `system-config-securitylevel` and add FTP as a trusted service. Also, if SELinux is enabled, it may prevent access to your FTP server that you might normally expect to work. To set SELinux to permissive mode, type `setenforce 0` as root. Or type `man ftpd_selinux` to learn how to use SELinux with vsftpd.

The next section explains the `/etc/vsftpd/vsftpd.conf` configuration file.

# ## Configuring vsFTpd

Most of the configuration of vsFTPd is done in the `/etc/vsftpd/vsftpd.conf` file. Although many values are not set explicitly in vsftpd.conf, you can override the defaults by setting *option*=*value* statements in this file. You can set such things as which users have access to your vsFTpd server, how logging is done, and how time-outs are set.

Read the following sections for more information about how vsFTpd is configured by default and how you can further configure your vsFTpd server.

# ### User Accounts

Users who can access your vsFTpd server are, by default, the anonymous user and any users with real user accounts on your system. A guest user is simply a real user account that is restricted to its own home directory. The following lines set these user access features:

```
anonymous_enable=YES
local_enable=YES
```

The anonymous_enable line lets users log in anonymously using either the anonymous or ftp username. If you want to disable access by anonymous users, don’t just comment out anonymous_enable. Anonymous access is on by default, so you must set anonymous_enable=NO to disable it.