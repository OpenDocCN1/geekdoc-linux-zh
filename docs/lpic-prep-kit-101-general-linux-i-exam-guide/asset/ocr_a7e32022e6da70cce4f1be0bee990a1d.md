Answer a is correct; this command specifies the vfat filesystem, which supports long filenames and specifies both the device and the mount point. Answer b is incorrect; there is no -1 option for the mount command and the -r option would only check to see whether the filesystem was mountable without mounting it. Answer c is incorrect; there is no --long_filenames option. Answer d is incorrect; this would mount the floppy with the filesystem defined in the /etc/fstab file, but as read-only.

2. After installing a new modem you want to see what interrupt it is using. What command will show this?

+   a. ls /proc/interrupts
+   b. cat /proc/interrupts
+   c. which interrupts
+   d. mount interrupts

Answer a is incorrect; the ls command would return /proc/interrupts. Answer b is correct; the cat command will list the contents of the /proc/interrupts file. Answer c is incorrect; the which command returns the complete path to a specific command. Answer d is incorrect; the mount command is used to make a filesystem available via the Linux hierarchy.

3. How can you get a listing of all the filesystems that are presently mounted?

+   a. mount -a
+   b. mount -f filesystem
+   c. cat /etc/mtab
+   d. cat /etc/fstab

Answer a is incorrect; this would mount all the filesystems defined in /etc/fstab. Answer b is incorrect; this would check the specified filesystem to see whether it is mountable. Answer c is correct; /etc/mtab contains a list of the mounted filesystems. Answer d is incorrect; the /etc/fstab lists the defined filesystems.

4. Which of the following steps is not required to set up disk quotas for your users?

+   a. Reboot the computer
+   b. Create the quota.user file in the root of the filesystem
+   c. Edit the /etc/fstab file
+   d. Use the edquota command to set the limits

Answer a is incorrect; you will have to reboot the system to activate quotas. Answer b is incorrect; you will need a quota.user in the root of each filesystem where you want to enforce quotas. Answer c is correct; you need to edit the /etc/fstab to add the quota option to the desired filesystem. Answer d is incorrect; you use the edquota command to set the quota limits.

![](bbox=[0.83, 0.75, 0.88, 0.88])