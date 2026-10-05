# 288 Part VI: The Part Tens

prevention: Make an emergency boot floppy disk, as I instruct you to during installation. Keep this disk handy when you update your system (or during any other significant system event, such as repartitioning disks or rebuilding your kernel). Then, if you make a mistake, you can boot the floppy, which will enable you to reboot your Linux operating system. When you've rebooted your system using the floppy, just log in as root and type **lilo** on the command line. This repairs the MBR by reinstalling LILO.

![](bbox=[0.115, 0.185, 0.178, 0.303])

If you are installing multiple operating systems on a new machine, do yourself a favor and install Linux last. Otherwise, you have to keep reinstalling LILO.

# # My Disk Numbers Have Changed Since Installation

**Problem:** Linux numbers disks each time it boots, counting SCSI names like sda, sdb, and sdc. Suppose sda holds your Microsoft system, sdb holds the bulk of Linux, sdc holds your user files, and sdb holds your swap space. You add another disk and your user files are on sdn and your swap space is on sde. The new disk is called sdc but has nothing on it. What happened?

**Solution:** SCSI disks are lettered according to the SCSI IDs on each disk. Linux names the disks using this ordering scheme. If you insert a new disk into the SCSI bus with a SCSI ID that is lower than an existing disk, you rename all with a SCSI ID above the one you just installed. It's best to start installing your SCSI disks with a SCSI ID of 0, 1, 2, and so on; then put other SCSI devices at the end of the SCSI bus with SCSI IDs 6, 5, 4, and so on). Note that most SCSI controllers are set to SCSI ID 7 by default.

IDE disks are numbered according to the IDE controller they are on and whether they are a master or a slave on that controller. Therefore, adding a new disk to a set of IDE controllers will not change the existing names, as shown here:

| Controller | Disk | Linux Name |
|---|---|--|
| ide0 | master | hda |
| ide0 | slave | hdb |
| ide1 | master | hdc |
| ide1 | slave | hdd |
| ide2 | master | hde |
| ide2 | slave | hdf |