The final three directives in the standard vsftpd.conf file have been added by Red Hat. First, RHEL 6 includes user lists associated with Pluggable Authentication Modules (PAM) described in Chapter 10.

```
pam_service_name=vsftpd
```

If you allow something more than anonymous-only access, it's important to keep out certain users such as root, as well as any other users with privileges. By default, vsFTP is configured to disable logins from sensitive users such as root, bin, and mail. The following directive implicitly refers to the user_list file in the /etc/vsftpd directory, through the userlist_deny directive.

```
userlist_enable=YES
```

While vsFTP has been compiled with TCP Wrappers libraries, you can't use the associated /etc/hosts.allow and/or the /etc/hosts.deny files unless this final directive is kept active:

```
tcp_wrappers=YES
```

As vsFTP also uses PAM for security, it also disables the users in /etc/vsftpd/ftpusers. The lists of users in the default versions of these files are identical.

# Other vsFTP Configuration Files

The contents of the user_list and the ftpusers files in the /etc/vsftpd directory are identical. They include a standard list of service users, including the root administrative user. In general, you don't want to give any such users login privileges, under any circumstances. The aforementioned userlist_enable=YES directive activates the userlist_deny=YES directive, which denies all listed in the user_list file.

The ftpusers file is used by the /etc/pam.d/vsftpd configuration file. Chapter 10, Lab 6, gave you an opportunity to explore and reconfigure that file. To review, the appropriate PAM directive in that file is

```
auth required pam_listfile.so item=user sense=deny
file=/etc/vsftpd/ftpusers onerr=succeed
```

The directive denies all users in the ftpusers file. There's one other file in the directory, vsftpd_conf_migrate.sh, which links configuration files created in previous versions of the vsFTP server.