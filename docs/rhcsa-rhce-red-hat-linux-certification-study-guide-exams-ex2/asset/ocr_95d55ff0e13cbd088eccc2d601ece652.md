+   5. Make sure the SELinux booleans are compatible; specifically, make sure the nfs_export_all_ro and nfs_export_all_rw booleans are both still set. You can do so either with the getsebool command or the SELinux Management tool.
+   6. Set fixed ports for the parameters described in the /etc/sysconfig/nfs file.
+   7. Open those ports in the firewall. Restart the firewall with the /etc/init.d/iptables restart command.
+   8. Restart the NFS service with the /etc/init.d/nfs restart command.

Then, on an NFS client, take the following steps:

+   9. Create a directory for the server share called /mnt/MIS.
+   10. Mount the shared NFS directory on /mnt/MIS.
+   11. List all exported shares from the server and save this output as /mnt/MIS/shares.list.
+   12. Make this service a permanent connection in the /etc/fstab file. Assume that the connection might be troublesome and add the appropriate options, such as soft mounting.
+   13. Run the mount -a command to reread /etc/fstab. Check to see if the share is properly remounted.
+   14. Test the NFS connection. Stop the NFS service on the server, and then try copying a file to the /mnt/MIS directory. While the attempt to copy will fail, it should not hang the client.
+   15. Restart the NFS service on the server.
+   16. Edit /etc/fstab again. This time, assume that NFS is reliable, and remove the special options added in Step 12.
+   17. Now shut down the server and test what happens. The mounted NFS directory on the client should hang when you try to access the service.
+   18. The client computer may lock. If so you can boot into single-user mode, as described in Chapter 5, to avoid the pain of a reboot. Restore the original configuration.