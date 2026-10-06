# Chapter 20: Setting Up an FTP Server 833

user puts a file with 600 permission (read/write only) in the /var/ftp directory, an anonymous user is not able to download that file.

+   * Root directory — The root directory (chroot) for anonymous users is /var/ftp. The root directory for regular users is the entire computer's root directory (/), although their current directory after connecting to FTP is /home/user, where user is the user name. So an anonymous user is restricted to downloads from the /var/ftp directory structure, while a regular user potentially has access to the whole file system. Another possibility is to create guest accounts by restricting some or all users to their home directories.

You can use the入手_local_user option to change the directory for regular users so that they are restricted to their home directory. To restart vsFTP, add this line to your vsftpd.conf file:

```
chroot_local_user=YES
```

To enable the concept of guest users, you can choose to limit only selected users to their home directories. You do this by setting chroot_list_enable=YES, and then adding a list of guest users to a file noted with the chroot_list_file path. The following examples let you add such a list (one user name per line) to the /etc/vsftpd/chroot_list file:

```
chroot_list_enable=YES
chroot_list_file=/etc/vsftpd/chroot_list
```

> TIP: To restrict a user to FTP access only, set the user's shell to /sbin/nologin in the /etc/passwd file. Do this by using the system-config-users command or usermod command and changing properties for the user, as described in Chapter 11.

You can add a setting to the vsftpd.conf file to affect how files are downloaded. To enable ASCII downloads, you can enable that follows:

```
ascii_download_enable=YES
```

Without making a change, all downloads are done in binary mode. Although vsFTPD will allow the user to enable change to ascii mode, ascii mode will not work if this setting is NO. Allowing ASCII file transfers is considered a security risk (vulnerable to denial-of-service attacks from an FTP client using the size command to check the size of files on the server) and should be avoided. With ASCII downloads disabled, it is up to the client side to handle ASCII mangling when required.

# Uploading (writing) files from local users

Two values set in the vsftpd.conf file allow the uploading of files during a vsFTPD session. The following defaults allow any users with regular, local account access to upload files: