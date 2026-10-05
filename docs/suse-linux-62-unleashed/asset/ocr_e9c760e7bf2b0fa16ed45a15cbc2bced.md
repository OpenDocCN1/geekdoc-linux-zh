# SuSE System Administration
PART III

You can discover the geometry of one of your hard disks by using the hdparm command (useful only for IDE drives), and typical output might look like the following:

```
$ hdparm -g /dev/hda
```

```
/dev/hda:
geometry = 970/128/63, sectors = 7825932, start = =
```

```
$ hdparm -g /dev/hdb

dev/hdb:
geometry = 523/255/63, sectors = 8406720, start = =
```

As you can see from the geometry specified in this example, these are the drives discovered previously.

> Note
IBM PCs with older BIOSs can have difficulty with large disks; see the Linux Large-Disk mini-HOWTO.

# Floppy Disks

Floppy disks are removable low-capacity storage media. As storage devices, they are far slower than hard disks, but they have the advantage of being removable, which makes them good media for transporting modest amounts of data.

The block devices corresponding to the floppy disks begin with the letters fd; /dev/fd0 is the first, and any additional ones have increasing numbers. There are many possible formats for a floppy disk, and the kernel needs to know the format (geometry) of a disk to read it properly. Linux can usually work out the correct format, so the automatic devices /dev/fd0 (plus /dev/fd1 and so) are usually sufficient, but if some reason it is necessary to specify the exact format, further device names are provided. The device /dev/fd144, for example, denotes a 1.44MB high-density floppy. There are many more devices indicating obscure formats, both older lower-capacity formats and other nonstandard high-capacity formats. You can create your own floppy-disk formats using the setfdparm program.

The most common reason to use the specific-format device names is that formatting a floppy for the first time. In this situation, the disk is not yet readable, so the kernel will not be able to autoprobe an existing format. You need to use the name /dev/fd0144,