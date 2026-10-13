# RHCSA Sample Exam 1 Discussion

In this discussion, I'll describe one way to check your work to meet the requirements listed for the Sample 1 RHCSA exam.

+   1. One way to see if SELinux is set in enforcing mode is to run the **sestatus** command.
+   2. If VM software is installed on the local system, you'll have access to the Virtual Machine Manager in the GUI, or at least the **virt-install** and **virsh** commands from the command line.
+   3. If successful, you should be able to access the new server2.example.com system, either via ssh or with the Virtual Machine Manager.
+   4. One way to set the noted system to start automatically the next time the host is booted is with the **virsh autostart server2.example.com** command. One way to confirm is in the output to the **virsh dominfo server2.example.com** command.
+   5. To review current logical volumes, run the **lvs** command.
+   6. Make sure the volume is encrypted. Did you run the **cryptsetup** command on the volume?
+   7. To make sure that volume is automatically mounted the next time the system is booted, it should be configured in /etc/fstab to the appropriate format, with the UUID associated with the encrypted volume, as defined by the **blkid** command.
+   8. The /home/angels directory should be owned by the group angels. As long as users donna and mike are not part of that group, and other users don't have permissions (or ACLs) on that directory, access should be limited to members of the angels group. The directory should also have SGID permissions.
+   9. If you've modified user mike's account to make his account expire in seven days, the right expiration date should appear in the output to the **chage -l mike** command.
+   10. There are a number of ways to set up a cron job; it could be configured in the /etc/cron.monthly directory or as a cron job for the user root or mike in the /var/spool/cron directory. In any of these cases, the delete command would be associated with an appropriate time stamp, with a line such as:

```
50 3 2 * * /bin/rm /home/mike/*
```