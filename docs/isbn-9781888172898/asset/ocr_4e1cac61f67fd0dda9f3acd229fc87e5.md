# E.3.3 Why am I missing some programs?

Try doing a `df` at the shell prompt. If you have `/` or `/usr` showing up as 100% used, chances are your partition was too small for the entire install. Unfortunately, this does not result in any type of error messages unless you are watching closely (which most people don’t when the thing tells you it is going to take 2 hours to install :-)). You will most likely need to reinstall and do one of two things: a) make your root or `/usr` partition larger or b) install fewer packages.

Also, if none of the partitions you made for Linux is full, you are probably just missing some packages. You will need to use glist or rpm to install those.

# E.3.4 How do I mount my CD-ROM?

If you installed from CD-ROM, you should be able to do:

```
mount /mnt/cdrom
```

If you get an error that says the mount point does not exist, do:

```
mkdir /mnt/cdrom
```

If you did an install via NFS: You need to know what type of CD-ROM you have. The best way is to watch the boot messages as you reboot, or look at /var/adm/messages (more /var/adm/messages). You most likely have an IDE CD-ROM that will show up as /dev/hdc or /dev/hdd, or you have a Sound Blaster type that is /dev/sbpcd, or you have a SCSI that is /dev/scd0.

In any case, you can do the following:

```
mount -t iso9660 /dev/xxxx /mnt/cdrom
```

and substitute xxxx for YOUR device. You can then: cd /mnt/cdrom and then: ls and you will be looking at the contents of the CD-ROM.