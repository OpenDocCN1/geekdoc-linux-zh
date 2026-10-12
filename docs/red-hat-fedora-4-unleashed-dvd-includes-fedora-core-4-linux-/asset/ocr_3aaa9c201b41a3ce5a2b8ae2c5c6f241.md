To log in at the text-based prompt, type your username and press Enter. You will then be prompted for your password. After you press Enter, you will be at the Linux command line. If you use a graphical login, you can use the shutdown or reboot menus in the screen's dialog to shut down or reboot your system. To immediately shut down your system from the command line of a text-based session, use the su command and its -c option to run the halt command, like this:

```
$ su - c halt
```

You can also use the reboot command to restart your computer like this:

```
$ su - c reboot
```

For new users, installing Fedora is just the beginning of a new and highly rewarding journey on the path to learning Linux. See Chapter 5 for additional information about using Linux commands. For Fedora system administrators, the task ahead is to fine-tune the installation and to customize the server or user environment.

# Related Fedora and Linux Commands

You might use the following commands while installing Fedora:

+   - dd—Convert and copy data
+   - fdisk—The Linux disk partitioning utility
+   - grub—The GNU boot loader for Linux and other operating systems
+   - LOADLIN—A Linux boot loader for DOS
+   - mkbootdisk—Red Hat's Linux boot disk creation utility
+   - RAWRITE—A disk image utility for DOS

# Reference

http://fedora.redhat.com—The place to start when looking for news, information, and documentation about installing, configuring, and using Fedora.

http://www.powerquest.com/partitionmagic/—Powerquest's PartitionMagic utility includes BootMagic, which can be used to support booting of Linux or, regrettably, other less-capable operating systems, such as Windows XP.

http://www.v-com.com/product/System_Commander_Home.html—V Communications, Inc.'s System Commander, a commercial 4.2MB download that can be used to support booting of any operating system capable of running on today's PCs. An intelligent partitioning utility, Partition Commander, is included.

http://www.nwc.com/columnists/1101colon.html—How to use Intel's Pre-execution Environment (PXE) protocol to remote boot workstations.

http://www.gnu.org/software/grub/—Home page for the GRUB boot loader.