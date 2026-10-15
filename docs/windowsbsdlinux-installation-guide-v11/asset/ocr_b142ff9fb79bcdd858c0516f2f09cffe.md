OpenBSD 3.2-RELEASE or NetBSD 1.6.1 and finally round-off by installing Red Hat Linux 7.3 (Valhalla). GNU GRUB is the boot loader used for booting these three operating systems.

# 1.3 Multi-booting Pros and Cons

An idea or thought as: "Hey! Dual and multi-booting computer systems only has advantages and absolutely no disadvantages" is wrong. Often an important question which readers do ask is: Where does it make sense to multi-boot a PC? The answer to this question is simple: Multi-booting systems only makes sense where you would like to experiment with a number of configurations (or operating systems in general) than you have computers for and more significantly where no data is at risk.

Let us consider a situation like this: Peter has a single PC at home which runs Slackware Linux. All his significant documents and downloaded files from the Internet are stored on it. He now decides to learn and practice hacking the FreeBSD Kernel. Thus, he decides to make his PC a dual-boot system. Converting one's only or in other words, the primary PC at home or at work into a dual or multi-booting system is a bad choice. If a primary home PC must be used as a dual or multi-booting system, it will be much safer to add a second hard disk and leave the first relatively untouched. A powerful boot loader like GRUB will allow booting from the other hard disk.

The Computer Science Department at my university has 15 laboratories for varying purposes that runs hardware ranging from i386s to Sun SPARCs. Where data and security is of absolute concern, computers run only one operating system whether Windows 2000 Professional, Red Hat Linux, Slackware, FreeBSD or Sun Solaris. However, we do have "test labs" of about 10–12 PCs each, where we have dual and multi-booting systems running ASP Linux, Red Hat Linux, Slackware, Windows 2000 Professional, FreeBSD and others. This can be considered as an ideal situation.

# 1.4 List of Assumptions

Though each and every step required has been explained from the very ground-up, yet a few significant assumptions have been taken into consideration while writing this guide, a few of which are as follows:

+   1. The reader possesses some theoretical and practical experience of partitioning hard disks utilizing Microsoft fdisk, BSD style partition table editor, Linux fdisk and so on.
+   2. Understands hard disk geometries, concept of a primary partition, an extended partition, logical disks within an extended partition; Linux disk naming and partitioning schemes, BSD style disk labeling and partitioning schemes.
+   3. Possesses theoretical and practical experience of compiling and configuring custom Linux and BSD Kernels.
+   4. Knowledge of basic Unix commands common to both Linux and FreeBSD/OpenBSD/NetBSD operating systems. For example, mounting filesystems, editing configuration files like the /boot/grub/grub.conf on Linux and other such trivial tasks.
+   5. The reader is using an Intel x86 computer system. I would be installing Windows, FreeBSD/OpenBSD/NetBSD and Linux operating systems on IA32 platform.