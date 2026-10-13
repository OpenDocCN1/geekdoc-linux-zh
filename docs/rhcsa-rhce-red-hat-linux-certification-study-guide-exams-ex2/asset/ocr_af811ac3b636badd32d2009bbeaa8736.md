+   4.  Check to see that the mounting has worked. If it did, you’ll see the NFS mount in the output to the mount command.

+   5.  Now look through the mounted /home directory for the special files that created in step 1. If found, you’ve succeeded in creating and connecting to the /home directory share.

+   6.  To make the mount permanent, add it to the /etc/fstab file on the client. Once you’ve added a line such as the following to that file, the Linux client automatically mounts the shared /home directory from the NFS server.
+       ```
+       server1.example.com:/home /remote nfs4 soft,timeout=100 0 0
+       ```

# **Lab 3: NFS and SELinux**

The reference to SELinux is deliberate and should provide an important hint. If you have to modify every directory shared and configured in the /etc/exports file on each NFS server, that can be time consuming. Perhaps the simplest way to prevent writes to shared NFS directories is to deactivate the associated SELinux boolean setting. While there are other methods, the quickest way to do so on a permanent basis is with the following command:

```
# setsebool -P nfs_export_all_rw off
```
You should then be able to test the result with the next mounting of a shared NFS directory.

# **Lab 4: Configure a vsFTP Server with Messages**

The vsFTP server can be installed from one RPM package. So if you have not installed this server earlier, you could install it with the following command:

```
# yum install vsftpd
```

This also installs configuration files in the /etc and /etc/vsftpd directories. The main configuration file is /etc/vsftpd/vsftpd.conf. Based on the RHEL default version of this file, you can make a couple of changes to enable messages. But by default, messages are already enabled for directory access on an FTP server, courtesy of the following command:

```
dirmessage_enable=yes
```

The actual configuration of a message is a matter of creating a text file and saving it as .message in the desired directories, /var/ftp and /var/ftp/pub. You could add a simple line such as “root directory for the FTP server” or “main download directory.”

Finally, to configure the Red Hat FTP server to start, run the `service vsftpd start` command. To make sure it starts the next time you boot your computer, run the `chkconfig vsftpd on` command.