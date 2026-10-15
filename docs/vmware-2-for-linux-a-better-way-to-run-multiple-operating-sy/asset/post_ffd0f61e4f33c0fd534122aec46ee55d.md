
![](img/b2b6702758c230ce537468351fc8af15_393_0.png)

Figure 6.5 Drives D and E are actually partitions on a real Windows hard drive, configured as a raw disk in VMware.

## Creating Plain Disks

Raw disks have their advantages, but their use is obviously predicated on having a spare hard drive you want to use directly inside a VMware virtual machine. If you simply want to break the 2GB virtual disk limit without employing a separate hard drive, plain disks might be the right choice.

The easiest, and arguably most useful, type of plain disk is made of files in your Linux file system. These files are, in essence, a series of large files strung together to form a single virtual disk. Although the files themselves are still subject to a 2GB limit, VMware creates as many as are necessary to accommodate the plain disk file size you request and divides the load equally between the files. (That is, if you use a 3GB plain disk, the two files will be 1.5GB in length, rather than one 2GB file and one 1GB file.)

The major disadvantage to plain disks over virtual disks is that they immediately consume the entire requested space on your Linux hard drive. Virtual disks, on the other hand, grow as necessary to your preset limit. So there is little or no advantage to using a file-based plain disk of less than 2GB.

To create a file-based plain disk, follow these steps:

- 1. Open the virtual machine configuration in the Configuration Editor.
- 2. Find a free slot in the IDE or SCSI Drives section.

> If you plan to boot from your plain disk, it is a good idea to use the Primary IDE (P-M) slot.

- 3. Set the Device Type to Plain Disk.
- 4. Type a name for your plain disk in the Name box. This will be the name of the plain disk descriptor file, a small file stored in your VMware configuration directory that describes the composition of the plain disk to VMware. At this point, your screen should look much like Figure A.6.
- 5. Click Create Plain Disk. A new window (shown in Figure A.7) appears, asking whether the plain disk should be built from files or from hard disk partitions.
- 6. Select Files in the host filesystem.
- 7. Enter the size of the plain disk and click OK.

![](img/b2b6702758c230ce537468351fc8af15_394_0.png)

Figure A.6 Use the Configuration Editor to start the creation of a new plain disk.

![](img/b2b6702758c230ce537468351fc8af15_394_1.png)

Figure A.7 File-based plain disks are easier to create and are probably the best choice for most system configurations.

Remember that you need to have all of the space required available on your Linux file system when you create the plain disk. Do not create plain disks under 2GB; use virtual disks instead.

- 8. The Plain Disk Editor appears (shown in Figure A.8). You should be able to accept the defaults, unless you for some reason want the plain disk to be read-only.

![](img/b2b6702758c230ce537468351fc8af15_395_0.png)

Figure A.8 The Plain Disk Editor governs the level of control the virtual machine has over the new plain disk.

It is easier and just as secure to leave the RO (read-only) option turned off and then use Nonpersistent mode if you want to write-protect your plain disk.

- 9. Creating the plain disk can take several minutes, during which time your mouse and keyboard response could be severely impaired.
- 10. Remember to click Install to commit the settings for the plain disk so that it will be recognized when you launch your virtual machine.
- 11. Launch your virtual machine, and format the plain disk inside the guest OS as you would any other disk partition. Figure A.9 shows a sample, using fdisk on a newly created Windows plain disk.

If you choose a partition-based plain disk instead of file-based, the major difference is in the Plain Disk Editor. You first indicate the hard drive device you want to use to build the plain disk (such as /dev/hda and so on), and then the Editor asks you which partitions should be included, as shown in Figure A.10.

In this example, the partitions are labeled /dev/hdc1 and /dev/hdc5. If the plain disk should only incorporate /dev/hdc1, you can opt to set /dev/hdc5 to read-only, or better yet, click Delete. (This does not delete the partition; it only deletes the entry for that partition from the plain disk description file!) You can leave all of the data files (plaindisk21.dat and plaindisk23.dat as shown in this example) alone; they take up very little space.
