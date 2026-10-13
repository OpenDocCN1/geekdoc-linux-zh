
## SELF TEST ANSWERS
### The Network File System (NFS) Server
- 1. The following entry in /etc/exports would export the /data directory as read-only to all hosts and grant read and write permission to the host super in example.com:
  `/data *(ro, sync) super.example.com(rw, sync)`
- 2. Once you’ve revised /etc/exports, the `exportfs -a` command exports all filesystems. Yes, you can re-export filesystems with the `exportfs -r` command. But there’s no indication that NFS shares have yet been exported.
- 3. The port number associated with the portmapper is 111.
- 4. The port number associated with NFSv4 is 2049.
- 5. The NFS configuration option that supports access by the root administrative user is no_root_squash.

### Test an NFS Client
- 6. Soft mounting and time-outs associated with the `soft` and `timeo` options can prevent problems such as lockups with NFS clients.
- 7. The command that can display NFS shared directories from the named remote system is `showmount -e outsider1.example.org`.

### The Very Secure FTP Server
- 8. The default directive in /etc/vsftpd/vsftpd.conf that you should disable to prevent users from logging into their accounts through the vsFTP server is `local_enable=YES`.
- 9. The directive that prevents regular users from getting to the top-level root directory (/) after logging into a vsFTP server is `chroot_local_user=YES`.
- 10. Based on the default RHEL 6 configuration, both ftpusers and user_list in the /etc/vsftpd directory include a list of users not allowed to log in to the vsFTP server. Strictly speaking, the user_list file is the right answer, as it’s associated with the userlist_enable directive. But the active contents of the standard ftpusers file are identical.
- 11. The default directory for anonymous access is the home directory of the user named ftp.
- 12. The additional directives to add to the default vsFTP configuration file to allow security using PAM and TCP wrappers are `pam_service_name=vsftpd` and `tcp_wrappers=YES`.

## LAB ANSWERS
### Lab 1: Basic NFS Configuration
When this lab is complete, you’ll see the following features on the system with the NFS server:
- Installed NFS packages, including related packages such as portreserve and rpcbind. Without these packages, communication won’t be possible with NFS clients.
- An active NFSv4 service, which can be confirmed in the output to the `rpcinfo -p` command.
- A firewall that supports access through the noted ports. It should also be limited by IP address network.

In addition, you’ll be able to perform the following tasks from the NFS client:
- Run the `showmount -e server1.example.com` command, where server1.example.com is the name of the NFS server system (substitute if and as needed).
- Mount the shared directory as the root user with the `mount.nfs4 server1.example.com:/shared /testing` command.
- The first time the share is mounted, you should be able to copy local files as the root user to the /testing directory.
- The second time the share is mounted, with the no_root_squash directive in effect, such copying should not work, at least from the client root user account.

### Lab 2: Standard NFS Configuration
This lab is the first step toward creating a single /home directory for your network. Once you get it working on a single client/server combination, you can set it up on all clients and servers. You can then use the LDAP server described in Chapter 8 to set up a single Linux/Unix database of usernames and passwords for the network. Alternatively, matching usernames (with matching UID and GID numbers) on different local systems should also work. On the NFS server, take the following steps:
- Set up a couple of users and identifying files such as user1 and user1.txt on the system being used as the NFS server.
- Configure the /etc/idmapd.conf file for the current domain, appropriate users, and the translation method for authentication. As discussed in the chapter, that refers to
```
Domain = example.com
Nobody-User = nfsnobody
Nobody-Group = nfsnobody
Method = nsswitch
```
- 3. Make the system reread the modified configuration file, using the /etc/init.d/rpcidmapd script.
- 4. Share the /home directory in /etc/exports on the server1.example.com client. You can do this in this file with the following command:
  `/home nfsclient (rw, sync)`
- 5. Export this directory with the following command:
  `# exportfs -a`
- 6. Restart the NFS service:
  `# service nfs restart`
- 7. Make sure that the exported /home directory shows in the export list. On the local server, you can do this with the following command:
  `# showmount -e server1.example.com`
- 8. If problems appear during this process, check the /etc/exports file carefully. Make sure there aren't extra spaces in /etc/exports, even at the end of a code line. Make sure the NFS service is actually running with the service nfs status command.
- 9. You may also want to check your firewall and make sure the appropriate services described in this chapter are running with the rpcinfo -p command.
- 10. Remember to make sure that the NFS server starts automatically the next time that system is booted. One way to do so is with the following command:
  `# chkconfig nfs on`

Now on the NFS client, take the following steps to connect to the shared /home directory:
- 1. First, make the same changes to the /etc/idmapd.conf file as was done on the server, and restart the rpcidmapd service script available from the /etc/init.d directory.
- 2. Make sure that you can see the shared /home directory. If there is no DNS server or the /etc/hosts file does not include the IP address of the server1.example.com system, substitute the IP address:
  `# showmount -e server1.example.com`
- 3. Now mount the share that is offered on the local /remote directory:
  `# mount.nfs4 server1.example.com:/home /remote`
- 4. Check to see that the mounting has worked. If it did, you’ll see the NFS mount in the output to the mount command.
- 5. Now look through the mounted /home directory for the special files that created in step 1. If found, you’ve succeeded in creating and connecting to the /home directory share.
- 6. To make the mount permanent, add it to the /etc/fstab file on the client. Once you’ve added a line such as the following to that file, the Linux client automatically mounts the shared /home directory from the NFS server.
  ```
  server1.example.com:/home /remote nfs4 soft,timeout=100 0 0
  ```

### Lab 3: NFS and SELinux
The reference to SELinux is deliberate and should provide an important hint. If you have to modify every directory shared and configured in the /etc/exports file on each NFS server, that can be time consuming. Perhaps the simplest way to prevent writes to shared NFS directories is to deactivate the associated SELinux boolean setting. While there are other methods, the quickest way to do so on a permanent basis is with the following command:
```
# setsebool -P nfs_export_all_rw off
```
You should then be able to test the result with the next mounting of a shared NFS directory.

### Lab 4: Configure a vsFTP Server with Messages
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
