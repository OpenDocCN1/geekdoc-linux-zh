# # Mounting Windows files from a floppy disk

The process of mounting and unmounting a file system provides a good example of the difference between Linux and Windows. If you use a floppy disk or CD with Windows, you just insert it into the drive and you have immediate access to what’s on it. With Linux, you must insert the floppy disk into the drive and then explicitly mount it. Sound complicated? Not really.

You can mount a Windows hard-drive partition or floppy-disk drive on your Linux computer. You can read and write to FAT or FAT32, but can only read from NTFS file systems. Here’s how to mount a Windows floppy disk:

+   1. Insert a Windows MS-DOS-formatted floppy disk into the drive, click the GNOME Menu button, and choose System Tools→Disk Management. Enter the root password if it’s requested.

+   2. Select the floppy disk and click the Mount button.

You know that the floppy disk has been mounted successfully when a floppy-disk icon shows up on the left side of the screen.

You can now read and write to the floppy disk (unless the read-only tab on your disk is set).

+   3. Click the Close button to close the utility.

Fedora Core and GNOME are configured to automatically start the process that mounts your floppy disk or CD when you insert it into the drive. We use the manual method here to show you how the process works. To mount the floppy disk manually from the command-line interface, log in as root, open the terminal window, and run the following command:

```
`mount -t msdos /dev/fd0 /mnt/floppy`
```

# # Unmounting file systems

Unmounting a Linux file system is a little simpler than mounting one. Because the file system is already mounted, you don’t have to specify any options or other information. You just have to tell the Red Hat disk management druid to unmount the file system. Follow these steps:

+   1. Click the Main Menu button and choose System Tools→Disk Management. Enter the root password, if you’re prompted.

+   2. When the User Mount Tool window appears, click the button of the file system in which you’re interested.

![](bbox=[0.15, 0.43, 0.25, 0.52])