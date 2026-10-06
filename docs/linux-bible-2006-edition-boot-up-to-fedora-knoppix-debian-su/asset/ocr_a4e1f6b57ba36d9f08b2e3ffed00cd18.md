# Chapter 8 ✦ Running Fedora Core and Red Hat Enterprise Linux 291

You can add other options to the linux boot command to identify particular hardware that is not being detected properly. For example, to specify the number of cylinders, heads, and sectors for your hard disk (if you believe the boot process is not detecting these properly), you can pass the information to the kernel as follows: linux hd=720,32,64.In this example, the kernel is told that the hard disk has 720 cylinders, 32 heads, and 64 sectors. You can find this information in the documentation that comes with your hard disk or stamped on the hard disk itself with a sticker (the serial number).

There are also other options you can add to the installation prompt to instruct the installation boot prompt to start the installation. Many of these options are described in Chapter 11.

+   7. Choose a keyboard. Some layouts enable dead keys (by default). Dead keys enable you to use special characters with special markings (such as circumflexes and umlauts).

+   8. Choose install type. Select either Install Fedora Core for a new install or Upgrading an Installation to upgrade an existing version of Fedora.

+   9. Select type for new install. Choose one of the following types (also referred as classes):

+   Personal Desktop—Installs software appropriate for a home or office personal computer or laptop computer. This includes the GNOME desktop (or KDE) and various desktop-related tools (word processors, Internet tools, and so on). Server tools, software development tools, and many system administration tools are not installed.

+   Workstation—Similar to a Personal Desktop installation adds tools for system administration and software development. No soft software is installed.

> Caution Any Linux partitions or free space on your hard disk(s) will be assigned to the new installation with the Personal Desktop or Workstation types of installation. Any Windows partitions (VFAT or FAT32 file systems) will not be touched by this. After installation, you will be able to boot Linux or Windows. If there is no free space outside your Windows partition, you must run Partition Magic, the parted utility, the FIPS program (described later), or other disk-resizing software before proceeding, or you will lose your Windows installation.

+   Server—Server installs the software packages that you would typically need for a Linux server (in particular, Web server, file server, and print server). It does not include many other servers (DHCP, DNS, FTP, SQL, or news servers). The default server install does not include a GUI (so you'd better know how to use the shell). This install type also erases all hard disks and assigns them to Linux by default.