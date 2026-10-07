# A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

```
root@forensic1:~# umount /mnt/analysis
```

+   - Note the proper command is umount, not un. This cleanly unmounts the file system. DO NOT remove the disk OR SWAP the disk until it is unmounted.
- If you get an error message that says the file system cannot be unmounted because it is busy, then you most likely have a file open from that directory, or are using directory from another terminal. Check all your terminals and virtual terminals and make sure you are no longer in the mounted directory.

Another Example: Reading a CDROM from DVD

+   - Insert the CDROM:
- We use the ISO9660 system format for mounting CD and DVD disks. You can check again with the file command run on our DVD device (/dev/sr0) with a disk inserted.

```
root@forensic1:~# file -s /dev/sr0
/dev/sr0: ISO 9660 CD-ROM filesystem data 'MY DATA'
```

Now we mount the device and change to the newly mounted file system:

```
root@forensic1:~# mount -t iso9660 /dev/sr0 /mnt/cdrom
mount: /dev/sr0 is write-protected, mounting read-only
```

```
root@forensic1:~# cd mnt/cdrom
ls
autorun.inf* document/ installmanager/ menu/ tools/
```

+   - You should be able to navigate the disk as usual.
- When you are finished, leave the /mnt/cdrom directory (change to your home directory again with cd or cd ~), and unmount the file system with:

```
root@forensic1:~# umount /mnt/cdrom
```

> If you want to see a list of file systems that are currently mounted, just use the mount command without any arguments or parameters. It will list the mount point and file system type of each device on system, along with the mount options used (if any). Note in the output below you can see the thumb drive and CD disk I just mounted (and not unmount):