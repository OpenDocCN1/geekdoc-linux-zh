
Makefile.bak.

3. Then, I open the Makefile using vi or any text editor. You may change the EXTRAVERSION value to anything of your choice. For example, on my system, the initial Linux Kernel was 2.4.18-3. Since then I built numerous others as 2.4.18-3ghosh, 2.4.18-3smp, 2.4.18-3_dummy, 2.4.18-3bsd and so on. Thus, the EXTRAVERSION code helps to distinguish between a large number of available Linux Kernels on a system.

4. Once done, I save and exit the Makefile. Then, execute: make mrproper. It cleans the compilation folders of any junk that was created while compiling Linux kernels on the same system earlier. Readers must note that all the commands executed (including this one) should be executed from within the /usr/src/linux-2.4 directory.

5. I then execute: make menuconfig. Readers may also use xconfig concerned they have access to X11 or the X Window system.

6. Once inside menuconfig, tinker with the options available. Make sure you enter the "File systems" section, then select the "UFS file system support (read-only)" and "UFS file system write support (DANGEROUS)" options. Thus, you should have something like this: <*> UFS file system support (read-only) and [*] UFS file system write support (DANGEROUS). The config Kernel-level options are as: CONFIG_UFS_FS and CONFIG_UFS_FS_WRITE for the read-only and write support respectively. Also, enter the "Partition types" section and select the [*] BSD disklabel (FreeBSD partition tables) option i.e. the CONFIG_BSD_DISKLABEL option. This allows you to access and read the FreeBSD disk labels in the FreeBSD slices.

7. With these three options enabled, I save the configuration file and exit. Now execute: make dep && clean.

8. Then execute: make bzImage && modules for creating the zipped (compressed) Linux kernel image file and the corresponding modules.

9. Then execute: make modules_install for installing the newly created modules into their own corresponding directories.

10. After this, I copy the bzImage file to the /boot directory. If required, you can also create an initial RAM-disk file image using the mkinitrd command.

11. Once this done, I open the /boot/grub/grub.conf file using the vi editor and make a corresponding entry into it. Save and exit. Reboot to check whether the new Kernel is properly working or not. I am sure it would!

Once the newly built custom Linux kernel is installed, you can start using it to mount UFS filesystems. Use this command: mount -t ufs /dev/hda2 /mnt/bsd; concerned /dev/hda2 is the FreeBSD slice and /mnt/bsd exists. Unmount using the command: umount /mnt/bsd simply.

For mounting Windows 95/98/ME FAT32 filesystems on Linux, use the command: mount -t vfat /dev/hda1 /mnt/windows. The /mnt/windows directory must exist on the system. Unmount by executing: umount /mnt/windows simply. For readers who are using the NTFS filesystem, there's bad news! They have to include the NTFS filesystem support in the configuration file and build a custom Linux kernel. Readers must note: NTFS writing support is DANGEROUS and limited.

## 4. Troubleshooting

Though FreeBSD, OpenBSD and GNU/Linux operating systems are very fine pieces of software, yet when dual or multi-booting PCs with all (or combinations) of them, one can often run into problems. It may range from easy ones to detect and troubleshoot to really weird ones. Troubleshooting, as known (and appreciated) by all UNIX-veterans is not an exact art. In this Chapter, I have listed some problems that I have had (and continue facing) while dual and multi-booting systems with varying operating systems and hardware.

Readers must note that depending on the particular hardware and distributions/releases used, they may experience slightly different versions of the problems listed below. If you encounter a new problem altogether or can contribute to this Guide by providing a better solution to one of the problems listed below, make sure you drop me a line at: subhasish_ghosh@linuxwaves.com.

My personal experience with multi-booting systems saw some weird kinds of failure and often erratic behavior, but mostly from Linux's fdisk and installation procedure. I often made notes of them for diagnosing and troubleshooting later. As I can conclude, amongst Linux distributions (which includes Red Hat, Slackware, SuSE and Mandrake), OpenBSD and FreeBSD releases, FreeBSD's fdisk, disklabel and overall installation procedure (/stand/sysinstall) is the best of them all with absolutely no errors and abrupt crashes. Initially, I always thought that there must be some exact way of installing all these operating systems or an exact order that needs to be followed, but with passing years, I have learnt the truth: Concerned the hardware support is fine, installation CD-ROMs okay, the erratic behavior of installation programs is due to unerased data from previous installs. So before committing yourself to creating a multi-booting system, make sure you start installation on a freshly formatted hard disk. Read on to follow the details of the procedure! Some of the common questions from readers include:

### Q1. I created an extended partition with logical disk drives or sub partitions within it. But when I installed FreeBSD, it completely ignored the inner partitions within that partition. Is that normal?

Ans1: Yes, it is absolutely normal. FreeBSD operating system software can only detect and represent primary hard disk partitions which it calls "slices". An extended partition, though would be represented in FreeBSD fdisk will not represent the constituents of the container.

### Q2. I installed FreeBSD and OpenBSD operating systems on my PC successfully. When I tried installing Red Hat Linux, Linux's fdisk displayed a "too many partitions" error message. What does it mean? What can I do now?

### Q3. I deleted earlier installs of FreeBSD, OpenBSD and/or NetBSD operating systems on my PC. When I tried installing Red Hat Linux, Linux's fdisk displayed a "too many partitions" error message. What am I supposed to do now?
