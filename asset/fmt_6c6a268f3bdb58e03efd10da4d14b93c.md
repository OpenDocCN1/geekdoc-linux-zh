
删除 Windows 分区。如果你可以删除一个足够大的 Windows 分区，就可以在其原位置安装 Linux。要删除 Windows 分区，必须在 Windows 下有多个分区，并且你愿意丢失要删除分区中的数据。在许多情况下，你可以通过将数据从要删除的分区移动到另一个 Windows 分区来保存这些数据。

一旦你确定分区中不包含有用的信息，就可以在安装 Fedora/RHEL 时将其删除。或者，你可以使用 `partimage` 将其删除（第 80 页）。删除分区后，你可以在原分区占用的空闲空间中安装 Fedora/RHEL。

## 将 FEDORA/RHEL 安装为第二个操作系统

在 Windows 系统上创建了足够的空闲空间之后（参见上一节），你可以开始安装 Fedora/RHEL。当你到达磁盘分区步骤时

screen (Figure 3-7, page 61), choose Use free space to have `Anaconda` partition the free space on the hard disk automatically. If you need to delete a Windows partition, you must choose Create custom layout; this selection calls `Disk Druid` (page 71) so you can delete the appropriate Windows partition and create Linux partitions in the free space. When you boot the system, you will be able to choose which operating system you want to run.

## THE X WINDOW SYSTEM

If you specified a graphical desktop environment such as GNOME or KDE, you installed the X.org (`x.org/wiki`) implementation of the X Window System when you installed Linux. The X Window System release `X11R7.2` comprises almost 50 software packages. The X configuration files are kept in `/etc/X11`.

### gnome-display-properties: CONFIGURES THE DISPLAY

You can use the `gnome-display-properties` (`FEDORA`) or `system-config-display` (`RHEL`) utility to display the Display Preferences window (Figure 3-27), which allows you to configure the monitor. Most users never need to run this utility. In almost all cases, Fedora/RHEL autoconfiguration sets up X.org to work properly. To run this utility, enter `gnome-display-properties` (`FEDORA`) or `gnome-config-display` (`RHEL`) on a command line or select Main menu: System➝Preferences➝Display (`Fedora`) or Main menu: System➝Administration➝Display (`RHEL`).

![](img/f28adb66a7398a382f0505e0ba74a872_124_0.png)

Figure 3-27 The Display Preferences window

Figure 3-27 shows the Display Preferences window, which allows you to specify the resolution for the monitor. Normally the system probes the monitor and fills in these values. If these values are missing, check the specifications for the monitor and select the appropriate values from the drop-down lists.

### MORE INFORMATION

*Web*

- X.org: www.x.org/wiki, www.freedesktop.org

- X.org FAQ: www.x.org/wiki/FAQ

## CHAPTER SUMMARY

Most installations of Fedora/RHEL begin by booting from the live CD or the install DVD. When the system boots from the CD/DVD, it displays a message saying when it will boot automatically. During the time it displays this message, you can give various commands and then have the system continue booting.

The program that installs Fedora/RHEL is named `Anaconda`. `Anaconda` identifies the hardware, builds the necessary filesystems, and installs or upgrades the Fedora/RHEL operating system. It can run in textual or graphical (default) interactive mode or in batch mode using Kickstart.

The `Disk Druid` graphical disk-partitioning program can add, delete, and modify partitions and logical volumes (`LVs`) on a hard disk during installation. The `partmpset` utility reports on and manipulates hard disk partitions before or after installation. The `system-config-lvm` utility works with logical volumes after installation.

A dual-boot system can boot one of two or more operating systems, frequently Windows and Linux. The biggest task in setting up a dual-boot system, assuming you want to add Linux to a Windows system, is finding enough disk space to hold Linux.

Fedora/RHEL uses the X.org X Window System version `X11R7.2`. Fedora/RHEL uses the GNOME display manager (`gdm`) to provide a graphical login.

### EXERCISES

- 1. What is a live system? What advantages does it have over an installed system?

- 2. Which boot parameter would you use to begin an FTP installation?

- 3. Describe the `Anaconda` installer.

- 4. Where on the disk should you put your `/boot` partition or the root (`/`) partition if you do not use a `/boot` partition?

- 5. If the graphical installer does not work, what three steps should you try?
