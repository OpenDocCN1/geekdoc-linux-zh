+   Launch a terminal window, and switch to the root user account by using this command:
+   ```
+   $ su -
+   ```

+   Insert Red Hat Linux 9 distribution Disk 2. Change to the directory on the CD that contains the RPM package files:
+   ```
+   # cd /mnt/cdrom/RedHat/RPMS
+   ```
+   
+   *If you get a No such file or directory message, it’s probably because the CD wasn’t mounted automatically when you inserted it. In this case, mount the CD manually:*
+   
+   ```
+   # mount /dev/cdrom
+   ```
+   
+   *Then try the above cd command again.*

+   Use the ls command to find out the exact version of samba-swat contained on the disk. For example:
+   ```
+   # ls samba-swat*.rpm
+   samba-swat-2.2.7a-6.i386.rpm
+   ```
+   
+   If this command doesn't find any matches, then remove the disk, replace it with Disk 1 or Disk 2, and return to Step 2.

+   Install the samba-swat package you've just found, by using the rpm command:
+   ```
+   # rpm -ihv samba-swat-2.2.7a-6.i386.rpm
+   Preparing... ########################################### [100%]
+    1:samba-swat ########################################### [100%]
+   ```
+   
+   *Alternatively, view the available package files on your disk by using the Nautilus file manager GUI to navigate to /mnt/cdrom/Redhat/RPMS. Locate the file matching the name samba-swat-*.rpm. Double-click on this file – this action will open RPM GUI tool, from which you can install the package.*

# Starting the SWAT Service

Starting the SWAT service is a two step process:

+   Launch gedit or your favorite text editor, and open the file /etc/xinetd.d/swat. This is the configuration file for the SWAT service, and it looks like this: