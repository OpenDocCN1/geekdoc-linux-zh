
on your video card and mouse type, which will be helpful in configuring X later on.

Third, check your machine for configuration problems with supported hardware that could cause an unrecoverable lockup during Linux installation.

![](img/a3584dae761d2e3abed8bf40d7637389_115_0.png)

**TIP**
It is possible for a DOS/Windows system using IDE hard drive(s) and CD-ROM to be functional even with the master /slave jumpers on the drives incorrectly set. Linux won't fly this way. If in doubt, check your master /slave jumpers!

Is any of your peripheral hardware designed with neither configuration jumpers nor non-volatile configuration memory? If so, it may require boot-time initialization via an MS-DOS utility to start up, and may not be easily accessible from Linux. CD-ROMs, sound cards, Ethernet cards and low-end tape drives can have this problem. If so, you may be able to work around this with an argument to the boot prompt; see the Linux Boot Prompt HOWTO, http://MetaLab.unc.edu/LDP/HOWTO/BootPrompt-HOWTO.html, for details.

![](img/a3584dae761d2e3abed8bf40d7637389_115_1.png)

**WARNING**
Some other operating systems will allow a bus mouse to share an IRQ with other devices. Linux doesn't support this; in fact, trying it may lock up your machine. If you are using a bus mouse, see the Linux Bus Mouse HOWTO, http://MetaLab.unc.edu/LDP/HOWTO/Busmouse-HOWTO.html, for details.

If possible, get the telephone number of an experienced Linux user you can call in case of emergency. Nine times out of ten, you won't need it, but it's comforting to have.

Budget time for installation. That will be about one hour on a bare system or one being converted to all-Linux operation—or up to three hours for a dual-boot system (they have a much higher incidence of false starts and hangups).

## Creating the Boot and Root Floppies

Your Linux CD-ROM may come with installation aids that will take you through the process of building boot, root, and rescue disks with interactive prompts. These may be an MS-DOS installation program (such as the Red Hat redhat.exe program) or a Unix script, or both.

# NOTE

This step is only needed if you can't boot from a CD-ROM.

If you have such a program and can use it, you should read the rest of this subsection for information only. Run the program to do actual installation--its authors certainly knew more about the specific distribution than I, and you'll avoid many error-prone hand-entry steps.

# TIP

For more detailed information on making boot and root disks, see the Linux Boot-disk HOWTO at http://MetaLab.unc.edu/LDP/HOWTO/Bootdisk-HOWTO.html.

Your first step will be to select a boot-disk image to fit your hardware. If you must do this by hand, you'll generally find that either (a) the boot-disk images on your CD-ROM are named in a way that will help you pick a correct one, or (b) there's an index file nearby describing each image.

Next, you must create floppies from the boot-disk image you selected and from the root and rescue disk images. This is where the MS-DOS program RAWWRITE.EXE comes into play.

Next, you must have two or three high-density MS-DOS formatted floppies. (They must be of the same type; that is, if your boot disk drive is a 3.5 drive, both floppies must be high-density 3.5 disks.) You will use RAWRITE.EXE to write the boot and root-disk images to the floppies.

Invoke it with no arguments, like this:

```
C:\ RAWRITE
```

Answer the prompts for the name of the file to write and the floppy to write it to (such as A: ). RAWRITE will copy the file, block-by-block, directly to the floppy. Also use RAWRITE for the root disk image (such as COLOR144). When you're done, you'll have two floppies: one containing the boot disk, the other containing the root disk. Note that these two floppies will no longer be readable by MS-DOS (they are Linux format floppies, in some sense).

You can use the dd commands on a Unix system to do the same job. (For this, you will need a Unix workstation with a floppy drive, of course.) For example, on a Sun workstation with the floppy drive on device /dev/rf00, you can use the command:

```
$ dd if=bare of=/dev/rf00 obs=18k
```

You must provide the appropriate output block size argument (the `obs` argument) on some workstations (e.g., Suns) or this will fail. If you have problems, the man page for dd(1) may be instructive.

Be sure that you're using brand-new, error-free floppies. The floppies must have no bad blocks on them.

Note that you do not need to be running Linux or MS-DOS in order to install Linux. However, running Linux or MS-DOS makes it easier to create the boot and root floppies from your CD-ROM. If you don't have an operating system on your machine, you can use someone else's Linux or MS-DOS just to create the floppies and install from there.

## Repartitioning Your DOS/Windows Drives

On most used systems, the hard drive is already dedicated to partitions for MS-DOS, OS/2, and so on. You'll need to resize these partitions in order to make space for Linux. If you're going to run a dual-boot system, it's strongly recommended that you read one or more of the following mini-HOWTOs, which describe different dual-boot configurations.

- The DOS-Win95-OS2-Linux mini-HOWTO: http://MetaLab.unc.edu/LDP/HOWTO/mini/Linux+DOS+Win95+OS2.html
- The Linux+Win95 mini-HOWTO: http://MetaLab.unc.edu/LDP/HOWTO/mini/Linux+Win95.html
- The Linux+NT-Loader mini-HOWTO: http://MetaLab.unc.edu/LDP/HOWTO/mini/Linux+NT-Loader.html

Even if they are not directly applicable to your system, they will help you understand the issues involved.

Note that some kinds of Linux will install to a directory on your MS-DOS partition. (This is different from installing *from* an MS-DOS partition.) Instead, you use the UMSDOS filesystem, which allows you to treat a directory of your MS-DOS partition as a Linux filesystem. In this way, you don't have to repartition your drive.

I only suggest using this method if your drive already has four partitions (the maximum supported by DOS) and repartitioning would be more trouble than it's worth (it slows down your Linux due to filename translation overhead). Or, if you want to try out Linux before repartitioning, this is a good way to do so. But in most cases you should repartition, as described here. If you do plan to use UMSDOS, you are on your own -- it is not documented in detail here. From now on, we assume that you are not using UMSDOS and that you will be repartitioning.

A *partition* is just a section of the hard drive set aside for a particular operating system to use. If you only have MS-DOS installed, your hard drive probably has just one partition, entirely for MS-DOS. To use Linux, however, you’ll need to repartition the drive so that you have one partition for MS-DOS and one (or more) for Linux.

Partitions come in three flavors: *primary*, *extended*, and *logical*. Briefly, primary partitions are one of the four main partitions on your drive. However, if you wish to have more than four partitions per drive, you need to create an extended partition, which can contain many logical partitions. You don’t store data directly on an extended partition—it is used only as a container for logical partitions. Data is stored only on either primary or logical partitions.

To put this another way, most people use only primary partitions. However, if you need more than four partitions on a drive, you create an extended partition. Logical partitions are then created on top of the extended partition, and there you have it—more than four partitions per drive.

Note that you can easily install Linux on the second drive on your system (known as D: to MS-DOS). You simply specify the appropriate device name when creating Linux partitions. This is described in detail later in this chapter.

Back to repartitioning your drive. The problem with resizing partitions is that there is no way to do it (easily) without deleting the data on those partitions. Therefore, you will need to make a full backup of your system before repartitioning. In order to resize a partition, we simply delete the partition(s) and re-create them with smaller sizes.

There is a nondestructive disk repartitioner called FIPS available for MS-DOS. Look at `http://Metalab.unc.edu/pub/Linux/system/install`. With FIPS, a disk optimizer (such as Norton Speed Disk), and a little bit of luck, you should be able to resize MS-DOS partitions without destroying the data on them. It’s still suggested that you make a full backup before attempting this.

If you’re not using FIPS, however, the classic way to modify partitions is with the program FDISK. For example, let’s say that you have an 80 meg hard drive dedicated to MS-DOS. You’d like to split it in half—40 megs for MS-DOS and 40 megs for Linux. In order to do this, run FDISK under MS-DOS, delete the 80 meg MS-DOS partition, and re-create a 40 meg MS-DOS partition in its place. You can then format the new partition and reinstall your MS-DOS software from backups. 40 megabytes of the drive is left empty. Later, you create Linux partitions on the unused portion of the drive.

![](img/a3584dae761d2e3abed8bf40d7637389_118_0.png)
