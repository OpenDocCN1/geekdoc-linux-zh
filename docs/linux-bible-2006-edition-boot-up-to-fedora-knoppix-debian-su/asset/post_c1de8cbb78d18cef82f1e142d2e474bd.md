
The DVD that comes with this book includes the first of five OpenSUSE 10.0 CDs that you can copy and use. If you want to download the complete OpenSUSE set or a trial version of SUSE Linux, go to the OpenSUSE download page (www.opensuse.org/private/Download). In either case, you have to burn the CD image to CD yourself (See Appendix A for information on how to do that).

If you use a commercial version, select the Buy Link at the SUSE Linux site (www.novel.com/products/suselinux). You can purchase a boxed set of SUSE Linux, which includes installation support, non-open source software (such as multimedia plug-ins and Java support) and hardcopy documentation. Or you can choose one of the other editions, such as the SUSE Linux Server edition, which also include support and documentation.

The installation description in this chapter installs on Intel x86 PCs. If you have AMD 64-bit or Intel Extended Memory 64 Technology systems, you need to purchase the SUSE Linux boxed set, which includes installation media for both of types of hardware.

## Before You Begin

To install SUSE, you will need at least 96MB of memory. The entry SUSE default installation requires at least 2GB of disk space, although you can get by with less by deselecting packages during installation. Installation should work on any Pentium-class PC.

The description here tells how to install by booting the installation CD and installing the software from that medium. If you don't have a bootable CD, you can create a boot floppy from the floppy image on the CD. To see boot images and descriptions of how to boot floppies, refer to the README file in /boot directory on the SUSE installation CD.

Although you need a boot CD or floppy to begin the installation, the software you are installing can reside in other locations. In fact, I'm providing the SUSE network install CD image, so you need a network card installed on your computer and connect to the Internet to complete the installation. Then, SUSE software can be gathered from the following types of locations:

- FTP—From the installation boot, identify the location of the directory on an FTP server that contains the contents of the SUSE packages. For example, install from the /install directory from the FTP server to 10.0.0.1, type the following:
`install-ftp://10.0.0.1/install`

- HTTP—To use a Web (http) server instead of an FTP server, type the following:
`install=http://10.0.0.1/install`

- NFS—To use a NFS server instead of an FTP server, type the following:
`install=nfs://10.0.0.1/install`

Other installation media that are supported include hard disk (with the SUSE soft-installed on a different hard disk or partition on the local computer) and Samba (where the software is on an SMB share from a Windows or other Linux system).

## Starting Installation

Here are the steps for installing SUSE Linux on your hard disk, using the network install CD:

- 1. **Insert the installation CD in your CD drive.** Reboot the computer. The SUSE installation boot screen.
- 2. **Installation type. Use your arrow keys** to highlight Installation and press Enter. The Yast screen appears to begin.

> Sometimes installation can fail because the computer hardware does not support certain features, such as power management (ACPI or IPM) or DMA on hard drives or removable media. For those cases, you can try installation by selecting ACPI Disabled (which) or Safe Settings (which turns off ACPI and APM as well as turning off DMA for any IDE CD, DVD, or hard drives).

The remaining steps in the installation process are divided into three sections: Preparation, Installation Settings, and Configuration.

## Preparation

Continue with Step 3 to prepare for installation.

- 3. **Language.** Select the Language you want to use for your SUSE Linux system and click Next. The License Agreement appears.
- 4. **License.** Read the Novel Software License Agreement. If you agree, select Yes and click Next. (If you select No, it ends the install process.) You are prompted to select an install mode.
- 5. **Mode.** Here you choose whether to run a new installation or upgrade of an older version. Choosing to upgrade an existing SUSE Linux installation will take more time than a c(new) installation.

> For either a new installation or upgrade, you should back up all your data before you start.

- 6. **Clock and Time zone.** Select the time zone in which you're located. If the time is wrong, click Change, and type your new date and/or time and click Apply. Select Next to continue. You are asked to choose a Desktop.
- 7. **Desktop Selection.** Choose KDE, GNOME, or Other to set your desktop environment. KDE is most commonly used with SUSE. With Other, you can have a minimal graphical interface or completely text-based (no GUI).

## Installation Settings

The installation settings that appear you to select the Overview or Expert tab. Review the settings on these tabs. The following steps describe how you might want to change the values.

- 8. **System.** Select System to probe your computer hardware. The result is details about the type and model of each hardware item on your computer. You can save this information to your hard disk (if there is an available partition) or to a floppy disk. Click Details to see further information about any selected item. You might find this information useful if, for some reason, the hardware is not properly configured after the install is.
- 9. **Keyboard layout.** Make the language/country associated with the keyboard.
- 10. **Partitioning.** It is very important, select Partitioning. SUSE recommends a partitioning scheme. If your disk is already partitioned, SUSE tries to use that scheme. You can simply accept that scheme (choose Accept AsIs and click Next) or elect to create a custom setup.

The Expert partitioning selection enables you to use a partitioning interface that is very similar to Disk. See the description of partitioning in Chapter 7. If you plan to move your partitions with a tool like fdisk, press Ctrl+Alt+F7 to return to the graphical.
- 11. **Software.** Select Software to see a list of packages available to install on your hard disk. The default install offers the following package groups:
- Graphical Base System — X Window System, window managers, and so on.
- KDE Desktop Environment — The KDE desktop and related applications.
- Help & Support Documentation — The SUSE help system and related tools.

You can install packages that are selected by default in the OpenSUSE install process from the OpenSUSE 10.0 disk #1 that comes with this book. If you want to install additional packages, you need to get them CDs 2–5 yourself or install the packages over the network after the initial install is complete.

Choose group selection to select the specific packages in each group. Check boxes indicate which packages you want to install. It is a good idea to look through this to see what you are getting. If you change any of the selections, click the Check Dependencies box to make sure that all packages that depend on are installed. Figure 10-3 shows the Yaast module for adding, removing, and finding out software packages.

- 12. **Booting.** Selecting Booting to see the information that is added to your boot loader (GRUB, by default, but you can use the LILBO boot loader as well). The boot loader includes the information needed to boot Linux: the boot loader, default operating system to boot, and other information.
