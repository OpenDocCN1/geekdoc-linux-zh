![](bbox=[0.3, 0.07, 0.75, 0.77])

# Figure 7.2 Partitioning a 720 Mb hard disk.

stallation will then be made into the root partition, which leaves the other partition initially empty and allows it to be used as user home directory and working space, by mounting it as /home. Many other arrangements are possible and you may need to experiment until you find the one that suits your own particular circumstances best.

The program used to partition disks is called fdisk, both under DOS and under Linux. In general, you should only create the partitions to be used within a particular operating system using that system’s own fdisk command. So the first task in our example is to install DOS from the master disks, using the DOS fdisk command to create just the required DOS partitions, leaving the rest of the disk space unallocated.

Most Linux distributions supply a one- or two-disk set, which you need to use to boot Linux on your machine initially. With the Slackware distribution there are two disks required, called the boot and root disks. In fact, there are several different versions of each of them, and you will need to select an appropriate one of each. The choice is based on what type of hard disk you will be installing to (SCSI or not) and what medium you will be using as the source of the files to install from (CD-ROM, floppy disk, hard disk or network).

You should consult the release notes supplied with your distribution (probably as a README file or a thin paper leaflet) to help you make the appropriate choice and to tell you how to create the boot and root disks from the files available.