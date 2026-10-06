
## CHAPTER 6
## Booting and Shutting Down

Linux Administration: A Beginner's Guide

As the complexity in modern-day operating systems has grown, so has the complexity in the starting up and shutting down processes. Anyone who has undergone the transition from a straight DOS-based system to a Microsoft Windows-based system has experienced this firsthand. Now is the core operating system being brought up and shut down, but like Windows, an impressive list of services and processes (some critical and others less) must be started and stopped.

In this chapter, we discuss the bootstrapping of the Linux operating system with GRUB and Linux Loader (LILO). We then step through the processes of starting up and shutting down the Linux environment, as well as modifications that might sometimes be desirable in the scripts. We finish with coverage of a few odds and ends that pertain to booting up and shutting down.

> NOTE: Apply a dose of common sense in following the practical exercises on this chapter on a real/production system. As you experiment with modifying startup and shutdown scripts, bear in mind that it is possible to bring your system to a non-own state that cannot be recovered by rebooting. Don't mess with a production system; if you must, make sure that you back up all the files you want to change, and most importantly, have a bootable rescue disk ready.

# Boot Loaders

For any operating system to boot on standard PC hardware, you need what is called a boot loader. If you have only dealt with Windows on a PC, you have probably never needed to interact directly with a boot loader. The boot loader is the first software program that runs when a computer starts. It is responsible for handing over control of the system to the operating system.

Typically, the boot loader will reside in the Master Boot Record (MBR) of the disk, and it knows how to get the operating system up and running. The main choices that come with Linux distributions are GRUB and, less, LILO. This chapter focuses on GRUB, because it is the most common boot loader that ships with the newer distributions of Linux and because it offers a lot more features than LILO. GRUB currently comes in two versions—GRUB Legacy and GRUB version 2 (GRUB 2).

A brief mention of LILO is made for historical reasons only. Both LILO and GRUB can be configured to boot other non-native operating systems.

# GRUB Legacy

Most modern Linux distributions use GRUB as the default boot loader during installation, including Fedora, Red Hat Enterprise Linux (RHEL), openSUSE, Debian, Mandrake, CentOS, Ubuntu, and a host of others. GRUB aims to be compliant with the Multiboot Specification and offers many features.

The GRUB boot process happens in stages. Each stage is taken off by special GRUB image files, with each stage helping the next stage along. Two of the stages are essential, and the other stages are optional and dependent on the particular system setup.

> CAUTION: Please remember that most of the information and all of the sample exercises in this GRUB Legacy section also apply systems running legacy versions of GRUB. This includes GRUB version 0.99 and earlier.

On RPM-based systems, you can check your GRUB version by running:

```bash
# rpm -qa | grep -i grub
# Debian-based systems, you can check your version of GRUB by running
# dpkg -l | grep -i grub
```

If the output shows you are running GRUB 2 or newer (version 1.98, 1.99, and so), you will not be able to follow along with the exercises without first downgrading to GRUB Legacy.

# Stage 1

The image file used in this stage is essential and is for booting GRUB in the first place. It is usually embedded in the MBR of a disk or in the boot sector of a partition. The image file used in this stage is appropriately named stage1. A Stage 1 image can either load Stage 1.5 or load Stage 2 directly.

# Stage 2

The Stage 2 actually consists of two types of images: the intermediate (optional image) and the actual stage2 image. To blur things, the optional images are called Stage 1.5. The Stage 1.5 images serve as a bridge between Stage 1 and Stage 2. The Stage 1.5 images are file-system specific; that is, they understand the semantics of one file system or the other.

The Stage 1.5 images have the name of x_stage_1_5, where x can be a file of type e2fs, ReiserFS, JFS, MINIX, and so on. For example, the Stage 1.5 that will be required to load an OS that resides on a File Allocation Table (FAT) file system will have a name similar to fat_stage1_5. The Stage 1 images allow GRUB to access several file systems. When used, the Stage 1.5 helps to locate the Stage 2 within the file system.

Next comes the actual stage2 image. It is the core of GRUB. It contains the actual code to load the kernel that boots the OS, it displays the boot menu, and it also contains the GRUB shell from which GRUB commands can be executed. The GRUB shell is interactive and helps to make GRUB flexible. For example, the shell can be used to boot items that are not currently listed in GRUB's boot menu or to bootstrap the OS from an alternative supported medium.

Other types of Stage 2 images are the stage2_forter image, the nbgroup image, and the pxegrub image. The stage2_forter is for optical discs. The nbgroup and pxegrub images are both network-type that can be used over the network (DHCP, PXE, or TFTP). A quick listing of these is shown below.

# Conventions Used in GRUB

GRUB has its own way of referring to devices. GRUB starts numbering from 0. For example, GRUB will refer to the primary disk as hd0. GRUB partitions are enclosed in parentheses, for example (hd0,0).

> NOTE: GRUB does not distinguish between different interface types (e.g., IDE, SATA, SCSI).

# Installing GRUB Legacy

Most Linux distributions give you a choice to install GRUB during normal installation. However, there are times, either by accident or design, you have another type of boot loader (such as LILO or the NT Loader) but you want to replace or overwrite that boot loader with GRUB.

This section will show you how to install GRUB. You will learn how to install it natively using the grub command inside the running Linux system.

# Backing Up the MBR

Before you proceed with the exercises that follow, it is a good idea to make a backup of your "known good" MBR. It is easy to do this with the dd command. Since the MBR of a PC resides in the first 512 bytes of the disk, you can easily copy the first 512 bytes to a file by typing the following:

```bash
dd if=/dev/sda of=/tmp/COPY_MBR bs=512 count=1
```

This command will save the MBR into a file COPY_OF_MBR under the /tmp directory.

# Installing GRUB from the GRUB Shell

Now that we have dealt with the safety measures, we can proceed to exploring GRUB in full. In this, you will learn how to install GRUB natively using the grub command inside the running system.

Launch GRUB's shell by issuing the grub command:

```bash
server:~ # grub
Probing devices to guess BIOS drives. This may take a long time.
```

Display GRUB's root device:

```bash
grub> root
root
(fd0): Filesystem type unknown, partition type 0x0
```

The output shows that GRUB will, by default, use the first floppy disk drive (fd0) as its root device, unless you tell it otherwise.

Set GRUB's root device to the partition that contains the boot directory on the local disk:

```bash
grub> root (hd0,0)
root (hd0,0)
Filesystem type is ext2fs, partition type 0x83
```
