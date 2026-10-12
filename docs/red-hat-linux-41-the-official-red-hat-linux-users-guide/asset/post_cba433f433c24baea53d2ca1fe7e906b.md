
- 4. `eb66.img` (EB66)
- 5. `eb66p.img` (EB66+)
- 6. `jensen.img` (Jensen's)
- 7. `avanti.img` (AlphaStation 200, 250, 400)
- 8. `xl.img` (Alpha XL)
- 9. `xlt.img` (Alpha XTL)
- 10. `eb164.img` (EB164 based machines)
- 11. `p2000.img` (Platform 2000)
- 12. `pc164.img` (Alcor based machines)
- 13. `alcor.img` (Alcor based machines)
- 14. `mikasa.img` (Mikasa based machines)

All of these images should work on machines with either VGA or TGA based graphics boards. To create a floppy from these images, use `rawrite.exe` under MS-DOS or MS-Windows (it is available in the `dosutils` directory), or `dd` under Linux or Unix.

### 3.4.2 Beginning the Install

Installing Red Hat Linux/Alpha requires the use of a ramdisk. Several ramdisk images are on the Red Hat Linux/Alpha CD in the `images` directory. To begin the install, boot to the MILO prompt and insert your boot disk in your first floppy drive. Then give this command to MILO:

```
boot fd0:vmlinux.gz root=/dev/fd0 load_ramdisk=1 prompt_ramdisk=1
```

MILO reads the Linux kernel from your boot disk and runs it. The kernel loads a basic system from the remainder of the floppy and runs the installation program. If you are using the SRM console, the `load_ramdisk=1 prompt_ramdisk=1` command must be given to the kernel as arguments for the install to begin properly. Red Hat Linux/Alpha supports two varieties of hard drive partitioning:

- Standard *fdisk*-style partitioning; this has the usual oddities (such as extended partitions) and is done in the same way as on Intel platforms (using Linux *fdisk*). This is the partitioning style you must use if you are using the ARC console.
- BSD-style disk-labelling. It is normal to make the first partition on a disk-labelled hard drive the swap partition. We don't recommend using BSD disk-labelling unless it is absolutely necessary.

### 3.4.3 Finishing Up

After the install is finished and your system is fully configured, you will be asked to reset your computer. This indicates that your system has been successfully installed.

### 3.5 Booting your Red Hat Linux/Alpha system

To boot Red Hat Linux from MILO, you must use the **boot** command. The command differs slightly depending on where your root partition is. For example, if your root partition is the second partition on your first SCSI hard drive, you would boot as follows:

```
boot sda2:vmlinux.gz root=/dev/sda2
```

If instead your root partition is the third partition on your second IDE drive, you would use this command:

```
boot hdb3:vmlinux.gz root=/dev/hdb3
```

For information on these commands and on automating the boot process, please read the MILO HOWTO in Appendix E.

# Chapter 4 Installing Red Hat Linux/SPARC

These are brief installation instructions for the Red Hat Linux/SPARC 4.1 release for the SPARC family of processors. This chapter describes the differences between installing Red Hat Linux/SPARC and Red Hat Linux/Intel. For further details on the installation procedure, please see Chapter 2.

### 4.1 Hardware

Red Hat Linux/SPARC is known to function on the following hardware:

- sun4c architecture machines (IPC, SS1, etc)
- sun4m architecture machines (Classic, SS5, SS10, etc)
- bwtwo, cg3, cg6, TCX framebuffers (24 bit on the TCX)
- cg14 framebuffer (in cg3 mode)
- SCSI and Ethernet on all of the above
- type 4 and type 5 keyboards and mice
- external SCSI drives
- CD-ROM drives (external and internal)
- SCSI/Ether SBUS expansion cards
- Any original equipment Sun monitor for the above framebuffers

A partial list of **unsupported** hardware:

- VME based sun4m machines, such as the 4/690
- sun4d (SS1000, SS2000)
- sun4u (UltraSparc1, UltraSparc2, EnterPrise UltraSparc servers)
- sun4 architecture
- Eurocard sun4c machines, called the 'sun4e' under Solaris2.4 and others, are not supported. These are VME-bus sun4c machines, to which the kernel has not been ported yet.

### 4.2 Booting from Floppy

First you need to boot your system to the install program. You will have to create your boot floppy, and creating it depends on which version of the PROM you have. The **images directory** on your Red Hat Linux/SPARC CD contains two images. Use *boot-r0.img* if you have a PROM version 0 or 1 (this is the major number...PROM 1.6 is a type 1 PROM), Use *boot-v2.img* if you have a PROM version 2.0 or greater. To create the floppy, you can use *rawrite.exe* under MS-DOS (located on your Red Hat Linux/SPARC CD in the *dosutils* directory), or you can use **dd** under Linux or Unix. Under MS-DOS, you would enter the following commands (assuming the CD-ROM is drive **d**):

```
d:            
cd \images     
..\dosutils\rawrite.exe
```

When prompted, enter the file name of the image to write to floppy. Under Linux or Unix, mount the CD, change to the directory it is mounted under, and use the following command:

```
dd if=images/boot-v2.img of=/dev/fd0
```

Replace boot-v2.img with boot-v0.img if you have a version 0 or 1 PROM. Also note, do not use /dev/rfd0 under Solaris; it will not work. Use /dev/fd0 instead.

Insert the diskette, and at the PROM prompt enter boot floppy. You will be presented with a SILO prompt. If you wish to do your install using a ramdisk (it will use about 2M of RAM and is recommended if you have 8M or more of RAM), you can simply press Enter at the SILO prompt. If you wish to do an NFS-rooted install, you will need to supply some parameters here. The formula is as follows:

```
linux nfsroot=nfs.server.IP.address:/path/to/RH/image
```

For this to work you will need a rarp entry or a bootp entry on your network that will give your SPARC its IP address. This is covered in Section 4.3 below.

### 4.3 Booting from a Network

If you do not have floppy drive, and your PROM is less than version 2, you will need to do a network boot. This is fairly easy to do, but you will need a rarp entry on a server on your local network to tell the target SPARC what its IP address is. This can be done on a Linux system that has RARP built into the kernel (or inserted as a module), using a command of this form:

```
rarp -s ip.address.of.sparc hw:address:of:sparc
```

You also need an ARP entry in most cases; for example:

```
arp -s ip.address.of.sparc hw:address:of:sparc
```

Now you need to setup a TFTP server on your local network to serve the kernel to the target SPARC. This should be the same machine that is doing the rarp above. Under Red Hat Linux, this can be done by editing /etc/inetd.conf. You need an entry that looks similar to:

```
tftp dgram udp wait root /usr/sbin/tcpd in.tftpd /home/tftp
```

You can now copy the /images/vmlinuz to /home/tftp on your server and create a symbolic link so that the PROM can get the proper file. This symbolic link is conditional based on the IP address and architecture of the target SPARC. You need to make the link be the hex value of your IP address “dot” the architecture. For example, to create a symbolic link for flanders.redhat.com, a sun4m machine with IP address 199.183.24.232, you would enter the command:

```
cd /home/tftp
ln -s vmlinuz C7B718E8.SUN4M
```

At this point you should be able to go to the PROM on your SPARC and type:

```
boot net nfsroot=nfs.server.IP.address:/path/to/RH/image
```

and it should get its rarp request from the TFTP server fulfilled and start loading the kernel via TFTP. The kernel should then boot and start the install.

After booting the installation disk you will be greeted by a welcome screen with a single button; press Enter to begin the installation.

Now, choose the medium you will be installing from: NFS, Hard Disk or FTP. Installing from hard disk will work if you have an existing partition with an EXT2 filesystem only; installation from UFS is not yet implemented.

#### 4.4 Network Installation

You can also do an FTP install by TFTPing an entire install image (kernel and root filesystem). You will want to do the same as the above example, ex-
