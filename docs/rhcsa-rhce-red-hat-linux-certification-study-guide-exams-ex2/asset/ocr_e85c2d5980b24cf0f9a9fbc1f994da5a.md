# SELF TEST ANSWERS

# The Network File System (NFS) Server

+   1. The following entry in /etc/exports would export the /data directory as read-only to all hosts and grant read and write permission to the host super in example.com:  
+   `/data (ro, sync)`    super.example.com(rw, sync)

+   2. Once you’ve revised /etc/exports, the `exportfs -a` command exports all filesystems. Yes, you can re-export filesystems with the `exportfs -r` command. But there’s no indication that NFS shares have yet been exported.

+   3. The port number associated with the portmapper is 111.

+   4. The port number associated with NFSv4 is 2049.

+   5. The NFS configuration option that supports access by the root administrative user is no_root_squash.

# Test an NFS Client

+   6. Soft mounting and time-outs associated with the `soft` and `timeo` options can prevent problems such as lockups with NFS clients.

+   7. The command that can display NFS shared directories from the named remote system is `showmount -e outsider1.example.org`.

# The Very Secure FTP Server

+   8. The default directive in /etc/vsftpd/vsftpd.conf that you should disable to prevent users from logging into their accounts through the vsFTP server is `local_enable=YES`.

+   9. The directive that prevents keep regular users from getting to the top-level root directory (/) after logging into a vsFTP server is `chroot_local_user=YES`.

+   10. Based on the default RHEL 6 configuration, both ftpusers and user_list in the /etc/vsftpd directory include a list of users not allowed to log in to the vsFTP server. Strictly speaking, the user_list file is the right answer, as it’s associated with the userlist_enable directive. But the active contents of the standard ftpusers file are identical.

+   11. The default directory for anonymous access is the home directory of the user named ftp.