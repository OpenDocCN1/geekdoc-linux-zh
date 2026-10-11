variable `VSFTPD_LOAD_CONF`. `vsftpd` loads the configuration file specified by this variable, allowing per-IP configuration.

Default: NO

Fedora/RHEL: YES

`user_config_dir` Specifies a directory that contains files named for local users. Each of these files, which mimic `vsftpd.conf`, contains parameters that override, on a per-user basis, default parameters and parameters specified in `vsftpd.conf`. For example, assume that `user_config_dir` is set to `/etc/vsftpd/user_conf`. If the default configuration file, `/etc/vsftpd/vsftpd.conf`, sets `idle/session_timeout=300` and Sam’s individual configuration file, `/etc/vsftpd/user_conf/sam`, sets `idle/session_timeout=1200`, all users’ sessions, except for Sam’s, will time out after 300 seconds of inactivity. Sam’s sessions will time out after 1,200 seconds.

Default: none

# FILES

In addition to `/etc/vsftpd/vsftpd.conf`, the following files control the functioning of `vsftpd`. The directory hierarchy that `user_config_dir` points to is not included in this list as it has no default name.

`/etc/vsftpd/ftpusers` Lists users, one per line, who are never allowed to log in on the FTP server, regardless of how `userlist_enable` (page 657) is set and regardless of the users listed in the `user_list` file. The default file lists root, bin, daemon, and others.

`/etc/vsftpd/user_list` Lists either the only users who can log in on the server or the users who are not allowed to log in on the server. The `userlist_enable` (page 657) option must be set to YES for `vsftpd` to examine the list of users in this file. Setting `userlist_enable` to YES and `userlist_deny` (page 657) to YES (or not setting it) prevents listed users from logging in on the server. Setting `userlist_enable` to YES and `userlist_deny` to NO permits only the listed users to log in on the server.

`/etc/vsftpd/chroot_list` Depending on the `chroot_list_enable` (page 659) and `chroot_local_user` (page 659) settings, this file lists either users who are forced into a chroot jail in their home directories or users who are not placed in a chroot jail.

`/var/log/vsftpd.log` Log file. For more information refer to “Logs” on page 663.

# CHAPTER SUMMARY

FTP is a protocol for downloading files from and uploading files to another system over a network. FTP is the name of both a client/server protocol (FTP) and a client