
> **NOTE:** The Trivial File Transfer Protocol server (`tftp-server` package), which is distributed with Fedora, can also be used to provide file transfer service. The `tftpd` daemon is used primarily to provide support for diskless devices, which gather the files they need to boot and run from a TFTP server. Because FTP uses TCP, and TFTP uses UDP, TFTP is considered safer to use over the Internet because it can be deployed with TCP/IP-related security features. Because TFTP is not securable, it is not intended for general, public FTP service and is generally used only on private LANs that are not accessible to public networks. Other FTP server packages now available from the Fedora software repository include ProFTPD (`http://proftpd.org`) and Pure-FTPD (`http://pureftpd.org`).

Red Hat, Inc. and Fedora both use vsFTpd on their own FTP servers (`ftp.redhat.com`). Other organizations in the open source software world have also made the switch to vsFTpd, including Debian Linux (`ftp.debian.org`) and the GNU Project (`ftp.gnu.org`).

Besides security and scalability, vsFTpd was designed for simplicity. Therefore, fewer options exist for configuring vsFTpd than you find in WU-FTPD, an older FTP server package that is still commonly used, so you are expected to rely on standard Linux file and directory permissions to provide refined access to your server. Getting started with vsFTpd, or using it to replace WU-FTPD, is fairly straightforward.

> **NOTE:** Although vsFTpd is the recommended FTP server software in Fedora, the WU-FTPD FTP server software, which was once part of Red Hat Linux, is still available on the Web. However, WU-FTPD is considered by most to be far less secure than vsFTpd and should, therefore, not be used in most cases.

## Quick-starting vsFTpd

By enabling the vsFTpd service, you can almost instantly have an FTP service running with the default values (set in the `/etc/vsftpd/vsftpd.conf` file). The following is a quick procedure for getting your vsFTpd server up and running. In case you didn't install vsFTpd when you originally installed Fedora, install it now by typing:

```
# yum install vsftpd
```

Here's how to start and try out the vsFTpd service.

1. To use the vsFTpd server, you must make sure that the vsFTpd software package is installed:

```
# rpm -q vsftpd
```

2. Enable the vsFTpd server by typing the following line (as root user):

```
# chkconfig vsftpd on
```

3. Start the vsFTpd server as follows:

```
# service vsftpd start
```

4. Try to log in to the FTP server as anonymous (using any password):

```
$ ftp localhost
```

```
Connected to yourhost (127.0.0.1)
220 (vsFTpd 2.2.0)
Name (localhost:chr): anonymous
331 Please specify the password.
Password:
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp>
```

If you saw messages similar to the preceding, your vsFTpd server is now up and running. Next, try to access the server from another computer on the network to be sure that it is accessible.

## Securing vsFTpd

If your FTP server is not accessible to the outside world, you may need to ensure that your network is configured properly and that vsFTpd is secured using one or more security features in Fedora. Security features and/or services that can be configured to allow or block access to vsFTpd include firewalls, TCP wrappers, and Security Enhanced Linux (SELinux).

- **Firewalls** — If your firewall is enabled, it must be set to allow access to port 21 and possibly port 20. The quick way to do that is to run `system-config-firewall` and add FTP as a trusted service. To allow passive FTP from the server, load the `ip_conntrack_ftp` module. The best way to do that is to edit the `/etc/sysconfig/iptables-config` file and change the `IPTABLES_MODULES` line so it appears as follows:

```
IPTABLES_MODULES="ip_conntrack_ftp"
```

- **TCP Wrappers** — You can use TCP wrappers to restrict access to vsFTpd by adding entries to the `/etc/hosts.allow` and/or `/etc/hosts.deny` files (type `man hosts_access` for information). The daemon name to use is `vsftpd`.

- **SELinux** — If SELinux is enabled, it may prevent access to your FTP server that you might normally expect to work. To set SELinux to permissive mode, type `setenforce 0` as root. Or type `man ftp_selinux` to learn how to use SELinux with vsftpd. Refer to Appendix B for information on getting your network services working. In particular, make sure that proper SELinux file contexts are set on files and directories you want to share from vsFTpd and that SELinux booleans are set to allow such features as access to home directories and file uploads.

The next section explains the `/etc/vsftpd/vsftpd.conf` configuration file.

## Configuring vsFTpd

Most of the configuration of vsFTpd is done in the `/etc/vsftpd/vsftpd.conf` file. Although many values are not set explicitly in `vsftpd.conf`, you can override the defaults by setting *option* = *value* statements in this file. You can set such things as which users have access to your vsFTpd server, how logging is done, and how timeouts are set.

Read the following sections for more information about how vsFTpd is configured by default and how you can further configure your vsFTpd server.

## User accounts

Users who can access your vsFTpd server are, by default, the anonymous user and any users with real user accounts on your system. (A *guest* user is simply a real user account that is restricted to its own home directory.) The following lines set these user access features:

```
anonymous_enable=Yes
local_enable=Yes
```

The *anonymous_enable* line lets users log in anonymously using either the *anonymous* or *ftp* user name. If you want to disable access by anonymous users, don't just comment out *anonymous_enable*. Anonymous access is on by default, so you must set *anonymous_enable*=NO to disable it.

Any users with local accounts (in /etc/passwd) and valid passwords can log into the FTP server with *local_enable* set to Yes. By default, *local_enable* is off and disallowed by SELinux. Even with this feature enabled, all user accounts listed in the /etc/vsftpd/user_list file are denied access.

There is another file called /etc/vsftpd/ftpubers that is also a list of users that are not allowed to log in. By default, it has the same contents as the *user_list* file, but the functionality is provided by the PAM facility. If you make changes to *user_list* you may also want to edit *ftpubers* and/or /etc/pam.d/vsftpd.

> **NOTE:** Before you start logging into your vsFTpd server with your personal user name and password, keep in mind that the FTP login service uses clear-text passwords. Because of this fact, a network sniffer is capable of seeing this information. If you want to use an FTP-type interface to access files on an FTP server using your personal account, consider using the OpenSSH (`http://www.openssh.org/`) `sftp` command instead of a normal FTP client. If the server running FTP includes an SSH service, you can use `sftp` to connect to that server using encrypted passwords.

Check the *user_list* file to see which users are denied access to the vsFTpd server. Note that root and other administrative logins are excluded. You can add other users to this list or change the location of the list by setting the *userlist_file* parameter to the file you want. To add a user to the *user_list* or use the *userlist_file* parameter to create a new list, you must also have *userlist_enable* set to Yes (as it is by default). For example:

```
userlist_file=/etc/vsftpd/user_list_local
userlist_enable=Yes
```

If you like, you can change the meaning of the `/etc/vsftpd/user_list` file so that only the users in that list are allowed to use the vsFTpd service. Set `userlist_deny=NO` and change the `/etc/vsftpd/user_list` to include only names of users to whom you want to grant access to the server. All other users, including anonymous and `ftp`, will be denied access.

### Setting FTP access

The vsFTpd server software provides a simple and seemingly secure approach to access permissions. Instead of using settings in the FTP service to selectively prevent downloads and uploads from particular directories (as FTP servers such as WU-FTPD do), you can use standard Linux file and directory permissions to limit access. There are, however, the following general settings in the `/etc/vsftpd/vsftpd.conf` file to let users get files from and put files onto your vsFTpd server.

### Downloading files

Anonymous users can download files from the vsFTpd server by default. Real users, excluding some administrative logins, can download and upload files if enabled, as described in the previous section. The ability to download a particular file or a file from a particular directory is governed by the following basic Linux features:

- **File and directory permissions** — Standard file and directory permissions apply as a means of limiting access to particular files, even in accessible file systems. So, if the root user puts a file with 600 permission (read/write to root only) in the `/var/ftp` directory, an anonymous user is not able to download that file.
- **Root directory** — The root directory (chroot) for anonymous users is `/var/ftp`. The root directory for regular users is the entire computer’s root directory (`/`), although their current directory after connecting to FTP is the user’s home directory, or typically `/home/user`, where *user* is the user name. So an anonymous user is restricted to downloads from the `/var/ftp` directory structure, while a regular user potentially has access to the whole file system. Another possibility is to create *guest* accounts by restricting some or all users to their home directories.

You can use the `chroot_local_user` option to change the root directory for regular users so that they are restricted to their home directory. To restrict all regular users to their home directory when using vsFTpd, add this line to the `vsftpd.conf` file:

```
chroot_local_user=YES
```

To enable the concept of *guest* users, you can choose to limit only selected users to their home directories. You do this by setting `chroot_list_enable` to `YES`, and then adding a list of guest users to a file (noted with the `chroot_list_file` option). The following example lets you add such a list (one user name per line) to the `/etc/vsftpd/chroot_list` file:

```
chroot_list_enable=YES
chroot_list_file=/etc/vsftpd/chroot_list
```
