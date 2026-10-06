# CHAPTER 6 Booting and Shutting Down

Mandrake, CentOS, Ubuntu, and a host of others. GRUB aims to be compliant with the Multiboot Specification and offers many features.

The GRUB boot process happens in stages. Each stage is taken of by special GRUB image files, with each stage helping the next stage along. Two of the stages are essential, and the other stages are optional and dependent on the particular system setup.

> CAUTION Please remember that most of the information and all of the sample exercises in this GR GR Legacy section also systems running legacy versions of GRUB. This includes GRUB version 0.99 and earlier.

On RPM-based systems, you can check your GRUB version by running

```
# rpm -qa | grep -i grub
# Debian-based systems, you can check your version of GRUB by running
# dpkg -l | grep -i grub
```

If the output shows you are running GRUB 2 or newer (version 1.98, 1.99, and so, you will not be able to follow along with the exercises without first downgrading to GRUB Legacy.

# Stage 1

The image file used in this stage is essential and is for booting GRUB in the first place. It is usually embedded in the MBR of a disk or in the boot sector of a partition. The image file used in this stage is appropriately named stage1. A Stage 1 image can either load Stage 1.5 or load Stage 2 directly.

# Stage 2

The Stage 2 actually consist of two types of images: the intermediate (optional image) and the actual stage2 image. To blur things, the optional images are called Stage 1.5. The Stage 1.5 images serve as a bridge between Stage 1 and Stage 2. The Stage 1.5 images are file-system specific; that is, they understand the semantics of one file system or the other.

The Stage 1.5 images have the name of x_stage_1_5, where x can be a file of type e2fs, ReiserFS, JFS, MINIX, and so on. For example, the Stage 1.5 that will be required to load an OS that resides on a File Allocation Table (FAT) file system will have a name similar to fat_stage1_5. The Stage 1 images allow GRUB to access several file systems. When used, the Stage 1.5 helps to locate the Stage 2 within the file system.

Next comes the actual stage2 image. It is the core of GRUB. It contains the actual code to load the kernel that boots the OS, it displays the boot menu, and it also contains the GRUB shell from which GRUB commands can be executed. The GRUB shell is interactive and helps to make GRUB flexible. For example, the shell can be used to boot items that are not currently listed in GRUB's boot menu or to bootstrap the OS from an alternative supported medium.