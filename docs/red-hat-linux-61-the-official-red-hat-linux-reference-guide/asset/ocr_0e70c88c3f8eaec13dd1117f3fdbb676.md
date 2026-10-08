# Chapter. Boot Process, Init, and Shutdown

2

order of the drives searched while booting is controlled with a setting in BIOS, and it looks on the master IDE device on the primary IDE bus. The BIOS then loads whatever program is residing in the first sector of this device, called the Master Boot Record or MBR. The MBR is only 512 bytes in size and contains machine instructions for booting the machine, called a boot loader, along with the partition table. Once the BIOS finds and loads the boot loader program into memory, it yields control of the boot process to.

# 1.2.2. The Boot Loader

This section looks at boot loaders for the x86 platform. Depending on the system's architecture, the boot process may differ slightly. See Section 1.2.2.1 Boot Loaders for Other Architectures for a brief overview of non-x86 boot loaders.

Under Hat Linux two boot loaders are available: GRUB or LILO. GRUB is the default boot loader, but LILO is available for those who require or prefer it. For more information about configuring and using GRUB or LILO, see Chapter 2 Boot Loaders.

Both boot loaders for the x86 platform are broken into two stages. The first stage is a small machine code binary on the mbr. Its sole job is to locate the second stage loader and load the first part of it into memory.

GRUB is the newer boot loader and has the advantage of being read ext2 and ext3 partitions and its configuration file — /boot/grub/grub.conf — at boot time. See Section 2.7 GRUB Menu Configuration for information on how to edit this.

LILO, the second stage loader uses information on the MBR to determine the boot options available to the user. Any means that a configuration change is made or is manually upgraded, the /sbin/lilo -v command must be executed to write the appropriate information to the MBR. For details on doing this, see Section 2.8 LILO.

> Tip

If upgrading the kernel using the Red Hat Update Agent, the boot loader configuration file is updated automatically. More information on Red Hat Network can be found on the following URL: https://rhn.redhat.com.

Once the second stage loader is in memory, it presents the user with the Red Hat Linux initial graphical screen showing the different operating systems or kernels which have been configured to. On this screen you can use the arrow keys to choose which operating system or kernel they wish to boot and press [Enter]. If no key is pressed, the boot loader will load the default selection after a configurable period of time has passed.

> Note

If Symmetric Multi-Processor (SMP) kernel support is installed, there will be more than one option present the first time the system is booted. In this situation, LILO will display linux, which is the SMP kernel, and linux-up, which is for single processors. GRUB displays Red Hat Linux (<kernel-version>), and Red Hat Linux (<kernel-version>), which is for single processors.

If any problems occur using the SMP kernel, selecting a non-SMP kernel upon rebooting.

+   1. GRUB reads ext3 file systems as ext2, disregarding the journal file. The chapter titled The ext3 File System in the Red Hat Linux Customization Guide for more information on the ext3 file system.

![](bbox=[0.093, 0.53, 0.118, 0.558])