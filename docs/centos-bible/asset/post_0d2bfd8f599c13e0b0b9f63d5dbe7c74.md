
## Part IV Networking

> **NOTE**
>
> The Trivial File-Transfer Protocol server (*tftp* server package), which is distributed with CentOS systems, can also be used to provide FTP service. The *tftpd* daemon is used primarily to provide support for diskless devices, which gather the files they need to boot and run from a TFTP server. TFTP is not intended for general, public FTP service. Because TFTP is considered a security risk to use publicly, it is generally used only on private LANs that are not accessible to public networks. Other FTP server packages now available from the RPMforge software repository include *ProFTPD* (http://proftpd.org) and *Pure-FTPd* (http://pureftpd.org).

Red Hat, Inc. uses *vsftpd* on its own FTP servers (ftp.redhat.com). Other organizations in the Open Source software world have also made the switch to *vsftpd*, including Debian Linux (ftp.debian.org), OpenBSD (ftp.openbsd.org) and the GNU Project (ftp.gnu.org).

Besides security and scalability, *vsftpd* was designed for simplicity. Therefore, fewer options exist for configuring *vsftpd* than you find in *WU-FTPd*, an older FTP server package that is still commonly used, so you are expected to rely on standard Linux file and directory permissions to provide refined access to your server. Getting started with *vsftpd*, or using it to replace *WU-FTPd*, is fairly straightforward.

### Quick-Starting vsFTPd

By enabling the *vsftpd* service, you can almost instantly have an FTP service running with the default values (set in the */etc/vsftpd/vsftpd.conf* file). The following is a quick procedure for getting your *vsftpd* server up and running. In case you didn’t install *vsftpd* when you originally installed CentOS, install it now by typing:

```
# yum install vsftpd
```

Here’s how to start and try out the *vsftpd* service.

1. To use the *vsftpd* server, you must make sure that the *vsftpd* software package is installed.

   ```
   # rpm -q vsftpd
   ```

2. Enable the *vsftpd* server by typing the following line (as **root** user):

   ```
   # chkconfig vsftpd on
   ```

3. Start the *vsftpd* server as follows:

   ```
   # service vsftpd start
   ```

4. Try to log in to the FTP server as **anonymous** (using any e-mail address as the password):

   ```
   $ ftp localhost
   Connected to yourhost (127.0.0.1)
   220 (vsftpd 2.0.7)
   Name (localhost:timothy): anonymous
   331 Please specify the password.
   Password: *****
   230 Login successful.
   Remote system type is UNIX.
   Using binary mode to transfer files.
   ftp>
   ```

If you saw messages similar to the preceding, your vsftpd server is now up and running. Next, try to access the server from another computer on the network to be sure that it is accessible.

> **NOTE** If your FTP server is not accessible to the outside world, you may need to ensure that your network is configured properly and that your firewall allows access to port 21 and possibly port 20. The quick way is to run `system-config-securitylevel` and add FTP as a trusted service. Also, if SELinux is enabled, it may prevent access to your FTP server that you might normally expect to work. To set SELinux to permissive mode, type `setenforce 0` as root. Or type `man ftpd_selinux` to learn how to use SELinux with vsftpd.

The next section explains the `/etc/vsftpd/vsftpd.conf` configuration file.

### Configuring vsFTpd

Most of the configuration of vsftpd is done in the `/etc/vsftpd/vsftpd.conf` file. Although many values are not set explicitly in vsftpd.conf, you can override the defaults by setting *option*=*value* statements in this file. You can set such things as which users have access to your vsftpd server, how logging is done, and how time-outs are set.

Read the following sections for more information about how vsftpd is configured by default and how you can further configure your vsftpd server.

#### User Accounts

Users who can access your vsftpd server are, by default, the anonymous user and any users with real user accounts on your system. A guest user is simply a real user account that is restricted to its own home directory. The following lines set these user access features:

```
anonymous_enable=YES
local_enable=YES
```

The anonymous_enable line lets users log in anonymously using either the anonymous or ftp username. If you want to disable access by anonymous users, don’t just comment out anonymous_enable. Anonymous access is on by default, so you must set anonymous_enable=NO to disable it.

Any users with local accounts in `/etc/passwd` and valid passwords can log into the FTP server with `local_enable` set to YES. An exception to this rule is that, by default, all user accounts listed in the `/etc/vsftpd/user_list` file are denied access.

> **NOTE** Before your start logging into an FTP service with your personal username and password, keep in mind that FTP service uses clear text passwords. Because of this fact, a network sniffer is capable of seeing this information. If you want to use an FTP interface to access files on an FTP server using your personal account, **consider using the `Cypasssh` (`www.openssh.org/`) `sftp` command** instead of a normal FTP client. If the FTP server includes an SSH server, you can use `sftp` to connect to that server using encrypted passwords.

Check the user list file to see which users are denied access to the vsftpd server. Note that **root** and other administrative logins are excluded. You can add other users to this list or change the location of the list by setting the `userlist_file` parameter to the file you want. To add a user to the user list or the `userlist_file` parameter to create a new list, you must also have `userlist_enable` set to YES (as it is by default). For example:

```
userlist_file=/etc/vsftpd/user_list_local
userlist_enable=YES
```

If you like, you can change the meaning of the `/etc/vsftpd/user_list` file so that only the users that list are allowed to use the vsftpd service. Set `userlist_deny=no` and change the `/etc/vsftpd/user_list` to include only names of users to whom you want to grant access to the server. All other users, including anonymous and ftp, will be denied access.

### Setting FTP Access

The vsftpd server software provides a simple and seemingly secure approach to access permissions. Instead of using settings in the FTP service to selectively prevent downloads and uploads of particular directories (as FTP servers like WU-FTPD do), you can use standard Linux file and directory permissions to limit access. There are, however, the following general settings in the `/etc/vsftpd/vsftpd.conf` file to let users get files from and put files onto your vsftpd server.

### Downloading Files

Any users with valid logins (anonymous or real users, excluding some administrative logins) can download files from the vsftpd server by default. The ability to download a particular file or a file from a particular directory is governed by the following basic Linux features:

- **File and Directory Permissions** — Standard file and directory permissions apply as a means of limiting access to particular files, even in accessible file systems. If the **root** user puts a file with 600 permission (Read/Write to **root** only) in the `/var/ftp` directory, an anonymous user is not able to download that file.

- **Root Directory** — The root directory (chroot) for anonymous users is `/var/ftp`. The root directory for regular users is the entire computer's root directory (`/`), although their current directory after connecting to FTP is `/home/user`, where user is the username. So, an anonymous user is restricted to downloads from the `/var/ftp` directory structure, while a regular user potentially has access to the whole file system. Another possibility is to create guest accounts by restricting some or all users to their home directories.
