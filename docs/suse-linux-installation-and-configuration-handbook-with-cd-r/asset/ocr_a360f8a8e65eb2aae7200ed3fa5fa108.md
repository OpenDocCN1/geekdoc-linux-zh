1sof utility to get some help, though. For example, if you are unable to unmount your CD-ROM that is mounted on /mnt/cdrom, type the following command:

```
# lsof /mnt/cdrom
```

The previous command shows you which processes are using your CD-ROM. You then can choose to kill them or close them gracefully.

# Spreading Your IDE Drives

The IDE architecture does not allow two devices connected to the same IDE controller to be active at the same time. Therefore, if you have a hard drive and a CD-ROM both connected to the same IDE controller, only one of them can be active at one time. For this reason, you should avoid putting drives on the same IDE controller. If you have more than two drives, you should at least avoid putting the CD-ROM on the same IDE with another hard drive because it will slow it down whenever you use it.

# Jailing Programs

If you are worried about a program damaging your files, you can jail it. Jailing it means limiting its view of your hard drive, which in turn limits its damage. Use the chroot command to jail a program. For example, to jail a program called funny to be able to see only /tmp and the underlying directory and file structure, use the following command:

```
# chroot funny /tmp
```

When you issue the previous command, the program will not be able to see anything but /tmp. Just make sure that any files it needs are available inside that jail or else it won't work.

# Safe Transfers

If you want to verify that a file you just transferred to your machine is the same file as the original one, you can use the md5sum utility. Run the utility on the original file to cause it to generate a checksum for that file. Then, when you transfer it, run the command on the new copy and compare the checksums to ensure nothing changed in the file. You can post md5sums of your files to people so they can be sure that what they are getting is what you posted originally.

# Identifying File Types

You can identify the type of a file using the file command. This command scans files and attempts to recognize their type. The following is an example:

```
$ file test.ps
test.ps: PostScript document text conforming at level 3.0
```