
1. To use the vsFTpd server, you must make sure that the vsFTpd software package is installed.
   `# rpm -q vsftpd`
2. Enable the vsFTpd server by typing the following line (as root user):
   `# chkconfig vsftpd on`
3. Start the vsFTpd server as follows:
   `# service vsftpd start`
4. Try to log in to the FTP server as anonymous (using any e-mail address as the password):
   ```
   $ ftp localhost
   Connected to yourhost.
   220 (vsFTpd 1.2.1)
   530 Please login with USER and PASS
   Name (localhost:chris): anonymous
   331 Please specify the password.
   Password: ******
   230 Login successful.
   Remote system type is UNIX.
   Using binary mode to transfer files.
   ftp>
   ```

If you saw messages similar to the preceding, your vsFTpd server is now up and running. Next, try to access the server from another computer on the network to be sure that it is accessible.

> NOTE: If your FTP server is not accessible to the outside world, you may need to ensure that your network is configured properly and that your firewall allows access to port 21. Refer to Appendix C for information on getting your network services working.

The next section explains the `/etc/vsftpd/vsftpd.conf` configuration file.

## Configuring vsFTpd

Most of the configuration of vsFTpd is done in the `/etc/vsftpd/vsftpd.conf` file. Although many values are not set explicitly in `vsftpd.conf`, you can override the defaults by setting *option=value* statements in this file. You can set such things as which users have access to your vsFTpd server, how logging is done, and how timeouts are set.

Read the following sections for more information about how vsFTpd is configured by default and how you can further configure your vsFTpd server.

### User accounts

Users who can access your vsFTPd server are, by default, the anonymous user and any users with real-user accounts on your system. (A *guest* user is simply a real user account that is restricted to its own home directory.) The following lines set these user access features:

```text
anonymous_enable=YES
local_enable=YES
```

The `anonymous_enable` line lets users log in anonymously using either the anonymous or `ftp` user name. Any users with local accounts (in `/etc/passwd`) can log into the FTP server with `local_enable` set to `YES`. An exception to this rule is that, by default, all user accounts listed in the `/etc/vsftpd.user_list` file are denied access.

> **NOTE:** If you want to disable access by anonymous users, don't just comment out `anonymous_enable`. Anonymous access is on by default, so you must set `anonymous_enable=NO` to disable it.

Check the `vsftpd.user_list` file to see which users are denied access to the vsFTPd server. Note that root and other administrative logins are excluded. You can add other users to this list or change the location of the list by setting the `userlist_file` parameter to the file you want. To add a user to the `vsftpd.user_list` or use the `userlist_file` parameter to create a new list, you must also have `userlist_enable` set to `YES` (as it is by default). For example:

```text
userlist_file=/etc/vsftpd.user_list_local
userlist_enable=YES
```

If you like, you can change the meaning of the `/etc/vsftpd.user_list` file so that only the users in that list are allowed to use the vsFTPd service. Set `userlist_deny=NO` and change the `/etc/vsftpd.user_list` to include only names of users to whom you want to grant access to the server. (All other users, including anonymous and ftp, will be denied access.)

### Setting FTP access

The vsFTPd server software provides a simple and seemingly secure approach to access permissions. Instead of using settings in the FTP service to selectively prevent downloads and uploads of particular directories (as FTP servers such as WU-FTPD do), you can use standard Linux file and directory permissions to limit access. There are, however, the following general settings in the `/etc/vsftpd/vsftpd.conf` file to let users get files from and put files onto your vsFTPd server.

### Downloading files

Any users with valid logins (anonymous or real users, excluding some administrative logins) can download files from the vsftpd server, by default. The ability to download a particular file or a file from a particular directory is governed by the following basic Linux features:

- **File and directory permissions** — Standard file and directory permissions apply as a means of limiting access to particular files, even in accessible file systems. So, if the root user puts a file with 600 permission (read/write to root only) in the /var/ftp directory, an anonymous user is not able to download that file.
- **Root directory** — The root directory (chroot) for anonymous users is /var/ftp. The root directory for regular users is the entire computer’s root directory (/), although their current directory after connecting to FTP is /home/user, where *user* is the user name. So an anonymous user is restricted to downloads from the /var/ftp directory structure, while a regular user potentially has access to the whole file system. Another possibility is to create *guest* accounts by restricting some or all users to their home directories.

You can use the chroot_local_user option to change the root directory for regular users so that they are restricted to their home directory. In general you will not want to do this, because using the same user name and password for general Linux logins doesn’t place such restrictions on your users. To restrict all regular users to their home directory when using vsftpd, add this line to the vsftpd.conf file:

```
chroot_local_user=YES
```

To enable the concept of *guest* users, you can choose to limit only selected users to their home directories. You do this by setting chroot_list_enable to YES, then adding a list of *guest* users to a file noted with the chroot_list_file option. The following example lets you add such a list (one user name per line) to the /etc/vsftpd.chroot_list file:

```
chroot_list_enable=YES
chroot_list_file=/etc/vsftpd.chroot_list
```

> **TIP**: To restrict a user to FTP access only, set the user’s shell to /sbin/nologin in the /etc/passwd file.

You can add a setting to the vsftpd.conf file to affect how files are downloaded. To enable ASCII downloads, you can enable that feature as follows:

```
ascii_download_enable=YES
```

Without making that change, all downloads are done in binary mode. Although vsftpd will seem to allow the user to change to *ascii* mode, *ascii* mode will not work if this setting is NO.

### Uploading (writing) files from local users

Two values set in the vsftpd.conf file allow the uploading of files during a vsftpd session. The following defaults allow any users with regular, local user accounts to upload files:

```
write_enable=YES
local_umask=022
```

The `write_enable` value must be `YES` if you intend to allow any users the ability to write to the FTP server. The `umask=022` value sets the default file permission used when a local user creates a file on the server. (The 022 value causes files created to have 644 permission, allowing the user read and write permission and everyone else only read permission.)

As with downloading, uploading in *ascii* mode is prohibited by default. Though *ascii* downloads create a potential security hole for draining resources from your server, *ascii* uploads are apparently not as dangerous and can be useful for uploading text files. To allow *ascii* uploads, add the following line:

```
ascii_upload_enable=YES
```

### Uploading (writing) files from anonymous users

The ability to upload files is turned off for anonymous FTP users. If you want to turn it on, add the following line to the vsftpd.conf file:

```
anon_upload_enable=YES
```

You must also make sure that the `/var/ftp` directory contains one or more directories with write permissions open to anonymous users. For example, you might want to create an *incoming* directory and open its permissions (`chmod 777 /var/ftp/incoming`).

Files uploaded by anonymous users will be created with 600 permission by default (read/write permission for the ftp user, not accessible to any other users so that even the user who uploaded the files can’t remove them). To allow 644 permission, for example, you can add the following line:

```
anon_umask=022
```

When you allow the anonymous user to upload files, you can grant limited ability to change the files he or she uploads. By adding the following line, you can allow anonymous users to rename or delete any files owned by anonymous users (provided that the files are in directories for which the users have write permission):

```
anon_other_write_enable=YES
```

If you also want to allow anonymous users to create their own directories, add the following:

```
anon_mkdir_write_enable=YES
```
