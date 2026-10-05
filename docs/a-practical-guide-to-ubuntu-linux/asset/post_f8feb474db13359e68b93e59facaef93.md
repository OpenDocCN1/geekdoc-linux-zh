
no_anon_password

YES skips asking anonymous users for passwords.

Default: NO

deny_email_enable

YES checks whether the password (email address) that an anonymous user enters is listed in /etc/vsftpd.banned_emails or another file specified by banned_email_file. If it is, the user is not allowed to log in the system. NO does not perform this check. Using gufw (page 876) or iptables (page 863) to block specific hosts is generally more productive than using this parameter.

Default: NO

banned_email_file

The name of the file consulted with /etc/vsftpd.banned_emails when banned_email_enable is set to YES.

Default: /etc/vsftpd.banned_emails

# THE WORKING DIRECTORY AND THE chroot JAIL

When a user logs in on a vsftpd server, standard filesystem access permissions control directories and files the user can access and how the user can access them. Three basic parameters control how a user is logged in on a vsftpd server:

- The user ID (UID)
- The initial working directory
- The root directory

By default, the vsftpd server sets the user ID of a local user to that user's username and sets the user ID of an anonymous user to ftp. A local user starts in her home directory and an anonymous user starts in /srv/ftp.

By default, anonymous users are placed in chroot jail for security; local users are not. For example, when an anonymous user logs in on a vsftpd server, his home directory is /srv/ftp. All users, however, that his home directory is /. The user sees the directory at /srv/ftp/upload. The user cannot see, or work with, for example, the /home,/user/local, or /tmp directory because the user is in a chroot jail. For more information refer to "Setting Up a chroot Jail" on page 466.

You can use the chroot_local_user option to put each local user in a chroot jail whose root is the user's home directory. You can use chroot_list_enable to put selected local users in chroot jails.

### chroot_list_enable

Upon login, YES checks whether a local user is listed in /etc/vsftpd.chroot_list (page 711) or another file specified by chroot_list_file.

# 704 CHAPTER 19 FTP: TRANSFERRING FILES ACROSS A NETWORK

When a user is in the list and chroot_local_user is set to NO, the user is put in a chroot jail in his home directory. Only users listed in /etc/vsftptd.chroot_local are put in chroot jails.

When a user is in the list and chroot_local_user is set to YES, the user is not put in a chroot jail. Users not listed in /etc/vsftptd.chroot_list are put in chroot jails.

Default: NO

### chroot_local_user

See chroot_list_enable. Set to NO for a more open system, remember to add new users to the chroot_list_file as needed when you add users to system. Set to YES for a more secure system. New users are automatically restricted unless you add them to chroot_list_file.

Default: NO

### chroot_list_file

The name of the file consulted when chroot_list_enable is set to YES.

Default: /etc/vsftptd.chroot_list

### passwd_chroot_enable

YES allows you to change the location of the chroot jail that the chroot_list_enable and chroot_local_user settings impose on a local user.

The location of the chroot jail can be moved up the directory structure by including a ../ within the home directory string for user in /etc/passwd. This change has no effect on the system login, just as a . command has no effect on the working directory.

For example, changing the home directory field in /etc/passwd (page 494) for Sam from /home/sam to /home/../sam Sam cd to /home after logging in vsftpd. Given the proper permissions, Sam can now view files and collaborate with another user.

Default: NO

### secure_chroot_dir

The name of an empty directory that is not writable by the user ftp. The vsftpd server uses this directory as a secure chroot jail when the user does not need access to the filesystem.

Default: /var/run/vsftptd/empty

### local_root

After a user logs in on the server, this directory becomes the user’s working directory. No error results if the specified directory does not exist.

Default: none

# DOWNLOADING AND UPLOADING FILES

By default, any user—whether local or anonymous—can download files from the vsftpd server, assuming proper filesystem access and permissions. You must change write_enable from NO (default) to YES to permit local users to upload files. By default, local_umask is set to 077, giving uploaded files 600 permissions (page 215). These permissions allow only the user who created a file to download and overwrite it. Change local_umask to 022 to allow users to download other users' files.

Security Refer to "Security" on page 699 for information on the security hole that is created when you allow local users to upload files.

The following actions set vsftpd to allow anonymous users to upload:

- 1. Set write_enable (page 705) to YES.
- 2. Create a directory /srv/uploads that anonymous user can write but not read (mode 333).
```
mkdir /srv/uploads
chmod 333 /srv/uploads
```
- 3. Because of the risk, vsftpd prevents one anonymous user to download a file that anonymous user uploaded.
- 4. Set anon_upload_enable (page 706) to YES.

# SETTING UP AN FTP Server (vsftpd)
# 705

## DOWNLOAD/UPLOAD FOR USERS

### local_umask

The mask (page 459) for local users. The default setting 077 makes uploaded files executable.

Default: 077

### file_open_mode

The permissions for files opened by local users. Change to 066 to make uploaded files executable.

Default: 666

### write_enable

Permits users to create and delete files, assuming appropriate filesystem permissions. The default setting prevents users from making changes to the filesystem.

Default: NO

## ANONYMOUS USERS

### anon_mkdir_write_enable

Permits an anonymous user to create directories where write_enable=YES and the anonymous user has permission to write to the directory. For a more secure site, do not set this parameter to YES.

Default: NO

### anon_root

After an anonymous user logs in on the server, this directory becomes the user’s working directory. No error results if the specified directory does not exist.

Default: none

### anon_umask

The umask (page 459) for anonymous users. The default setting 077 gives only anonymous users access to files uploaded by anonymous users; set this parameter to 022 to give everyone read access to these files.

Default: 077

### anon_upload_enable

Allows anonymous users to upload files when write_enable=YES and the anonymous user has permission to write to the directory.

Default: NO

### anon_world_readable_only

Limits the files that a user can download to those that are readable by the owner of the file, members of the group file is associated with, and others. may not be desirable to allow one anonymous user to download a file that anonymous user uploaded. Setting this parameter to YES can avoid this scenario.

Default: YES

### ascii_download_enable

Allows a user to download files using ASCII mode. Setting this parameter to YES can create a security risk (page 695).

Default: NO

### ascii_upload_enable

Allows a user to upload files using ASCII mode (page 694).

Default: NO

### chown_uploads

Causes files uploaded by anonymous users to be owned by *root* (or another user specified by *chown_username*). To improve security, change *chown_username* to a name other than *root* if you set this parameter to YES.

Default: NO

### chown_username

See *chown_uploads.*

Default: root

### ftp_username

The username of anonymous users.

Default: ftp

### nopriv_user

The name of the user with minimal privileges, as used by *vsftpd*. Other programs use *nobody*, to enhance security you can replace *nobody* with the name of a dedicated user such as *ftp*.

Default: nobody
