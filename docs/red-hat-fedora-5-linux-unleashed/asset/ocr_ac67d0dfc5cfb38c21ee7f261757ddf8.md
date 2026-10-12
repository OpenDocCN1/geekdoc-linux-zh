Mount it as follows:

```
# mount -o loop /tmp/initrd-2.6.7-1.478.img /mnt/image
```

and browse the directory to your heart's content.

Not every system will have an *initrd.img* file. It is typically used to load device drivers for file systems (such as Reiser) or hardware (such as the Promise RAID IDE controller) that must be in place before the system can continue booting. Some floppy-disc-based Linux distributions use *initrd.img* to load a minimal operating system that can then uncompress and load the working file system from the floppy.

You can also mount .iso images in the same way, but remember that they are always read-only because of the nature of the underlying iso9660 file system; you can write to the other images unless you explicitly mount them as read-only. If you want to read and write to the files in an ISO file system, you must first copy the files to a device that is mounted read-write, make your changes, and then use mkisofs to create a new .iso image. This is a common "gotcha" for many users.

# Managing Files for Character Devices, Block Devices, and Special Devices

For UNIX and Linux, *everything* is a file. In this section, you learn about special types of files found in Linux that represent all the devices found on your system and handle all the input and output on your system. You also learn how to identify and create them.

If you have installed the kernel documentation, it will contain a text file named /usr/src/linux-2.6/Documentation/devices.txt, an excerpt of which reads

```
3 char Pseudo-TTY slaves
	0 = /dev/tty0	First PTY slave
	1 = /dev/tty1	Second PTY slave
	...
	255 = /dev/ttyer	256th PTY slave
```

These are the old-style (BSD) PTY devices; Unix98 devices are on major 136 and above.

```
block	First MFM, RLL and IDE hard disk/CD-ROM interface
	0 = /dev/hda	Master: whole disk (or CD-ROM)
	64 = /dev/hdb	Slave: whole disk (or CD-ROM)
```

For partitions, add to the whole disk device number:

```
0 = /dev/hd?	Whole disk
1 = /dev/hd?1	First partition
2 = /dev/hd?2	Second partition
...
63 = /dev/hd?63	63rd partition
```