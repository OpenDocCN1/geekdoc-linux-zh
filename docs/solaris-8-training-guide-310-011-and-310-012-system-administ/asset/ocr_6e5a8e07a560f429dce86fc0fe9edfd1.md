# APPLY YOUR KNOWLEDGE

# Exercises

# 6.1 Displaying Disk Configuration Information

In this exercise, you determine the disk geometry and slice information of your disk drive.

Estimated Time: 20 minutes

+   1. Log in as root.
2. Display and record your current disk configuration information using the prtvtoc command, as shown here:
   `prtvtoc <raw disk device name>`
   How are the disk slices arranged? What disk geometry does it display?
3. Now, follow these steps to look at your disk information using the format utility:
   A. Type format. The Main Menu appears, displaying your disk drives. You’re going to select the disk numbered 0, so note all of the information on that line.
   B. Type 0. This will select the first disk listed. The Format Menu will appear.
   C. Type partition. The Partition menu will appear.
   D. Type print. All of your disk partition information will be displayed.
   E. Press Ctrl+D. You’ll exit the format utility.

# 6.2 Creating a File System

The following exercise requires that you have a spare disk drive connected to your system or a spare, unused slice on a disk. You will practice creating a disk slice and creating a file system.

Estimated Time: 30 minutes

+   1. Practice creating a slice on your spare disk drive using the steps outlined in the earlier section titled “Using the format Utility to Create Slices.”
2. Create a file system on the new or unused slice using the newfs command as follows:
   `newfs <raw device name>`
3. Create a directory in the root partition named /test, as shown here:
   `mkdir /test`
4. Mount the new file system using the following command:
   `mount <block device name> /test`
5. Unmount the file system, as shown here:
   `umount /test`
6. View the contents of the /etc/vfstab file on your system by typing cat /etc/vfstab.
7. Add the following line to the /etc/vfstab file for the file system you’ve just created so that it gets mounted automatically at boot time:
   `<Raw device name>   <block device name> \
   /test   ufs   2   yes`
8. Reboot the system:
   `/usr/sbin/shutdown -y -g0 -i6`
9. Verify that the file system was mounted automatically:
   `mount`