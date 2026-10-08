# CHAPTER 5 | Filesystems, Volumes, and Encryption

| TABLE 5-6 vsFTP security related service directives |
| DIRECTIVE | DESCRIPTION |
| anon_upload_enable | Allows uploads by anonymous users; can be set to NO |
| anon_mkdir_write_enable | Allows anonymous users to create directories; can be set to NO |
| chroot_list_file | Sets up a list of users who are limited to their home directories |
| local_umask | Configures permissions for created files and directories |
| pam_service_name | Specifies the PAM configuration file in the /etc/pam.d/ directory |
 rsa_cert_file | Specifies the RSA certificate file |
 rsa_private_key_file | Specifies the file with the RSA private key |
 secure_chroot_dir | Configures a directory that should not be writable by the ftp server |
 userlist_enable | Configures a list to allow or deny users |
 write_enable | Allows users to write to a server; can also apply to anonymous users |

# ## Filesystems and Quotas

Quotas can limit the resources taken by a user or by a group of users. When appropriate, quotas are enabled. Limits are configured on the amount of space (based on blocks) and on the number of files (based on *inodes*). Quotas can protect the space available on critical directories. Quotas can give you time if there's a legitimate reason to expand the space allocated to a directory such as /home/. Quotas can help limit damage if a black-hacker has compromised an account on one of your systems.

Poorly configured logs or message systems can create large numbers of files. For example, systems configured in debug mode create logs for every event. Systems configured to see, say every second can create tens of thousands of files every day. Such systems could easily affect the life of hard-drive media.

While quotas may not directly enhance system security, they can certainly help limit damage should there be a security breach. In the following sections, you'll see how to configure quotas on a selected filesystem, the commands used to manage quotas, and how to get quota reports on your users.