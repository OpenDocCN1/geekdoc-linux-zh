
information about your network devices and configuration. It displays information on the traffic handled by your Ethernet devices and detailed configuration information (IP, netmask, broadcast address, and so on).
In addition, it displays the current routing table. (This information shows how packets are forwarded from your computer to other networks.)

- **Display Boot Process Messages**: This area displays the boot messages from the last boot. Checking this area after installing a new kernel can tell you if your hardware was recognized properly. When your computer boots, it is very hard to follow these messages because they scroll by so quickly. This information is also available from `/var/log/messages`, but that file includes every boot plus other running information. The Boot Process area is more succinct.
- **Display Script Configuration File**: This area displays the `/etc/lst.cnf` file. This file contains information that packages use to find out information about your system. You should not edit this file by hand. It makes for interesting (or boring) reading, depending on your interests.
- **Display System Configuration File**: This area displays another configuration file, `/etc/system.cnf`, used by the system to configure itself. You should not change this file by hand.

## Software Package Administration

This area is a front end to RPM (discussed in Chapter 20, “Installing Programs and Applications”). You can use LISA to perform tasks similar to what you can do with RPM. For novice users, this could be an easier way to perform those tasks.

The Software Package Administration area subdivides into four sections:

- **Select installation source**: This allows you to select the source for the RPM packages. You can install packages using a path or a specific CD-ROM on the local hard disk or available through the Network via NFS. At the time of this writing Caldera has a public NFS server available at IP 207.179.39.2; the path is `/OpenLinux-1.3`. You can use this method to upgrade and install new packages provided you have the bandwidth. This method for installation relies on fast network access, so PPP connection via a modem is probably not fast enough for this.
- **Information about the available software packages**: This area displays a screen listing all the installed packages. Select one to see the details. This is similar to going into RPM and issuing `rpm -qi packagename`.
- **Installation of additional software packages**: You can install additional packages using this area if you provide an installation path (CD-ROM or NFS) volume. This is an installation interface to RPM.
- **Remove software packages that have already been installed**: This is a de-installation interface to RPM.

## Complete Idiot's Guide to Linux

Publisher: Macmillan Computer Publishing
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

## System Configuration

The system configuration area provides a simplified interface to configuring your system. This is much easier than mucking with configuration files directly. As usual, you should understand what you are doing, or you could make your system unbootable.

The System Configuration area subdivides into four major areas:

- Hardware Configuration Area
- System Configuration Area
- Network Configuration Area
- Boot Manager Configuration

### Hardware Configuration Area

The hardware configuration area provides other configuration screens for configuring your disks, keyboard, modem, mouse, printer, tape drives, and the X11 Server:

- **Diskette drives:** Provides options for specifying the drives you have installed.
- **Hard disks:** Provides options for configuring a disk, changing partition information, and formatting new disks.
- **Keyboard map:** Allows you to pick your keyboard locale map.
- **Modem:** Allows you to select your modem type and configuration.
- **Mouse:** Select and configure your mouse.
- **Printer:** You can easily add a printer to your system in this area. Printer drivers are provided for the more popular printers. If yours is not listed, don’t despair. Choosing a similar model from your manufacturer might do the trick. Also, check http://www.caldera.com for additional printer configuration tips and instructions.
- **CD-ROM:** Provides a list of CD-ROMs that you can use and configure with Linux.
- **Streamer:** Allows you to configure your tape backup drive.
- **X11 Server:** Allows you to select the X11 server appropriate for your video card and create a customized configuration file.

### System Configuration Area

The system configuration area provides an interface for the following:

- **User Administration:** You can add, delete, and manage users and groups, as well as set default values for users added through LISA. This interface is very serviceable for novice users. The LISA user administration area doesn’t currently take advantage of UPG schemes, which simplify user collaboration. For more information, see Chapter 18, “Users, Groups, and Passwords.”
- **Configuring the Mount Table:** This provides you with an interface to modify the `/etc/fstab` file for adding network mounts.
- **Configure the Swap Area:** This area allows you to format a partition designated as a swap partition and add it to the list of swap areas. Linux supports multiple swap partitions.
- **Set Hostname:** Provides you with an interface to assign the host name of the machine. The information you enter here is propagated at boot time through scripts. This is the preferred way to set the name and domain of your computer. Use a fully qualified domain name such as `host.domain.dom`.
- **Configure Timezone:** Allows you to configure how the hardware clock on your computer should be read. If you have a dual boot computer, more than likely your other operating system (OS) sets the clock to the local time. UNIX and UNIX-like systems typically have their clock set to GMT (Greenwich Mean Time) and then calculate your local time based on your time zone. With this control, you can tell Linux how to read your clock so that you can share it with other OSs.
- **Configure daemons/server autostart:** This screen allows you to enable and disable services that start when your computer boots. If you are not using a service, it is best to leave it off, saving your resources. You should only disable things that you know are not necessary for the proper use of your computer, or some failures will occur.
- **Kernel module administration:** This area displays information about modules available to your kernel. From here you can add and remove modules. The names of the modules displayed are cryptic, so some familiarity with the modules is helpful. You should take a look at Chapter 24, “Customizing Your Linux Kernel.” Familiarity with the kernel configuration programs might be helpful.

## Network Configuration Area

This area configures various network options, from your network card to services that you need to collaborate on a network. The basic subareas follow:

- Add a computer to the host table
- Configure network access
- Configure General Network Services

### Host Table Configuration

This option allows you to view and manipulate the /etc/hosts file via an interface. It has commands to

- Display the current /etc/hosts file
- Add a new entry to the /etc/hosts file
- Delete an entry from the /etc/hosts file

The /etc/hosts file keeps track of computers on your network so that users can reference them by name instead of by their IP address. If your network is large, you will not use /etc/hosts; you will use a Domain Name System (DNS) system to provide the name-to-IP and IP-to-name translations. Without a translation service like that provided by the /etc/hosts file or DNS, you will need to know the IP address of every machine with which you want to communicate.

If you have a small network (a tiny area network, or TAN) for several PCs at home, you can use /etc/hosts to provide the name translation that your
