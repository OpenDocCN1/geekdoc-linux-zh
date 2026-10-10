Use the Unix dd utility to write the files to the floppies. On a FreeBSD system, it looks like this:

```
dd if=boot.flp of=/dev/rfd0
```

When the copy finishes, remove the first floppy from the drive and insert the second one. Once again, use dd to create the second floppy. On a FreeBSD system, it would look something like this:

```
dd if=mfsroot.flp of=/dev/rfd0
```

Note that for the previous commands to work, you must have write access to the raw floppy device. Also, on other versions of Unix, the device name may be different. See the documentation for your version of Unix to find out the name of the floppy device.

Now that you have created the installation disks, you are ready to begin the installation.

# ## Booting into the Install Program

> **CAUTION**
> If you are installing on a system that already has Windows or some other operating system on it and you don't want to lose that operating system and all its data, stop here and read “Potential Problems with and Limitations of Dual Boot Systems” in Chapter 3. It is very important that you read this first. Failure to follow the instructions in that section could result in the loss of all data on your hard disk!

The next few sections assume that you either plan to wipe out everything currently on your hard disk to install FreeBSD, that you are installing on a new disk, or that you have already followed the instructions in Chapter 3 to create space for FreeBSD on a system that already has another operating system installed on it. These sections also assume that you are installing from the included CD-ROM. If this is not the case, stop here and read the relevant sections in Chapter 3 on NFS installs, FTP installs, or floppy installs. After you do that, come back and continue with the instructions given here.

When you are ready to begin the installation, insert the included CD-ROM into your CD-ROM drive. If you need to boot from floppy disks, also insert the floppy disk on which you installed boot.flp into your A drive. Reboot your system. If necessary, enter your BIOS setup program and enable booting from the CD-ROM drive. Some BIOS also have a security feature that prevents booting from the floppy drive. If you have to boot from the floppy drive, you might need to check for this option and set it to allow booting from the A drive. See your system documentation for the way to configure the BIOS settings to control boot devices.

As the system boots, you should see some messages on your screen. You should also see a “twirling baton.” As long as the baton keeps twirling, the system is doing something. If