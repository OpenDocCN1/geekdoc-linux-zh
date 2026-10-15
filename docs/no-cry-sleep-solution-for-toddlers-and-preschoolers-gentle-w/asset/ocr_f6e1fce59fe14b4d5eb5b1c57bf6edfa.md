# Tip

If you are not using GRUB, or if for some reason you do not want to modify the /etc/grub.conf file, you can configure the /etc/modules.conf file (/etc/modprob.conf on 2.5 and 2.6 kernels) to load and implement the SCSI emulation for your IDE CD drives. This involves entering several module configuration commands in the /etc/modules.conf file. When your system starts up, it will load the modules as specified in that file.

# scanbus

To check that your IDE drives are being recognized as SCSI drives, run cdrecord with the -scanbus option (or dvdrecord for DVD writers). This example shows two IDE CD drives now emulating SCSI CD drives. One is a Plextor IDE CD-RW drive (scd0), and the other is a Toshiba DVD-ROM drive (scd1).

```
# cdrecord -scanbus
Cdrecord 1.9 (i686-pc-linux-gnu) Copyright (C) 1995-2000 Jörg Schilling
Linux sg driver version: 3.1.17
Using libscg version 'schily-0.1'
scsibus0:
 0,0,0 0) 'PLEXTOR ' 'CD-R   PX-W1210A' '1.02' Removable CD-ROM
 0,1,0 1) *
 0,2,0 2) *
 0,3,0 3) *
 0,4,0 4) *
 0,5,0 5) *
 0,6,0 6) *
 0,7,0 7) *
```

# Creating File Systems: mkfs, mke2fs, mkswap, parted, and fdisk

Linux provides a variety of tools for creating and managing file systems, letting you add new hard disk partitions, create CD images, and format floppies. To use a new hard drive, you will first have to partition it and then create a file system on it. You can use either parted or fdisk to partition your hard drive. To create the file system on the partitions, you use the mkfs command, which is a front end for various file system builders. For swap partitions, you use a special tool, mkswap, and to create file systems on a CD-ROM, you use the mkisofs tool. Linux partition and file system tools are listed in Table 30-10.

# fdisk

To start fdisk, enter fdisk on the command line with the device name of the hard disk you are partitioning. This brings up an interactive program you can use to create your Linux partition. Be careful using Linux fdisk. It can literally erase entire hard disk partitions and all the data on those partitions if you are not careful. The following command invokes fdisk for creating partitions on the hdb hard drive.

```
fdisk /dev/hdb
```

The partitions have different types that you need to specify. Linux fdisk is a line-oriented program. It has a set of one-character commands that you simply press. Then you may be prompted to type in certain information and press ENTER. If you run into trouble during the