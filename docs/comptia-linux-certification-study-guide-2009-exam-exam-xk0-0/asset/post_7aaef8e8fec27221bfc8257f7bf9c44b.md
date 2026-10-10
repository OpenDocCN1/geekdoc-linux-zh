
5. What does FHS stand for?
A. Free home space
B. Similar to NFS, but works on an Apple Mac
C. File Hierarchy Specification
D. Filesystem Hierarchy Standard

6. Which Linux command is used to attach a separate storage device to an existing directory?
A. `mkmount`
B. `mount`
C. `umount`
D. `fdisk`

7. What is contained in the /var/log directory?
A. A variation in system device drivers
B. Contains data as the result of spooling, logging, and system temporary files.
C. A shareable read-only directory for all users to access
D. System libraries and packages

8. What argument do you use to obtain an easy readable output for the Linux `du` command?
A. `-h`
B. `-i`
C. `-v`
D. [no options]

9. Your manager has asked you to mount a CD disc on the community workstation in the lobby, so that everyone can access it. The CD disc needs to be mounted on the /media/cdplayer directory. Which `-t` filesystem option must you include?
A. `-t iso9660`
B. `-t iso`
C. `-t iso9000`
D. `-t ext3`

10. What is another format for DVDs besides the ISO9660 format?
A. /swap
B. SCSI
C. Universal Disk Format (UDF)
D. SMBFS

11. You need to use `fdisk` to establish a partition for a new SCSI disk drive you want to add for extra storage space. The original drives all are IDE drives. Which is the correct syntax?
A. `fdisk /dev/SCSI1`
B. `fdisk /dev/IDE`
C. `fdisk /dev/sda`
D. `fdisk /dev/sdb`

12. Which file, when the system initially starts up, will automatically mount filesystems?
A. `/etc/fstab`
B. `/boot/fstab`
C. `/dev/devices.map`
D. `/etc/grub.conf`

13. What is an ISO loopback device?
A. The transformation of a special file into a virtual Linux filesystem
B. A device that returns feedback tests to the monitor
C. The `/null` driver device
D. The IP address 127.0.0.1

14. Which Linux command is used to designate a specific file or partition for swapping?
A. `/swap`
B. `fileswap`
C. `swapon`
D. `grub`

15. What is the purpose of the Linux `exportfs` command?
A. It functions as the Linux bootloader
B. To partition a storage device
C. To designate a specific file or partition for swapping
D. To activate the access of shared NFS directories

## SELF TEST QUICK ANSWER KEY

1. B
2. A
3. C
4. C
5. D
6. B
7. B
8. A
9. A
10. C
11. C
12. A
13. A
14. C
15. D

# Boating Linux

**Exam objectives in this chapter**

- GRUB
- Runlevels
- Troubleshooting Boot Issues

## UNIQUE TERMS AND DEFINITIONS

- **GRand Unified Bootloader (GRUB)** An application used on most modern versions of the Linux operating system. It is a dynamically configurable program used to perform a sequence of events on a computer to load the main operating system. It receives control from the system BIOS, performs a sequence of events, and then transfers control to the operating systems kernel.
- **Runlevel** A specialized script that starts a different set of services, permitting multiple configurations in the same system.
- **Kernel** The core operational code of an operating system. In Linux, it integrates the CPU architecture and supports the loading of modules and instructions to implement all operating system services (for example, process management, concurrency, and memory management).

## INTRODUCTION

The Linux+ certified professional needs to have a good understanding of the overall Linux boot process. This knowledge is required to successfully install the Linux operating system, modify boot configurations, execute different runlevels, and troubleshoot boot issues. The Linux boot process, more complex than most operating systems, is based on four stages. The four stages are powering-up your system, loading and executing GRand Unified Boot-loader (GRUB), loading and executing the Linux kernel, and loading the root. Figure 4.1 presents the four stages. For the Linux+ exam, this diagram can assist you in understanding how the Linux boot process works.

![](img/95b3ebd6248b36778ccf73988aaab2f2_104_0.png)

**FIGURE 4.1** *Linux boot process model.*

The first stage, *"powering-up your system,"* commences with the applying of electrical power to your targeted system. This normally entails pushing in the **power on/off** button. This process starts the initiation of the system BIOS. The system BIOS performs three different subtasks. The first subtask, *power-up self test* (known as POST), identifies, tests, and initializes critical system components such as the hard and floppy disk drives, random access memory (RAM), keyboard, video display card, and other hardware. The system BIOS, in addition, loads the system date and time.

**Exam Warning**

For the Linux+ exam, the Linux booting process is based on the intel x86 CPU architecture. Linux also supports the booting of other CPU hardware architectures (for example, AMD, Alpha, ARM, IA-64, m68k, MIPS, PA-RISC, PowerPC, S/390, SPARC), but the booting processes are different.

The second subtask, *boot device selection*, determines what device will be used to boot the operating system. For this subtask, system BIOS is able to select from various devices for booting (for example, floppy disk drive, hard disk drive, CD/DVD drive) the Linux operating system. The system BIOS selects the first drive and loads the disk geometry characteristics (for example, cylinders, heads, and sectors).

In the third subtask, *boot sector loading*, the system BIOS reads the first sector of the boot device. This sector is 512 bytes in size. For a hard disk drive, this special sector is known as the *master boot record* [MBR]. This sector contains the Linux bootloading program. The Linux operating system functions with various boot loaders (for example, LILO, GRUB, NTLOADER), openSUSE uses the GRUB program. The system BIOS loads GRUB into memory and executes the program. The system control is now transferred to the boot loader.

The second stage, "GRUB bootloader," performs two subtasks. For the first subtask, GRUB loads the Linux kernel (vmlinuz-version.gz). For the second subtask, GRUB creates and loads a virtual file system in system memory [RAM]. This virtual file system is called the *initial ramdisk* [initrd]. The initrd image contains various programs that are used to perform several tasks. This includes the *"init"* program and the necessary hardware drivers the Linux kernel will need to access storage drives. The init program contained in the initrd file is a bash script that loads the needed kernel modules.

The third stage uses the Linux kernel to execute the init program. The Linux kernel is an architecture designed to function dynamically. It supports the loading of modules and instructions to implement all operating system services [for example, process management, concurrency, and memory management]. The Linux kernel integrates the CPU architecture through a series of device drivers and kernel extensions. The init program will perform one of two different options, as shown in Table 4.1. The first option is the execution of a preinstalled (existing) copy of the Linux operating system. The second option is for a new installation of the Linux operating system.

**Table 4.1 Dual Roles of init Command**

| Existing Linux init Role | New Installation init Role |
| :--- | :--- |
| 1. Loading the source containing the Linux distribution installation medium for installation | 1. System drivers loading for Linux kernel |
| 2. Hardware scanning and selecting of hardware drivers | 2. Creating special system files for the kernel |
| 3. Loading the installation system or rescue system | 3. Managing redundant array of inexpensive disks (RAID) and Logical Volume Manager (LVM) setups |
| 4. Linux installation package and system configuration tool | 4. Managing network configuration |

More details about the `init` command will be provided later in the “Installing GRUB and Booting Linux” section. Regardless of which approach init takes, the init program mounts a mass storage device to obtain access to the root filesystem. Before granting access, the init program performs error checking. After the error checking process, the init program removes the virtual disk file system (initrd) from the memory.

The fourth stage, “loading the root filesystem,” is the final stage. During this stage, the Linux kernel will use the init program to load and grant access to the actual root filesystem. This entails making sure the Linux kernel has access to the necessary hardware device drivers and the execution of any specific instructions for starting the Linux operating system (known as *run-levels*). More details about runlevels will be provided later in the “Runlevels” section. To perform this task, while making sure the Linux kernel has access, the original init program will execute a new init program that resides on a mounted hard drive. This new “`init`” program will load the Linux Login screen, as shown in Figure 4.2.

The four stages provide an overview of the Linux booting process for the Linux+ certified professional. The remaining focus of the chapter is on GRUB, runlevels, and troubleshooting boot issues.
