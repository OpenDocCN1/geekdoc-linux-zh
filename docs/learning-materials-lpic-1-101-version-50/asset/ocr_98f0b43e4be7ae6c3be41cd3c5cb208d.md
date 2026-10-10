Some of the command line parameters to umount are:

+   **-a**
+   This will unmount all filesystems listed in /etc/fstab.

+   **-f**
+   This will force the unmounting of a filesystem. This may be useful if you mounted a remote filesystem that has become unreachable.

+   **-r**
+   If the filesystem cannot be unmounted, this will try to make it read-only.

# ## Dealing with Open Files

When unmounting a filesystem, you may encounter an error message stating that the target is busy. This will happen if any files on the filesystem are open. However, it may not be immediately obvious where an open file is located, or what is accessing the filesystem.

In such cases you may use the lsof command, followed by the name of the device containing the filesystem, to see a list of processes accessing it and which files are open. For example:

```
```
# umount /dev/sdb1
umount: /media/carol/External_Drive: target is busy.

# lsof /dev/sdb1
COMMAND PID USER FD TYPE DEVICE SIZE/OFF NODE NAME
evince 3135 carol 16r REG 8,17 21881768 5195 /media/carol/External_Drive/Documents/E-Books/MagPi40.pdf
```
```

COMMAND is the name of the executable that opened the file, and PID is the process number. NAME is the name of the file that is open. In the example above, the file MagPi40.pdf is opened by the program evince (a PDF viewer). If we close the program, then we will be able to unmount the filesystem.

> Before the lsof output appears GNOME users may see a warning message in the terminal window.

> > **NOTE**
> > lsof: WARNING: can't stat() fuse.gvfsd-fuse file system /run/user/1000/gvfs
> > Output information may be incomplete.