
That’s a long list of tasks! I don’t cover all of them in this chapter, but the rest of the minibook describes most of these tasks. Here, I focus on some of the basics by introducing you to some GUI tools, explaining how to become `root` (the superuser), describing the system configuration files, and showing you how to monitor system performance, manage devices, and set up periodic jobs.

## Introducing Some GUI Sysadmin Tools

Each Linux distribution comes with GUI tools for performing system administration tasks. The GUI tools prompt you for input and then run the necessary Linux commands to perform the task. In the following sections, I briefly introduce the GUI sysadmin tools in Debian, Fedora Core, SUSE, and Xandros.

### GUI sysadmin tools in Debian

Debian uses the GNOME desktop by default and provides some GUI tools for performing sysadmin tasks. These tools are available in the Applications➔System Tools menu. Table 1-1 lists some common tasks and the menu choices you use to start the GUI tool that enables you to perform that task.

| Table 1-1 | Performing Sysadmin Tasks with GUI Tools in Debian |
| :--- | :--- |
| To Do This | Choose the Following from the Debian GNOME Desktop |
| Add or remove software packages | Applications➔System Tools➔Synaptic Package Manager |
| Change date or time | Applications➔System Tools➔Time and Date |
| Change password | Main Menu➔Settings➔Change Password |
| Configure desktop | Applications➔Desktop Preferences |
| Configure network | Applications➔Networking |
| Format floppy | Applications➔System Tools➔Floppy Formatter |
| Manage printers | Applications➔System Tools➔Printers |
| Manage user accounts | Applications➔System Tools➔Users and Groups |
| Monitor system performance | Applications➔System Tools➔System Monitor |
| View system logs | Applications➔System Tools➔System Log |

### GUI sysadmin tools in Fedora Core

Fedora Core comes with a set of GUI system configuration tools that can ease the burden of performing typical sysadmin chores. Table 1-2 briefly summarizes the menu choices you use to start a GUI tool for a specific task.

**Table 1-2 Starting GUI Sysadmin Tools in Fedora Core**

| To Configure or Manage This | Start GUI Tool by Choosing This |
| :------------------------- | :----------------------------- |
| Date and time | System→Administration→ Date & Time |
| Disks and DVD/CD-ROM | Applications→ System Tools→ Disk Management |
| Display settings | System→Administration→ Display |
| Firewall settings | System→Administration→ Security Level and Firewall |
| Hardware | Applications→ System Tools→ Hardware Browser |
| Internet connection | System→Administration→ Network |
| Network | System→Administration→ Network |
| Preferences such as desktop and password | System→ Preferences |
| Printer | System→ Administration→ Printing |
| root password | System→ Administration→ Root Password |
| Servers | System→ Administration→ Server Settings |
| Software | System→ Administration→ Add/Remove Applications |
| System performance | Applications→ System Tools→ System Monitor |
| User accounts | System→ Administration→ Users and Groups |

### GUI sysadmin tools in Knoppix

Knoppix is a Live CD distribution that you can use either to try out Linux or to fix problems in an existing Linux system. As such, Knoppix comes with several GUI tools that you can use for system administration tasks. Table 1-3 summarizes some of the GUI tools in Knoppix.

**Table 1-3 Using GUI tools for Sysadmin Tasks in Knoppix**

| To Do This | Choose This from the Knoppix GUI Desktop |
| :--------- | :---------------------------------------- |
| Configure desktop | Main Menu→ Settings→ Desktop Settings Wizard |
| Configure KDE | Main Menu→ Settings→ Control Center |
| Configure network | Main Menu→ KNOPPIX→ Network/Internet→ Network card configuration |
| Configure printer | Main Menu→ KNOPPIX→ Configure→ Configure printer(s) |
| Find files | Main Menu→ Find Files |
| Manage disk partitions (for troubleshooting existing Linux installations) | Main Menu→ System→ QTParted |
| Open a terminal window with root permission | Main Menu→ KNOPPIX→ Root Shell |
| Start Samba server | Main Menu→ KNOPPIX→ Services→ Start Samba Server |
| Start SSH server | Main Menu→ KNOPPIX→ Services→ Start SSH Server |

### GUI sysadmin tools in MEPIS

You can run MEPIS as a Live CD or install it on the hard drive. MEPIS uses the KDE desktop and includes some GUI tools for sysadmin tasks. One of the unique aspects of MEPIS is the MEPIS OS Center that allows you to perform sysadmin tasks. You can start it by choosing Main Menu➔ MEPIS OS Center. Figure 1-1 shows the main window for the MEPIS OS Center from which you can install MEPIS on the hard drive (when you're running MEPIS as a Live CD) and also perform some system configuration and maintenance tasks.

![](img/792720823146d68f19fd50c99ebfce4b_402_0.png)

Besides the MEPIS OS Center, you can also use the KDE Control Center (choose Main Menu➔ Control Center) for some system administration and configuration tasks. Table 1-4 lists a few other GUI tools by specific sysadmin tasks that you can use in MEPIS.

**Table 1-4 Some GUI Tools for Sysadmin Tasks in MEPIS**

| To Do This | Choose This from the MEPIS GUI Desktop |
| :--------- | :------------------------------------- |
| Configure desktop | Main Menu➔ System➔ Settings➔ Desktop Settings Wizard |
| Configure KDE | Main Menu➔ Control Center |
| Configure printer | Main Menu➔System➔Settings➔Printing Manager |
| Find files | Main Menu➔Find Files |
| Install software | Main Menu➔System➔Synaptic Package Manager |
| Manage disk partitions (for troubleshooting existing Linux installations) | Main Menu➔System➔Filesystem➔QTparted |
| Manage user accounts | Main Menu➔System➔KUser |
| Open a terminal window with root permission | Main Menu➔System➔Terminal Program - Super User Mode |

### GUI sysadmin tools in SUSE

In SUSE, choose Main Menu➔System➔YaST to start your system administration tasks in the YaST Control Center. Figure 1-2 shows the YaST Control Center window.

![](img/792720823146d68f19fd50c99ebfce4b_403_0.png)

The left side of the YaST Control Center shows icons for the categories of tasks you can perform. The right side shows icons for specific tasks in the currently selected category. When you click an icon in the right side of the YaST Control Center, a new YaST window appears and enables you to perform that task.

Table 1-5 summarizes the tasks for each of the category icons you see in the left side of the YaST Control Center. As you can see from the entries in the second column of Table 1-5, YaST Control Center is truly one-stop shopping for all of your sysadmin chores.

**Table 1-5 Tasks by Category in the YaST Control Center**

| This Category | Enables You to Configure/Manage the Following |
| :--- | :--- |
| Software | Online Update, Installation Source, Installation in Xen Environment, Installation into Directory, Media Check, Patch CD Server, Software Management, System Update |
| Hardware | Bluetooth, CD-ROM Drives, Disk Controller, Graphics Card and Monitor, Hardware Information, IDE DMA Mode, Infrared Device, Joystick, Keyboard Layout, Mouse Model, Printer, Scanner, Sound, TV Card |
| System | /etc/sysconfig Editor, Boot Loader Configuration, Boot or Rescue Floppy, Date and Time, LVM, Language, PCI Device Drivers, Partitioner, Power Management, Powerweark, Profile Manager, System Backup, System Restoration, System Services (Run level) |
| Network Devices | DSL, Fax, ISDN, Modem, Network Card, Phone Answering Machine |
| Network Services | DHCP Server, DNS Server, DNS Host and Name, HTTP Server, Host Names, Kerberos Client, LDAP Client, Mail Transfer Agent, NFS Client, NFS Client, NIS Client, NIS Server, NTP Client, Network Services (xinetd), Proxy, Remote Administration, Routing, SLP Browser, Samba Client, Samba Server, TFTP Server |
| Security and Users | Firewall, Group Management, Local Security, User Management |
| Miscellaneous | Autoinstallation, Post a Support Query, Vendor Driver CD, View Start-up Log, View System Log |

### GUI sysadmin tools in Ubuntu

Ubuntu uses the GNOME desktop, and its menu organization is similar to that of Fedora Core’s GNOME desktop. You can find Ubuntu’s GUI system administration tools in the following menus: Applications→System Tools, System→Administration, and System→Preferences. Table 1-6 lists the menu choices for starting some of the GUI tools.
