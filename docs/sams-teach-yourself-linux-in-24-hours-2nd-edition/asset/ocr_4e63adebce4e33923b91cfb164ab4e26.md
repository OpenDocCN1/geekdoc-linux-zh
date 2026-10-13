# Q&A

Q I tried formatting a floppy with the fdformat command. After I inserted a floppy, typed the command, and specified the /dev/fd0 device, the command reported Could not determine current format type: No such device. I know my floppy works. What's going on?

A It's possible that you didn't have a floppy inserted in the drive. If you get this error with an inserted floppy, the floppy was not blank and was previously formatted. The best approach to use when performing a low-level format is to specify the exact type of device (such as /dev/fd0H1440) as in fdformat /dev/fd0H1440.

Q How do I create a folder for my KDE desktop xe "KDE (K Desktop Environment):desktop" xe "K Desktop Environment (KDE):desktop" that, when opened, shows the contents of my Windows partition?

A Mount your Windows partition xe "Windows partition:mounting" and then create a symbolic link xe "symbolic links" with a name such as dos inside the Desktop folder in your home directory. Make sure this link points to the Windows desktop folder—for example, ln -s /mnt/dos/windows/desktop $HOME/Desktop/dos.

# Exercises

+   1. Format a floppy and then prepare the diskette with the Linux ext2 filesystem. Mount the floppy and copy files from your home directory to the diskette. What utilities did you use?
+   2. Make a backup of your system's filesystem table and copy it to a diskette. Then, edit your filesystem to allow others to mount and unmount CD-ROMs.
+   3. Open the KDE help application from your desktop's panel and then click the Using Templates to access Applications and Devices item. Follow the directions and create a desktop icon for your floppy drive. After you finish, copy files to your floppy by dragging them from your home folder.