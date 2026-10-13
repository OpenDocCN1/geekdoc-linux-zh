+   - The mount point is the directory where the filesystem for the device is located. If you are adding a hard drive so that you have more storage space for user files, you could create a mount point as a subdirectory of the /home or /usr/local directories.
+   - GNU/Linux supports a variety of filesystem types. As you've seen earlier in the hour, you can use DOS floppies and CD-ROM drives. The Linux native filesystem type is ext2.
+   - Options are used to set the parameters under which the device operates. The device can be set to be read-write or read-only; it can be mounted automatically at boot time or not; and user storage space on the filesystem can be limited.
+   - The filesystem can be backed up (using the dump utility) on a regular frequency. This might not be used by all systems.
+   - The fsck utility checks each filesystem at boot time. The order in which the filesystem is checked is indicated in the last column.

![](bbox=[0.18, 0.51, 0.26, 0.6])

> When making configuration changes, make only one change at a time and then test the change. If the change is successful, make the next change. This is the easiest way to recover from an error. If you make several changes at one time, it is hard to determine what might have gone wrong. Also, testing configuration changes is easier if you make one change at a time.

# Task: Backing Up Configuration Files

Here's how to make a duplicate of the /etc/fstab file so that you can always retain the original configuration for reference or to recover from a failed configuration attempt:

![](bbox=[0.18, 0.79, 0.26, 0.88])

> The solemn and unbreakable rule of thumb here is NEVER tinker with any configuration file without backing it up first.

+   1. Log into the root account.
+   2. Change to the /etc directory. Type cd /etc and press Enter.
+   3. Copy the fstab file. Type cp fstab fstab.orig and press Enter. This identifies the file as being the original configuration. If you use the -p command option, you can change the modification date and time to the time that the copy was made.