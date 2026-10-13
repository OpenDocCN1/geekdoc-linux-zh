The vsftpd server makes use of the PAM service to authenticate local users that are remotely accessing their accounts through FTP. In the vsftpd.conf file, the PAM script used for the server is specified with the pam_service_name option.

```
pam_service_name=vsftpd
```

In the etc/pam.d directory, you will find a PAM file named vsftpd with entries for controlling access to the vsftpd server. PAM is currently set up to authenticate users with valid accounts, as well as deny access to users in the /etc/vsftpd.ftppusers file. The default /etc/pam.d/vsftpd file is shown here:

```
#PAM-1.0
auth required pam_listfile.so item=user sense=deny
    file=/etc/vsftpd.ftppusers onerr=succeed
auth  required  pam_stack.so service=system-auth
auth  required  pam_shells.so
account required pam_stack.so service=system-auth
session required pam_stack.so service=system-auth
```

# Command Access

Command usage is highly restricted by vsftpd. Most options for the ls command that lists files are not allowed. Only the asterisk file-matching operation is supported (see Chapter 8). To enable recursive listing of files in subdirectories, you have to enable the use of the -R option by setting the ls_recurs_enable option to YES. Some clients, such as ncftp (see Chapter 14), will assume that the recursive option is enabled.

Table 21-3: Files for vsftpd

| File | Description |
|---|---|
| vsftpd.ftppusers | Users always denied access |
| vsftpd.user_list | Specified users denied access (allowed access if userlist_deny is NO) |
| vsftpd.chroot_list | Local users allowed access (denied access if chroot_local_user is on) |
| /etc/vsftpd/vsftpd.conf | vsftpd configuration file |
| /etc/pam.d/vsftpd | PAM vsftpd script |
| /etc/rc.d/init.d/vsftpd | Service vsftpd server script, standalone (Red Hat default) |
| /etc/xinetd.d/vsftpd | Xinetd vsftpd server script |

# vsftpd Virtual Hosts

Though the capability is not inherently built in to vsftpd, you can configure and set up the vsftpd server to support virtual hosts. Virtual hosting is where a single FTP server operates as if it has two or more IP addresses. Several IP addresses can then be used to access the same server. The server will then use a separate FTP user directory and files for each host. With vsftpd, this involves manually creating separate FTP users and directories for each virtual host, along with separate vsftpd configuration files for each virtual host in the /etc/vsftpd directory. On Red Hat, vsftpd is configured to run as a standalone service. Its /etc/rc.d/init.d/vsftpd start-up script will automatically search for and read any configuration files listed in the /etc/vsftpd directory. If, on the other hand, you wish to run vsftpd as a xinetd service, you would have to create a separate xinetd service script for each host in the /etc/xinetd.d directory. In effect, you have several vsftpd services running in parallel for each separate virtual host. The following example uses two IP addresses for an FTP server. First, create an FTP user for each host. Create directories for each host. (You could use the one already set up for one of the users.) For example, for the first virtual host you could use