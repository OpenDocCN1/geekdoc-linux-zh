```
ls -F /mnt/cdrom
```

When you're done using the DVD — and before you eject it from the drive — you have to "unmount" the disc drive with the following umount command:

```
umount /dev/cdrom
```

It's customary to mount devices on directories in the /mnt directory. Red Hat Linux comes with the two predefined directories: /mnt/cdrom for mounting the DVD and /mnt/floppy for mounting the floppy drive.

![](bbox=[0.12, 0.33, 0.18, 0.47])

# Commands for checking disk-space usage

I want to tell you about two commands — df and du — that you can use to check the disk-space usage on your system. These commands are simple to use. The df command shows you a summary of disk-space usage for all mounted devices, as shown in this example:

```
df
Filesystem           1K-blocks    Used Available Use% Mounted on
/dev/hda5             7392428  3583420   3433492  52% /
/dev/hda3             101107    9322     8656   10% /boot
none                  127376       0    127376   0%
/dev/shm
/dev/cdrom            658144   658144        0 100%
/mnt/cdrom
```

The output is a table that shows the device, the total kilobytes of storage, how much is in use, how much is available, the percentage being used, and the mount point.

![](bbox=[0.12, 0.74, 0.18, 0.88])

To see the output of df in a more human-readable format, type df -h. Here is the output of the df -h command:

```
Filesystem     Size  Used Avail Use% Mounted on
/dev/hda5      7.1G  3.5G  3.3G  52% /
/dev/hda3       99M  9.2M   85M  10% /boot
none           125M     0  125M   0% /dev/shm
/dev/cdrom     643M  643M     0 100% /mnt/cdrom
```

If you compare this output with the output of plain df (see previous listing), you see that df -h prints the sizes with terms like M for megabytes and G for gigabytes. These are clearly easier to understand than 1K-blocks.

The other command — du — is useful for finding out how much space a directory takes up. For example, type the following command to view the