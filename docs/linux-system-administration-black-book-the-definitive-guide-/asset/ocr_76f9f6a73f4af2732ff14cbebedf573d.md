4. Create a new directory with the original name using the `mkdir` command. For example, `mkdir /home`.

5. Mount the partition onto the now empty mount point, which is the new directory you just made.

6. Use the `cd` command to change into the moved version of the hierarchy. For example, `cd /old-home`.

7. Use the `cp` tool in the form `cp -rp . newdir` to recursively copy the files—along with their owner, group, permission, and timestamp settings—from the current location to the new partition. For example, `cp -rp . /home`.

8. Use the `cd` command to change to the new partition. Take a few moments to ensure that everything copied over properly. Try running programs and editing files and generally putting the partition through its paces.

9. Once you're sure that the transfer went well, delete the old version with the `rm` command in the format `rm -r olddir`. For example, `rm -r /old-home`.

> WARNING! Double-, triple-, and quadruple-check that you have typed this command properly before you press Enter. The last thing anyone needs is to delete the wrong portion of the file system!

10. See the section “Adding Permanent Media” on how to add this partition to `/etc/fstab`.

# ## Adding And Removing Media To The File System

There are two different approaches to adding and removing media, depending on its purpose. Temporary media, such as floppy disks and CD-ROMs, are often added and removed in short periods of time. However, if you are adding new partitions that you want to permanently make part of the file system, then you will use a different approach.

# ### Adding Temporary Media

To add media temporarily to the file system, do the following:

1. Physically add the media to the file system. This act may involve putting a floppy disk in a drive, a Zip disk in a Zip drive, or a CD-ROM in the CD-ROM bay.

2. Determine which device driver pertains to the media. Table 3.10 lays out the paths for commonly used drivers.

3. Determine which file system is used on this device. Table 3.11 lays out the file system formats commonly used with temporary media in Linux.