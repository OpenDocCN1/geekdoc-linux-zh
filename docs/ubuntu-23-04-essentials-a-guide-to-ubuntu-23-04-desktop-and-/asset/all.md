![](image/ubuntu_23.04_front_cover_large_pubdrive.png)

Ubuntu 23.04 Essentials

Ubuntu 23.04 Essentials

© 2023 Neil Smyth / Payload Media, Inc. All Rights Reserved.

This book is provided for personal use only. Unauthorized use, reproduction and/or distribution strictly prohibited. All rights reserved.

The content of this book is provided for informational purposes only. Neither the publisher nor the author offers any warranties or representation, express or implied, with regard to the accuracy of information contained in this book, nor do they accept any liability for any loss or damage arising from any errors or omissions.

This book contains trademarked terms that are used solely for editorial purposes and to the benefit of the respective trademark owner. The terms used within this book are not intended as infringement of any trademarks.

Rev: 1.0

1. Introduction

Ubuntu is arguably one of the most highly regarded and widely used Linux distributions available today. Praised both for its ease of use and reliability, Ubuntu also has a loyal following of Linux users and an active community of developers.

Ubuntu 23.04 Essentials is intended to provide detailed information on the installation, use, and administration of the Ubuntu distribution. For beginners, the book covers topics such as operating system installation, the basics of the GNOME desktop environment, configuring email and web servers, and installing packages and system updates. Additional installation topics, such as dual booting with Microsoft Windows, are also covered, together with all important security topics, such as configuring a firewall and user and group administration.

For the experienced user, topics such as remote desktop access, the Cockpit web interface, logical volume management (LVM), disk partitioning, swap management, KVM virtualization, Secure Shell (SSH), Linux Containers, and file sharing using both Samba and NFS are covered in detail to provide a thorough overview of this enterprise class operating system.

1.1 Superuser Conventions

Ubuntu, in common with Linux in general, has two types of user accounts, one being a standard user account with restricted access to many of the administrative files and features of the operating system and the other a superuser (root) account with elevated privileges. Typically, a user can gain root access either by logging in as the root user or using the su - command and entering the root password. In the following example, a user is gaining root access via the su - command:

[demo@demo-server ~]$ su -

Password:

[demo@demo-server ~]#

Note that the command prompt for a regular user ends with a $ sign while the root user has a # character. When working with the command line, this is a useful indication of whether you are currently issuing commands as the root user.

If the su - command fails, the root account on the system has most likely been disabled for security reasons. In this case, the sudo command can be used instead, as outlined below.

Using sudo, a single command requiring root privileges may be executed by a non-root user. Consider the following attempt to update the operating system with the latest patches and packages:

$ apt update

Reading package lists... Done

E: Could not open lock file /var/lib/apt/lists/lock - open (13: Permission denied)

Optionally, user accounts may be configured so that they have access to root-level privileges. Instead of using the su - command to first gain root access, user accounts with administrative privileges are able to run otherwise restricted commands using sudo:

$ sudo apt update

[sudo] password for demo:

Hit:1 http://us.archive.ubuntu.com/ubuntu bionic InRelease

.

.

To perform multiple commands without repeatedly using the sudo command, a command prompt with persistent super-user privileges may be accessed as follows:

[demo@demo-server]$ sudo su -

[demo@demo-server]#

The reason for raising this issue so early in the book is that many of the command-line examples outlined in this book will require root privileges. Rather than repetitively preface every command-line example with directions to run the command as root, the command prompt at the start of the line will be used to indicate whether or not the command needs to be performed as root. If the command can be run as a regular user, the command will be prefixed with a $ command prompt as follows:

$ date

If, on the other hand, the command requires root privileges, the command will be preceded by a # command prompt:

# apt install openssh-server

1.2 Opening a Terminal Window

If you are using the GNOME desktop and need to access a command prompt, you will need to open a Terminal window. This can be achieved by right-clicking on the desktop background and selecting the Open in Terminal menu option as shown in [Figure 1-1](#Introduction.xhtml__idTextAnchor008):

![](image/ubuntu_open_in_terminal.jpg)

Figure 1-1

A terminal window may also be opened within the GNOME desktop using the Ctrl-Alt-T keyboard accelerator.

1.3 Editing Files

Configuring a Linux system typically involves editing files. For those new to Linux, it can be unclear which editor to use. If you are running a terminal session and do not already have a preferred editor, we recommend using the nano editor. To launch nano in a terminal window, enter the following command:

# nano <file>

Where <file> is replaced by the path to the file you wish to edit. For example:

# nano /etc/passwd

Once loaded, nano will appear as illustrated in [Figure 1-2](#Introduction.xhtml__idTextAnchor010):

![](image/ubuntu_18.04_nano.jpg)

Figure 1-2

To create a new file run nano as follows:

# nano

When you have finished editing the file, type Ctrl-S to save the file, followed by Ctrl-X to exit. To open an existing file, use the Ctrl-R keyboard shortcut.

If you prefer to use a graphical editor within the GNOME desktop environment, gedit is a useful starting point for basic editing tasks. To launch gedit from the desktop press Alt-F2 to display the Enter a Command window as shown in [Figure 1-3](#Introduction.xhtml__idTextAnchor011):

![](image/ubuntu_run_command.jpg)

Figure 1-3

Enter gedit into the text field and press the Enter key. After a short delay, gedit will load ready to open, create, and edit files:

![](image/ubuntu_gedit.jpg)

Figure 1-4

Alternatively, launch gedit from a terminal window either with or without the path to the file to open:

# gedit

# gedit /etc/passwd

1.4 Feedback

We want you to be satisfied with your purchase of this book. If you find any errors in the book or have any comments, questions, or concerns, please contact us at [feedback@ebookfrenzy.com](mailto:feedback%40ebookfrenzy.com?subject=).

1.5 Errata

While we make every effort to ensure the accuracy of the content of this book, it is inevitable that a book covering a subject area of this size and complexity may include some errors and oversights. Any known issues with the book will be outlined, together with solutions, at the following URL:

[https://www.ebookfrenzy.com/errata/Ubuntu2304.html](https://www.ebookfrenzy.com/errata/ubuntu2304.html)

In the event that you find an error not listed in the errata, please let us know by emailing our support team at [feedback@ebookfrenzy.com](mailto:feedback%40ebookfrenzy.com?subject=).

2. A Brief History of Ubuntu Linux

Ubuntu Linux is one of a number of variants (also referred to as distributions) of the Linux operating system and is the product of a U.K. company named Canonical Ltd. The company was founded in 1994 by Mark Shuttleworth. The origins of Linux, however, go back even further. This chapter will outline the history of both the Linux operating system and Ubuntu.

2.1 What exactly is Linux?

Linux is an operating system in much the same way that Windows is an operating system (and there any similarities between Linux and Windows end). The term operating system is used to describe the software that acts as a layer between the hardware in a computer and the applications that we all run on a daily basis. When programmers write applications, they interface with the operating system to perform such tasks as writing files to the hard disk drive and displaying information on the screen. Without an operating system, every programmer would have to write code to access the hardware of the system directly. In addition, the programmer would have to be able to support every single piece of hardware ever created to be sure the application would work on every possible hardware configuration. Because the operating system handles all of this hardware complexity, application development becomes a much easier task. Linux is just one of a number of different operating systems available today.

2.2 UNIX Origins

To understand the history of Linux, we first have to go back to AT&T Bell Laboratories in the late 1960s. During this time, AT&T had discontinued involvement in developing a new operating system named Multics. However, two AT&T engineers, Ken Thompson, and Dennis Ritchie, decided to take what they had learned from the Multics project and create a new operating system named UNIX which quickly gained popularity and wide adoption both with corporations and academic institutions.

A variety of proprietary UNIX implementations eventually came to market, including those created by IBM (AIX), Hewlett-Packard (HP-UX), and Sun Microsystems (SunOS and Solaris). In addition, a UNIX-like operating system named MINIX was created by Andrew S. Tanenbaum and designed for educational use with source code access provided to universities.

2.3 Who Created Linux?

The origins of Linux can be traced back to the work and philosophies of two people. At the heart of the Linux operating system is something called the kernel. This is the core set of features necessary for the operating system to function. The kernel manages the system’s resources and handles communication between the hardware and the applications. The Linux kernel was developed by Linus Torvalds, who, taking a dislike to MS-DOS and impatient for the availability of MINIX for the new Intel 80386 microprocessor, decided to write his own UNIX-like kernel. When he had finished the first version of the kernel, he released it under an open-source license that enabled anyone to download the source code and freely use and modify it without having to pay Linus any money.

Around the same time, Richard Stallman at the Free Software Foundation, a strong advocate of free and open-source software, was working on an open-source operating system of his own. Rather than focusing initially on the kernel, however, Stallman began by developing open-source versions of all the UNIX tools, utilities, and compilers necessary to use and maintain an operating system. By the time he had finished developing this infrastructure, the obvious solution was to combine his work with the kernel Linus had written to create a complete operating system. This combination became known as GNU/Linux. Purists insist that Linux always be referred to as GNU/Linux (in fact, at one time, Richard Stallman refused to give press interviews to any publication which failed to refer to Linux as GNU/Linux). This is not unreasonable, given that the GNU tools developed by the Free Software Foundation make up a significant and vital part of GNU/Linux. Unfortunately, most people and publications refer to Linux as Linux, which will probably always continue to be the case.

2.4 The History of Ubuntu

As mentioned previously, Ubuntu is one of a number of Linux distributions. The source code that makes up the Ubuntu distribution originates from a highly regarded Linux distribution known as Debian, created by Ian Murdoch.

A South African internet mogul named Mark Shuttleworth (who made his fortune selling his company to VeriSign for around $500 million) decided it was time for a more user-friendly Linux. He took the Debian distribution and worked to make it a more human-friendly distribution which he called Ubuntu. He subsequently formed a company called Canonical Ltd to promote and provide support for Ubuntu.

If you are new to Linux or already use Linux and want to try a different Linux distribution, it is unlikely you will find a better option than Ubuntu.

2.5 What does the word “Ubuntu” Mean?

The word “Ubuntu” is an ancient Zulu and Xhosa word that means “humanity to others”. Ubuntu also means “I am what I am because of who we all are”. It was chosen because these sentiments precisely describe the spirit of the Ubuntu distribution.

2.6 Summary

The origins of the Linux operating system can be traced back to the work of Linus Torvalds and Richard Stallman in the form of the Linux kernel combined with the tools and compilers built by the GNU project.

Over the years, the open-source nature of Linux has resulted in the release of a wide range of different Linux distributions. One such distribution is Ubuntu, based on the Debian Linux distribution created by Canonical Ltd, a company founded by Mark Shuttleworth

3\. Installing Ubuntu on a Clean Disk Drive

There are now three ways in which an Ubuntu system can be deployed. One method is to either purchase new hardware or re-purpose an existing computer system on which to install and run the operating system. Alternatively, a virtualization platform such as VirtualBox or VMware can be used to install and run Ubuntu inside a virtual machine on an existing operating system. Another option is to create a cloud-based operating system instance using services such as Amazon AWS, Google Cloud, or Microsoft Azure (to name but a few). Since cloud-based instances are typically created by selecting a pre-configured, ready to run operating system image that is already optimized for the cloud platform and using that as the basis for the Ubuntu system, there is no need to perform a manual operating system installation in this situation.

If, on the other hand, you plan to install Ubuntu on your own hardware or make use of a virtualization environment, the first step on the path to learning about Ubuntu involves installing the operating system.

Ubuntu can be installed either in a clean disk environment (where an entire disk is cleared of any existing partitions and dedicated entirely to Ubuntu) or in a dual boot environment where Ubuntu co-exists with another operating system on the disk (typically a member of the Microsoft Windows family of operating systems).

In this chapter, we will cover the clean disk approach to installation from local or remote installation media. Dual boot installation with a Windows 10 system will be covered in [”Dual Booting Ubuntu with Windows”](#Ubuntu_Installation_Dual_Boot.xhtml__idTextAnchor060).

3.1 Ubuntu Installation Options

Ubuntu can be downloaded free of charge from the following web page:

[https://ubuntu.com/download](https://ubuntu.com/download)

This page provides a number of download options depending on how the operating system is to be installed and used:

•Ubuntu Desktop - Downloads the installation media for the desktop edition of the operating system. This edition is intended for use on desktop and laptop systems where a graphical desktop environment is needed and is only available for 64-bit x86 systems. The desktop edition can be downloaded in the form of an ISO image which you can then write to a USB drive using the steps outlined later in this chapter. When booted, the desktop media will allow you to test out Ubuntu by running a Live Ubuntu session prior to performing the installation.

•Ubuntu Server - Downloads the Live Server ISO installation media for the server edition of the operating system. This image is intended for performing an installation on servers on which the graphical desktop environment is not required and is available for x86, ARM, IBM POWER (PowerPC), and s390x (IBM System z mainframe) systems. The installation media does not include the option to try Ubuntu before installing and uses the text-based installer instead of the graphical installer used for Ubuntu Desktop. This allows Ubuntu to be installed on systems without a graphical console.

The Ubuntu Server image may also be used to perform Preboot Execution Environment (PXE) network installations. When using PXE to install Ubuntu, the Ubuntu image is installed on a specially configured server (referred to as a PXE boot server). The client system on which Ubuntu is to be installed is then configured to boot over the network from the image on the PXE boot server (assuming the client hardware supports PXE) to initiate the installation.

3.2 Server vs. Desktop Editions

Clearly, a decision between the Desktop and the Server Edition images needs to be made before installation can begin. If you would like to try Ubuntu before installing it, then the Desktop option is the best solution since it allows you to boot Ubuntu from the installation media without first installing it on a disk drive. This option also allows the installation to be initiated from within the live session.

If the graphical desktop environment is not required, and the destination system does not have internet access or a graphical console, then the Live Server ISO image is recommended since this allows a fully functional server to be built without the need to download any additional packages.

Regardless of the chosen installation method, packages can be added to and removed from the system after installation to configure the system to specific needs.

3.3 Obtaining the Ubuntu Installation Media

For the purposes of this chapter, the Ubuntu Desktop environment will be installed using the graphical installer. Begin, therefore, by downloading the Ubuntu Desktop 23.04 ISO image from the following URL:

[https://ubuntu.com/download/desktop](https://ubuntu.com/download/desktop)

The DVD ISO image is self-contained, including all of the packages necessary to install an Ubuntu system, and is named using the following convention:

ubuntu-<version>-<edition>-<architecture>.iso

For example, the Ubuntu 23.04 Desktop ISO image for 64-bit Intel/AMD systems is named as follows:

ubuntu-23.04-desktop-amd64.iso

Having downloaded the image, either burn it to disk or use the steps in the next section to write the media to a USB drive and configure your virtualization environment to treat it as a DVD drive.

3.4 Writing the ISO Installation Image to a USB Drive

These days it is more likely that an operating system installation will be performed from a USB drive than from a DVD. Having downloaded the ISO installation image for Ubuntu, the steps to write that image to a USB drive will differ depending on whether the drive is attached to a Linux, macOS, or Windows system. The steps outlined in the remainder of this section assume that the USB drive is new or has been reformatted to remove any existing data or partitions:

3.4.1 Linux

The first step in writing an ISO image to a USB drive on Linux is identifying the device name. Before inserting the USB drive, identify the storage devices already detected on the system by listing the devices in /dev as follows:

# ls /dev/sd*

/dev/sda /dev/sda1 /dev/sda2

Attach the USB drive to the Linux system and run the dmesg command to get a list of recent system messages, one of which will be a report that the USB drive was detected and will be similar to the following:

[445597.988045] sd 6:0:0:0: [sdb] Attached SCSI removable disk

This output tells us that we should expect the device name to include “sdb” which we can confirm by listing device names in /dev again:

# ls /dev/sd*

/dev/sda /dev/sda1 /dev/sda2 /dev/sdb

From this output, we can tell that the USB drive has been assigned to /dev/sdb. The next step before writing the ISO image to the device is to run the findmnt command to make sure it has not been auto-mounted:

# findmnt /dev/sdb?

TARGET SOURCE FSTYPE OPTIONS

/media/demo/C24E-6727 /dev/sdb1 vfat rw,nosuid,nodev, ...

If the findmnt command indicates that the USB drive has been mounted, unmount it before continuing:

# umount /media/demo/C24E-6727

Once the filesystem has been unmounted, use the dd command as follows to write the ISO image to the drive:

# dd if=/path/to/iso/<image name>.iso of=/dev/sdb bs=512k

The writing process can take some time (as long as 10 - 15 minutes) to complete depending on the image size and speed of the system on which it is running. Once the image has been written, output similar to the following will appear and the USB drive is ready to be used to install Ubuntu:

4056+1 records in

4056+1 records out

2126544896 bytes (2.1 GB, 2.0 GiB) copied, 625.911 s, 3.4 MB/s

3.4.2 macOS

The first step in writing an ISO image to a USB drive attached to a macOS system is to identify the device using the diskutil tool. Before attaching the USB device, open a Terminal window and run the following command:

$ diskutil list

/dev/disk0 (internal, physical):

   #: TYPE NAME SIZE IDENTIFIER

   0: GUID_partition_scheme *1.0 TB disk0

   1: EFI EFI 209.7 MB disk0s1

   2: Apple_APFS Container disk2 1000.0 GB disk0s2

/dev/disk1 (internal):

   #: TYPE NAME SIZE IDENTIFIER

   0: GUID_partition_scheme 28.0 GB disk1

   1: EFI EFI 314.6 MB disk1s1

   2: Apple_APFS Container disk2 27.7 GB disk1s2

/dev/disk2 (synthesized):

   #: TYPE NAME SIZE IDENTIFIER

   0: APFS Container Scheme - +1.0 TB disk2

                                 Physical Stores disk1s2, disk0s2

   1: APFS Volume Macintosh HD 473.6 GB disk2s1

   2: APFS Volume Preboot 42.1 MB disk2s2

   3: APFS Volume Recovery 517.0 MB disk2s3

   4: APFS Volume VM 1.1 GB disk2s4

Having established a baseline of detected devices, insert the USB drive into a port on the macOS system and run the command again. The same results should appear with one additional entry for the USB drive resembling the following:

/dev/disk3 (external, physical):

   #: TYPE NAME SIZE IDENTIFIER

   0: *16.0 GB disk3

In the above example, the USB drive has been assigned to /dev/disk3\. Before proceeding, unmount the disk as follows:

$ diskutil unmountDisk /dev/disk3

Unmount of all volumes on disk3 was successful

Finally, use the dd command to write the ISO image to the device, taking care to reference the raw disk device (/dev/rdisk3) and entering your user password when prompted:

$ sudo dd if=/path/to/iso/image.iso of=/dev/rdisk3 bs=1m

Once the image has been written, the USB drive is ready.

3.4.3 Windows/macOS

Several free tools are available for Windows and macOS that will write an ISO image to a USB drive, but one written specifically for writing Linux ISO images is the Fedora Media Writer tool which can be downloaded from the following URL:

https://getfedora.org/en/workstation/download/

Once installed, insert the destination USB drive, launch the writer tool, and choose the Select .iso file option as highlighted in [Figure 3-1](#Ubuntu_Installation_Clean_Disk.xhtml__idTextAnchor045):

![](image/fedora_media_writer.jpg)

Figure 3-1

Click Next to proceed to the Write Options screen and select the USB Drive before clicking on the Select... button:

![](image/ubuntu_write_to_usb.jpg)

Figure 3-2

In the resulting file selection dialog, navigate to and select the Ubuntu installation ISO image and click the Open button. Finally, click the Write button to start writing the image to the USB drive:

![](image/ubuntu_usb_writing.jpg)

Figure 3-3

Once the image has been written, the device is ready to perform the installation.

3.5 Booting from the Ubuntu USB Image

Insert the Ubuntu installation media into the appropriate drive and power on the system. If the system tries to boot from the hard disk drive, you will need to enter the BIOS set up for your computer and change the boot order so that it boots from the installation media drive first. After the initial boot sequence completes, the GRUB menu shown in [Figure 3-4](#Ubuntu_Installation_Clean_Disk.xhtml__idTextAnchor048) will appear:

![](image/ubuntu_grub_screen.jpg)

Figure 3-4

Use the arrow keys to select the Try or Install Ubuntu menu option, then press Enter to boot into an Ubuntu Live session. After Ubuntu has booted completely, the window shown in [Figure 3-5](#Ubuntu_Installation_Clean_Disk.xhtml__idTextAnchor049) below will appear:

![](image/ubuntu_install_choose_language.jpg)

Figure 3-5

Select your preferred language followed by the Next button. On the next screen, options are provided to either try the Ubuntu Live session or to begin the installation process:

![](image/ubuntu_install_or_try.jpg)

3.6 Installing Ubuntu

Select the Install Ubuntu option, then click the Next button to proceed to the Keyboard layout screen:

![](image/ubuntu_install_keyboard.jpg)

Figure 3-6

Either select your keyboard layout or, if you are unsure, click on the Detect button to work through some steps to identify your keyboard before clicking on Next to select the network connection to use during the installation:

![](image/ubuntu_install_network.jpg)

Figure 3-7

On the next screen, choose whether to perform the Normal or Minimal installation:

![](image/ubuntu_install_type.jpg)

Figure 3-8

Select the Normal option if you have plenty of disk space and want to explore the main applications and utilities included with Ubuntu without having to manually install them later. Alternatively, to avoid cluttering the system with software you may never need, select the Minimal option. Regardless of the choice made here, all of the software provided with Ubuntu can be easily installed or removed at any point in the future if needed.

The option is also available to update the software packages that comprise the Ubuntu distribution during the installation. Ubuntu, as with most actively supported operating systems, continues to be updated with bug fixes and security patches long after it has been released to the public. If this option is selected and the system is connected to the internet, the installer will download any updates issued since the Ubuntu installation image was released and applies them to the system during installation. If you choose not to perform this update during the installation process, these updates may still be applied at any time after the installation completes.

A second option provides the choice of whether to install 3rd party non-open source software to support specific hardware devices and the playback of proprietary media files on the system. Some users object fervently to using any software which is not published under a public license. If you are one of those people, then do not select this option. If, on the other hand, you just want the best experience from your Ubuntu installation, then this option is recommended.

Having made appropriate selections, click the Next button to proceed to the disk allocation screen:

![](image/ubuntu_install_disk.jpg)

Figure 3-9

Assuming that this is a new disk on which an existing operating system is not present, the installer will provide the option to erase the entire disk and use it for Ubuntu (in which case the installer will calculate and implement a typical and recommended partition layout). Alternatively, to define your own custom disk layout, select the Manual partitioning option to manually create and size the disk partitions that will contain the operating system and your data.

Clicking on the Advanced Features... button will provide the option to use Logical Volume Management (LVM). LVM is strongly recommended to make the management of the disks and partitions on the system easier, a topic covered in detail in the chapter entitled [“Adding a New Disk to an Ubuntu 23.04 Volume Group and Logical Volume”](#Volume_Groups.xhtml__idTextAnchor506):

![](image/ubuntu_install_disk_lvm.jpg)

Figure 3-10

If the security of the data stored on the disk is of paramount concern, select the option to encrypt the Ubuntu installation. If this option is selected, the next screen will prompt you to choose a security key which will then need to be entered each time the system starts.

For this example, select the option to use LVM and click on OK.

Once the selections have been made, click the Next button to review the disk partitioning information:

![](image/ubuntu_install_disk_info.jpg)

Figure 3-11

Click the Install button to start the installation. While the installation is in progress, the installer will ask for information about your geographical location to configure time zone settings:

![](image/ubuntu_install_timezone.jpg)

Figure 3-12

Next, the installer will ask you to provide a username and password for the first account on the system:

![](image/ubuntu_install_username.jpg)

Figure 3-13

The option is also provided to dictate whether the password must be specified each time the user wishes to log into the system. By default, each time Ubuntu starts, a login screen will be presented seeking username and password credentials. If you are the sole user of the system and would like to bypass this screen and be logged in automatically each time the system boots, be sure to turn off the Require my password to log in switch before proceeding.

Once all the questions have been answered, the installer will simply proceed with the installation. Depending on the speed of your system, and whether or not you opted to download updates during the installation, this process can take some time. For a more detailed view of the steps being performed by the installer, click on the button highlighted in [Figure 3-14](#Ubuntu_Installation_Clean_Disk.xhtml__idTextAnchor051):

![](image/ubuntu_installing.jpg)

Figure 3-14

When the installation is complete, a dialog will update to inform you the system is ready to be restarted:

![](image/ubuntu_install_restart.jpg)

Figure 3-15

When you are ready to reboot, press the Restart now button. The installer may prompt you to remove the installation media, and the system will take a few moments to shut down. At this point, remove the USB flash drive and press the Enter key to proceed.

3.7 Accessing the Ubuntu Desktop

Once the system has started, if the password requirement option was enabled the GNOME Display Manager (GDM) login screen ([Figure 3-16](#Ubuntu_Installation_Clean_Disk.xhtml__idTextAnchor053)) will appear. To access the system, select the user name and enter the password specified during installation:

![](image/ubuntu_login_screen.jpg)

Figure 3-16

Alternatively, if the installation was configured to log directly into the desktop, the GNOME desktop ([Figure 3-17](#Ubuntu_Installation_Clean_Disk.xhtml__idTextAnchor054)) will appear after the system has restarted:

![](image/ubuntu_23.04_desktop.jpg)

Figure 3-17

3.8 Installing Updates

As with most operating systems today, each particular release of the Ubuntu distribution continues to evolve after it has been released. This generally takes the form of bug fixes and security updates and, occasionally, new features that may be downloaded over the internet and installed on your system.

Best practices dictate that the first step after installing Ubuntu is to ensure any available updates are applied to the system. When updates are available, the Software Updater will display the following dialog from which updates may be installed:

![](image/ubuntu_software_updater.jpg)

Figure 3-18

Updates can also be installed via the command-line prompt in a Terminal window using the apt package manager tool. To check for the availability of updates, right-click on the desktop background and, from the resulting menu, select the Open in Terminal option:

![](image/ubuntu_desktop_menu.jpg)

Figure 3-19

Within the Terminal window, run the following commands to gain root privileges and update the package list:

$ sudo su -

# apt update

If updated packages are available, the command will display output similar to the following:

.

.

.

Reading package lists... Done

Building dependency tree

Reading state information... Done

220 packages can be upgraded. Run 'apt list --upgradable' to see them.

Any pending updates may be applied using the apt tool:

# apt upgrade

Upon execution, the apt tool will provide a list of packages that are available for update and prompt for permission to perform the update:

220 upgraded, 7 newly installed, 0 to remove and 0 not upgraded.

Need to get 75.2 MB/286 MB of archives.

After this operation, 34.8 MB of additional disk space will be used.

Do you want to continue? [Y/n]

Once the upgrade is complete, the installation is essentially finished.

3.9 Displaying Boot Messages

During the boot process, the system will display the Ubuntu splash screen, which hides from view all of the boot messages generated by the system as it loads. To make these messages visible during the boot process (as shown in [Figure 3-20](#Ubuntu_Installation_Clean_Disk.xhtml__idTextAnchor058)), simply press the keyboard Esc key while the system is starting:

![](image/ubuntu_boot_messages.jpg)

Figure 3-20

The default behavior can be changed so that messages are always displayed by default by editing the /etc/default/grub file and changing the GRUB_CMDLINE_LINUX setting which, by default, will resemble the following:

GRUB_CMDLINE_LINUX="... rhgb quiet"

If you are new to Linux and are not familiar with the editors available, refer to the editor recommendations outlined in the [“Introduction”](#Introduction.xhtml__idTextAnchor000) chapter. For example, to use the nano editor, enter the following command to start the editor and load the grub file:

# nano /etc/default/grub

To remove the graphical boot screen so that messages are visible without pressing the Esc key, remove the “splash” and “quiet” options from the setting:

GRUB_CMDLINE_LINUX=""

This change will cause the system to display all of the boot messages generated by the system.

Once the changes have been made, run the following command to generate a new boot configuration to take effect the next time the system starts:

# grub-mkconfig --output=/boot/grub/grub.cfg

3.10 Summary

The first step in working with Ubuntu is to install the operating system. In the case of a cloud-based server, this task is typically performed automatically when an operating system image is selected for the system based on a range of options offered by the cloud service provider. Installation on your own hardware or in a virtual machine, however, involves downloading the installation media in the form of an ISO image, writing that image to suitable storage such as a DVD or USB drive and booting from it. Once installation is complete, it is important to install any operating system updates that may have been released since the original installation image was created.

4\. Dual Booting Ubuntu with Windows

Ubuntu, just like most Linux distributions, will happily co-exist on a hard disk drive with just about any version of Windows. This is a concept known as dual-booting. Essentially, when you power up your PC, you will be presented with a menu providing the option to boot either Ubuntu or Windows. Obviously, you can only run one operating system at a time, but it is worth noting that the files on the Windows partition of your disk drive will be available to you from Ubuntu regardless of whether your Windows partition was formatted using NTFS, FAT16 or FAT32\.

During the installation process, the Ubuntu installer will detect the Windows installation on the drive and provide the option of deleting it and using the entire disk for Ubuntu, or sharing the disk with Windows. In the latter case, you will be able to specify the percentage of the disk to be used for Ubuntu.

According to the Ubuntu documentation, a minimum of 25 GB of disk space is required for a full Ubuntu Desktop Edition installation, and more space to store any files you may subsequently create. Once the disk space for Ubuntu has been selected, the installer will resize the Windows partition (without destroying any data) and use the remainder of the disk for Ubuntu.

This chapter will demonstrate how to set up a dual boot system with Ubuntu and Windows 10, change the system that boots by default when the computer system is powered on, and outline how to access files located on the Windows partition of the disk from within Ubuntu.

Within this chapter, the assumption is made that the steps outlined in the previous chapter have been followed to create a bootable Ubuntu installation USB drive using the Ubuntu Desktop installation image and that the system has been configured to boot from the USB drive when started.

4.1 Beginning the Ubuntu Installation

Insert the Ubuntu installation media into the appropriate drive and power on the system. If the system starts Windows, you will need to enter the BIOS set up for your computer and change the boot order so that it boots from the installation media drive first. After the initial boot sequence completes, the GRUB menu shown in [Figure 4-1](#Ubuntu_Installation_Dual_Boot.xhtml__idTextAnchor062) will appear:

![](image/ubuntu_grub_screen.jpg)

Figure 4-1

Use the arrow keys to select the Try or Install Ubuntu menu option, then press Enter to boot into an Ubuntu Live session. After Ubuntu has booted completely, the window shown in [Figure 4-2](#Ubuntu_Installation_Dual_Boot.xhtml__idTextAnchor063) below will appear:

![](image/ubuntu_install_choose_language.jpg)

Figure 4-2

Select your preferred language followed by the Next button. On the next screen, options are provided to either try the Ubuntu Live session or to begin the installation process:

![](image/ubuntu_install_or_try.jpg)

Figure 4-3

4.2 Installing Ubuntu

Select the Install Ubuntu option, then click the Next button to proceed to the Keyboard layout screen:

![](image/ubuntu_install_keyboard.jpg)

Figure 4-4

Either select your keyboard layout or, if you are unsure, click on the Detect button to work through some steps to identify your keyboard before clicking on Next to select the network connection to use during the installation:

![](image/ubuntu_install_network.jpg)

Figure 4-5

On the next screen, choose whether to perform the Normal or Minimal installation:

![](image/ubuntu_install_type1.jpg)

Figure 4-6

Select the Normal option if you have plenty of disk space and want to explore the main applications and utilities included with Ubuntu without having to manually install them later. Alternatively, to avoid cluttering the system with software you may never need, select the Minimal option. Regardless of the choice made here, all of the software provided with Ubuntu can be easily installed or removed at any point in the future if needed.

The option is also available to update the software packages that comprise the Ubuntu distribution during the installation. Ubuntu, as with most actively supported operating systems, continues to be updated with bug fixes and security patches long after it has been released to the public. If this option is selected and the system is connected to the internet, the installer will download any updates issued since the Ubuntu installation image was released and applies them to the system during installation. If you choose not to perform this update during the installation process, these updates may still be applied at any time after the installation completes.

A second option provides the choice of whether to install 3rd party non-open source software to support specific hardware devices and the playback of proprietary media files on the system. Some users object fervently to using any software which is not published under a public license. If you are one of those people, then do not select this option. If, on the other hand, you just want the best experience from your Ubuntu installation, then this option is recommended.

Having made appropriate selections, click the Next button to proceed to the disk allocation screen:

![](image/ubuntu_install_with_windows.jpg)

Figure 4-7

Given that it is our intention to configure a dual boot system, the option to Install Ubuntu alongside Windows Boot Manager is the desired choice. With this option selected, click the Continue button to proceed. The subsequent screen allows the amount of disk space allocated to each operating system (in this case, Windows and Ubuntu) to be configured:

![](image/ubuntu_windows_disk_divide.jpg)

Figure 4-8

At this point, you must decide how much of your Windows partition you wish to donate to the Ubuntu installation. Move the slider (positioned between the Windows and Ubuntu partitions in the diagram) until the Ubuntu partition allocation is a size you are comfortable with. At least 25GB of space should be made available for a full Ubuntu Desktop installation.

Once the selections have been made, click the Next button to review the disk partitioning information:

![](image/ubuntu_windows_install.jpg)

Figure 4-9

Click the Install button to start the installation. While the installation is in progress, the installer will ask for information about your geographical location to configure time zone settings:

![](image/ubuntu_install_timezone.jpg)

Figure 4-10

Next, the installer will ask you to provide a username and password for the first account on the system:

![](image/ubuntu_install_username.jpg)

Figure 4-11

The option is also provided to dictate whether the password must be specified each time the user wishes to log into the system. By default, each time Ubuntu starts, a login screen will be presented seeking username and password credentials. If you are the sole user of the system and would like to bypass this screen and be logged in automatically each time the system boots, be sure to turn off the Require my password to log in switch before proceeding.

Once all the questions have been answered, the installer will simply proceed with the installation. Depending on the speed of your system, and whether or not you opted to download updates during the installation, this process can take some time. For a more detailed view of the steps being performed by the installer, click on the button highlighted in [Figure 4-12](#Ubuntu_Installation_Dual_Boot.xhtml__idTextAnchor065):

![](image/ubuntu_installing.jpg)

Figure 4-12

When the installation is complete, a dialog will update to inform you the system is ready to be restarted:

![](image/ubuntu_install_restart.jpg)

Figure 4-13

When you are ready to reboot, press the Restart now button. The installer may prompt you to remove the installation media, and the system will take a few moments to shut down. At this point, remove the USB flash drive and press the Enter key to proceed.

When you are ready to reboot, press the Restart Now button. The installer may prompt you to remove the installation media, and the system will take a few moments to shut down. At this point, remove the USB flash drive and press the Enter key to proceed.

4.3 Booting Ubuntu for the First Time

When the system reboots, a screen similar to the one illustrated below will appear, providing the option to boot either Windows or Ubuntu:

![](image/ubuntu_dual_boot_grub_menu.jpg)

Figure 4-14

Press Enter to boot Ubuntu. If you wish to boot Windows, use the keyboard arrow keys to select the Windows Boot Manager option. If you choose to boot Ubuntu, the operating system will load, and the Ubuntu login screen will appear (unless the automatic login option was selected). Enter the user name and password you set up during the installation process, and you will be logged into the Ubuntu Desktop environment.

4.4 Changing the Default Boot Option

When the system starts, the boot options screen will appear, and wait 10 seconds for the user to make an operating system choice. If no selection has been made before the timeout elapses, the default operating system will be started. On a newly configured system, the default operating system will be the standard Ubuntu image. This default can, however, be changed from within Ubuntu.

A range of boot configuration options (including the 10-second timeout and the boot settings outlined in [“Installing Ubuntu on a Clean Disk Drive”](#Ubuntu_Installation_Clean_Disk.xhtml__idTextAnchor037)) are declared in the /etc/default/grub file, which reads as follows on a new installation:

GRUB_DEFAULT=0

GRUB_TIMEOUT_STYLE=hidden

GRUB_TIMEOUT=10

GRUB_DISTRIBUTOR=`lsb_release -i -s 2> /dev/null || echo Debian`

GRUB_CMDLINE_LINUX_DEFAULT=”quiet splash”

GRUB_CMDLINE_LINUX=""

The first step in changing the default boot system is to declare the GRUB_SAVEDEFAULT setting within this file and to change the GRUB_DEFAULT setting to saved:

GRUB_DEFAULT=saved

GRUB_SAVEDEFAULT=true

GRUB_TIMEOUT_STYLE=hidden

GRUB_TIMEOUT=10

.

.

This setting allows a new default value to be saved within the boot configuration. Next, run the grub-set-default command to change the default setting using a numbering system that counts the first option as 0. For example, if the Windows 10 option is position 5 in the menu, the command to make Windows 10 the default boot option would read as follows:

# grub-set-default 4

Check that the new setting has taken effect by running the following command:

# grub-editenv list

saved_entry=4

Note that the saved_entry value is now set to 4. After changing the default, regenerate the boot configuration file as follows:

# grub-mkconfig --output=/boot/grub/grub.cfg

Reboot the system and verify that the boot menu defaults to the Windows 10 option and that Windows loads after the timeout expires.

4.5 Accessing the Windows Partition from the Command-line

When running Ubuntu in a dual boot configuration, it is still possible to access files located on the Windows partition. This can be achieved by manually mounting the partition from the command-line or from the desktop using the Disks (gnome-disks) graphical utility.

When working from the command line, the first step in this process is to create a directory to use as the mount point for our Windows partition. In this example, we will create a directory named /mnt/windows:

# mkdir /mnt/windows

In order to identify the device name that has been assigned to the Windows partition, use the fdisk command as follows:

# fdisk -l

.

.

Disk /dev/nvme0n1: 64 GiB, 68719476736 bytes, 134217728 sectors

Disk model: VMware Virtual NVMe Disk

Units: sectors of 1 * 512 = 512 bytes

Sector size (logical/physical): 512 bytes / 512 bytes

I/O size (minimum/optimal): 512 bytes / 512 bytes

Disklabel type: gpt

Disk identifier: F0D04B58-29F5-4B6B-B10F-07295BEF9AAC

Device Start End Sectors Size Type

/dev/nvme0n1p1 2048 206847 204800 100M EFI System

/dev/nvme0n1p2 206848 239615 32768 16M Microsoft reserved

/dev/nvme0n1p3 239616 80184560 79944945 38.1G Microsoft basic data

/dev/nvme0n1p4 132833280 134213631 1380352 674M Windows recovery environment

/dev/nvme0n1p5 80185344 132833279 52647936 25.1G Linux filesystem

.

.

In the above output, the main Windows partition containing the files we need access to is represented by /dev/nvme0n1p3. Next, we need to run the mount command (assuming the Windows partition is /dev/nvme0n1p3) as follows:

# mount /dev/nvme0n1p3 /mnt/windows 

Check that the mount was successful by listing the contents of the top-level directory of the mount point:

# ls /mnt/windows

'$Recycle.Bin' pagefile.sys swapfile.sys

'$WinREAgent' PerfLogs 'System Volume Information'

'Documents and Settings' ProgramData Users

 DumpStack.log 'Program Files' Windows

 DumpStack.log.tmp 'Program Files (x86)'

 OneDriveTemp Recovery

To automate the mount each time the system is booted, simply add the appropriate mount line to the /etc/fstab file:

/dev/nvme0n1p3 /mnt/windows ntfs defaults 0 0

To unmount the Windows file system at any time:

# umount /mnt/windows

4.6 Accessing the Windows Partition from the Desktop

The first step in mounting a partition using the desktop environment is to launch the disks utility. With the desktop loaded, right-click on the desktop background and select Open Terminal from the resulting menu. Within the terminal window, gain root privileges before launching the Disks utility as follows:

$ gnome-disks

Once the disks tool has launched, a window similar to that shown in [Figure 4-15](#Ubuntu_Installation_Dual_Boot.xhtml__idTextAnchor071) will appear:

![](image/ubuntu_gnome_disks_main.jpg)

Figure 4-15

To view information about a partition, select it from the graphical representation in the Volumes section of the dialog. In the above example, the Windows system partition is selected and highlighted. To mount the partition so that the contents can be accessed from within Ubuntu, select the partition and click on the options button indicated in [Figure 4-16](#Ubuntu_Installation_Dual_Boot.xhtml__idTextAnchor072) to display the menu:

![](image/ubuntu_gnome_disks_menu.jpg)

Figure 4-16

From the menu, select Edit Mount Options... to display the dialog shown in [Figure 4-17](#Ubuntu_Installation_Dual_Boot.xhtml__idTextAnchor073). Turn off the User Session Defaults switch and make sure that Show in user interface option is enabled. Within the Mount Point text field, change the path to /mnt/windows. If the partition needs to be automatically mounted each time the system reboots, also enable the Mount at system startup option:

![](image/ubuntu_gnome_disks_mount_options.jpg)

Figure 4-17

With the changes made, click on the OK button to return to the main dialog. To mount the partition, simply click on the mount button highlighted in [Figure 4-18](#Ubuntu_Installation_Dual_Boot.xhtml__idTextAnchor074) below:

![](image/ubuntu_gnome_disks_mount_button.jpg)

Figure 4-18

Once the partition is mounted, exit from gnome-disks and note that an icon for the volume has appeared in the dock as shown in [Figure 4-19](#Ubuntu_Installation_Dual_Boot.xhtml__idTextAnchor075) (note that if the Show in user interface option has been disabled, this icon would not be present):

![](image/ubuntu_windows_partition_in_dock.jpg)

Figure 4-19

Double-click on the icon to browse the partition using the Files tool:

![](image/ubuntu_windows_in_files.jpg)

Figure 4-20

To unmount the partition, click on the mount button (which will have changed to a stop button), as shown in [Figure 4-18](#Ubuntu_Installation_Dual_Boot.xhtml__idTextAnchor074) above.

4.7 Summary

Ubuntu can safely co-exist on the same disk drive as a Windows operating system by creating a dual boot environment. This involves shrinking the amount of space occupied by the Windows system to make room for Ubuntu during the installation. Once Ubuntu has been installed, the boot menu configuration can be modified to change the default operating system. The Windows partition on the disk drive may be accessed from Ubuntu either via the command line or using the Disks desktop utility.

5\. Allocating Windows Disk Partitions to Ubuntu

In the previous chapter, we looked at installing Ubuntu on the same disk as Windows. This so-called “dual boot” configuration allows the user to have both operating systems installed on a single disk drive with the option to boot one or the other when the system is powered on.

This chapter is intended for users who have decided they like Ubuntu enough to delete Windows entirely from the disk and use the resulting space for Linux. In the following sections, we will work through this process step by step using both the command-line tools and the gnome-disks utility.

5.1 Unmounting the Windows Partition

If the steps in the [“Dual Booting Ubuntu with Windows”](#Ubuntu_Installation_Dual_Boot.xhtml__idTextAnchor060) chapter were followed to mount the Windows partition from within Ubuntu, steps should be taken to unmount the partition before continuing with this chapter. Assuming that the Windows partition was mounted as /mnt/windows, it can be unmounted as follows:

# umount /mnt/windows

The /etc/fstab file should also be edited to remove the /mnt/windows auto-mount if it was previously added.

5.2 Deleting the Windows Partitions from the Disk

The first step in freeing up the Windows partition for use by Ubuntu is to delete that partition. Before doing so, however, any data you need to keep must be backed up from both the Windows and partitions. Having done that, it is safe to proceed with this chapter.

To remove the Windows partitions, we first need to identify the disk on which they reside using the fdisk tool:

# fdisk -l

Disk /dev/nvme0n1: 64 GiB, 68719476736 bytes, 134217728 sectors

Disk model: VMware Virtual NVMe Disk

Units: sectors of 1 * 512 = 512 bytes

Sector size (logical/physical): 512 bytes / 512 bytes

I/O size (minimum/optimal): 512 bytes / 512 bytes

Disklabel type: gpt

Disk identifier: F0D04B58-29F5-4B6B-B10F-07295BEF9AAC

Device Start End Sectors Size Type

/dev/nvme0n1p1 2048 206847 204800 100M EFI System

/dev/nvme0n1p2 206848 239615 32768 16M Microsoft reserved

/dev/nvme0n1p3 239616 80184560 79944945 38.1G Microsoft basic data

/dev/nvme0n1p4 132833280 134213631 1380352 674M Windows recovery environment

/dev/nvme0n1p5 80185344 132833279 52647936 25.1G Linux filesystem

In the above example output, the system contains one physical disk drive referenced by device name /dev/nvme0n1. On that disk drive are six partitions accessed via the device names /dev/nvme0n1p1 through /dev/nvme0n1p5, respectively. Based on the values in the Types column, three Windows-related partitions exist. The first is the Windows system partition, while the second, much larger, partition is the Windows boot partition containing the Windows operating system and user data, followed by the Windows recovery partition.

To remove the partitions, start the fdisk tool using the device name of the disk containing the partition (/dev/nvme0n1 in this instance) and follow the instructions to display the partition and sector information once again:

# fdisk /dev/nvme0n1

Welcome to fdisk (util-linux 2.37.2).

Changes will remain in memory only, until you decide to write them.

Be careful before using the write command.

Command (m for help): p

 Disk /dev/nvme0n1: 64 GiB, 68719476736 bytes, 134217728 sectors

Disk model: VMware Virtual NVMe Disk

Units: sectors of 1 * 512 = 512 bytes

Sector size (logical/physical): 512 bytes / 512 bytes

I/O size (minimum/optimal): 512 bytes / 512 bytes

Disklabel type: gpt

Disk identifier: F0D04B58-29F5-4B6B-B10F-07295BEF9AAC

Device Start End Sectors Size Type

/dev/nvme0n1p1 2048 206847 204800 100M EFI System

/dev/nvme0n1p2 206848 239615 32768 16M Microsoft reserved

/dev/nvme0n1p3 239616 80184560 79944945 38.1G Microsoft basic data

/dev/nvme0n1p4 132833280 134213631 1380352 674M Windows recovery environment

/dev/nvme0n1p5 80185344 132833279 52647936 25.1G Linux filesystem

Partition table entries are not in disk order.

Command (m for help):

Before proceeding, note the start and end addresses of the partitions we will delete (in other words, the start of /dev/nvme0n1p2 and the sector before the start of /dev/nvme0n1p5).

At the command prompt, delete the Windows partitions (these being partitions 2, 3, and 4 on our example system):

Command (m for help): d

Partition number (1-5, default 5): 2

Partition 2 has been deleted.

Command (m for help): d

Partition number (1,3-5, default 5): 3

Partition 3 has been deleted.

Command (m for help): d

Partition number (1,4,5, default 5): 4

Partition 4 has been deleted.

Now that we have deleted the Windows partitions, we must create the new Ubuntu partition in the vacated disk space. The partition number must match the number of the first partition removed (in this case, 2). It will also be necessary to enter the Start and End sectors of the partition precisely as reported for the old partition (fdisk will typically offer the correct values by default, though it is wise to double-check):

Command (m for help): n

Partition number (2-4,6-128, default 2): 2

First sector (206848-134217694, default 206848):

Last sector, +/-sectors or +/-size{K,M,G,T,P} (206848-80185343, default 80185343):

Created a new partition 2 of type 'Linux filesystem' and of size 38.1 GiB.

Having made these changes, the next step is to check that the settings are correct:

Command (m for help): p

Disk /dev/nvme0n1: 64 GiB, 68719476736 bytes, 134217728 sectors

Disk model: VMware Virtual NVMe Disk

Units: sectors of 1 * 512 = 512 bytes

Sector size (logical/physical): 512 bytes / 512 bytes

I/O size (minimum/optimal): 512 bytes / 512 bytes

Disklabel type: gpt

Disk identifier: F0D04B58-29F5-4B6B-B10F-07295BEF9AAC

Device Start End Sectors Size Type

/dev/nvme0n1p1 2048 206847 204800 100M EFI System

/dev/nvme0n1p2 206848 80185343 79978496 38.1G Linux filesystem

/dev/nvme0n1p5 80185344 132833279 52647936 25.1G Linux filesystem

To commit the changes, we now need to write the new partition information to disk and quit from the fdisk tool:

Command (m for help): w

The partition table has been altered.

Syncing disks.

5.3 Formatting the Unallocated Disk Partition

To make the new partition suitable for use by Ubuntu, it needs to have a file system created on it. The recommended file system type for the current release of Ubuntu is XFS which will be covered in greater detail in the chapter entitled [“Adding a New Disk Drive to an Ubuntu 23.04 System”](#Adding_New_DIsk.xhtml__idTextAnchor494). Creation of the file system is performed using the mkfs.xfs command as follows (installing the xfsprogs package if necessary):

# apt install xfsprogs

# mkfs.xfs -f /dev/nvme0n1p2

meta-data=/dev/nvme0n1p2 isize=512 agcount=4, agsize=2499328 blks

         = sectsz=512 attr=2, projid32bit=1

         = crc=1 finobt=1, sparse=1, rmapbt=0

         = reflink=1 bigtime=0 inobtcount=0

data = bsize=4096 blocks=9997312, imaxpct=25

         = sunit=0 swidth=0 blks

naming =version 2 bsize=4096 ascii-ci=0, ftype=1

log =internal log bsize=4096 blocks=4881, version=2

         = sectsz=512 sunit=0 blks, lazy-count=1

realtime =none extsz=4096 blocks=0, rtextents=0

5.4 Mounting the New Partition

Next, we need to mount the new partition. In this example, we will mount it in a directory named /data. You are free, however, to mount the new partition using any valid mount point you desire or to use it as part of a logical volume (details of which are covered in the chapter entitled [“Adding a New Disk to an Ubuntu 23.04 Volume Group and Logical Volume”](#Volume_Groups.xhtml__idTextAnchor506)). First, we need to create the directory to act as the mount point:

# mkdir /data

Secondly, we need to edit the mount table in /etc/fstab so that the partition is automatically mounted each time the system starts. At the bottom of the /etc/fstab file, add the following line to mount the new partition (modifying the /dev/nvme0n1p2 device to match your environment):

/dev/nvme0n1p2 /data xfs defaults 0 0

Finally, we can manually mount the new partition (note that this will not be necessary on subsequent reboots as the partition will automount due to the setting we added to the /etc/fstab file above):

# mount /data

To check the partition, run the following command to display the available space:

# df -h /data

Filesystem Size Used Avail Use% Mounted on

/dev/nvme0n1p2 39G 305M 38G 1% /data

5.5 Editing the Boot Menu

The next step is to modify the Ubuntu boot menu. Since this was originally a dual boot system, the menu is configured to provide the option of booting either Windows or Ubuntu. Now that the Windows partition is gone, we need to remove this boot option. On Ubuntu this can be achieved using the following steps:

# rm -r /boot/efi/EFI/Microsoft

# update-grub

Since there is now only one operating system to boot, the system will automatically boot Ubuntu on the next restart without displaying the boot menu. If you need to access this boot menu, for example to use the advanced boot options, simply press the Esc key during the initial stages of the startup process.

5.6 Using GNOME Disks Utility

The gnome-disks utility provides a user-friendly graphical alternative to reclaiming the Windows partitions from the command-line. Since the example used here will convert the Windows NTFS partitions to XFS format, the first step is to install the xfsprogs package as follows:

# apt install xfsprogs

Once the package has been installed, open a terminal window and launch the gnome-disks utility:

# gnome-disks

After a short delay, the gnome-disks tool will appear as shown in [Figure 5-1](#Reclaim_Windows_Partition.xhtml__idTextAnchor089):

![](image/ubuntu_gnome_disks_windows_mounted.jpg)

Figure 5-1

In the above example, the disk contains two Windows NTFS partitions that will need to be deleted. Any NTFS partitions with a star shown in the disk map (as is the case for the highlighted partition in the above figure) will need to be unmounted before they can be deleted. This can be achieved by selecting the partition and clicking on the unmount button as indicated in [Figure 5-2](#Reclaim_Windows_Partition.xhtml__idTextAnchor090) below:

![](image/ubuntu_gnome_disks_unmount_button.jpg)

Figure 5-2

With all the NTFS partitions unmounted, the next step is to delete them. Select the left-most NTFS partition in the disk map and click on the Delete button as shown in [Figure 5-3](#Reclaim_Windows_Partition.xhtml__idTextAnchor091):

![](image/ubuntu_gnome_disks_delete_partition.jpg)

Figure 5-3

Review the information in the confirmation dialog before clicking on the Delete button to commit the change. Once the first partition has been deleted, repeat this step for any remaining NTFS partitions. Once the NTFS partitions have been removed, the space should now be shown as being free within the disk map. A new partition now needs to be created to make use of this free space. With the space selected, click on the new partition button (indicated by the arrow in [Figure 5-4](#Reclaim_Windows_Partition.xhtml__idTextAnchor092)):

![](image/ubuntu_gnome_new_partition_button.jpg)

Figure 5-4

In the Create Partition dialog, choose whether the partition is to occupy all of the available space, or reduce the size if you plan to use the space for more than one partition:

![](image/ubuntu_gnome_disks_new_partition.jpg)

Figure 5-5

Click Next and, on the subsequent screen, enter a name for the new partition and choose whether the partition should be erased during creation. This causes the creation process to take more time but is a recommended option. Finally, choose a filesystem type for the partition. This will typically be either ext4 or XFS. Given the benefits of XFS, select Other before clicking the Next button.

![](image/ubuntu_gnome_disks_format.jpg)

Figure 5-6

On the next screen, select the XFS option before clicking on the Create button:

![](image/ubuntu_gnome_disks_xfs.jpg)

Figure 5-7

The gnome-disks utility will begin the formatting process and display the status of the process:

![](image/ubuntu_gnome_disks_progress.jpg)

Figure 5-8

Once the partition is ready, it can be mounted either from the command-line or using the gnome-disks utility. To configure a mount point, select the partition and click on the settings button as shown in [Figure 5-9](#Reclaim_Windows_Partition.xhtml__idTextAnchor093):

![](image/ubuntu_gnome_disks_Settings_button.jpg)

Figure 5-9

From the settings menu, select the Edit Mount Options... item to display the dialog shown in [Figure 5-10](#Reclaim_Windows_Partition.xhtml__idTextAnchor094).

![](image/ubuntu_gnome_disks_mount_options1.jpg)

Figure 5-10

Turn off the User Session Defaults switch and configure the mount point to your requirements. In the above figure, the partition is mounted at /mnt/Data at system startup and is configured to be identified by the label “Data”.

Once the settings are complete, click on OK, then click the mount button highlighted in [Figure 5-11](#Reclaim_Windows_Partition.xhtml__idTextAnchor095):

![](image/ubuntu_gnome_disks_mount_button1.jpg)

Figure 5-11

To check the partition is now mounted and ready for use, run the following command to display the available space:

$ df -h /mnt/Data

Filesystem Size Used Avail Use% Mounted on

/dev/sda3 253G 1.8G 251G 1% /mnt/Data

Finally, update the boot menu to remove the Windows option using the steps outlined earlier in this chapter.

5.7 Summary

The Windows partitions in a dual boot configuration can be removed anytime to free up space for a Ubuntu system by identifying which partitions belong to Windows and then deleting them. Once deleted, the unallocated space can be used to create a new filesystem and mounted to make it available to the Ubuntu system.

6\. A Guided Tour of the GNOME 44 Desktop

Ubuntu 23.04 includes the GNOME 44 desktop environment. Although lacking the complexity of Windows and macOS desktops, GNOME provides an uncluttered and intuitive desktop environment that includes all of the essential features of a windowing environment with the added advantage that it can be learned quickly.

In this chapter, the main features of the GNOME desktop will be covered together with an outline of how basic tasks are performed.

6.1 Installing the GNOME Desktop

If the Ubuntu Desktop image was used for the Ubuntu 23.04 installation process, the GNOME desktop will already be installed and will automatically launch each time the system starts.

If an Ubuntu server configuration was installed, the GNOME desktop will not have been included in the packages installed on the system. On server-based systems without a display attached, the idea of installing a graphical desktop environment may seem redundant. It is worth noting, however, that remote access to the GNOME desktop is also possible so, even on so called headless servers (i.e. servers lacking a monitor, keyboard, and mouse), it may still be beneficial to install the GNOME desktop packages. The topic of establishing remote desktop access will be covered in detail in the [“Ubuntu 23.04 Remote Desktop Access with Vino”](#Ubuntu_Remote_Desktop_Access.xhtml__idTextAnchor295)  chapter of this book.

If the installation configuration did not include the GNOME desktop, it may be installed at any time using the following command:

# apt install ubuntu-gnome-desktop

Once the installation is complete, the desktop login screen will appear the next time the system restarts.

6.2 An Overview of the GNOME 44 Desktop

The screen shown in [Figure 6-1](#Ubuntu_GNOME_Desktop.xhtml__idTextAnchor102) below shows the appearance of a typical, newly launched GNOME desktop session before any other programs have been launched or configuration changes made.

The main desktop area (marked A) is where windows will appear when applications and utilities are launched.

The bar at the top of the screen (B) is called the top bar and includes the Activities menu (C), the day and time and a collection of buttons and icons, including network status, audio volume, battery power, and other status and account settings:

![](image/ubuntu_23.04_gnome_desktop.jpg)

Figure 6-1

The application menu for the currently active application running on the desktop will also appear in the top bar. [Figure 6-2](#Ubuntu_GNOME_Desktop.xhtml__idTextAnchor103), for example, shows the application menu for the Terminal app:

![](image/ubuntu_gnome_terminal_menu.jpg)

Figure 6-2

Depending on the app, a menu containing additional options may be available in the app’s window bar. [Figure 6-3](#Ubuntu_GNOME_Desktop.xhtml__idTextAnchor104), for example, shows the built-in menu for the Terminal app:

![](image/ubuntu_gnome_terminal_menu2.jpg)

Figure 6-3

Another menu is available by right-clicking on the app icon in the dock, as shown in [Figure 6-4](#Ubuntu_GNOME_Desktop.xhtml__idTextAnchor105):

![](image/ubuntu_gnome_terminal_menu3.jpg)

Figure 6-4

6.3 Launching Activities

Applications and utilities are launched using the dock, shown in [Figure 6-5](#Ubuntu_GNOME_Desktop.xhtml__idTextAnchor107) below:

![](image/ubuntu_gnome_dock.jpg)

Figure 6-5

By default, the dock will display an icon for a predefined set of commonly used applications and will also include an icon for any applications that are currently running. If the application is currently running, it will appear with a dot marker to the left of the icon and if multiple copies are running, a dot will appear for each instance.

To launch an application, simply click on the icon in the dock.

To find an application not included on the dock, one option is to select Show Applications (marked A in [Figure 6-5](#Ubuntu_GNOME_Desktop.xhtml__idTextAnchor107) above) to display a browsable list of applications as shown in [Figure 6-6](#Ubuntu_GNOME_Desktop.xhtml__idTextAnchor108):

![](image/ubuntu_gnome_show_apps.jpg)

Figure 6-6

Note that the list can be filtered to display all applications or only those used frequently by selecting the buttons at the bottom center of the screen. It is also important to be aware that some entries in the list are actually folders holding additional applications. In the above screenshot, for example, the Utilities entry provides access to a collection of other tools, such as the system monitor and disk management tools and the Terminal window application.

An alternative to browsing the applications is to perform a search using the search bar, which appears when the dashboard by clicking Activities in the top bar, as shown in [Figure 6-7](#Ubuntu_GNOME_Desktop.xhtml__idTextAnchor109):

![](image/ubuntu_gnome_app_search.jpg)

Figure 6-7

As text is typed into the search box, the list of possible matches will be refined.

To add an application to the dock for more convenient access, locate the icon for the application, right-click on it, and select the Add to Favorites menu option:

![](image/ubuntu_gnome_add_to_favorites.jpg)

Figure 6-8

To remove an app from the dock, right-click on the icon in the dash and select Remove from Favorites.

6.4 Managing Windows

As with other desktop environments, applications run on GNOME in windows. When multiple application windows are open, the Super + Tab keyboard shortcut will display the switcher panel ([Figure 6-9](#Ubuntu_GNOME_Desktop.xhtml__idTextAnchor111)), allowing a different window to be chosen as the currently active window (the Super key is either the Windows key or, in the case of a Mac keyboard, the Cmd key):

![](image/ubuntu_gnome_switcher.jpg)

Figure 6-9

If a single application has more than one window open, the switcher will display those windows in a second panel so that a specific window can be selected:

![](image/ubuntu_gnome_desktop_switcher_windows.jpg)

Figure 6-10

To cycle backward through the icons in the switcher, use the Shift + Tab keyboard shortcut.

To maximize a window to fill the entire screen, click the title bar and drag the window to the top of the screen. To return the window to its original size, click on the title bar and drag it downwards. Alternatively, simply double-click on the title bar to toggle between window sizes. Similarly, dragging a window to the left or right side of the screen will cause the window to fill that half of the screen.

6.5 Using Workspaces

The area of the screen where the application windows appear is referred to as the workspace, and GNOME allows multiple workspaces to be configured. To view the current workspaces, click Activities in the top bar (marked C in [Figure 6-1](#Ubuntu_GNOME_Desktop.xhtml__idTextAnchor102) above) or press the keyboard Super key to display the following screen:

![](image/ubuntu_gnome_workspaces.jpg)

Figure 6-11

The area marked A in the above figure is the currently selected workspace. Clicking in the areas marked B and C will select and display the previous and next workspaces, respectively. The center workspace panel (A) displays the currently active applications windows. Hovering the mouse pointer of a window will display a close button that can be used to exit the window. To move a window from one workspace to another, display the workspaces panel and drag and drop the application window onto the destination workspace. When a window is added to a blank workspace, another blank workspace is added to the workspace panel, allowing multiple workspaces to be created.

The workspace thumbnails (D) provide a convenient way to switch between workspaces and are particularly helpful when working with many workspaces.

To remove a workspace, either close all the windows on that workspace, or move them to another workspace.

The Show Applications screen also provides access to the current workspaces, as illustrated in [Figure 6-12](#Ubuntu_GNOME_Desktop.xhtml__idTextAnchor115) below:

![](image/ubuntu_show_apps_workspaces.jpg)

Figure 6-12

6.6 Calendar and Notifications

When the system needs to notify you of an event (such as the availability of system or application updates), a popup panel will appear at the top of the workspace. Access to the calendar and any previous notifications is available by clicking on the day and time in the top bar, as shown in [Figure 6-13](#Ubuntu_GNOME_Desktop.xhtml__idTextAnchor117):

![](image/ubuntu_gnome_calendar.jpg)

Figure 6-13

6.7 Desktop Settings

To access desktop settings, click on the button on the far right of the top bar to display the menu shown in [Figure 6-14](#Ubuntu_GNOME_Desktop.xhtml__idTextAnchor119):

![](image/ubuntu_gnome_settings_menu.jpg)

Figure 6-14

The menu provides quick access to common settings such as the system power saving modes, desktop theme, volume, and current network connection. The power button allows you to log out of the desktop, or restart or shutdown the system. Click the button in the top left corner of the menu to take a screenshot. The button to the right of the screenshot button displaying a gear icon opens the GNOME Settings application.

The Settings application provides a wide range of options, such as Ethernet and WiFi connections, screen background customization options, screen locking and power management controls, and language preferences. To explore the settings available in each category, simply select an option from the left-hand panel in the Settings window:

![](image/ubuntu_gnome_settings.jpg)

Figure 6-15

The menu shown in [Figure 6-14](#Ubuntu_GNOME_Desktop.xhtml__idTextAnchor119) above also includes options to switch user, adjust audio volume, change to a different WiFi network, and log out, restart, or power off the system.

6.8 Customizing the Dock

The size, position, and behavior of the dock may be changed from within the Settings app by selecting the Ubuntu Desktop option, as shown in [Figure 6-16](#Ubuntu_GNOME_Desktop.xhtml__idTextAnchor121):

![](image/ubuntu_desktop_settings_dock.jpg)

Figure 6-16

The position can be set to any of the four sides of the screen, while the Icon size can be used to reduce the size of the dock. Finally, the auto-hide dock option, if enabled, will cause the dock to recede from view until the mouse pointer moves to the edge of the screen where it is currently located.

6.9 Installing Ubuntu Software

In common with other operating systems such as macOS, Windows, iOS, and Android, Ubuntu has an “app store” in the form of the Ubuntu Software tool. An icon is usually placed in the dock, as indicated in [Figure 6-17](#Ubuntu_GNOME_Desktop.xhtml__idTextAnchor123) and includes the number of applications for which an update is available:

![](image/ubuntu_gnome_software_launcher.jpg)

Figure 6-17

Once loaded, the tool provides a list of applications available for installation on the system grouped together based on categories, recommendations, and editor’s picks. The library of available applications may also be search to find a specific item:

![](image/ubuntu_gnome_software_app.jpg)

Figure 6-18

To install an application, simply select it in the Ubuntu Software window and click on the Install button:

![](image/ubuntu_software_app_spotify.jpg)

Figure 6-19

6.10 Beyond Basic Customization

The GNOME desktop is, by design, a clean and uncluttered environment with minimal customization options. That does not mean, however, that it is not possible to make additional changes to the desktop. In fact, the GNOME Project has developed a tool called GNOME Tweaks for this very purpose. To install this tool, open the Ubuntu Software tool, and search for and install the GNOME Tweaks application. Once installed and launched, the Tweaks dialog will appear as shown below:

![](image/ubuntu_gnome_tweaks.jpg)

Figure 6-20

A wide range of options for customizing the desktop are now available. Too many, in fact, to cover in this chapter, so take some time to experiment with these settings before proceeding to the next chapter.

6.11 Summary

Ubuntu includes the GNOME 44 desktop environment which may either be included during the initial installation or installed. Unlike most other desktop environments, GNOME is intended to provide a clean and easy to use windowing user interface. Key areas of the GNOME desktop include the top bar, Activities overview, and dash. In addition, GNOME supports multiple workspaces keeping running applications organized and the screen uncluttered. A variety of configuration options is also available within the Settings app, including desktop background settings, audio, network configuration, and WiFi network selection.

7\. An Overview of the Cockpit Web Interface

Although equipped with the latest Linux desktop environment, Ubuntu is very much a server operating system. As such, most Ubuntu deployments will be to remote physical servers or as cloud-based virtual machine instances. Invariably, these systems run without a keyboard, mouse, or monitor, with direct access only available via the command prompt over a network connection. This presents a challenge in terms of administering the system from remote locations. While much can certainly be achieved via remote access to the command-line and desktop environments, there needs to be a consistent and cohesive solution to the administrative and monitoring tasks that must be performed daily on an enterprise-level operating system such as Ubuntu.

The Cockpit web-based administration interface provides this functionality. This chapter will explain how to install, configure and access the Cockpit interface while also providing an overview of the key features of Cockpit, many of which will be covered in greater detail in later chapters.

7.1 An Overview of Cockpit

Cockpit is a lightweight, web-based interface that allows general system administrative tasks to be performed remotely. When installed and configured, the system administrator opens a local browser window and navigates to the Cockpit port on the remote server. After loading the Cockpit interface into the browser and logging in, a wide range of tasks can be performed visually using administration and monitoring tools.

Behind the scenes, Cockpit uses the same tools to perform tasks typically used when working at the command line and updates automatically to reflect changes occurring elsewhere on the system. This allows Cockpit to be used with other administration tools and techniques without the risk of one approach overriding another. Cockpit can also be configured to access more than one server, allowing multiple servers to be administered and monitored simultaneously through a single browser session.

Cockpit is installed by default with a wide range of tools already bundled and allows additional extension plugins to be installed as needed. Cockpit is also designed so that you can create your own extensions using a combination of HTML and JavaScript to add missing or custom functionality.

Cockpit’s modular design also allows many features to be embedded into other web-based applications.

7.2 Installing and Enabling Cockpit

Cockpit is generally not installed on Ubuntu by default but can be set up and enabled in a few simple steps. The first step is to install the Cockpit package as follows:

# apt install cockpit

Next, the Cockpit socket service needs to be enabled:

# systemctl enable --now cockpit.socket

Finally, the necessary ports need to be opened on the firewall to allow remote browser connections to reach Cockpit if a firewall is enabled on your system (for details on firewalls, refer to the chapter entitled [“Ubuntu 23.04 Firewall Basics”](#Firewall_Basics.xhtml__idTextAnchor234)).

If ufw is enabled:

# ufw allow 9090

If firewalld is enabled:

# firewall-cmd --add-service=cockpit --permanent

# firewall-cmd --reload

7.3 Accessing Cockpit

If you have access to the desktop environment of the server on which Cockpit has been installed, open a browser window and navigate to https://localhost:9090 to access the Cockpit sign-in screen. If, on the other hand, the server is remote, navigate to the server using the domain name or IP address (for example, https://myserver.com:9090).

When the connection is established, the browser may warn that the connection is not secure. This is because the Cockpit service uses a self-signed certificate. Select the option to proceed to the website or, to avoid this message in the future, select the advanced option and add an exception for the server address. Once connected, the browser will load the login page shown in [Figure 7-1](#Ubuntu_Cockpit_Overview.xhtml__idTextAnchor130) below:

![](image/ubuntu_23.04_cockpit_login.jpg)

Figure 7-1

Sign in to the Cockpit interface either as root or with your user account credentials. Note that some tasks will be restricted within the Cockpit interface when signed in as a user due to permission constraints. In this situation, the Cockpit console will display a button labeled “Limited Access,” as shown in [Figure 7-2](#Ubuntu_Cockpit_Overview.xhtml__idTextAnchor131):

![](image/rocky_cockpit_limited_access.jpg)

Figure 7-2

To elevate your privileges, click on the limited access button and enter your password when you are prompted to do so:

![](image/rhel_cockpit_access_password.jpg)

Figure 7-3

After signing in, Cockpit will display the Overview screen.

7.4 Overview

The Overview screen provides an overview of the current system, including access to CPU, memory, storage, and network activity performance metrics. This screen also includes information about the system, including the underlying hardware, hostname, system time, and whether the system software is up to date. Options are also provided to restart or shut down the system.

[Figure 7-4](#Ubuntu_Cockpit_Overview.xhtml__idTextAnchor133), for example, shows the Overview page of the Cockpit interface:

![](image/ubuntu_23.04_cockpit_overview.jpg)

Figure 7-4

For more information on a particular category, click on the corresponding link. [Figure 7-5](#Ubuntu_Cockpit_Overview.xhtml__idTextAnchor134), for example, shows the system performance history screen:

![](image/ubuntu_220.04_cockpit_performance.jpg)

Figure 7-5

7.5 Logs

When the Logs category is selected, Cockpit displays the contents of the systemd journal logs. Choosing a log entry will display the entire log message. The log entries are ordered with the most recent at the top, and menus are included to filter the logs for different time durations and based on message severity.

![](image/rhel_cockpit_logs.jpg)

Figure 7-6

7.6 Storage

Select the Storage option to review and manage the storage on the system, including disks, partitions, volume groups, Network File System (NFS) mounts, and RAID storage. This screen also allows disk I/O activity to be monitored in real-time and lists log output from the system udisksd service used to query and manage storage devices:

![](image/centos_cockpit_storage.jpg)

Figure 7-7

7.7 Networking

The Networking screen provides information on various network-related configurations and services, including network interfaces and firewall settings. In addition, it allows configuration changes such as creating network bridges or setting up virtual networks:

![](image/rhel_cockpit_networking.jpg)

Figure 7-8

7.8 Accounts

Select this option to view the current user accounts configured on the system and create accounts for additional users. The topic of user management will be covered later in the chapter entitled [“Managing Ubuntu 23.04 Users and Groups”](#User_Management.xhtml__idTextAnchor178):

![](image/ubuntu_cockpit_users.jpg)

Figure 7-9

Click on an existing account to view details and make changes. The user account details page may also be used to review and add Public SSH keys to the user’s account for remote access to the server, as outlined in the chapter [“Configuring SSH Key-based Authentication on Ubuntu 23.04”](#SSH_Authentication.xhtml__idTextAnchor281).

7.9 Services

This screen displays a list of the system services running on the server and allows those services to be added, removed, stopped, and started.

![](image/rhel_cockpit_services.jpg)

Figure 7-10

The topic of services will be covered in detail in the chapter [“Managing Ubuntu 23.04 systemd Units”](#Systemd_Targets_and_States.xhtml__idTextAnchor188).

7.10 Applications

As previously mentioned, additional functionality can be added to Cockpit as extensions. These can either be self-developed extensions or those provided by third parties. The Applications screen lists installed extensions and allows extensions to be added or removed:

![](image/rhel_cockpit_applications.jpg)

Figure 7-11

If the Applications option is not available within the cockpit interface, it can be installed as follows:

# apt install cockpit-packagekit

7.11 Virtual Machines

Virtualization allows multiple operating system instances to run simultaneously on a single computer system, with each system running inside its own virtual machine. The Virtual Machines Cockpit extension provides a way to create and manage the virtual machine guests installed on the server:

![](image/rhel_8_cockpit_virtual_machines.jpg)

Figure 7-12

The Virtual Machines extension is not installed by default but can be added via the Cockpit Applications screen or by running the following command:

# apt install cockpit-machines

The use of virtualization with Ubuntu is covered starting with the chapter [“An Overview of Virtualization Techniques”](#Virtualization_Overview.xhtml__idTextAnchor361).

7.12 Software Updates

If any software updates are available for the system, they will be listed here and can be installed from this screen:

![](image/ubuntu_220.04_cockpit_software_updates.jpg)

Figure 7-13

If the Cockpit Software Updates screen is not available, it can be installed as follows:

# apt install cockpit-packagekit

7.13 Terminal

As the name suggests, the Terminal screen provides access to the command-line prompt:

![](image/cockpit_terminal.jpg)

Figure 7-14

7.14 Connecting to Multiple Servers

Cockpit can be configured to administer multiple servers from within a single session. To add another host to the Cockpit session, click on the button highlighted in [Figure 7-15](#Ubuntu_Cockpit_Overview.xhtml__idTextAnchor154) to display the Hosts panel:

![](image/cockpit_hosts.jpg)

Figure 7-15

Click the Add new host button and enter the IP address or hostname of the other system and select a color by which to distinguish this server from any others added to Cockpit before clicking on the Add button:

![](image/rhel_cockpit_add_new_host.jpg)

Figure 7-16

Cockpit will ask you to accept a new SSH key if you are connecting to the remote server for the first time. After accepting the key, you will be prompted to enter the password for the user name specified in [Figure 7-16](#Ubuntu_Cockpit_Overview.xhtml__idTextAnchor155) above. The option is also provided to set up and authorize a password-protected SSH key to enable automatic login to the second host system next time you need to access it:

![](image/rhel_cockpit_remote_login.jpg)

Figure 7-17

To switch between the hosts, display the Hosts panel ([Figure 7-15](#Ubuntu_Cockpit_Overview.xhtml__idTextAnchor154) above) and select the required system.

7.15 Enabling Stored Metrics

In a standard installation, Cockpit does not retain any performance metric data beyond what is displayed in the short time window covered by the graphs. To retain the data collected by Cockpit, the Cockpit Co-Pilot (PCP) package needs to be installed. Begin by installing the cockpit-pcp package as follows:

# apt install cockpit-pcp

After installing cockpit-pcp, log out of the current Cockpit session and back in.

Next, display the Performance Metrics screen and click on the Metrics settings button to display the screen shown in [Figure 7-18](#Ubuntu_Cockpit_Overview.xhtml__idTextAnchor158), switch on the Collect metrics option, and click Save:

![](image/rhel_cockpit_collect_metrics.jpg)

Figure 7-18

After sufficient time has elapsed for Cockpit to gather data, the metric information will appear as shown in [Figure 7-19](#Ubuntu_Cockpit_Overview.xhtml__idTextAnchor160), categorized in hourly blocks:

![](image/ubuntu_220.04_cockpit_stored_metrics.jpg)

Figure 7-19

7.16 Summary

The Cockpit web interface allows remote system administration tasks to be performed visually from within a web browser without relying on the command prompt and command-line tools. Once installed and enabled, the system administrator opens a web browser, connects to the remote server, and signs into the Cockpit interface. Behind the scenes, Cockpit uses the same command-line tools as those available via the command prompt, allowing both options to be used without the risk of configuration conflicts. In addition, Cockpit uses a modular framework enabling additional extensions to be added and for custom extensions to be developed and integrated. A Cockpit session can be used to administer a single server or configured to access multiple servers simultaneously.

8. Using the Bash Shell on Ubuntu 23.04

An essential part of learning to work with Ubuntu and Linux distributions generally involves gaining proficiency in working in the shell environment. While graphical desktop environments such as GNOME, included with Linux, provide a user-friendly interface to the operating system, the shell environment provides far greater capabilities, flexibility, and automation than can ever be achieved using graphical desktop tools. The shell environment also provides a means for interacting with the operating system when a desktop environment is unavailable, a common occurrence when working with a server-based operating system such as Ubuntu or a damaged system that will not fully boot.

Therefore, this chapter aims to provide an overview of the default shell environment on Ubuntu (specifically the Bash shell).

8.1 What is a Shell?

The shell is an interactive command interpreter environment within which commands may be typed at a prompt or entered into a file as a script and executed. The origins of the shell can be traced back to the early days of the UNIX operating system. In fact, in the early days of Linux, before the introduction of graphical desktops, the shell was the only way for a user to interact with the operating system.

A variety of shell environments have been developed over the years. The first widely used shell was the Bourne shell, written by Stephen Bourne at Bell Labs.

Yet another early creation was the C shell which shared some syntax similarities with the C Programming Language and introduced usability enhancements such as command-line editing and history.

The Korn shell (developed by David Korn at Bell Labs) is based on features provided by both the Bourne and C shells.

The default shell on Ubuntu is the Bash shell (shorthand for Bourne Again SHell). This shell, which began life as an open-source version of the Bourne shell, was developed for the GNU Project by Brian Fox and is based on features provided by both the Bourne shell and the C shell.

8.2 Gaining Access to the Shell

From within the GNOME desktop environment, the shell prompt may be accessed from a Terminal window by selecting the Activities option in the top bar, entering Terminal into the search bar, and clicking the Terminal icon.

When remotely logging into an Ubuntu server, for example, using SSH, the user is presented with a shell prompt. The chapter entitled [“Configuring SSH Key-based Authentication on Ubuntu 23.04”](#SSH_Authentication.xhtml__idTextAnchor281) will cover details on accessing a remote server using SSH. When booting a server-based system in which a desktop environment has not been installed, the shell is entered immediately after the user completes the login procedure at the physical console terminal or remote login session.

8.3 Entering Commands at the Prompt

Commands are entered at the shell command prompt simply by typing the command and pressing the Enter key. While some commands perform tasks silently, most will display some form of output before returning to the prompt. For example, the ls command can be used to display the files and directories in the current working directory:

$ ls

Desktop Documents Downloads Music Pictures Public Templates Videos

The available commands are either built into the shell itself or reside on the physical file system. The location on the file system of a command may be identified using the which command. For example, to find out where the ls executable resides on the file system:

$ which ls

alias ls=’ls --color=auto’

/usr/bin/ls

Clearly, the ls command resides in the /usr/bin directory. Note also that an alias is configured, a topic that will be covered later in this chapter. Using the which command to locate the path to commands built into the shell will result in a message indicating the executable cannot be found. For example, attempting to find the location of the history command (which is built into the shell rather than existing as an executable on the file system) will result in output similar to the following:

$ which history

/usr/bin/which: no history in (/home/demo/.local/bin:/home/demo/bin:/usr/share/Modules/bin:/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin)

8.4 Getting Information about a Command

Many of the commands available to the Linux shell can seem cryptic. To find out detailed information about what a command does and how to use it, use the man command specifying the name of the command as an argument. For example, to learn more about the pwd command:

$ man pwd

A detailed description of the pwd command will be displayed when the above command is executed. Many commands will also provide additional information when run with the --help command-line option:

$ wc --help

8.5 Bash Command-line Editing

Early shell environments did not provide any form of line editing capabilities. This meant that if you spotted an error at the beginning of a long command-line, you were typing, you had to delete all the following characters, correct the error and then re-enter the remainder of the command. Fortunately, Bash provides a wide range of command-line editing options, as outlined in the following table:

| Key Sequence | Action |
| Ctrl-b or Left Arrow | Move the cursor back one position |
| Ctrl-f or Right Arrow | Move the cursor forward one position |
| Delete | Delete the character currently beneath the cursor |
| Backspace | Delete the character to the left of the cursor |
| Ctrl-_ | Undo previous change (can be repeated to undo all previous changes) |
| Ctrl-a | Move the cursor to the start of the line |
| Ctrl-e | Move the cursor to the end of the line |
| Meta-f or Esc then f | Move cursor forward one word |
| Meta-b or Esc then b | Move the cursor back one word |
| Ctrl-l | Clear the screen of everything except the current command |
| Ctrl-k | Delete to the end of the line from the current cursor position |
| Meta-d or Esc then d | Delete to end of the current word |
| Meta-DEL or Esc then DEL | Delete beginning to the current word |
| Ctrl-w | Delete from the current cursor position to the previous white space |

Table 8-1

8.6 Working with the Shell History

In addition to command-line editing features, the Bash shell provides command-line history support. A list of previously executed commands may be viewed using the history command:

$ history

    1 ps

    2 ls

    3 ls –l /

    4 ls

    5 man pwd

    6 man apropos

In addition, Ctrl-p (or up arrow) and Ctrl-n (or down arrow) may be used to scroll back and forth through previously entered commands. Finally, when the desired command from the history is displayed, press the Enter key to execute it.

Another option is to enter the ‘!’ character, followed by the first few characters of the command to be repeated, followed by the Enter key.

8.7 Filename Shorthand

Many shell commands take one or more filenames as arguments. For example, to display the content of a text file named list.txt, the cat command would be used as follows:

$ cat list.txt

Similarly, the content of multiple text files could be displayed by specifying all the file names as arguments:

$ cat list.txt list2.txt list3.txt list4.txt

Instead of typing in each name, pattern matching can be used to specify all files with names matching certain criteria. For example, the ‘*’ wildcard character can be used to simplify the above example:

$ cat *.txt

The above command will display the content of all files ending with a .txt extension. This could be further restricted to any file names beginning with list and ending in .txt:

$ cat list*.txt

Single character matches may be specified using the ‘?’ character:

$ cat list?.txt

8.8 Filename and Path Completion

Rather than typing in a complete file name or path or using pattern matching to reduce the amount of typing, the shell provides the filename completion feature. To use filename completion, enter the first few characters of the file or path name and then press the Esc key twice. The shell will then complete the filename for you with the first file or path name in the directory that matches the characters you entered. To obtain a list of possible matches, press Esc = after entering the first few characters.

8.9 Input and Output Redirection

As previously mentioned, many shell commands output information when executed. By default, this output goes to a device file named stdout which is essentially the terminal window or console in which the shell is running. Conversely, the shell takes input from a device file named stdin, which by default is the keyboard.

Output from a command can be redirected from stdout to a physical file on the file system using the ‘>’ character. For example, to redirect the output from an ls command to a file named files.txt, the following command would be required:

$ ls *.txt > files.txt

Upon completion, files.txt will contain the list of files in the current directory. Similarly, the contents of a file may be fed into a command in place of stdin. For example, to redirect the contents of a file as input to a command:

$ wc –l < files.txt

The above command will display the number of lines in the files.txt file.

It is important to note that the ‘>’ redirection operator creates a new file or truncates an existing file when used. To append to an existing file, use the ‘>>’ operator:

$ ls *.dat >> files.txt

In addition to standard output, the shell also provides standard error output using stderr. While output from a command is directed to stdout, any error messages generated by the command are directed to stderr. This means that if stdout is directed to a file, error messages will still appear in the terminal. This is generally the desired behavior, though stderr may also be redirected if desired using the ‘2>’ operator:

$ ls dkjfnvkjdnf 2> errormsg

On completion of the command, an error reporting that the file named dkjfnvkjdnf could not be found will be contained in the errormsg file.

Both stderr and stdout may be redirected to the same file using the &> operator:

$ ls /etc dkjfnvkjdnf &> alloutput

On completion of execution, the alloutput file will contain both a listing of the contents of the /etc directory and the error message associated with the attempt to list a non-existent file.

8.10 Working with Pipes in the Bash Shell

In addition to I/O redirection, the shell also allows output from one command to be piped directly as input to another command. A pipe operation is achieved by placing the ‘|’ character between two or more commands on a command line. For example, to count the number of processes running on a system, the output from the ps command can be piped through to the wc command:

$ ps –ef | wc –l

There is no limit to the number of pipe operations that can be performed on a command line. For example, to find the number of lines in a file that contain the name Smith:

$ cat namesfile | grep Smith | wc –l

8.11 Configuring Aliases

As you gain proficiency with the shell environment, you will likely frequently issue commands with the same arguments. For example, you may often use the  ls command with the l and t options:

$ ls –lt

To reduce the amount of typing involved in issuing a command, it is possible to create an alias that maps to the command and arguments. For example, to create an alias such that entering the letter l will cause the ls –lt command to be executed, the following statement would be used:

$ alias l="ls –lt"

Entering l at the command prompt will now execute the original statement.

8.12 Environment Variables

Shell environment variables provide temporary storage of data and configuration settings. The shell itself sets up several environment variables that the user may change to modify the behavior of the shell. A listing of currently defined variables may be obtained using the env command:

$ env

SSH_CONNECTION=192.168.0.19 61231 192.168.0.28 22

MODULES_RUN_QUARANTINE=LD_LIBRARY_PATH

LANG=en_US.UTF-8

HISTCONTROL=ignoredups

HOSTNAME=demo-pc.ebookfrenzy.com

XDG_SESSION_ID=15

MODULES_CMD=/usr/share/Modules/libexec/modulecmd.tcl

USER=demo

ENV=/usr/share/Modules/init/profile.sh

SELINUX_ROLE_REQUESTED=

PWD=/home/demo

HOME=/home/demo

SSH_CLIENT=192.168.0.19 61231 22

SELINUX_LEVEL_REQUESTED=

.

.

Perhaps the most useful environment variable is PATH. This defines the directories in which the shell will search for commands entered at the command prompt and the order in which it will do so. The PATH environment variable for a user account on a newly installed Ubuntu system will likely be configured as follows:

$ echo $PATH

/home/demo/.local/bin:/home/demo/bin:/usr/share/Modules/bin:/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin

Another useful variable is HOME, which specifies the current user’s home directory. If, for example, you wanted the shell to also look for commands in the scripts directory located in your home directory, you would modify the PATH variable as follows:

$ export PATH=$PATH:$HOME/scripts

The current value of an existing environment variable may be displayed using the echo command:

$ echo $PATH

You can create your own environment variables using the export command. For example:

$ export DATAPATH=/data/files

A useful trick to assign the output from a command to an environment variable involves using back quotes (`) around the command. For example, to assign the current date and time to an environment variable called NOW:

$ export NOW=`date`

$ echo $NOW

Wed Mar 29 12:39:20 PM EDT 2023

If there are environment variables or alias settings that need to be configured each time you enter the shell environment, they may be added to a file in your home directory named .bashrc. For example, the following .bashrc file is configured to set up the DATAPATH environment variable and an alias:

# .bashrc

# Source global definitions

if [ -f /etc/bashrc ]; then

. /etc/bashrc

fi

# User specific environment

PATH="$HOME/.local/bin:$HOME/bin:$PATH"

export PATH

# Uncomment the following line if you don’t like systemctl’s auto-paging feature:

# export SYSTEMD_PAGER=

# User specific aliases and functions

export DATAPATH=/data/files

alias l="ls -lt"

8.13 Writing Shell Scripts

So far, we have focused exclusively on the interactive nature of the Bash shell. By interactive, we mean manually entering commands individually and executing them at the prompt. In fact, this is only a small part of what the shell is capable of. Arguably one of the most powerful aspects of the shell involves the ability to create shell scripts. Shell scripts are text files containing statement sequences that can be executed within the shell environment to perform tasks. In addition to the ability to execute commands, the shell provides many programming constructs, such as for and do loops and if statements, that you might reasonably expect to find in a scripting language.

Unfortunately, a detailed overview of shell scripting is beyond the scope of this chapter. However, many books and web resources dedicated to shell scripting do the subject much more justice than we could ever hope to achieve here. In this section, therefore, we will only be providing a very small taste of shell scripting.

The first step in creating a shell script is to create a file (for this example, we will name it simple.sh) and add the following as the first line:

#!/bin/sh

The #! is called the “shebang” and is a special sequence of characters indicating that the path to the interpreter needed to execute the script is the next item on the line (in this case, the sh executable located in /bin). This could equally be, for example, /bin/csh or /bin/ksh if either were the interpreter you wanted to use.

The next step is to write a simple script:

#!/bin/sh

for i in *

do

     echo $i

done

All this script does is iterate through all the files in the current directory and display the name of each file. This script may be executed by passing the name of the script through as an argument to sh:

$ sh simple.sh

To make the file executable (thereby negating the need to pass it through to the sh command), the chmod command can be used:

$ chmod +x simple.sh

Once the execute bit has been set on the file’s permissions, it may be executed directly. For example:

$ ./simple.sh

8.14 Summary

We briefly toured the Bash shell environment in this chapter of Ubuntu Essentials. In the world of graphical desktop environments, it is easy to forget that an operating system’s true power and flexibility can often only be utilized by dropping down below the user-friendly desktop interface and using a shell environment. Moreover, familiarity with the shell is necessary to administer and maintain server-based systems that do not have the desktop installed or when attempting to repair a system damaged to the point that the desktop or Cockpit interface will no longer launch.

The shell’s capabilities go far beyond the areas covered in this chapter. If you are new to the shell, we strongly encourage you to seek additional resources. Once familiar with the concepts, you will quickly find that it is quicker to perform many tasks using the shell in a terminal window than to wade through menus and dialogs on the desktop.

9. Managing Ubuntu 23.04 Users and Groups

During the installation of Ubuntu, the installer created a root or superuser account and required that a password be configured. The installer also provided the opportunity to create a user account for the system. We should remember that Ubuntu is an enterprise-class, multi-user, and multi-tasking operating system. To use the full power of Ubuntu, therefore, it is likely that more than one user will need to be given access to the system. Each user should have their own user account login, password, home directory, and privileges.

Users are further divided into groups for easier administration, and those groups can have different levels of privileges. For example, you may have a group of users who work in the Accounting department. In such an environment, you can create an accounts group and assign all the Accounting department users to that group.

This chapter will cover the steps to add, remove and manage users and groups on an Ubuntu system. Users and groups may be managed on Ubuntu using command-line tools, the Cockpit web interface, and the desktop Settings app. In this chapter, we will look at each of these approaches to user management.

9.1 User Management from the Command-line

New users may be added to an Ubuntu system via the command line using the adduser utility. To create a new user account, enter a command similar to the following:

# adduser john

By default, this will create a home directory for the user in the /home directory (in this case, /home/john). To specify a different home directory, use the --home command-line option when creating the account:

# adduser --home /users/johnsmith john

The adduser command will prompt for a password during the account creation. This password can be changed later using the passwd command:

# passwd john

Changing password for user john.

New password:

Retype new password:

passwd: all authentication tokens updated successfully.

An existing user may be deleted via the command line using the deluser utility. While this will delete the account, the user’s files and data will remain intact on the system:

# deluser john

It is also possible to remove the user’s home directory and mail spool as part of the deletion process:

# deluser --remove-home john

All users on an Ubuntu system are members of one or more groups. By default, new users are added to a private group with the same name as the user (in the above example, the account created for user john was a member of a private group also named john). However, as an administrator, it makes sense to organize users into more logical groups. For example, all salespeople might belong to a sales group, and accounting staff might belong to the accounts group, and so on. New groups are added from the command line using the groupadd command-line tool, for example:

# groupadd accounts

Use the usermod tool to add an existing user to an existing group from the command line:

# usermod -G accounts john

To add an existing user to multiple existing groups, run the usermod command with the -G option:

# usermod -G accounts,sales,support john

Note that the above commands remove the user from supplementary groups not listed after the -G but to which the user is currently a member. To retain any current group memberships, use the -a flag to append the new group memberships:

# usermod -aG accounts,sales,support john

An existing group may be deleted from a system using the groupdel utility:

# groupdel accounts

Note that if the group to be deleted is the primary or initial group for any user, it cannot be deleted. The user must first be deleted or assigned a new primary group using the usermod command before the group can be removed. A user can be assigned to a new primary group using the usermod -g option:

# usermod -g sales john

# groupdel accounts

Run the groups command to find out the groups to which a user belongs. For example:

$ groups john

john : accounts support

By default, a user account cannot perform tasks requiring superuser (root) privileges unless they know the root password. It is, however, possible to configure a user account so that privileged tasks can be performed using the sudo command. This involves adding the user account as a member of the sudo group, for example:

# adduser john sudo

Once added to the sudo group, the user will be able to perform otherwise restricted tasks using sudo as follows:

# apt update

Hit:1 http://us.archive.ubuntu.com/ubuntu jammy InRelease

Hit:2 http://security.ubuntu.com/ubuntu jammy-security InRelease

The sudo capabilities of the sudo group may be modified by editing the /etc/sudoers file and locating the following section:

## Allows people in group sudo to run all commands

%sudo ALL=(ALL) ALL

To disable sudo for all sudo group members, comment out the second line as follows:

## Allows people in group sudo to run all commands

# %sudo ALL=(ALL) ALL

To allow sudo group members to use sudo without entering a password (for security reasons, this is not recommended), modify the sudoers file as follows:

## Same thing without a password

%sudo ALL=(ALL) NOPASSWD: ALL

Behind the scenes, all these commands are simply changing the /etc/passwd, /etc/group, and /etc/shadow files on the system.

9.2 User Management with Cockpit

If the Cockpit web interface is installed and enabled on the system (a topic covered in the chapter entitled “An Overview of the Cockpit Web Interface”), several user and group management tasks can be performed within the Accounts screen shown in [Figure 9-1](#User_Management.xhtml__idTextAnchor181) below:

![](image/ubuntu_cockpit_users1.jpg)

Figure 9-1

The screen will display any existing user accounts on the system and provides a button to add additional accounts. To create a new account, click the Create New Account button and enter the requested information in the resulting dialog ([Figure 9-2](#User_Management.xhtml__idTextAnchor182)). Note that the option is also available to create the account but to lock it until later:

![](image/rhel_cockpit_new_account.jpg)

Figure 9-2

To modify a user account, select it from the main screen and make any modifications to the account details:

![](image/rhel_cockpit_modify_account.jpg)

Figure 9-3

This screen allows various tasks, including locking or unlocking the account, changing the password, or forcing the user to configure a new password to be performed. In addition, if the Server Administrator option is selected, the user will be added to the sudo group and permitted to use sudo to perform administrative tasks. A button is also provided to delete the user from the system.

If the user is accessing the system remotely using an SSH connection with key encryption, the user’s public key may be added within this screen. SSH access and authentication will be covered later in [“Configuring SSH Key-based Authentication on Ubuntu 23.04”](#SSH_Authentication.xhtml__idTextAnchor281).

9.3 User Management using the Settings App

A third user account management option is available via the GNOME desktop settings app. This app is accessed by clicking on icons in the top right-hand corner of the GNOME desktop and selecting the Settings option, as shown in Figure 9-4:

![](image/ubuntu_gnome_settings_menu1.jpg)

Figure 9-4

When the main settings screen appears, click the Users option in the left-hand navigation panel. By default, the settings will be locked, and making any changes to the user accounts on the system will not be possible. To unlock the Settings app, click the Unlock button in [Figure 9-5](#User_Management.xhtml__idTextAnchor184) below and enter your password. Note that it will only be possible to unlock the settings if you are logged in as a user with sudo privileges:

![](image/ubuntu_settings_users.jpg)

Figure 9-5

Once the app has been unlocked, click on Add User... to display the dialog shown in [Figure 9-6](#User_Management.xhtml__idTextAnchor185) below:

![](image/ubuntu_settings_add_user.jpg)

Figure 9-6

Select the Administrator option to assign sudo access to the new user if required. Next, enter the user’s full name and username and assign a password now, or allow the user to set up the password when they first log into their account. Once the information has been entered, click the Add button to create the account.

The settings for an existing user can be viewed, modified, or the account deleted at any time by selecting the corresponding icon within the Users screen, as shown in [Figure 9-7](#User_Management.xhtml__idTextAnchor186). The option is also available to view the user’s login activity. Note that it will be necessary to unlock the Settings app again before any changes can be made to an account:

![](image/ubuntu_settings_user_details.jpg)

Figure 9-7

9.4 Summary

As a multi-user operating system, Ubuntu has been designed to support controlled access for multiple users. During installation, the root user account was created and assigned a password, and the option to create a user account was also provided. Additional user accounts may be added to the system using a set of command-line tools via the Cockpit web interface or the GNOME Settings app. In addition to user accounts, Linux also implements the concept of groups. New groups can be added, and users assigned to those groups using command-line tools, and each user must belong to at least one group. By default, a standard, non-root user does not have permission to perform privileged tasks. Users that are members of the special sudo group, however, may perform privileged tasks by making use of the sudo command.

10\. Managing Ubuntu 23.04 systemd Units

To gain proficiency in Ubuntu system administration, it is essential to understand the concepts of systemd units with a particular emphasis on two specific types known as targets and services. This chapter provides a basic overview of the different systemd units supported by Ubuntu and how to configure the many services that run in the background of a running Linux system.

10.1 Understanding Ubuntu systemd Targets

Ubuntu can be configured to boot into one of several states (referred to as targets), each designed to provide a specific level of operating system functionality. The system administrator configures the target to which a system will boot by default based on the purpose for which the system is being used. A desktop system, for example, will likely be configured to boot using the graphical user interface target. In contrast, a cloud-based server system would be more likely to boot to the multi-user target level.

During the boot sequence, a process named systemd looks in the /etc/systemd/system folder to find the default target setting. Having identified the default target, it proceeds to start the systemd units associated with that target so that the system boots with all the necessary processes running.

For those familiar with older Ubuntu versions, systemd targets replace the older runlevel system.

10.2 Understanding Ubuntu systemd Services

A service is a process, typically running in the background, that provides specific functionality. The sshd service, for example, is the background process (also referred to as a daemon) that provides secure shell access to the system. Different systemd targets are configured to automatically launch different collections of services, depending on the functionality to be provided by that target.

Targets and services are types of systemd unit, a topic that will be covered later in this chapter.

10.3 Ubuntu systemd Target Descriptions

As previously outlined, Ubuntu can be booted into one of several target levels. The default target to which the system is configured to boot will, in turn, dictate which systemd units are started. The targets that relate specifically to system startup and shutdown can be summarized as follows:

• poweroff.target - This target shuts down the system. It is unlikely you would want this as your default target.

• rescue.target – Causes the system to start in a single-user mode under which only the root user can log in. The system does not start any networking, graphical user interface, or multi-user services in this mode. This run level is ideal for system administrators to perform system maintenance or repair activities.

• multi-user.target - Boots the system into a multi-user mode with text-based console login capability.

• graphical.target - Boots the system into a networked, multi-user state with X Window System capability. By default, the graphical desktop environment will start at the end of the boot process. This is the most common run level for desktop or workstation use.

• reboot.target - Reboots the system. Another target that, for obvious reasons, you are unlikely to want as your default.

In addition to the above targets, the system includes about 70 other targets, many of which are sub-targets used by the above main targets. Behind the scenes, for example, multi-user.target will also start a target named basic.target which will, in turn, start the sockets.target unit, which is required for communication between different processes. This ensures that all the services on which the multi-user target depends are also started during the boot process.

A list of the targets and services on which a specified target is dependent can be viewed by running the following command in a terminal window:

# systemctl list-dependencies <target>

Figure 11-1, for example, shows a partial listing of the systemd unit dependencies for the graphical target (the complete listing contains over 140 targets and services required for a fully functional multi-user system):

![](image/ubuntu_systemd_dependencies.jpg)

Figure 10-1

The listing is presented as a hierarchical tree illustrating how some dependencies have sub-dependencies of their own. Scrolling to the bottom of the list, for example, would reveal that the graphical target depends on a cloud-related service called cloud-init.target, which, in turn, has its own service dependencies:

![](image/ubuntu_systemd_subdependencies.jpg)

Figure 10-2

The colored dots to the left of each entry in the list indicate the current status of that service or target as follows:

•Green - The service or target is active and running.

•White - The service or target is inactive (dead). Typically because the service or target has yet to be enabled, has been stopped for some reason, or a condition on which the service or target depends has not been met.

•Red - The service or target failed to start due to a fatal error.

To find out more details about the status of a systemd unit, use the systemctl status command followed by the unit name as follows:

# systemctl status systemd-machine-id-commit.service

○ systemd-machine-id-commit.service - Commit a transient machine-id on disk

     Loaded: loaded (/usr/lib/systemd/system/systemd-machine-id-commit.service; static)

     Active: inactive (dead)

  Condition: start condition failed at Thu 2023-03-30 08:41:05 EDT; 16min ago

             └─ ConditionPathIsMountPoint=/etc/machine-id was not met

       Docs: man:systemd-machine-id-commit.service(8)

10.4 Identifying and Configuring the Default Target

The current default target for an Ubuntu system can be identified using the systemctl command as follows:

# systemctl get-default

multi-user.target

In the above case, the system is configured to boot using the multi-user target by default. The default setting can be changed anytime using the systemctl command with the set-default option. The following example changes the default target to start the graphical user interface the next time the system boots:

# systemctl set-default graphical.target

Removed /etc/systemd/system/default.target.

Created symlink /etc/systemd/system/default.target → /lib/systemd/system/graphical.target.

The output from the default change operation reveals the steps performed in the background by the systemctl command to implement the change. The current default is configured by establishing a symbolic link from the default.target file located in /etc/systemd/system to point to the corresponding target file located in the /usr/lib/systemd/system folder (in this case the graphical.target file).

10.5 Understanding systemd Units and Unit Types

As previously mentioned, targets and services are both types of systemd unit. All the files within the /usr/lib/systemd/system folder are called systemd unit configuration files, each representing a systemd unit. Each unit is, in turn, categorized as being of a particular unit type. Ubuntu supports 12 different unit types, including the target and service unit types already covered in this chapter.

The type of a unit file is represented by the filename extension as outlined in [Table 10-1](#Systemd_Targets_and_States.xhtml__idTextAnchor194) below:

| Unit Type | Filename Extension | Type Description |
| Service | .service | System service. |
| Target | .target | Group of systemd units. |
| Automount | .automount | File system auto-mount point. |
| Device | .device | Device file recognized by the kernel. |
| Mount | .mount | File system mount point. |
| Path | .path | File or directory in a file system. |
| Scope | .scope | Externally created process. |
| Slice | .slice | Group of hierarchically organized units that manage system processes. |
| Snapshot | .snapshot | Saved state of the systemd manager. |
| Socket | .socket | Inter-process communication socket. |
| Swap | .swap | Swap device or a swap file. |
| Timer | .timer | Systemd timer. |

Table 10-1

Note that the target unit type differs from other types in that it comprises a group of systemd units such as services or other targets.

10.6 Dynamically Changing the Current Target

The systemctl set-default command outlined previously specifies the target that will be used the next time the system starts but does not change the current system’s state. To change to a different target dynamically, use the systemctl command again, using the isolate option followed by the destination target. To switch the current system to the graphical target without rebooting, for example, the following command would be used:

# systemctl isolate graphical.target

Once executed, the system will start the graphical desktop environment.

10.7 Enabling, Disabling, and Masking systemd Units

A newly installed Ubuntu system will include the base systemd service units but is unlikely to include all the services the system will eventually need once it goes into a production environment. A basic Ubuntu installation, for example, will typically not include the packages necessary to run an Apache web server, a key element of which is the apache2.service unit.

The system administrator will resolve this problem by installing the necessary apache2 packages using the following command:

# apt install apache2

Having configured the web server, the next task will be to check the status of the apache2 service unit to identify whether it was activated as part of the installation process:

# systemctl status apache2.service

● apache2.service - The Apache HTTP Server

     Loaded: loaded (/lib/systemd/system/apache2.service; disabled; vendor prese>

     Active: active (running) since Mon 2023-07-17 14:01:13 UTC; 40s ago

       Docs: https://httpd.apache.org/docs/2.4/

   Main PID: 22328 (apache2)

      Tasks: 55 (limit: 4517)

     Memory: 4.7M

        CPU: 24ms

     CGroup: /system.slice/apache2.service

             ├─22328 /usr/sbin/apache2 -k start

             ├─22329 /usr/sbin/apache2 -k start

             └─22330 /usr/sbin/apache2 -k start

Note that the service status may be listed as loaded but inactive, which happens when it is preset by the vendor to be disabled when first installed. To start an inactive service, the following command can be used:

# systemctl start apache2.service

In the above example output, the status indicates that the service is disabled. This means that the next time the system reboots, the apache2 service will not start automatically and will need to be started manually by the system administrator.

To configure a service to start automatically each time the system starts, it must be enabled as follows:

# systemctl enable apache2.service

A currently running service may be stopped at any time as follows:

# systemctl stop apache2.service

Now that it has been enabled, the next time the system reboots to the current target, the apache2 service will start automatically. Assuming, for example, that the service was enabled while the system was running the multi-user target, the apache2 service will have been added as another dependency to the multi-user.target systemd unit.

Behind the scenes, systemctl adds dependencies to targets by creating symbolic links in the .wants folder for the target within the /etc/systemd/system folder. For example, the multi-user.target unit has a folder named multi-user.target.wants in /etc/systemd/system containing symbolic links to all of the systemd units located in /usr/lib/systemd/system on which it is dependent. A review of this folder will show a correlation with the dependencies listed by the systemctl list-dependencies command outlined earlier in the chapter.

To configure a service so that it no longer starts automatically as a target dependency, deactivate it as follows:

# systemctl disable apache2.service

This command will remove the symbolic link to the apache2.service unit file from the .wants directory so that it is no longer a dependency and, as such, will not be started the next time the system boots.

The .wants folder contains dependencies that, if not available, will not prevent the unit from starting and functioning. Mandatory dependencies (in other words, dependencies that will cause the unit to fail if not available) should be placed in the  .requires folder (for example, multi-user.target.requires).

In addition to enabling and disabling, it is also possible to mask a systemd unit as follows:

# systemctl mask apache2.service

A masked systemd unit cannot be enabled, disabled, or started under any circumstances, even if it is listed as a dependency for another unit. As far as the system is concerned, it is as though a masked systemd unit no longer exists. This can be useful for ensuring that a unit is never started, regardless of the system conditions. The only way to regain access to the service is to unmask it:

# systemctl unmask apache2.service

10.8 Working with systemd Units in Cockpit

In addition to the command-line techniques outlined in this chapter, it is also possible to review and manage systemd units from within the Cockpit web-based interface. For example, assuming that Cockpit has been installed and set up as outlined in the chapter entitled “An Overview of the Cockpit Web Interface”, access to the list of systemd units on the system can be accessed by logging into Cockpit and selecting the Services option in the left-hand navigation panel marked A in [Figure 10-3](#Systemd_Targets_and_States.xhtml__idTextAnchor198):

![](image/ubuntu_cockpit_services.jpg)

Figure 10-3

The row of options marked B displays units of specific types in the main area marked C, where the current status of each unit is listed in the State column.

Selecting a unit from the list will display detailed information. [Figure 10-4](#Systemd_Targets_and_States.xhtml__idTextAnchor199), for example, shows the detail screen for an apache2 instance, including service logs (A) and a switch and menu (B) for performing tasks such as starting, stopping, enabling/disabling, and masking/unmasking the unit:

![](image/ubuntu_cockpit_apache_service.jpg)

Figure 10-4

10.9 Summary

A newly installed Ubuntu system includes a base set of systemd units, many of which run in the background to provide much of the system’s functionality. These units are categorized by type, the most common being targets and services. A target unit is a group of other units to be started collectively. The system has a default target unit that defines the other units to be started up each time the system boots. The most common targets are those which boot the system to either multi-user or graphical mode. In addition, the systemctl command-line tool provides a range of options for performing systemd unit configuration tasks, many of which are also available through the Cockpit web-based interface.

11\. Ubuntu Software Package Management and Updates

It is highly unlikely that a newly installed Ubuntu system will contain all of the software packages necessary to perform the tasks for which it is intended. Even once all the required software has been installed, it is almost certain that newer versions of many of those packages will be released during the lifespan of the system. In some cases, you will need to ensure that these latest package releases are installed on the system so that bugs and security vulnerabilities are fixed.

This chapter introduces the basic concepts of software management on Ubuntu, explains how these issues are addressed, and explores the concepts of repositories and software packages while exploring how to list, install and remove the software packages that make up a functioning Ubuntu system.

11.1 Repositories

Linux is essentially comprised of a set of base packages that provide the core functionality of the operating system together with a range of other packages and modules that add functionality and features on top of the base operating system.

When Ubuntu is first installed, a number of different packages will be installed depending on the software options selected during the installation phase. Once the system is up and running, however, additional software can be installed as needed. Typically, all software that is part of Ubuntu (in other words, software that is not provided by a third-party vendor) is downloaded and installed on the system using the Advanced Package Tool (apt) command. As we have seen in earlier chapters, this typically consists of a command similar to the following being issued at the command prompt:

# apt install apache2

When such a command is issued, the requested software is downloaded from a remote repository and installed on the local system. By default, Ubuntu is configured to download software from a number of different repositories:

•main - Contains the core set of packages that are officially supported, tested and updated by Ubuntu.

•restricted - Proprietary drivers for hardware devices for which no open source equivalent exists.

•universe - Contains packages that are not officially supported by the Ubuntu team at Canonical. These packages are, however, maintained by the Ubuntu community and include packages not available within the main repository.

•multiverse - Packages that may not conform to the open-source licensing terms under which Ubuntu is released due to copyright or other legal issues.

The list of currently enabled repositories on an Ubuntu system is contained within the /etc/apt/sources.list file which can be loaded into an editor to be viewed and modified. The file may be manually loaded into an editor, or edited using a choice of available editors using the following command:

# apt edit-sources

The first few lines of this file usually reference the main and restricted repositories, for example:

deb http://ports.ubuntu.com/ubuntu-ports/ jammy main restricted

In the above example the list is configured to allow packages to be downloaded from the main and restricted repositories. Entries for the universe and multiverse repositories will also be included in the file:

## N.B. software from this repository may not have been tested as

## extensively as that contained in the main release, although it includes

## newer versions of some applications which may provide useful features.

## Also, please note that software in backports WILL NOT receive any review

## or updates from the Ubuntu security team.

deb http://us.archive.ubuntu.com/ubuntu/ lunar-backports main restricted universe multiverse

To disable a repository so that it will no longer be used to download packages, simply comment out the line by prefixing it with a ‘#’ character:

#deb http://ports.ubuntu.com/ubuntu-ports/ lunar-backports main restricted universe multiverse

In addition to the standard repositories there are also many third-party repositories. In the event that you need to use one of these, simply add an entry for it to the sources.list file. One such example is the partners repository, which can be added to the sources.list file as follows:

deb http://archive.canonical.com/ubuntu lunar partner

After making the change, run the following command to commit the changes:

# apt update

11.2 Managing Repositories with Software & Updates

As an alternative to using the command-line, repositories may be configured from within the GNOME desktop environment using the Software & Updates app. To launch this app, press the special key on the keyboard (on Windows keyboards this is the Windows key, on macOS the Command key and on Chromebooks the key displaying a magnifying glass) and enter Software & Updates into the search bar. In the results panel click on the corresponding icon to launch the app. Alternatively, open a terminal window and run the following command:

$ update-manager

When the app loads, click on the Settings button as shown in [Figure 11-1](#Ubuntu_Package_Management.xhtml__idTextAnchor204):

![](image/ubuntu_software_updates.jpg)

Figure 11-1

From the settings screen, enable or disable the required repositories listed under the Downloadable from the Internet heading:

![](image/ubuntu_downloadable_updates.jpg)

Figure 11-2

To enable partner repositories, select the Other Software tab as shown in [Figure 11-3](#Ubuntu_Package_Management.xhtml__idTextAnchor205):

![](image/ubuntu_other_software.jpg)

Figure 11-3

To add other third-party repositories, click on the Add... button and enter the repository information in the resulting dialog:

![](image/ubuntu_add_repo.jpg)

Figure 11-4

11.3 Managing Packages with APT

The apt tool provides a way to perform most package management tasks directly from the command line. In this section we will explore some of the more frequently used apt command-line options.

An Ubuntu system keeps a local copy of the latest package information and, as such, it is recommended that this list be updated before performing any other apt operations as follows:

# apt update

One of the most common apt activities is to perform a package installation:

# apt install package_name

Similarly, an installed package may be removed from the system using the remove option:

# apt remove package_name

When a package is removed this way, configuration files associated with the package will remain on the system. This allows the package to be reinstalled later without losing any custom configuration settings. To remove these files either during the deletion, or even after the deletion as been performed, use the purge option:

# apt purge package_name

To obtain a list of packages available for installation, use apt as follows:

# apt list

Alternatively, to list only those packages which are already installed, use the list option with the --installed flag:

# apt list --installed

To check whether a specific package is already installed on the system, combine the list option with the package name:

# apt list package_name

Use the search option to list all packages that match certain criteria. For example to list all packages that relate to the Apache web server:

# apt search apache

To find which package contains a specific file, use the apt-file command. For example, to list the name of the packages which contain a file named gimp:

# apt-file --package-only list gimp

To view details about a package, run apt with the show option:

# apt show apache2

Typical output from running the above command might read as follows:

Package: apache2

Version: 2.4.52-1ubuntu4.5

Priority: optional

Section: web

Origin: Ubuntu

Maintainer: Ubuntu Developers <ubuntu-devel-discuss@lists.ubuntu.com>

Original-Maintainer: Debian Apache Maintainers <debian-apache@lists.debian.org>

Bugs: https://bugs.launchpad.net/ubuntu/+filebug

Installed-Size: 546 kB

Provides: httpd, httpd-cgi

Pre-Depends: init-system-helpers (>= 1.54~)

Depends: apache2-bin (= 2.4.52-1ubuntu4.5), apache2-data (= 2.4.52-1ubuntu4.5), apache2-utils (= 2.4.52-1ubuntu4.5), lsb-base, mime-support, perl:any, procps

Recommends: ssl-cert

Suggests: apache2-doc, apache2-suexec-pristine | apache2-suexec-custom, www-browser, ufw

Conflicts: apache2.2-bin, apache2.2-common

Replaces: apache2.2-bin, apache2.2-common

Homepage: https://httpd.apache.org/

Task: lamp-server

Download-Size: 97.8 kB

APT-Manual-Installed: yes

APT-Sources: http://us.archive.ubuntu.com/ubuntu jammy-updates/main amd64 Packages

Description: Apache HTTP Server

 The Apache HTTP Server Project's goal is to build a secure, efficient and

extensible HTTP server as standards-compliant open source software. The

 result has long been the number one web server on the Internet.

 .

 Installing this package results in a full installation, including the

 configuration files, init scripts and support scripts.

11.4 Performing Updates

Over the lifetime of both the base operating system and the installed software packages, multiple updates will be issued to resolve problems and add functionality. To manually download and install any pending updates from the command-line, the first step is to update the package information stored on the local system using apt with the update option:

# apt update

Once the package information has been updated, the upgrade can be performed. This will download any updates for currently installed packages from the repositories configured in the sources.list file and install them on the system:

# apt upgrade

As an alternative to the command-line, the system may be updated using the Software & Updates GNOME desktop app. If updates are available the dialog shown in [Figure 11-5](#Ubuntu_Package_Management.xhtml__idTextAnchor208) will appear providing the option to view information about the available updates and to perform the upgrade:

![](image/ubuntu_software_updater1.jpg)

Figure 11-5

11.5 Enabling Automatic Updates

The previous section looked at how to manually install package upgrades. Ubuntu systems may also be configured to install upgrades automatically. This can be configured either from the command-line or from within the Software & Updates tool.

From within the Software & Updates tool, open the Settings screen as outlined previously and click on the Updates tab to display the screen shown in [Figure 11-6](#Ubuntu_Package_Management.xhtml__idTextAnchor210):

![](image/ubuntu_update_schedule.jpg)

Figure 11-6

Select how often the system should check for updates (daily, every other day, weekly, etc.). Next choose what is to be done when updates are available (download only, download and install, or display a notification on the desktop). You can also configure the updater to let you know when new versions of Ubuntu are available.

To configure automatic updates from the command-line, follow these steps:

1. Install the unattended-upgrades package:

# apt install unattended-upgrades

2. Edit the /etc/apt/apt.conf.d/50unattended-upgrades file and locate the following lines:

.

.

        "${distro_id}ESMApps:${distro_codename}-apps-security";

        "${distro_id}ESM:${distro_codename}-infra-security";

// "${distro_id}:${distro_codename}-updates";

// "${distro_id}:${distro_codename}-proposed";

// "${distro_id}:${distro_codename}-backports";

.

.

3. Remove the // comment markers from the repository types for which updates are to be automatically installed.

4. Edit the /etc/apt/apt.conf.d/20auto-upgrades file and declare the frequency (in days) with which the system is to check for updates:

APT::Periodic::Update-Package-Lists "1";

APT::Periodic::Download-Upgradeable-Packages "1";

APT::Periodic::AutocleanInterval "0";

APT::Periodic::Unattended-Upgrade "1";

4. Perform a dry run update to make sure the settings are valid:

# unattended-upgrades --dry-run --debug

A few days after configuring automatic updates, check the log files to confirm that the updates are occurring as planned:

# cat /var/log/unattended-upgrades/unattended-upgrades.log

11.6 Summary

The Ubuntu operating system comprises thousands of software packages downloaded and installed from the main, restricted, universe, multiverse, partner, and third-party repositories.

Software packages are installed using the Advanced Package Tool (apt) or one of several graphical desktop tools and downloaded from the repositories defined within the sources.list file.

In addition to installing and removing software packages, apt may also be used to upgrade those packages with the latest updates. These software upgrades can be performed manually or configured to update automatically.

12\. Ubuntu Snap Package Management

The previous chapter explored the use of the Advanced Packaging Tool (APT) to install and update software packages on an Ubuntu system. In recent years a new package management system called Snap has been under development by the Ubuntu team at Canonical, Ltd. Although there are no official plans to replace APT entirely with Snap, the list of packages that can now be installed as “snaps” continues to grow.

The goal of this chapter is to introduce the Snap system, highlight the key advantages it has over the APT system and to outline how to use the snap command-line tool to install and manage snap -based software packages.

12.1 Managing Software with Snap

The apt tool installs software that is packaged in .deb files. A package installed using apt will often be dependent upon other packages that will also need to be installed in order to function. During an installation, apt will also download and install these additional package dependencies.

Consider a graphics design app which depends on a particular imaging library. During installation, apt will install the graphics app package in addition to the package containing the library on which it depends. Now, assume that the user decides to install a different graphics tool that also relies on the same graphics library. Usually this would not be a problem since the apps will both share the same library, but problems may occur if the two apps rely on different versions of the library. Installing the second app may, therefore, stop the first app from working correctly.

Another limitation of apt and .deb packages is that it is difficult to have two different versions of the same tool or app installed in parallel on a system. A user might, for example, want to keep version 1.0 of the graphics app installed while also trying out the latest beta release of the 2.0 version. After trying out version 2.0, the user may then want to remove version 1.0, leaving the new version installed, a task that would be hard to achieve using apt.

The snap system has been designed specifically to address these types of shortcomings. The snap tool installs .snap packages that contain all of the libraries and assets that are required for the software to function. This avoids the need to install any dependencies as separate, independent packages. Once a snap has been installed it is placed in a self-contained location so that no dependencies are shared with other packages. Our hypothetical graphics apps, for example, each have their own copies of the exact imaging library version used by the app developer which cannot be deleted, replaced with an incompatible version or overwritten by any other package installations.

Of course the use of snaps results in larger package files which leads to longer package download times, slower installation performance and increased disk space usage. That being said, these shortcomings are generally more than outweighed by the advantages of snap packages.

Snap also supports the concept of channels which allow app developers to publish different versions of the same app. Snap channels are the mechanism by which multiple versions of the same software are able to be installed in parallel.

12.2 Basic Snap Commands

Although many software packages are still provided in .deb format and installed using apt, the number of apps and tools now provided in snap format is increasing rapidly. In fact, all of the software listed in the Ubuntu Software tool (outlined previously in the chapter entitled “A Guided Tour of the GNOME 3 Desktop”) are packaged and installed using snap. Snap-based software may also be installed using the snap command-line tool, the basics of which will be covered in this section.

To list the snap packages that are available for a specific category of software, run a command similar to the following:

# snap find "image editor"

Name Version Publisher Notes Summary

gimp 2.10.18 snapcrafters - GNU Image Manipulation Program

paintsupreme-3d 1.0.41 braindistrict - PaintSupreme 3D

.

.

The above command will list all snap packages available for download and installation containing software related in some way to image editing. One such result will be the gimp image editor. Details about the gimp snap can be found as follows:

# snap info gimp

name: gimp

summary: GNU Image Manipulation Program

publisher: Snapcrafters

store-url: https://snapcraft.io/gimp

contact: https://github.com/snapcrafters/gimp/issues

license: GPL-3.0+

description: |

  Whether you are a graphic designer, photographer, illustrator, or scientist, GIMP provides you

with sophisticated tools to get your job done. You can further enhance your productivity with GIMP

  thanks to many customization options and 3rd party plugins.

  This snap is maintained by the Snapcrafters community, and is not necessarily endorsed or

  officially maintained by the upstream developers.

  Upstream Project: https://www.gimp.org/

  snapcraft.yaml Build Definition:

  https://github.com/snapcrafters/gimp/blob/master/snap/snapcraft.yaml

snap-id: KDHYbyuzZukmLhiogKiUksByRhXD2gYV

channels:

  latest/stable: 2.10.30 2022-08-19 (393) 546MB -

  latest/candidate: ↑

  latest/beta: ↑

  latest/edge: 2.10.32 2022-08-23 (399) 547MB -

  preview/stable: –

  preview/candidate: –

  preview/beta: –

  preview/edge: 2.99.10 2022-08-17 (397) 650MB -

The snap find command can also be used to find a specific package by name, together with other packages that provide similar features. Searching for the VLC media player app, for example, also lists similar software packages:

# snap find vlc

Name Version Publisher Notes Summary

vlc 3.0.18 videolan - The ultimate media player

orion-desktop 2.0.0 keshavnrj - Complete torrent client and streamer for Linux Desktop

gridplayer 0.4.3 vzhd1701 - Play multiple videos side-by-side

mjpg-streamer 2.0 ogra - UVC webcam streaming tool

audio-recorder 3.0.5+rev1432+pkg-7b07 brlin - A free audio-recorder for Linux (EXTREMELY BUGGY)

ustreamer 5.41 pgentili - Lightweight and fast MJPEG-HTTP streamer

The snap list command-line option can be used to obtain a list of snap packages that are already installed on a system:

# snap list

Name Version Rev Tracking Publisher Notes

bare 1.0 5 latest/stable canonical base

canonical-livepatch 10.6.0 235 latest/stable canonical -

core 16-2.59.5 15511 latest/stable canonical core

core20 20230622 1974 latest/stable canonical base

core22 20230703 817 latest/stable canonical base

firefox 115.0-2 2850 latest/stable/… mozilla -

gnome-3-38-2004 0+git.efb213a 143 latest/stable/… canonical -

gnome-42-2204 0+git.ff35a85 120 latest/stable canonical -

.

.

To install a snap package (for example, to install the Remmina remote desktop tool), run the snap command with the install option followed by the name of the package to be installed:

# snap install remmina

To remove a snap package, simply specify the package name when running snap with the remove option:

# snap remove remmina

12.3 Working with Snap Channels

If no channel is specified when performing an installation, snap will default to the stable channel. This ensures that the latest reliable version of the software is installed. To perform the installation from a different channel, begin by identifying the channels that are currently available for the required package using the snap info option:

# snap info remmina

name: remmina

summary: Remote Desktop Client

.

.

channels:

  latest/stable: v1.4.29 2022-12-20 (5599) 146MB -

  latest/candidate: ↑

  latest/beta: ↑

  latest/edge: v1.4.31+git102.f5485fcfd 2023-07-17 (5925) 144MB -

From the above output we can see that while the stable version of the Remmina app is v1.4.3+git13.688f5f75 a more recent version is available in the edge channel.

Of course the candidate, beta and edge channels provide access to the software in increasingly unstable forms (referred to as risk level), but if you would like to try out an early access version of upcoming features of a package, install from a higher risk channel. For example:

# snap install --channel=edge remmina

The channel selection may also be abbreviated to --stable, --candidate, --beta or --edge, for example:

# snap install --edge remmina

If the package is already installed, the risk level can be changed using the switch option:

# snap switch channel=edge remmina

This will change the channel that snap is tracking for the specified package. The current channel being tracked for a package can be identified using the snap info command:

# snap info remmina

name: remmina

.

.

tracking: latest/edge

.

.

Simply running a snap switch command will not immediately refresh the package to use the new channel. To understand how this works, it will help to explore the snap refresh schedule.

12.4 Snap Refresh Schedule

The snap system includes a background service named snapd which is responsible for refreshing installed snaps based on the channels that they are tracking. By default, snapd performs refresh operations at regular intervals (typically four times a day). To identify when the last refresh was performed, and the next is due, run the following command:

# snap refresh --time

timer: 00:00~24:00/4

last: today at 07:23 EDT

next: today at 14:25 EDT

The above output also includes timer information which indicates that the refresh will be performed four times within each 24-hour period:

.

.

timer: 00:00~24:00/4

.

.

The snap command can also be used to force a refresh of all installed snap packages as follows:

# snap refresh

Alternatively, to refresh a specific package:

# snap refresh remmina

To switch a package to a different channel without having to wait for the next snapd service refresh, simply run the snap refresh command as follows, specifying the target channel:

# snap refresh remmina --channel=edge

The snap system also has a set of four properties that may be modified to adjust the refresh schedule used by snapd:

•refresh.timer: Stores the current refresh schedule and frequency.

•refresh.hold: Used to delay refresh operations until the specified day and time (in RFC 3339 format).

•refresh.metered: Pauses refresh operations when network access is via a metered connection (such as a mobile data connection).

•refresh.retain: Used to configure the number of revisions of each snap installation that are to be retained.

For example, to schedule the refresh to occur on weekdays between 1:00am and 2:00am:

# snap set system refresh.timer=mon-fri,1:00-2:00

Similarly, the following command will configure refreshes twice every day to occur between the hours of 6:00am and 7:00am, and 10:00pm and 11:00pm:

# snap set system refresh.timer=6:00-7:00,22:00-23:00

A full explanation of the timer format and syntax can be found online at the following URL:

[https://snapcraft.io/docs/timer-string-format](https://snapcraft.io/docs/timer-string-format)

After making a change to the timer, be sure to check the settings as follows:

# snap refresh --time

timer: mon-fri,1:00-2:00

last: today at 07:23 EDT

next: tomorrow at 01:00 EDT

To pause refreshes, the date and time at which refreshing is to resume must be specified using the RFC 3339 format, details of which can be found at the following URL:

[https://tools.ietf.org/html/rfc3339](https://tools.ietf.org/html/rfc3339)

In summary, the date and time should use the following format:

YYYY-MM-DDTHH:MM.SS<UTC offset>

For example, to specify a hold until October 12, 2020 at 3:20am for a system located in New York, the date and time would be formatted as follows:

2020-10-12T03:20:50.0-05:00

Note that since New York uses Eastern Standard Time (EST) it has a -5 hour offset from Coordinated Universal Time (UTC-5:00). Having formatted the date and time, the following command would be used to set the hold:

# snap set system refresh.hold="2020-10-12T03:20:50.0-05:00"

To check the current hold setting, use snap with the system get option:

# snap get system refresh.hold

2020-10-12T03:20:50.0-04:00

To remove the hold, simply assign a null value to the property:

# snap set system refresh.hold=null

The refresh.retain property can be set to any value between 0 and 20, for example:

# snap set system refresh.retain=10

Finally, to pause refresh updates while the system is on a metered connection, set the refresh.metered property to hold as follows:

# snap set system refresh.metered=hold

As with the hold property, disable this setting by assigning a null value to the property:

# snap set system refresh.metered=null

12.5 Snap Services

It is worth noting that some snap packages include their own services, which run in the background when the package is installed (much like the systemd services described in the chapter entitled “Managing Ubuntu systemd Units”). To obtain a list of snap services that are currently running on a system, execute the snap command with the services option:

# snap services

Service Startup Current Notes

remmina.ssh-agent enabled active -

The above output indicated that the Remmina Secure Shell agent snap service is currently enabled and active. To stop or stop a service the following snap commands can be used:

# snap start remmina.ssh-agent

# snap stop remmina.ssh-agent

Similarly the snap enable and disable options may to used to control whether or not a service starts automatically on system startup:

# snap enable remmina.ssh-agent

# snap disable remmina.ssh-agent

If the snap service generates a log file, that file can be viewed as follows:

# snap logs remmina.ssh-agent

It is also still possible to manage snap services using the systemctl command. This usually involves prefixing the service name with “snap.”. For example:

# systemctl status snap.remmina.ssh-agent

12.6 Summary

Until recently, all Ubuntu software packages were stored in .deb files and installed using the Advanced Packaging Tool (APT). An increasing number of packages are now available for installation using Snap, a package management system developed by Canonical, Ltd. Unlike apt packages, snap bundles all of the dependencies for a package into a single .snap file. This ensures that the software package is self-contained with its own copy of all of the libraries and assets needed to run. This avoids the potential conflicts of packages relying on different versions of the same shared assets and libraries. The Snap system also allows different versions of the same packages to be installed in parallel. All of the software listed in the Ubuntu Software tool are supplied as snap packages. In addition, snap can be used to install, remove and manage packages from the command-line.

13\. Ubuntu 23.04 Network Management

It is difficult to envisage an Ubuntu system that does not have at least one network connection, and harder still to imagine how such an isolated system could be of much practical use. The simple fact is that Ubuntu is designed to provide enterprise-level services over network and internet connections. Therefore, a crucial part of learning how to administer an Ubuntu system involves learning how to configure and manage the network interfaces installed on the system.

This chapter provides an overview of network management on Ubuntu, including the NetworkManager service and tools and some other useful utilities.

13.1 An Introduction to NetworkManager

NetworkManager is a service and set of tools designed specifically to make it easier to manage the networking configuration on Linux systems and is the default network management service on Ubuntu.

In addition to a service that runs in the background, NetworkManager also includes the following tools:

•nmcli - A tool for working with NetworkManager via the command line. This tool is useful when access to a graphical environment is unavailable and can also be used within scripts to make network configuration changes.

•nmtui - A basic text-based user interface for managing NetworkManager. This tool can be run within any terminal window and allows changes to be made by making menu selections and entering data. While helpful in performing basic tasks, nmtui lacks many of the features provided by the nmcli tool.

•nm-connection-editor - A complete graphical management tool providing access to most NetworkManager configuration options.

•GNOME Settings - The Network screen of the GNOME desktop Settings application allows basic network management tasks to be performed.

•Cockpit Network Settings - The Network screen of the Cockpit web interface allows a range of network management tasks to be performed.

Although there are several ways to manage the network environment on an Ubuntu system, this chapter will focus on the nmcli command. While the graphical tools are certainly helpful when you have access to a desktop environment or Cockpit has been enabled, understanding the command-line interface is essential for situations where a command prompt is all that is available. Also, the graphical tools (Cockpit included) only include some of the capabilities of the nmcli tool. Finally, once you are familiar with NetworkManager and nmcli, those skills will translate easily when using the more intuitive tool options. The same cannot be said of the graphical tool options. It is harder to use nmcli if, for example, you have only ever used nm-connection-editor.

13.2 Installing and Enabling NetworkManager

NetworkManager should be installed by default for most Ubuntu installations. Use the apt  command to find out if it needs to be installed:

# apt -qq list network-manager

network-manager/lunar,now 1.42.4-1ubuntu2 amd64 [installed,automatic]

If necessary, install the package as follows:

# apt install network-manager

Once the package is installed, the NetworkManager daemon will need to be enabled so that it starts each time the system boots:

# systemctl enable NetworkManager

Finally, start the service running and check the status to verify that the launch was successful:

# systemctl start NetworkManager

# systemctl status NetworkManager

● NetworkManager.service - Network Manager

     Loaded: loaded (/lib/systemd/system/NetworkManager.service; enabled; vendor preset: enabled)

     Active: active (running) since Sun 2023-07-16 12:46:48 EDT; 24h ago

       Docs: man:NetworkManager(8)

   Main PID: 725 (NetworkManager)

      Tasks: 3 (limit: 4352)

     Memory: 11.9M

        CPU: 5.018s

     CGroup: /system.slice/NetworkManager.service

             └─725 /usr/sbin/NetworkManager --no-daemon

13.3 Basic nmcli Commands

The nmcli tool will have been installed as part of the NetworkManager package and can be executed from the command line using the following syntax:

# nmcli [Options] Object {Command | help}

In the above syntax, Object will be one of general, networking, radio, connection, monitor, device, or agent, which can be abbreviated to a few letters of the word (for example, con, or even just the letter c, for connection). For example, all of the following commands will output help information relating to the device object:

# nmcli device help

# nmcli dev help

# nmcli d help

To check the overall status of NetworkManager on the system, use the following command:

# nmcli general status

STATE CONNECTIVITY WIFI-HW WIFI WWAN-HW WWAN

connected full enabled enabled enabled enabled

To check the status of the devices installed on a system, the following command can be used:

# nmcli dev status

DEVICE TYPE STATE CONNECTION

eno1 ethernet connected eno1

wlp0s26u1u2 wifi connected zoneone

virbr0 bridge connected virbr0

lo loopback unmanaged --

virbr0-nic tun unmanaged --

The output may also be modified by using the -p (pretty) option to make the output more human-friendly:

# nmcli -p dev status

=====================

  Status of devices

=====================

DEVICE TYPE STATE CONNECTION

-------------------------------------------------------------------

eno1 ethernet connected eno1

wlp0s26u1u2 wifi connected zoneone

virbr0 bridge connected virbr0

lo loopback unmanaged --

virbr0-nic tun unmanaged --

Conversely, the -t option may be used to make the output more terse and suitable for automated processing:

# nmcli -t dev status

eno1:ethernet:connected:eno1

wlp0s26u1u2:wifi:connected:emilyzone

virbr0:bridge:connected:virbr0

lo:loopback:unmanaged:

virbr0-nic:tun:unmanaged:

The status output shows that the system has two physical devices installed, one Ethernet and the other a WiFi device.

The bridge (virbr) entries are virtual devices used to provide networking for virtual machines (the topic of virtualization will be covered starting with the chapter entitled [“An Overview of Virtualization Techniques”](#Virtualization_Overview.xhtml__idTextAnchor361)). Finally, the loopback interface is a special virtual device that allows the system to communicate with itself and is typically used to perform network diagnostics.

When working with NetworkManager, it is important to understand the difference between a device and a connection. As described above, a device is either a physical or virtual network device, while a connection is a network configuration that the device connects to.

The following command displays information about the connections configured on the system:

# nmcli con show

NAME UUID TYPE DEVICE

zoneone 2abecafa-4ea2-47f6-b20f-4fb0c0fd5e94 wifi wlp0s26u1u2

eno1 99d40009-6bb1-4182-baad-a103941c90ff ethernet eno1

virbr0 e13e9552-1765-42d1-b739-ff981668fbee bridge virbr0

zonetwo f940a2d1-8c18-4a9e-bf29-817702429b8a wifi --

zonethree fd65c5e5-3e92-4e9e-b924-1b0b07b70032 wifi --

The above output shows that the WiFi device (wlp0s26u1u2) is connected to a wireless network named zoneone while the Ethernet device (eno1) is connected to a connection named eno1\. In addition to zoneone, NetworkManager has also listed two other WiFi connections named zonetwo and zonethree, neither of which currently has a device connected.

To find out the IP address allocated to a connection, the ip tool can be used with the address option:

# ip address

The above command can also be abbreviated:

# ip a

.

.

3: wlp0s26u1u2: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000

    link/ether 74:da:38:ee:be:50 brd ff:ff:ff:ff:ff:ff

    inet 192.168.1.121/24 brd 192.168.1.255 scope global dynamic noprefixroute wlp0s26u1u2

       valid_lft 57584sec preferred_lft 57584sec

.

.

The ip command will output information for all the devices detected on the system. For example, the above output shows that the WiFi device has been assigned an IP address of 192.168.1.121.

If we only wanted to list active connections, the nmcli command could have been used with the -a option:

# nmcli con show -a

NAME UUID TYPE DEVICE

zoneone 2abecafa-4ea2-47f6-b20f-4fb0c0fd5e94 wifi wlp0s26u1u2

eno1 99d40009-6bb1-4182-baad-a103941c90ff ethernet eno1

virbr0 e13e9552-1765-42d1-b739-ff981668fbee bridge virbr0

To switch the WiFi device connection from zoneone to zonetwo, we can run the following command:

# nmcli device wifi connect zonetwo -ask

Password:

The -ask flag causes nmcli to prompt the user to enter the password for the WiFi network. To include the WiFi password on the command line (particularly useful if the command is being executed in a script), use the password option:

# nmcli device wifi connect zonetwo password <password here>

The nmcli tool may also be used to scan for available WiFi networks as follows:

# nmcli device wifi list

IN-USE SSID MODE CHAN RATE SIGNAL BARS SECURITY

        zoneone Infra 6 195 Mbit/s 80 WPA2

* zonetwo Infra 11 130 Mbit/s 74 WPA1 WPA2

A currently active connection can be deactivated as follows:

# nmcli con down <connection name>

Similarly, an inactive connection can be brought back up at any time:

# nmcli con up <connection name>

When a connection is brought down, NetworkManager automatically searches for another connection, activates it, and assigns it to the device to which the previous connection was established. To prevent a connection from being used in this situation, disable the autoconnect option as follows:

# nmcli con mod <connection name> connection.autoconnect no

The following command may be used to obtain additional information about a specific connection. This includes the current values for all the connection properties:

# nmcli con show eno1

connection.id: eno1

connection.uuid: 99d40009-6bb1-4182-baad-a103941c90ff

connection.stable-id: --

connection.type: 802-3-ethernet

connection.interface-name: eno1

connection.autoconnect: yes

connection.autoconnect-priority: 0

connection.autoconnect-retries: -1 (default)

connection.multi-connect: 0 (default)

connection.auth-retries: -1

connection.timestamp: 1554833695

connection.read-only: no

connection.permissions: --

connection.zone: --

connection.master: --

connection.slave-type: --

connection.autoconnect-slaves: -1 (default)

.

.

All of these properties can be modified using nmcli with the modify option using the following syntax:

# nmcli con mod <connection name> connection.<property name> <setting>

13.4 Working with Connection Profiles

So far, we have explored using connections without explaining how a connection is configured. The configuration of a connection is referred to as a connection profile and is stored in a file located in the /etc/NetworkManager/system-connections directory, the contents of which might read as follows:

# ls /etc/NetworkManager/system-connections

zoneone.nmconnection eno1.nmconnection

zonethree.nmconnection zonetwo.nmconnection

Consider, for example, the contents of the eno1.nmconnection file:

id=eno1

uuid=efc69a99-17a3-3636-b68f-bfcc56a73844

type=ethernet

autoconnect-priority=-999

interface-name=eno1

timestamp=1679678184

[ethernet]

[ipv4]

method=auto

[ipv6]

addr-gen-mode=eui64

method=auto

[proxy]

The file contains basic information about the connection, including the type (Ethernet) of the device to which it is currently assigned (eno1) and the fact that the connection is to be automatically activated on system boot with an IP address obtained using DHCP (auto). Changes to the connection profile can be implemented by modifying this file and instructing nmcli to reload the connection configuration files:

# nmcli con reload

New connection profiles can also be created manually or generated automatically by nmcli. For example, assume a new network device has been installed on the system. When this happens, the NetworkManager service will detect the new hardware and create a device for it. In the example below, the new device has been assigned the name eno2:

# nmcli dev status

DEVICE TYPE STATE CONNECTION

en01 ethernet connected eno1

eno2 ethernet connected Wired connection 1

NetworkManager automatically detected the device, activated it, and assigned it to a connection named “Wired connection 1”. This is a default connection over which we have no configuration control because there is no interface configuration file for it in /etc/NetworkManager/system-connections. Therefore, the next steps are to delete the “Wired connection 1” connection and use nmcli to create a new connection and assign it to the device. The command to delete a connection is as follows:

# nmcli con delete "Wired connection 1"

Next, nmcli can be used to create a new connection profile configured either with a static IP address or a dynamic IP address obtained from a DHCP server. To create a dynamic connection profile named dyn_ip, the following command would be used:

# nmcli connection add type ethernet con-name dyn_ip ifname eno2

Connection 'dyn_ip' (160d9e10-bbc8-439a-9c47-a2ec52990472) successfully added.

To create a new connection profile without locking it to a specific device, simply omit the ifname option in the command:

# nmcli connection add type ethernet con-name dyn_ip

After creating the connection, a file named dyn_ip.nmconnection will be added to the /etc/NetworkManager/system-connections directory.

Alternatively, to create a connection named static_ip assigned a static IP address (in this case 192.168.1.200) the following command would be used:

# nmcli con add type ethernet con-name static_ip ifname eno0 ip4 192.168.1.200/24 gw4 192.168.1.1

Connection 'static_ip' (3fccafb3-e761-4271-b310-ad0f28ee8606) successfully added.

The corresponding static_ip.nmconnection file will read as follows:

[connection]

id=static_ip

uuid=41eca181-381c-4d12-b6c9-30446d4e29d1

type=ethernet

interface-name=eno0

[ethernet]

[ipv4]

address1=192.168.1.200/24,192.168.1.1

method=manual

[ipv6]

addr-gen-mode=default

method=auto

[proxy]

The command to add a new connection may be altered slightly to assign both IPv4 and IPv6 static addresses:

# nmcli con add type ethernet con-name static_ip ifname eno0 ip4 192.168.1.200/24 gw4 192.168.1.1 gw4 192.168.1.1 ip6 cabf::4532 gw6 2010:dfa::1

13.5 Interactive Editing

In addition to using nmcli with command-line options, the tool also includes an interactive mode that can be used to create and modify connection profiles. The following transcript, for example, shows interactive mode being used to create a new Ethernet connection named demo_con:

# nmcli con edit

Valid connection types: 6lowpan, 802-11-olpc-mesh (olpc-mesh), 802-11-wireless (wifi), 802-3-ethernet (ethernet), adsl, bluetooth, bond, bridge, cdma, dummy, generic, gsm, infiniband, ip-tunnel, macsec, macvlan, ovs-bridge, ovs-interface, ovs-port, pppoe, team, tun, vlan, vpn, vxlan, wimax, wpan, bond-slave, bridge-slave, team-slave

Enter connection type: ethernet

===| nmcli interactive connection editor |===

Adding a new '802-3-ethernet' connection

Type 'help' or '?' for available commands.

Type 'print' to show all the connection properties.

Type 'describe [<setting>.<prop>]' for detailed property description.

You may edit the following settings: connection, 802-3-ethernet (ethernet), 802-1x, dcb, sriov, ethtool, match, ipv4, ipv6, tc, proxy

nmcli> set connection.id demo_con

nmcli> set connection.interface eno1

nmcli> set connection.autoconnect yes

nmcli> set ipv4.method auto

nmcli> set 802-3-ethernet.mtu auto

nmcli> set ipv6.method auto

nmcli> save

Saving the connection with 'autoconnect=yes'. That might result in an immediate activation of the connection.

Do you still want to save? (yes/no) [yes] yes

Connection 'demo_con' (cb837408-6c6f-4572-9548-4932f88b9275) successfully saved.

nmcli> quit

The following transcript, on the other hand, modifies the previously created static_ip connection profile to use a different static IP address than the one originally specified:

# nmcli con edit static_ip

===| nmcli interactive connection editor |===

Editing existing '802-3-ethernet' connection: 'static_ip'

Type 'help' or '?' for available commands.

Type 'print' to show all the connection properties.

Type 'describe [<setting>.<prop>]' for detailed property description.

You may edit the following settings: connection, 802-3-ethernet (ethernet), 802-1x, dcb, sriov, ethtool, match, ipv4, ipv6, tc, proxy

nmcli> print ipv4.addresses

ipv4.addresses: 192.168.1.200/24

nmcli> set ipv4.addresses 192.168.1.201/24

nmcli> save

Connection 'static_ip' (3fccafb3-e761-4271-b310-ad0f28ee8606) successfully updated.

nmcli> quit

After modifying an existing connection, remember to instruct NetworkManager to reload the configuration profiles:

# nmcli con reload

When using interactive mode, it is useful to know that an extensive built-in help system is available to learn how to use the tool. The help topics can be accessed by typing help or ? at the nmcli > prompt:

nmcli> ?

------------------------------------------------------------------------------

---[ Main menu ]---

goto [<setting> | <prop>] :: go to a setting or property

remove <setting>[.<prop>] | <prop> :: remove setting or reset property value

set [<setting>.<prop> <value>] :: set property value

describe [<setting>.<prop>] :: describe property

print [all | <setting>[.<prop>]] :: print the connection

verify [all | fix] :: verify the connection

save [persistent|temporary] :: save the connection

activate [<ifname>] [/<ap>|<nsp>] :: activate the connection

back :: go one level up (back)

help/? [<command>] :: print this help

nmcli <conf-option> <value> :: nmcli configuration

quit :: exit nmcli

------------------------------------------------------------------------------

13.6 Configuring NetworkManager Permissions

In addition to making it easier to manage networks on Ubuntu, NetworkManager also allows permissions to be specified for connections. The following command, for example, restricts a connection profile to root and user accounts named john and caitlyn:

# nmcli con mod static_ip connection.permissions user:root,john,caitlyn

Once NetworkManager has reloaded the connection profiles, the static_ip connection will only be active and accessible to other users when at least one designated user is logged in to an active session on the system. As soon as the last of these users logs out, the connection will go down and remain inactive until one of the users signs back in.

In addition, only users with permission can change the connection status or configuration.

13.7 Summary

The NetworkManager service handles network management on Ubuntu. NetworkManager views a network as consisting of network interface devices and connections. A network device can be a physical Ethernet or WiFi device or a virtual device used by a virtual machine guest. Connections represent the network to which the devices connect and are configured by connection profiles. A configuration profile will, among other settings, define whether the connection has a static or dynamic IP address, the IP address of any gateway used by the network, and whether or not the connection should be established automatically each time the system starts up.

NetworkManager can be administered using several tools, including the nmcli and nmtui command-line tools, the nm-connection-editor graphical tool, and the network settings section of the Cockpit web interface. In general, the nmcli command-line tool provides the most features and flexibility.

14. Ubuntu 23.04 Firewall Basics

A firewall is a vital component in protecting an individual computer system or network of computers from external attacks (typically from an internet connection). Any computer connected directly to an internet connection should ideally run a firewall to protect against malicious activity. Similarly, any internal network must have some form of firewall between it and an external internet connection.

Ubuntu is supplied with powerful firewall technology known as iptables built-in. Entire books can, and indeed have, been written about configuring iptables. If you would like to learn about iptables, we recommend the following:

[https://www.linuxtopia.org/Linux_Firewall_iptables/index.html](https://www.linuxtopia.org/Linux_Firewall_iptables/index.html)

This chapter will cover some basic concepts of firewalls, TCP/IP ports, and services. Firewall configuration on Ubuntu will be covered in the chapters entitled “Ubuntu 22.04 Firewall Configuration with firewalld” and [“Using gufw and ufw to Configure an Ubuntu Firewall”](#Ubuntu_ufw_Firewall.xhtml__idTextAnchor240).

14.1 Understanding Ports and Services

The predominant network communications protocol in use these days is TCP/IP. It is the protocol used by the internet and, as such, has swept away most of the formerly popular protocols used for local area networks (LANs).

TCP/IP defines a total of 65,535 ports, of which 1023 are considered well-known ports. It is essential to understand that these are not physical ports into which network cables are connected but rather virtual ports on each network connection which can be used by applications and services to communicate over a TCP/IP network connection. In reality, the number of ports used by popular network clients and services comprises an even smaller subset of the well-known group of ports.

An operating system can provide several different TCP/IP services. A comprehensive list of such services is provided in the table at the end of this chapter. Still, such services include HTTPS for running a secure web server, FTP for allowing file transfers, SSH for providing secure remote login access and file transfer, and SMTP for transporting email messages. Each service is, in turn, assigned to a standard TCP/IP port. For example, HTTPS is assigned to port 443, while SSH communication occurs on port 22.

14.2 Securing Ports and Services

A large part of securing servers involves defining roles and, based on the roles, defining which services and ports should be enabled. For example, a server that acts solely as a web server should only run the HTTPS service (in addition to perhaps SSH for remote administration access). All other services should be disabled and, ideally, removed entirely from the operating system (thereby making it harder for an intruder to re-enable the service).

Securing a system involves removing any unnecessary services from the operating system and ensuring that the ports associated with the non-essential services are blocked using a firewall. The rules that define which ports are accessible and under what circumstances are determined using iptables.

Many operating systems are installed with several services installed and activated by default. Before installing a new operating system, the installation must be carefully planned. This planning involves deciding which services are not required and identifying which services have been installed and enabled by default. Deployment of new operating system installations should never be rushed. The fewer services and open ports available on a system, the smaller the surface area and opportunities for attackers.

14.3 Ubuntu Services and iptables Rules

By default, a newly installed Ubuntu system has no iptables rules defined to restrict access to ports. The following command may be executed in a terminal window to view the current iptables settings:

# iptables -L

Chain INPUT (policy ACCEPT)

target prot opt source destination

Chain FORWARD (policy ACCEPT)

target prot opt source destination

Chain OUTPUT (policy ACCEPT)

target prot opt source destination

As illustrated in the above output, no rules are currently defined. While this may appear to be an unsafe configuration, it is essential to remember that a newly installed Ubuntu system also has few services running by default, making the ports useless to a potential attacker. For example, accessing a web server on a newly installed Ubuntu system is impossible because no web server services are installed or running by default. Once services begin to be activated on the system, it will be important to establish a firewall strategy by defining iptables rules.

Several methods are available for defining iptables rules, including using command line tools and configuration files. For example, to block access to port 25 (used by the SMTP mail transfer protocol) from IP address 192.168.2.76, the following command could be issued in a terminal window:

# iptables -A INPUT -s 192.168.2.76 -p tcp --destination-port 25 -j DROP

If we now check the current rules, we will see that this one is currently listed:

# iptables -L

Chain INPUT (policy ACCEPT)

target prot opt source destination

DROP tcp -- 192.168.2.76 anywhere tcp dpt:smtp

Chain FORWARD (policy ACCEPT)

target prot opt source destination

Chain OUTPUT (policy ACCEPT)

target prot opt source destination

The rule may subsequently be removed as follows:

# iptables -D INPUT -s 192.168.2.76 -p tcp --destination-port 25 -j DROP

Given the complexity of iptables it is unsurprising that several user-friendly configuration tools have been created to ease the rule creation process. One such tool is the firewall-cmd command-line tool which will be covered in the chapter “Ubuntu 22.04 Firewall Configuration with firewalld”.

14.4 Well-Known Ports and Services

Before moving on to cover more complex firewall rules, it is first worth taking time to outline some of the key services that can be provided by a Ubuntu system, together with the corresponding port numbers:

| Port | Assignment | Description |
| 20 | FTP | File Transfer Protocol (Data) - The File Transfer protocol provides a mechanism for transferring specific files between network-connected computer systems. The transfer is typically performed using the ftp client. Most modern web browsers can also browse and download files on a remote FTP server. FTP uses TCP (rather than UDP) to transfer files, which is considered a highly reliable transport mechanism. FTP does not encrypt data and is not considered a secure file transfer protocol. Secure Copy Protocol (SCP) and Secure File Transfer Protocol (SFTP) are strongly recommended in place of FTP. |
| 21 | FTP | File Transfer (Control) - Traditionally, FTP has two ports assigned (port 20 and port 21). Port 20 was initially considered the data transfer port, while port 21 was assigned to communicate control information. However, in modern implementations, port 20 is rarely used, with all communication taking place on port 21. |
| 22 | SSH | Secure Shell - The Secure Shell provides a safe, encrypted, remote login session to a host over a TCP/IP network. The original mechanism for remote access was the Telnet protocol. However, because Telnet transmits data in plain text, its use is strongly discouraged in favor of the secure shell, which encrypts all communications, including login and password credentials. SSH also provides the mechanism by which files can be securely transferred using the Secure Copy Protocol (SCP) and is also the basis for the Secure File Transfer Protocol (SFTP). SSH also replaces both the rsh and rlogin clients. |
| 23 | Telnet | Telnet - Telnet is a terminal emulation protocol that can log into a remote system over a TCP/IP connection. The access is text-based, allowing the user to type into a command prompt on the remote host, and text displayed by the remote host is displayed on the local Telnet client. Telnet encrypts neither the password nor the text communicated between the client and server. As such, the use of telnet is strongly discouraged. Most modern systems will have port 23 closed and the telnet service disabled to prevent its use. SSH should be used in place of Telnet. |
| 25 | SMTP | Simple Mail Transfer Protocol - SMTP defines the mechanism by which email messages are sent from one network host to another. SMTP is a straightforward protocol requiring the mail service to always be available at the receiving host. Typically the receiving host will store incoming messages in a spool for subsequent access by the recipient using the POP3 or IMAP protocols. In addition, SMTP uses the TCP transport protocol to ensure error-free message delivery. |
| 53 | DNS | Domain Name Server - The service used by TCP/IP networks to translate host names and Fully Qualified Domain Names (FQDN) to IP addresses. |
| 69 | TFTP | Trivial File Transfer Protocol - TFTP is a stripped-down version of the File Transfer Protocol (FTP). It has a reduced command set and lacks authentication. The most significant feature of TFTP is that it uses UDP to transfer data. This results in high-speed transfer speeds but, consequently, lacks data reliability. TFTP is typically used in network-based booting for diskless workstations. |
| 80 | HTTP | Hypertext Text Transfer Protocol - HTTP is used to download text, graphics, and multimedia from a web server to a web browser. It defines the command and control mechanism between the browser and server, defining client requests and server responses. HTTP is based on the TCP transport protocol and, as such, is a connection-oriented protocol. |
| 110 | POP3 | Post Office Protocol - The POP3 protocol is a mechanism for storing and retrieving incoming email messages from a server. In most corporate environments, incoming email is stored on an email server and then downloaded to an email client running on the user’s desktop or laptop when the user checks email. However, POP3 downloads all new messages to the client and does not allow the user to choose which messages to download, view headers, or download only parts of messages. For this reason, the IMAP protocol is increasingly being used in place of POP3\. |
| 119 | NNTP | Network News Transfer Protocol - The protocol responsible for posting and retrieving messages to and from Usenet News Servers (i.e., newsgroups and discussion forums hosted on remote servers). NNTP operates at the Application layer of the OSI stack and uses TCP to ensure error-free message retrieval and transmission. |
| 123 | NTP | Network Time Protocol - A protocol designed to synchronize computer clocks with an external time source. Using this protocol, an operating system or application can request the current time from a remote NTP server. The remote NTP server is usually based on the time provided by a nuclear clock. NTP is useful for ensuring that all systems in a network are set to the same, accurate time of day. This is of particular importance in security situations when, for example, the time a file was accessed or modified on a client or server is in question. |
| 143 | IMAP4 | Internet Message Access Protocol, Version 4 - IMAP4 is an advanced and secure email retrieval protocol. IMAP is similar to POP3, allowing users to access email messages stored on an email server. However, IMAP includes many additional features, such as the ability to selectively download messages, view message headers, search messages, and download part of a message. In addition, IMAP4 uses authentication and fully supports Kerberos authentication. |
| 161 | SNMP | Simple Network Management Protocol - Provides a mechanism whereby network administrators can collect information about network devices (such as hubs, bridges, routers, and switches). The SNMP protocol enables agents running on network devices to communicate their status to a central manager and, in turn, allows the manager to send new configuration parameters to the device agent. The agents can further be configured to notify the manager when certain events, known as traps, occur. SNMP uses UDP to send and receive data. |
| 443 | HTTPS | Hypertext Transfer Protocol Secure - The standard HTTP (non-secure) protocol transfers data in clear text (i.e., with no encryption and visible to anyone who might intercept the traffic). While this is acceptable for most web browsing purposes, it poses a severe security risk when confidential information such as credit card details needs to be transmitted from the browser to the web server. HTTPS addresses this using the Secure Sockets Layer (SSL) to send encrypted data between the client and server. |
| 2049 | NFS | Network File System - Originally developed by Sun Microsystems and subsequently widely adopted throughout the industry, NFS allows a file system on a remote system to be accessed over the network by another system as if the file system were on a local disk drive. NFS is widely used on UNIX and LINUX-based systems. Later versions of Microsoft Windows can also access NFS-shared file systems on UNIX and LINUX-based systems. |

Table 14-1

14.5 Summary

A newly installed Ubuntu system is generally considered secure due to the absence of services running on the system ports. Once the system begins to be configured for use, however, it is important to ensure that it is protected by implementing a firewall. When configuring firewalls, it is important to understand the various ports and the corresponding services.

Several firewall options are available, the most basic being the command-line configuration of the iptables firewall interface. More intuitive and advanced options are available via firewalld, which will be covered in the next chapter.

15\. Using gufw and ufw to Configure an Ubuntu Firewall

In the previous chapter, we looked at ports and services on an Ubuntu system. We also briefly looked at iptables firewall rules on Ubuntu including the creation of a few very simple rules from the command line. In this chapter, we will look at a more user-friendly approach to iptables configuration using two tools named gufw and ufw. As we will see, gufw and ufw provide a high level of control over both inbound and outbound network traffic and connections without the need to understand the lower-level iptables syntax.

15.1 An Overview of gufw and ufw

Included with Ubuntu is a package called ufw which is an acronym for Uncomplicated Firewall. This package provides a command line interface for managing and configuring rules for the Netfilter iptables-based firewall. The gufw tool provides a user-friendly graphical interface to ufw designed to make firewall management possible without the need to issue ufw commands at the command line.

15.2 Installing gufw on Ubuntu

Whilst ufw is installed on Ubuntu by default, the gufw package is not. To install gufw, therefore, open a Terminal window (Ctrl-Alt-T) and enter the following command at the resulting prompt:

# apt install gufw

15.3 Running and Enabling gufw

Once installed, launch gufw by pressing Alt-F2 within the GNOME desktop and entering gufw into the Run a command text box. When invoked for the first time, it is likely that the firewall will be disabled, as illustrated in [Figure 15-1](#Ubuntu_ufw_Firewall.xhtml__idTextAnchor245).

To enable the firewall, move the Status switch (A) to the on position. By default, the main panel (D) will be displaying the gufw home page containing some basic information about the tool. Selecting options from the row of buttons (C) will change the information displayed in the panel. For example, select the Rules button to add, remove and view rules.

The gufw tool is provided with a small set of pre-configured profiles for work, home, and public environments. To change the profile and view the settings, select the profile from the menu (B). To modify an existing profile, select it from the menu and use the Incoming and Outgoing menus to change the selections. To configure specific rules, display the Rules screen and add, remove, and modify rules as required. These will then be applied to the currently selected profile.

![](image/ubuntu_gufw.jpg)

Figure 15-1

The currently selected profile dictates how the firewall handles traffic in the absence of any specific policy rules. By default, the Home profile, for example, is configured to deny all incoming traffic and allow all outgoing traffic. These default policy settings are changed using the Incoming: and Outgoing: menus (E).

Exceptions to the default policy are defined through the creation of additional rules. With the Home profile denying incoming traffic, for example, rules would need to be added to enable certain acceptable types of incoming connections. Such rules are referred to in the security community as a whitelist.

If, on the other hand, the incoming policy was changed to Allow all traffic, then all incoming traffic would be permitted unless rules were created for specific types of connections that must be blocked. These rules, unsurprisingly, are referred to as a blacklist. The blacklist/whitelist approach applies equally to incoming and outgoing connections.

15.4 Creating a New Profile

While it is possible to modify the pre-defined profiles, it will typically make more sense to create one or more profiles to configure the firewall for your specific needs. New profiles are created by selecting the Edit -> Preferences... menu option to display the dialog shown in [Figure 15-2](#Ubuntu_ufw_Firewall.xhtml__idTextAnchor247):

![](image/ubuntu_gufw_preferences.jpg)

Figure 15-2

To add a new profile, click on the ‘+’ button located beneath the list of profiles. A new profile named Profile 1 will appear in the list. To give the profile a more descriptive name, double-click on the entry to enter edit mode and enter a new name:

![](image/ubuntu_gufw_new_profile.jpg)

Figure 15-3

Once the profile has been created and named, click on the Close button to return to the main screen, select it from the Profile menu and turn on the Status switch:

![](image/ubuntu_gufw_enabled.jpg)

Figure 15-4

With the custom profile selected, it is ready to set up some custom rules that override the default incoming and outgoing settings.

15.5 Adding Preconfigured Firewall Rules

New rules are created by clicking on the Rules button followed by the + button located at the bottom of the rules panel, as highlighted in [Figure 15-5](#Ubuntu_ufw_Firewall.xhtml__idTextAnchor249):

![](image/ubuntu_gufw_add_rule.jpg)

Figure 15-5

Once selected, the dialog shown in [Figure 15-6](#Ubuntu_ufw_Firewall.xhtml__idTextAnchor250) will appear with the Preconfigured tab selected.  The Preconfigured panel allows rules to be selected that match specific applications and services. For example, traffic from such tools as Skype and BitTorrent may be enabled by selecting the entry from the Application menu and the Policy and Direction menus accordingly to restrict or allow traffic.

To help find a specific application or service, use the Category and Subcategory menus to filter the items that appear in the Application menu. Alternatively, simply enter the application or service name in the Application Filter field to filter the menu items:

![](image/ubuntu_gufw_preconfigured.jpg)

Figure 15-6

The Policy menu provides the following options for controlling traffic for the selected application or service:

• Allow – Traffic is permitted on the port.

• Deny – Traffic is not permitted on the port. The requesting system is not notified of the denial. The data packet is simply dropped.

• Reject - Traffic is not permitted on the port. The data packet is dropped, and the requesting system is notified of the rejection.

• Limit - Connections are denied if the same IP address has attempted to establish 6 or more connections over a 30-second time frame.

Once a rule has been defined, clicking the Add button will implement the rule, dismiss the Add Rule dialog and the new rule will be listed in the main screen of the gufw tool (with rules for both IPv4 and IPv6 protocols):

![](image/ubuntu_gufw_rule_added.jpg)

Figure 15-7

To delete a rule, select it within the list and click on the ‘-’ button located at the bottom of the dialog. Similarly, edit an existing rule by selecting it and clicking on the gear button to the right of the ‘-’ button.

15.6 Adding Simple Firewall Rules

Whereas preconfigured rules allow the firewall to be configured based on well known services and applications, the Simple tab of the Add Rule dialog allows incoming and outgoing rules to be defined simply by referencing the corresponding TCP/IP port. The ports used by known applications and services represent only a small subset of the ports available for use by applications and for which firewall rules may need to be defined. A third-party application might, for example, use port 5700 to communicate with a remote server. That being the case, it may be necessary to allow traffic on this specific port using the Simple panel:

![](image/ubuntu_gufw_simple.jpg)

Figure 15-8

The rule may be configured to filter either TCP, UDP or both traffic types. In addition, the port may be specified as a single port number or as a range of ports with the start and end ports separated by a colon (1000:1500, for example, would apply the rule to all ports between 1000 and 1500). Alternatively, enter the name of the service associated with the port (for example, https or ssh)

15.7 Adding Advanced Rules

So far, we have looked at rules to control only the type of traffic to block (incoming traffic on port 22, for example) regardless of the source or destination of the traffic. It is often the case, however, that rules will need to be defined to allow or deny traffic based on an IP address or range of IP addresses.

For the purposes of an example, assume that the local system has an IP address of 192.168.0.102\. The firewall may be configured to only allow access on port 22 from a system with the IP address of, for example, 192.168.0.105\. To achieve this, the From: field of the Advanced settings panel should be set to the IP address of the system from which the connection request is originating (in this case 192.168.0.105).

The To: fields provide the option to specify the IP address and port of the system to which the connection is being made. In this example, this would be port 22 on the local system (192.168.0.102). The To: IP address is actually optional and may be left blank:

![](image/ubuntu_gufw_advanced.jpg)

Figure 15-9

Assuming that the incoming default policy is still set to Deny or Reject on the main screen, the above rule will allow SSH access via port 22 to the local system only from the remote system with the IP address of 192.168.0.105. SSH access attempts from systems with other IP addresses will fail. Note that if the target system is the local system the To: IP address field may be left blank.

The Insert field in the above dialog allows the new rule to be inserted at the specified position in the list of existing rules, thereby allowing you to control the order in which the rules are applied within the firewall.

It is also possible to specify a range of addresses by using the IP address bitmask. For example, to create a rule for a range of IP addresses from 192.168.0.1 to 192.168.0.255 the IP address should be entered into the From: field as 192.168.0.0/24.

Similarly, to specify a rule covering IP address range 192.168.0.1 to 192.168.0.30, a bitmask of 27 would be used, i.e. 192.168.0.0/27\.

A useful calculator for identifying the address range covered by each bit mask value is available online at [http://subnet-calculator.com](http://subnet-calculator.com).

15.8 Configuring the Firewall from the Command Line using ufw

All of the firewall configuration options available through the graphical gufw tool are also available from the underlying command line using ufw command.

To enable or disable the firewall:

# ufw enable

# ufw disable

The current status of the firewall may be obtained using the status option:

# ufw status

Status: active

To Action From

-- ------ ----

22 ALLOW 192.168.86.30

For more details status information, combine the above command with the verbose option:

# ufw status verbose

Status: active

Logging: on (full)

Default: deny (incoming), allow (outgoing), deny (routed)

New profiles: skip

To Action From

-- ------ ----

22 ALLOW IN 192.168.86.30

The output in the above example shows that the default policy for the firewall is to deny all incoming and routed connections while allowing all outgoing connections. To change any of these default settings, use the ufw command with the default option using the following syntax:

# ufw default <policy> <direction>

For example, to enable all incoming connections by default:

# ufw default allow incoming

To allow or block traffic on a specific port, use the following syntax:

# ufw <policy> <port number>/<optional protocol>

For example, to allow both TCP and UDP incoming traffic on port 30:

# ufw allow 30

Similarly, to deny incoming TCP traffic on port 5700:

# ufw deny 5700/tcp

Rules may also be declared by referencing the name of the service corresponding to the port. For example, to enable SSH access on port 22:

# ufw allow ssh

As with the gufw tool, ufw also allows access to be controlled from specific external IP addresses. For example, to allow all incoming traffic from IP address 192.168.0.20:

# ufw allow from 192.168.0.20

To specifically deny traffic from an IP address:

# ufw deny 192.168.0.20

To limit access for IP address 192.168.0.20 to only port 22:

# ufw allow from 192.168.0.22 to any port 22

To further restrict access for the IP address to only TCP packets, use the following syntax:

# ufw allow from 192.168.0.20 to any port 22 proto tcp

The position of a new rule within the list of existing rules may be declared using the insert option. For example to create a new rule and insert it at position 3 in the rules list:

# ufw insert 3 allow from 192.168.0.123 to any port 2

To display the list of rules with associated numbers:

# ufw status numbered

Status: active

     To Action From

     -- ------ ----

[ 1] 22 ALLOW IN 192.168.86.30

[ 2] 30 ALLOW IN Anywhere

[ 3] 22 ALLOW IN 192.168.0.123

[ 4] 5700/tcp DENY IN Anywhere

[ 5] 22/tcp ALLOW IN Anywhere

[ 6] Anywhere ALLOW IN 192.168.0.20

[ 7] 22 ALLOW IN 192.168.0.4

[ 8] 30 (v6) ALLOW IN Anywhere (v6)

[ 9] 5700/tcp (v6) DENY IN Anywhere (v6)

[10] 22/tcp (v6) ALLOW IN Anywhere (v6)

Having identified the number assigned to a rule, that number may be used to remove the rule from the firewall:

# ufw delete 4

To obtain a full listing of the capabilities of the ufw tool run the command with the –help argument:

# ufw help

Logging of firewall activity can be enabled and disabled using the logging command-line option:

# ufw logging on

# ufw logging off

The amount of logging performed by ufw may also be declared, including a low, medium, high, or full setting when turning on logging, for example:

# ufw logging on low

The ufw log file can be found at:

/var/log/ufw.log

Use the reload option to restart the firewall and reload all current settings:

# ufw reload

Finally, to reset the firewall to the default settings (thereby removing all existing rules and settings):

# ufw reset

15.9 Summary

Any computer system that is connected to other systems, either via an internal network or through an internet connection should implement some form of firewall to mitigate the risk of attack. The Uncomplicated Firewall provided with Ubuntu provides a simple yet effective firewall that allows basic rules to be defined either using the command-line or the graphical gufw tool. This chapter has outlined the basics of enabling the firewall and configuring firewall rules.

16\. Basic Ubuntu Firewall Configuration with firewalld

All Linux distributions are provided with a firewall solution of some form. In the case of Ubuntu this takes the form of the Uncomplicated Firewall outlined in the previous chapter. This chapter will introduce a more advanced firewall solution available for Ubuntu in the form of firewalld.

16.1 An Introduction to firewalld

Originally developed for Red Hat-based Linux distributions, the firewalld service uses a set of rules to control incoming network traffic and define which traffic is to be blocked and which is to be allowed to pass through to the system and is built on top of a more complex firewall tool named iptables.

The firewalld system provides a flexible way to manage incoming traffic. The firewall could, for example, be configured to block traffic arriving from a specific external IP address or to prevent all traffic arriving on a particular TCP/IP port. Rules may also be defined to forward incoming traffic to different systems or to act as an internet gateway to protect other computers on a network.

In keeping with common security practices, a default firewalld installation is configured to block all access with the exception of SSH remote login and the DHCP service used by the system to obtain a dynamic IP address (both of which are essential if the system administrator is to be able to gain access to the system after completing the installation).

The key elements of firewall configuration on Ubuntu are zones, interfaces, services, and ports.

16.1.1 Zones

By default, firewalld is installed with a range of pre-configured zones. A zone is a preconfigured set of rules which can be applied to the system at any time to quickly implement firewall configurations for specific scenarios. The block zone, for example, blocks all incoming traffic, while the home zone imposes less strict rules on the assumption that the system is running in a safer environment where a greater level of trust is expected. New zones may be added to the system, and existing zones modified to add or remove rules. Zones may also be deleted entirely from the system. [Table 16-1](#Ubuntu_Firewall_Configuration.xhtml__idTextAnchor261) lists the set of zones available by default on an Ubuntu system:

| Zone | Description |
| --- | --- |
| drop | The most secure zone. Only outgoing connections are permitted and all incoming connections are dropped without any notification to the connecting client. |
| block | Similar to the drop zone with the exception that incoming connections are rejected with an icmp-host-prohibited or icmp6-adm-prohibited notification. |
| public | Intended for use when connected to public networks or the internet where other computers are not known to be trustworthy. Allows select incoming connections. |
| external | When a system is acting as the internet gateway for a network of computers, the external zone is applied to the interface that is connected to the internet.This zone is used in conjunction with the internal zone when implementing masquerading or network address translation (NAT) as outlined later in this chapter. Allows select incoming connections |
| internal | Used with the external zone and applied to the interface that is connected to the internal network. Assumes that the computers on the internal network are trusted. Allows select incoming connections. |
| dmz | For use when the system is running in the demilitarized zone (DMZ). These are generally computers that are publicly accessible but isolated from other parts of your internal network. Allows select incoming connections. |
| work | For use when running a system on a network in a work environment where other computers are trusted. Allows select incoming connections. |
| home | For use when running a system on a home network where other computers are trusted. Allows select incoming connections. |
| trusted | The least secure zone. All incoming connections are accepted. |

Table 16-1

To review specific settings for a zone, refer to the corresponding XML configuration file located on the system in the /usr/lib/firewalld/zones directory. The following, for example, lists the content of the public.xml zone configuration file:

<?xml version=”1.0” encoding=”utf-8”?>

<zone>

  <short>Public</short>

<description>For use in public areas. You do not trust the other computers on networks to not harm your computer. Only selected incoming connections are accepted.</description>

  <service name=”ssh”/>

  <service name=”mdns”/>

  <service name=”dhcpv6-client”/>

</zone>

16.1.2 Interfaces

Any Ubuntu system connected to the internet or a network (or both) will contain at least one interface in the form of either a physical or virtual network device. When firewalld is active, each of these interfaces is assigned to a zone allowing different levels of firewall security to be assigned to different interfaces. Consider a server containing two interfaces, one connected externally to the internet and the other to an internal network. In such a scenario, the external facing interface would most likely be assigned to the more restrictive external zone, while the internal interface might use the internal zone.

16.1.3 Services

TCP/IP defines a set of services that communicate on standard ports. Secure HTTPS web connections, for example, use port 443, while the SMTP email service uses port 25\. To selectively enable incoming traffic for specific services, firewalld rules can be added to zones. The home zone, for example, does not permit incoming HTTPS connections by default. This traffic can be enabled by adding rules to a zone to allow incoming HTTPS connections without having to reference the specific port number.

16.1.4 Ports

Although common TCP/IP services can be referenced when adding firewalld rules, situations will arise where incoming connections need to be allowed on a specific port that is not allocated to a service. This can be achieved by adding rules that reference specific ports instead of services.

16.2 Checking firewalld Status

The firewalld service is not usually installed and enabled by default on all Ubuntu installations. The status of the service can be checked via the following command:

# systemctl status firewalld

● firewalld.service - firewalld - dynamic firewall daemon

     Loaded: loaded (/lib/systemd/system/firewalld.service; enabled; vendor preset: enabled)

     Active: active (running) since Mon 2023-07-17 19:21:53 UTC; 16s ago

       Docs: man:firewalld(1)

   Main PID: 27151 (firewalld)

      Tasks: 2 (limit: 4517)

     Memory: 24.0M

        CPU: 244ms

     CGroup: /system.slice/firewalld.service

             └─27151 /usr/bin/python3 /usr/sbin/firewalld --nofork --nopid

Jul 17 19:21:53 demoserver systemd[1]: Starting firewalld - dynamic firewall daemon...

Jul 17 19:21:53 demoserver systemd[1]: Started firewalld - dynamic firewall daemon.

If necessary, the firewalld service may be installed as follows:

# apt install firewalld

The firewalld service is enabled by default, so it will start automatically both after installation is complete and each time the system boots.

16.3 Configuring Firewall Rules with firewall-cmd

The firewall-cmd command-line utility allows information about the firewalld configuration to be viewed and changes to be made to zones and rules from within a terminal window.

When making changes to the firewall settings, it is important to be aware of the concepts of runtime and permanent configurations. By default, any rule changes are considered to be runtime configuration changes. This means that while the changes will take effect immediately, they will be lost next time the system restarts or the firewalld service reloads, for example, by issuing the following command:

# firewall-cmd --reload

To make a change permanent, the --permanent command-line option must be used. Permanent changes do not take effect until the firewalld service reloads but will remain in place until manually changed.

16.3.1 Identifying and Changing the Default Zone

To identify the default zone (in other words, the zone to which all interfaces will be assigned unless a different zone is specifically selected), use the firewall-cmd tool as follows:

# firewall-cmd --get-default-zone

public

To change the default to a different zone:

# firewall-cmd --set-default-zone=home

success

16.3.2 Displaying Zone Information

To list all of the zones available on the system:

# firewall-cmd --get-zones

block dmz drop external home internal public trusted work

Obtain a list of zones currently active together with the interfaces to which they are assigned as follows:

# firewall-cmd --get-active-zones

external

  interfaces: eth0

internal

 interfaces: eth1

All of the rules currently configured for a specific zone may be listed as follows:

# firewall-cmd --zone=home --list-all

home (active)

  target: default

  icmp-block-inversion: no

  interfaces: eth0

  sources:

  services: cockpit dhcpv6-client http mdns samba-client ssh

  ports:

  protocols:

  masquerade: no

  forward-ports:

  source-ports:

  icmp-blocks:

  rich rules:

Use the following command to list the services currently available for inclusion in a firewalld rule:

# firewall-cmd --get-services

RH-Satellite-6 amanda-client amanda-k5-client amqp amqps apcupsd audit bacula bacula-client bgp bitcoin bitcoin-rpc bitcoin-testnet bitcoin-testnet-rpc ceph ceph-mon cfengine cockpit ...

To list the services currently enabled for a zone:

# firewall-cmd --zone=public --list-services

cockpit dhcpv6-client ssh

A list of port rules can be obtained as follows:

# firewall-cmd --zone=public --list-ports

9090/tcp

16.3.3 Adding and Removing Zone Services

To add a service to a zone, in this case adding HTTPS to the public zone, the following command would be used:

# firewall-cmd --zone=public --add-service=https

success

By default, this is a runtime change, so the added rule will be lost after a system reboot. To add a service permanently so that it remains in effect next time the system restarts, use the --permanent flag:

# firewall-cmd --zone=public --permanent --add-service=https

success

To verify that a service has been added permanently, be sure to include the --permanent flag when requesting the service list:

# firewall-cmd --zone=public --permanent --list-services

cockpit dhcpv6-client http https ssh

Note that as a permanent change, this new rule will not take effect until the system restarts or firewalld reloads:

# firewall-cmd --reload

Remove a service from a zone using the --remove-service option. Since this is a runtime change, the rule will be re-instated the next time the system restarts:

# firewall-cmd --zone=public --remove-service=https

To remove a service permanently, use the --permanent flag, remembering to reload firewalld if the change is required to take immediate effect:

# firewall-cmd --zone=public --permanent --remove-service=https

16.3.4 Working with Port-based Rules

To enable a specific port, use the --add-port option. Note that when manually defining the port, both the port number and protocol (TCP or UDP) will need to be provided:

# firewall-cmd --zone=public --permanent --add-port=5000/tcp

It is also possible to specify a range of ports when adding a rule to a zone:

# firewall-cmd --zone=public --permanent --add-port=5900-5999/udp

16.3.5 Creating a New Zone

An entirely new zone may be created by running the following command. Once created, the zone may be managed in the same way as any of the predefined zones:

# firewall-cmd --permanent --new-zone=myoffice

success

After adding a new zone, firewalld will need to be restarted before the zone becomes available:

# firewall-cmd --reload

success

16.3.6 Changing Zone/Interface Assignments

As previously discussed, each interface on the system must be assigned to a zone. The zone to which an interface is assigned can also be changed using the firewall-cmd tool. In the following example, the eth0 interface is assigned to the public zone:

# firewall-cmd --zone=public --change-interface=eth0

success

16.3.7 Masquerading

Masquerading is better known in networking administration circles as Network Address Translation (NAT). When using an Ubuntu system as a gateway to the internet for a network of computers, masquerading allows all of the internal systems to use the IP address of that Ubuntu system when communicating over the internet. This has the advantage of hiding the internal IP addresses of any systems from malicious external entities and also avoids the necessity to allocate a public IP address to every computer on the network.

Use the following command to check whether masquerading is already enabled on the firewall:

# firewall-cmd --zone=external --query-masquerade

Use the following command to enable masquerading (remembering to use the --permanent flag if the change is to be permanent):

# firewall-cmd --zone=external --add-masquerade

16.3.8 Adding ICMP Rules

The Internet Control Message Protocol (ICMP) is used by client systems on networks to send information such as error messages to each other. It is also the foundation of the ping command, which network administrators and users alike use to detect whether a particular client is alive on a network. The ICMP category allows for the blocking of specific ICMP message types. For example, an administrator might choose to block incoming ping (Echo Request) ICMP messages to prevent the possibility of a ping-based denial of service (DoS) attack (where a server is maliciously bombarded with so many ping messages that it becomes unable to respond to legitimate requests).

To view the ICMP types available for inclusion in firewalld rules, run the following command:

# firewall-cmd --get-icmptypes

address-unreachable bad-header beyond-scope communication-prohibited destination-unreachable echo-reply ...

The following command, for example, permanently adds a rule to block echo-reply (ping request) messages for the public zone:

# firewall-cmd --zone=public --permanent --add-icmp-block=echo-reply

16.3.9 Implementing Port Forwarding

Port forwarding is used in conjunction with masquerading when the Ubuntu system acts as a gateway to the internet for an internal network of computer systems. Port forwarding allows traffic arriving at the firewall via the internet on a specific port to be forwarded to a particular system on the internal network. This is perhaps best described by way of an example.

Suppose that an Ubuntu system is acting as the firewall for an internal network of computers and one of the systems on the network is configured as a web server. Let’s assume the web server system has an IP address of 192.168.2.20\. The domain record for the web site hosted on this system is configured with the public IP address behind which the Ubuntu firewall system sits. When an HTTP web page request arrives on port 80 the Ubuntu system acting as the firewall needs to know what to do with it. By configuring port forwarding it is possible to direct all web traffic to the internal system hosting the web server (in this case, IP address 192.168.2.20), either continuing to use port 80 or diverting the traffic to a different port on the destination server. In fact, port forwarding can even be configured to forward the traffic to a different port on the same system as the firewall (a concept known as local forwarding).

To use port forwarding, begin by enabling masquerading as follows (in this case the assumption is made that the interface connected to the internet has been assigned to the external zone):

# firewall-cmd --zone=external --add-masquerade

To forward from a port to a different local port, a command similar to the following would be used:

# firewall-cmd --zone=external --add-forward-port=port=22:proto=tcp:toport=2750

In the above example, any TCP traffic arriving on port 22 will be forwarded to port 2750 on the local system. The following command, on the other hand, forwards port 20 on the local system to port 22 on the system with the IP address of 192.168.0.19:

# firewall-cmd --zone=external \

          --add-forward-port=port=20:proto=tcp:toport=22:toaddr=192.168.0.19

Similarly, the following command forwards local port 20 to port 2750 on the system with IP address 192.168.0.18:

# firewall-cmd --zone=external --add-forward-port=port=20:proto=tcp:toport=2750:toaddr=192.168.0.18

16.4 Managing firewalld using firewall-config

If you have access to the graphical desktop environment, the firewall may also be configured using the firewall-config tool. Though not installed by default, firewall-config may be installed as follows:

# apt install firewall-config

When launched, the main firewall-config screen appears as illustrated in [Figure 16-1](#Ubuntu_Firewall_Configuration.xhtml__idTextAnchor279):

![](image/ubuntu_firewall-config.jpg)

Figure 16-1

The key areas of the tool can be summarized as follows:

A - Displays all of the currently active interfaces and the zones to which they are assigned. To assign an interface to a different zone, select it from this panel, click on the Change Zone button and select the required zone from the resulting dialog.

B - Controls whether the information displayed and any changes made within the tool apply to the runtime or permanent rules.

C - The list of zones, services or IPSets configured on the system. The information listed in this panel depends on the selection made from toolbar F. Selecting an item from the list in this panel updates the main panel marked D.

D - The main panel containing information about the current category selection in toolbar E. In this example, the panel is displaying services for the public zone. The checkboxes next to each service control whether the service is enabled or not within the firewall. It is within these category panels that new rules can be added or existing rules configured or removed.

E - Controls the content displayed in panel D. Selecting items from this bar displays the current rule for the chosen category.

F - Controls the list displayed in panel C.

The firewall-config tool is straightforward and intuitive to use and allows many of the tasks available with firewall-cmd to be performed in a visual environment.

16.5 Summary

A carefully planned and implemented firewall is a vital component of any secure system. In the case of Ubuntu, the firewalld service provides a firewall system that is both flexible and easy to administer.

The firewalld service uses the concept of zones to group together sets of firewall rules and includes a suite of pre-defined zones designed to meet a range of firewall protection requirements. These zones may be modified to add or remove rules or entirely new zones created and configured. The network devices on the system that connect to networks or the internet are referred to as interfaces. Each interface, in turn, is assigned to a zone. The primary tools for working with firewalld are the firewall-cmd command-line tool and the firewall-config graphical utility.

17\. Configuring SSH Key-based Authentication on Ubuntu 23.04

When an Ubuntu system is first installed, it is configured by default to allow remote command-line access via Secure Shell (SSH) connections. SSH provides password-protected and encrypted access to the system for the root account and any other users added during the installation phase. However, this level of security is inadequate and should be upgraded to SSH key-based authentication as soon as possible.

This chapter will outline the steps to increase the security of an Ubuntu system by implementing key-based SSH authentication.

17.1 An Overview of Secure Shell (SSH)

SSH allows secure remote access to systems to gain shell access and transfer files and data. A basic SSH configuration consists of a client (used on the computer establishing the connection) and a server (running on the system to which the connection is to be established). A user might, for example, use an SSH client running on a Linux, Windows, or macOS system to connect to the SSH server running on an Ubuntu system to gain access to a shell command-line prompt or to perform file transfers. All communications between the client and server, including the password entered to gain access, are encrypted to prevent outside parties from intercepting the data.

The inherent weakness in a basic SSH implementation is that it depends entirely on the strength of the passwords assigned to the accounts on the system. If a malicious party is able to identify the password for an account (either through guesswork, deception, or a brute force attack), the system becomes vulnerable. This weakness can be addressed by implementing SSH key-based authentication.

17.2 SSH Key-based Authentication

SSH key-based authentication uses asymmetric public key encryption to add an extra layer of security to remote system access. The concept of public key encryption was devised in 1975 by Whitfield Diffie and Martin Hellman and is based on using a pair of private and public keys.

In a public key encryption system, the public key is used to encrypt data that can only be decrypted by the owner of the private key.

In the case of SSH key-based authentication, the host holds the private key on which the SSH client is located, while the corresponding public key resides on the system on which the SSH server is running. Therefore, it is vital to protect the private key since ownership of the key will allow anyone to log into the remote system. As an added layer of protection, the private key may also be encrypted and protected by a password which must be entered each time a connection is established to the server.

17.3 Setting Up Key-based Authentication

There are four steps to setting up key-based SSH authentication, which can be summarized as follows:

1\. Generate the public and private keys.

2\. Install the public key on the server.

3\. Test authentication.

4\. Disable password-based authentication on the server.

The remainder of this chapter will outline these steps in greater detail for Linux, macOS, and Windows-based client operating systems.

17.4 Installing and Starting the SSH Service

If the SSH server is not already installed and running on the system, it can be added using the following commands:

# apt install openssh-server

# systemctl start ssh.service

# systemctl enable ssh.service

17.5 SSH Key-based Authentication from Linux and macOS Clients

The first step in setting up SSH key-based authentication is to generate the key pairs on the client system. If the client system is running Linux or macOS, this is achieved using the ssh-keygen utility:

# ssh-keygen

This command will result in output similar to the following:

Generating public/private rsa key pair.

Enter file in which to save the key (/home/<username>/.ssh/id_rsa):

Press the Enter key to accept the default location for the key files. This will place two files in the .ssh sub-directory of the current user’s home directory. The private key will be stored in a file named id_rsa while the public key will reside in the file named id_rsa.pub.

Next, ssh-keygen will prompt for a passphrase with which to protect the private key. If a passphrase is provided, the private key will be encrypted on the local disk, and the passphrase will be required to access the remote system. Therefore, for better security, the use of a passphrase is recommended.

Enter passphrase (empty for no passphrase):

Finally, the ssh-keygen tool will generate the following output indicating that the keys have been generated:

Your identification has been saved in /home/neil/.ssh/id_rsa.

Your public key has been saved in /home/neil/.ssh/id_rsa.pub.

The key fingerprint is:

SHA256:FOLGWEEGFIjWnCT5wtTOv5VK4hdimzWghZizUEMYbfo <username>@<hostname>

The key’s randomart image is:

+---[RSA 2048]----+

|.BB+=+*.. |

|o+B= * . . |

|===.. + . |

|*+ * . . |

|.++ o S |

|..E+ * o |

| o B * |

| + + |

| . |

+----[SHA256]-----+

The next step is to install the public key onto the remote server system. This can be achieved using the ssh-copy-id utility as follows:

$ ssh-copy-id username@remote_hostname

For example:

$ ssh-copy-id neil@192.168.1.100

/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/home/neil/.ssh/id_rsa.pub"

/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed

/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys

neil@192.168.1.100’s password:

Number of key(s) added: 1

Now try logging into the machine, with: "ssh 'neil@192.168.1.100'"

and check to make sure that only the key(s) you wanted were added.

Once the key is installed, test that the authentication works by attempting a remote login using the ssh client:

$ ssh -l <username> <hostname>

If the private key is encrypted and protected with a passphrase, enter the phrase when prompted to complete the authentication and establish remote access to the Ubuntu system:

Enter passphrase for key '/home/neil/.ssh/id_rsa':

Last login: Fri Mar 31 14:29:28 2023 from 192.168.86.21

[neil@demosystem02 ~]$

Repeat these steps for any other accounts on the server for which remote access is required. If access is also required from other client systems, copy the id_rsa private key file to the .ssh sub-directory of your home folder on the other systems.

As currently configured, access to the remote system can still be achieved using less secure password authentication. Once you have verified that key-based authentication works, password authentication will need to be disabled on the system. To understand how to change this setting, begin by opening the /etc/ssh/sshd_config file and locating the following line:

Include /etc/ssh/sshd_config.d/*.conf

This tells us that sshd configuration settings are controlled by files in the /etc/ssh/sshd_config.d directory. These filenames must be prefixed with a number and have a .conf filename extension, for example:

01-permitrootlogin.conf

50-cloud.conf

The number prefix designates the priority assigned to the file relative to the other files in the folder, with 01 being the highest priority. This ensures that if a configuration file contains a setting conflicting with another file, the one with the highest priority will always take precedence.

Within the /etc/ssh/sshd_config.d folder, create a new file named 02-nopasswordlogin.conf with content that reads as follows:

PasswordAuthentication no

Save the file and restart the sshd service to implement the change:

# systemctl restart sshd.service

From this point on, it will only be possible to remotely access the system using SSH key-based authentication, and when doing so, you won’t be required to enter a password.

17.6 Managing Multiple Keys

It is common for multiple private keys to reside on a client system, each providing access to a different server. As a result, several options exist for selecting a specific key when establishing a connection. It is possible, for example, to specify the private key file to be used when launching the ssh client as follows:

$ ssh -l neilsmyth -i ~/.ssh/id_work 35.194.18.119

Alternatively, the SSH client user configuration file may associate key files with servers. The configuration file is named config, must reside in the .ssh directory of the user’s home directory, and can be used to configure a wide range of options, including the private key file, the default port to use when connecting, the default user name, and an abbreviated nickname via which to reference the server. The following example config file defines different key files for two servers and allows them to be referenced by the nicknames home and work. In the case of the work system, the file also specifies the user name to be used when authenticating:

Host work

  HostName 35.194.18.119

  IdentityFile ~/.ssh/id_work

  User neilsmyth

Host home

  HostName 192.168.0.21

  IdentityFile ~/.ssh/id_home

Before setting up the configuration file, the user would have used the following command to connect to the work system:

$ ssh -l neilsmyth -i ~/.ssh/id_work 35.194.18.119

Now, however, the command can be shortened as follows:

$ ssh work

A full listing of configuration file options can be found by running the following command:

$ man ssh_config

17.7 SSH Key-based Authentication from Windows Clients

Recent releases of Windows include a subset of the OpenSSH implementation used by most Linux and macOS systems as part of Windows PowerShell. This allows SSH key-based authentication to be set up from a Windows client using similar steps to those outlined above for Linux and macOS.

On Windows, search for Windows PowerShell and select it from the results. Once running, the PowerShell window will appear, as shown in [Figure 17-1](#SSH_Authentication.xhtml__idTextAnchor289):

![](image/windows_powershell.jpg)

Figure 17-1

If you already have a private key from another client system, copy the  id_rsa file to a folder named .ssh on the Windows system. Once the file is in place, test the authentication within the PowerShell window as follows:

$ ssh -l <username>@<hostname>

For example:

PS C:\Users\neil> ssh -l neil 192.168.1.101

Enter passphrase for key 'C:\Users\neil\.ssh\id_rsa':

Enter the passphrase when prompted and complete the authentication process.

If the private key does not yet exist, generate a new private and public key pair within the PowerShell window using the ssh-keygen utility using the same steps outlined for Linux and macOS. Once the keys have been generated, they will again be located in the .ssh directory of the current user’s home folder, and the public key file id_rsa.pub will need to be installed on the remote Ubuntu system. Unfortunately, Windows PowerShell does not include the ssh-copy-id utility, so this task must be performed manually.

Within the PowerShell window, change directory into the .ssh sub-directory and display the content of the public key id_rsa.pub file:

PS C:\Users\neil> cd .ssh

PS C:\Users\neil\.ssh> type id_rsa.pub

ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDFgx1vzu59lll6/uQw7FbmKVsQ3fzLz9MW1fgo4sdsxXp81wCHNAlqcjx1Pgr9BJPXWUMInQOi7BQ5I+vc2xQ2AS0kMq3ZH9ybWuQe/U2GjueXZd0FKrEXrT55wM36Rm6Ii3roUCoGCzGR8mn95JvRB3VtCyDdzTWSi8JBpK5gV5oOxNTNPsewlLzouBlCT1qW3CKwEiIwu8S9MTL7m3nrcaNeLewTTHevvHw4QDwzFQ+B0PDg96fzsYoTXVhzyHSWyo6H0gqrft7aK+gILBtEIhWTkSVEMAzy1piKtCr1IYTmVK6engv0aoGtMUq6FnOeGp5FjvKkF4aQkh1QR28r neil@DESKTOP-S8P8D3N

Highlight the file’s content and copy it using the Ctrl-C keyboard shortcut.

Remaining within the PowerShell window, log into the remote system using password authentication:

PS C:\Users\neil\.ssh> ssh -l <username> <hostname>

Once signed in, check if the .ssh sub-directory exists. If it does not, create it as follows:

$ mkdir .ssh

Change directory into .ssh and check whether a file named authorized_keys already exists. If it does not, create it and paste the content of the public key file from the Windows system into it.

If the authorized_keys file already exists, it likely contains other keys. If this is the case, edit the file and paste the new public key at the end of the file. The following file, for example, contains two keys:

ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCzRWH27Xs8ZA5rIbZXKgxFY5XXauMv+6F5PljBLJ6j+9nkmykVe3GjZTp3oD+KMRbT2kTEPbDpFD67DNL0eiX2ZuEEiYsxZfGCRCPBGYmQttFRHEAFnlS1Jx/G4W5UNKvhAXWyMwDEKiWvqTVy6syB2Ritoak+D/Sc8nJflQ6dtw0jBs+S7Aim8TPfgpi4p5XJGruXNRScamk68NgnPfTL3vT726EuABCk6C934KARd+/AXa8/5rNOh4ETPstjBRfFJ0tpmsWWhhNEnwJRqS2LD0ug7E3yFI2qsNKGEzvAYUC8Up45MRP7liR3aMlCBil1tsy9R+IB7oMEycZAe/qj neil@localhost.localdomain

ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDFgx1vzu59lll6/uQw7FbmKVsQ3fzLz9MW1fgo4sdsxXp81wCHNAlqcjx1Pgr9BJPXWUMInQOi7BQ5I+vc2xQ2AS0kMq3ZH9ybWuQe/U2GjueXZd0FKrEXrT55wM36Rm6Ii3roUCoGCzGR8mn95JvRB3VtCyDdzTWSi8JBpK5gV5oOxNTNPsewlLzouBlCT1qW3CKwEiIwu8S9MTL7m3nrcaNeLewTTHevvHw4QDwzFQ+B0PDg96fzsYoTXVhzyHSWyo6H0gqrft7aK+gILBtEIhWTkSVEMAzy1piKtCr1IYTmVK6engv0aoGtMUq6FnOeGp5FjvKkF4aQkh1QR28r neil@DESKTOP-S8P8D3N

Once the public key is installed on the server, test the authentication by logging in to the server from within the PowerShell window, for example:

PS C:\Users\neil\.ssh> ssh -l neil 192.168.1.100

Enter passphrase for key 'C:\Users\neil\.ssh\id_rsa':

When key-based authentication has been set up for all the accounts and verified, disable password authentication on the Ubuntu system as outlined at the end of the previous section.

17.8 SSH Key-based Authentication using PuTTY

For Windows systems that do not have OpenSSH available or as a more flexible alternative to using PowerShell, the PuTTY tool is a widely used alternative. The first step in using PuTTY is downloading and installing it on any Windows system that needs an SSH client. PuTTY is a free utility and can be downloaded using the following link:

[https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)

Download the Windows installer executable that matches your Windows system (32-bit and 64-bit versions are available), then execute the installer to complete the installation.

If a private key already exists on another system, create the .ssh folder in the current user’s home folder and copy the private id_rsa key into it.

Next, the private key file needs to be converted to a PuTTY private key format file using the PuTTYgen tool. Locate this utility by typing “PuTTY Key Generator” into the search bar of the Windows Start menu and launch it:

![](image/putty_key_generator.jpg)

Figure 17-2

Once launched, click on the Load button located in the Actions section and navigate to the private key file previously copied to the .ssh folder (note that it may be necessary to change the file type filter to All Files (*.*) for the key file to be visible). Once located, select the file and load it into PuttyGen. When prompted, enter the passphrase used initially to encrypt the file. Once the private key has been imported, save it as a PuTTY key file by clicking the Save Private Key button. For consistency, save the key file to the .ssh folder but give it a different name to differentiate it from the original key file.

Launch PuTTY from the Start menu and enter the IP address or hostname of the remote server into the main screen before selecting the Connection -> SSH -> Auth -> Credentials category in the left-hand panel, as highlighted in [Figure 17-3](#SSH_Authentication.xhtml__idTextAnchor291):

![](image/putty_credentials.jpg)

Figure 17-3

Click the Browse button next to the Private key for authentication field and navigate to and select the previously saved PuTTY private key file. Then, optionally, scroll to the top of the left-hand panel, select the Session entry, and enter a name for the session in the Saved Sessions field before clicking on the Save button. This will save the session configuration for future use without re-entering the settings each time.

Finally, click on the Open button to establish the connection to the remote server, entering the user name and passphrase when prompted to do so to complete the authentication.

17.9 Generating a Private Key with PuTTYgen

The previous section explored using existing private and public keys when working with PuTTY. If keys do not exist, they can be created using the PuTTYgen tool, which is included in the main PuTTY installation.

To create new keys, launch PuttyGen and click on the Generate button highlighted in [Figure 17-4](#SSH_Authentication.xhtml__idTextAnchor293):

![](image/putty_key_generator_generate.jpg)

Figure 17-4

Move the mouse pointer to generate random data as instructed, then enter an optional passphrase to encrypt the private key. Once the keys have been generated, save the files to suitable locations using the Save public key and Save private key buttons. As outlined in the previous section, the private key can be used with PuTTY. To install the public key on the remote server, use the steps covered in the earlier section on SSH within PowerShell on Windows.

17.10 Summary

Any remote access to an Ubuntu system must be implemented in a way that provides a high level of security. By default, SSH allows remote system access using password-based authentication. However, this leaves the system vulnerable to anyone who can guess a password or find out the password through other means. For this reason, key-based authentication is recommended to protect system access. Key-based authentication uses public key encryption involving public and private keys. When implemented, users can only connect to a server if they are using a client with a private key that matches a public key on the server. As an added layer of security, the private key may also be encrypted and password protected. Once key-based encryption has been implemented, the server system is configured to disable support for the less secure password-based authentication.

This chapter has provided an overview of SSH key-based authentication and outlined the steps involved in generating keys and configuring clients on macOS, Linux, and Windows, as well as installing and managing public keys on an Ubuntu server.

18\. Ubuntu 23.04 Remote Desktop Access with Vino

Ubuntu can be configured to provide remote access to the graphical desktop environment over a network or internet connection. Although not enabled by default, it is relatively straightforward to display and access an Ubuntu desktop from a system anywhere else on a network or the internet. This can be achieved regardless of whether that system is running Linux, Windows, or macOS. In fact, there are even apps available for Android and iOS that will allow you to access your Ubuntu desktop from just about anywhere that a data signal is available.

Remote desktop access can be useful in a number of scenarios. It enables you or another person, for example, to view and interact with your Ubuntu desktop environment from another computer system either on the same network or over the internet. This is useful if you need to work on your computer when you are away from your desk, such as while traveling. It is also useful in situations where a co-worker or IT support technician needs access to your desktop to resolve a problem.

The Ubuntu remote desktop supports connections using either Virtual Network Computing (VNC) or Microsoft’s Remote Desktop Protocol (RDP). An advantage of using RDP is that it makes the Ubuntu desktop easily accessible from Windows clients. In this chapter, therefore, we will cover the key aspects of configuring and using remote desktops within Ubuntu using RDP.

18.1 Remote Desktop Access Types

Before starting, it is important to understand that there are essentially two types of remote desktop access. The approach covered in this chapter is useful if you primarily use Ubuntu as a desktop operating system and require remote access to your usual desktop session. When configured, you will take over your desktop session and view and control it remotely.

The second option is intended for situations where you need to start and access one or more remote desktop sessions on a remote server-based system, regardless of whether the remote system has a graphical console attached. This allows you to launch multiple desktop sessions in the background on the remote system and view and control those desktops over a network or internet connection.

18.2 Secure and Insecure Remote Desktop Access

In this chapter, we will cover both secure and insecure remote desktop access methods. Assuming that you are accessing one system from another within the context of a secure internal network then it is generally safe to use the insecure access method. If, on the other hand, you plan to access your desktop remotely over any kind of public network, you must use the secure method of access to avoid your system and data being compromised.

18.3 Enabling Remote Desktop Access on Ubuntu

Remote desktop access on Ubuntu is provided by the Vino package. Vino is a remote desktop server that was developed specifically for use with the GNOME desktop.

The first step in enabling remote access is to install this package:

# apt install vino

Once Vino has been installed, the next step is to enable remote desktop access from within GNOME. Begin by opening the settings app as shown in [Figure 18-1](#Ubuntu_Remote_Desktop_Access.xhtml__idTextAnchor299):

![](image/ubuntu_settings_menu.jpg)

Figure 18-1

From within the Settings application, select the Sharing option (marked A in [Figure 18-2](#Ubuntu_Remote_Desktop_Access.xhtml__idTextAnchor300)):

![](image/ubuntu_sharing_settings.jpg)

Figure 18-2

Turn on the Sharing switch (B) and click on the Remote Desktop option (C) to display the dialog shown in [Figure 18-3](#Ubuntu_Remote_Desktop_Access.xhtml__idTextAnchor301) below:

![](image/ubuntu_remote_desktop_settings.jpg)

Figure 18-3

The Remote Desktop dialog provides the following configuration options to manage remote desktop access:

•Remote Desktop - Controls whether remote desktop access is permitted.

•Remote Control - If enabled, the remote session will be able to use the mouse and keyboard to interact with the desktop environment. If this option disabled, the remote session will only allow the desktop to be viewed.

•User Name and Password - The user name and password that will be required to remotely access the desktop.

After configuring the settings, close both the Remote Desktop and Settings dialogs.

18.4 Connecting to the Shared Desktop

Although Remote Desktop viewer implementations are available for a wide range of operating systems, a tool such as the Remmina Desktop Client is recommended when connecting from Ubuntu or other Linux-based systems. Remmina is a user-friendly tool with a graphical interface that supports the encryption used by Vino to ensure a secure remote connection.

Remmina is usually installed by default on Ubuntu but can be installed if necessary as follows:

# apt install remmina

Launch Remmina on the remote Linux computer and change the connection type menu (marked A in [Figure 18-4](#Ubuntu_Remote_Desktop_Access.xhtml__idTextAnchor303)) to RDP, and enter into the address field (B) the IP address or hostname of the remote system to which you wish to connect (you can also create a connection and save it using the button marked C):

![](image/ubuntu_remmina_client.jpg)

Figure 18-4

To establish the connection, tap the keyboard Enter key to begin the connection process. Click to accept the certificate, after which a second screen will appear requesting the desktop access password:

![](image/ubuntu_remmina_auth.jpg)

Figure 18-5

After entering the password, click on OK to access the remote screen:

![](image/ubuntu_remote_desktop_connected.jpg)

Figure 18-6

18.5 Connecting from Windows

Because we have configured Vino to use RDP, the Ubuntu desktop is also accessible from Windows clients using Microsoft’s Remote Desktop Connection application. On a Windows system, start Remote Desktop Connection and click on the Show Options button in the bottom right-hand corner to display additional configuration settings. Enter the hostname or IP address of the Ubuntu system and the user name that was configured earlier in the chapter:

![](image/windows_remote_desktop_to_ubuntu.jpg)

Figure 18-7

Click the connect button and, when prompted, enter the password to gain access to the Ubuntu desktop:

![](image/windows_remote_desktop_credentials.jpg)

Figure 18-8

18.6 Summary

Remote access to the GNOME desktop environment of an Ubuntu system can be enabled by making use of Virtual Network Computing (VNC) or the Remote Desktop Protocol (RDP). Comprising the server running on the remote server and a corresponding client on the local host, VNC and RDP allow remote access to desktop instances running on the server.

The standard remote server solution for the GNOME desktop is Vino. Once installed, remote desktop sessions can be established from other Linux systems using a remote desktop viewer such as Remmina. When using RDP, the desktop is also accessible to Windows and Mac systems using the Microsoft Remote Desktop Connection application.

19. Displaying Ubuntu 23.04 Applications Remotely (X11 Forwarding)

In the previous chapter, we looked at how to display the entire Ubuntu desktop on a remote computer. While this works well if you need to display the entire desktop remotely, it could be considered overkill if you only want to display a single application. Therefore, this chapter will look at displaying individual applications on a remote system.

19.1 Requirements for Remotely Displaying Ubuntu Applications

There are some prerequisites to running an application on one Ubuntu system and displaying it on another. First, the system on which the application is to be displayed must be running an X server. If the system is a Linux or UNIX-based system with a desktop environment running, then this is no problem. However, if the system is running Windows or macOS, you must install an X server on it before you can display applications from a remote system. Several commercial and free Windows-based X servers are available for this purpose, and a web search should provide you with a list of options.

Second, the system on which the application is being run (as opposed to the system on which the application is to be displayed) must be configured to allow SSH access. Details on configuring SSH on an Ubuntu system can be found in the chapter [“Configuring SSH Key-based Authentication on Ubuntu 23.04”](#SSH_Authentication.xhtml__idTextAnchor281). This system must also run the X Window System from X.org instead of Wayland. To enable the X.org system from within the desktop, log out of the Gnome desktop, select your user account from the login screen, and then click the settings button in the bottom right-hand corner of the screen:

![](image/ubuntu_change_to_xorg.jpg)

Figure 19-1

Select the GNOME on Xorg option from the menu before logging in as usual. To revert to Wayland, repeat these steps, selecting the Ubuntu option from the login screen settings menu.

Another option is to edit the /etc/gdm3/custom.conf file, uncomment the WaylandEnable line as follows and restart the system:

# Uncomment the line below to force the login screen to use Xorg

WaylandEnable=false

Once you have logged back into the desktop, open a Terminal window and run the following command to confirm that the X.org system has been enabled:

$ echo $XDG_SESSION_TYPE

The above command will output either x11 or wayland, depending on the current configuration.

Finally, SSH must be configured to allow X11 forwarding. This is achieved by adding the following directive to the SSH configuration on the system from which forwarding is to occur. By default on Ubuntu, the /etc/ssh/sshd_config file contains a directive to include all of the configuration files contained in the /etc/ssh/sshd_config.d directory:

Include /etc/ssh/sshd_config.d/*.conf

Create a new file in the /etc/ssh/sshd_config.d folder named 05_x11forwarding and edit it to enable the X11Forwarding property is enabled as follows:

X11Forwarding yes

After making the change, save the file and restart the SSH service:

# systemctl restart ssh

Once the above requirements are met, it should be possible to display an X-based desktop application remotely. Keep in mind that not all GNOME apps are compatible with X11 forwarding. If an app is not compatible, the following error will appear when you try to run it using X11 forwarding:

X11 connection rejected because of wrong authentication.

19.2 Displaying an Ubuntu Application Remotely

The first step in remotely displaying an application is to move to the system where the application is to be displayed. At this system, establish an SSH connection to the remote system so that you have a command prompt. This can be achieved using the ssh command. When using the ssh command, we need to use the -X flag to tell it that we plan to tunnel X11 traffic through the connection:

$ ssh -X user@hostname

In the above example, user is the user name to use to log into the remote system, and hostname is the hostname or IP address of the remote system. Enter your password at the login prompt and, once logged in, run the following command to see the DISPLAY setting:

$ echo $DISPLAY

The command should output something similar to the following:

localhost:10.0

To display an application, run it from the command prompt. For example:

$ xclock

When executed, the above command should run xclock on the remote system but display the user interface on the local system.

19.3 Trusted X11 Forwarding

You can also enable trusted X11 forwarding by adding the following line to the 05_x11forwarding and restarting the ssh server:

ForwardX11Trusted yes

Trusted X11 forwarding is slightly faster than untrusted forwarding but is less secure since it does not engage the X11 security controls. The -Y flag is needed when using trusted X11 forwarding:

$ ssh -Y user@hostname

19.4 Compressed X11 Forwarding

When using slower connections, the X11 data can be compressed using the ssh -C flag to improve performance:

$ ssh -X -C user@hostname

19.5 Displaying Remote Ubuntu Apps on Windows

To display Ubuntu-based apps on Windows, an SSH client and an X server must be installed on the Windows system. Installing and using the PuTTY client on Windows was covered earlier in the book in the [“Configuring SSH Key-based Authentication on Ubuntu 23.04”](#SSH_Authentication.xhtml__idTextAnchor281) chapter. Refer to this chapter if you have not already installed PuTTY on your Windows system.

In terms of the X server, several options are available, though a popular choice appears to be VcXsrv which is available for free from the following URL:

[https://sourceforge.net/projects/vcxsrv/](https://sourceforge.net/projects/vcxsrv/)

Once the VcXsrv X server has been installed, an application named XLaunch will appear on the desktop and in the start menu. Start XLaunch and select a display option (the most flexible being the Multiple windows option which allows each client app to appear in its own window):

![](image/vcxsrvr_xlaunch_settings.jpg)

Figure 19-2

Click the Next button to proceed through the remaining screens, accepting the default configuration settings. On the final screen, click the Finish button to start the X server. If the Windows Defender dialog appears, click the button to allow access to your chosen networks.

Once running, XLaunch will appear in the taskbar and can be exited by right-clicking on the icon and selecting the Exit... menu option:

![](image/vcxsrvr_xlaunch_menu.jpg)

Figure 19-3

With the X server installed and running, launch PuTTY and either enter the connection information for the remote host or load a previously saved session profile. Before establishing the connection, however, X11 forwarding needs to be enabled. Therefore, within the PuTTY main window, scroll down the options in the left-hand panel, unfold the SSH section, and select the X11 option, as shown in [Figure 19-4](#X11_Forwarding.xhtml__idTextAnchor323):

![](image/win_10_putty_ssh.jpg)

Figure 19-4

Turn on the Enable X11 forwarding checkbox highlighted in [Figure 19-5](#X11_Forwarding.xhtml__idTextAnchor324), return to the sessions screen, and open the connection (saving the session beforehand if you plan to use it again):

![](image/putty_enable_x11_forwarding.jpg)

Figure 19-5

Log into the Ubuntu system within the PuTTY session window and run a desktop app. After a short delay, the app will appear on the Windows desktop in its own window. Any dialogs the app opens will also appear in separate windows, just as they would on the Ubuntu GNOME desktop. [Figure 19-6](#X11_Forwarding.xhtml__idTextAnchor325), for example, shows the Ubuntu nm-connection-editor tool displayed on a Windows 11 system:

![](image/x11_windows_forwarding.jpg)

Figure 19-6

19.6 Summary

For situations where remote access to individual Ubuntu desktop applications is required as opposed to the entire GNOME desktop, X11 forwarding provides a lightweight solution to remotely displaying graphical applications. The system on which the applications are to appear must be running an X Window System-based desktop environment (such as GNOME) or have an X server installed and running. Once X11 forwarding has been enabled on the remote server and a secure SSH connection established from the local system using the X11 forwarding option, most applications can be displayed remotely on the local X server.

20\. Using NFS on Ubuntu 23.04 to Share Files with Remote Systems

Ubuntu provides two mechanisms for sharing files and folders with other systems on a network. One approach is to use a technology called Samba. Samba is based on Microsoft Windows Folder Sharing and allows Linux systems to make folders accessible to Windows systems and access Windows-based folder shares from Linux. This approach can also be used to share folders between other Linux and UNIX-based systems if they have Samba support installed and configured. This is the most popular approach to sharing folders in heterogeneous network environments. Folder sharing using Samba is covered in [“Sharing Files between Ubuntu 23.04 and Windows with Samba”](#Samba_File_Sharing.xhtml__idTextAnchor340).

Another option, explicitly targeted at sharing folders between Linux and UNIX-based systems, uses Network File System (NFS). NFS allows the file system on one Linux computer to be accessed over a network connection by another Linux or UNIX system. NFS was originally developed by Sun Microsystems (now part of Oracle Corporation) in the 1980s and remains the standard mechanism for sharing remote Linux/UNIX file systems.

NFS is very different from the Windows SMB resource-sharing technology used by Samba. This chapter will look at the network-based sharing of folders between Ubuntu and other UNIX/Linux-based systems using NFS.

20.1 Ensuring NFS Services are running on Ubuntu

The first task is to verify that the NFS services are installed and running on your Ubuntu system. This can be achieved from the command line or the Cockpit interface.

Begin by installing the NFS service by running the following command from a terminal window:

# apt install nfs-kernel-server

Next, configure the service to automatically start at boot time:

# systemctl enable nfs-kernel-server

Once the service has been enabled, start it as follows:

# systemctl start nfs-kernel-server

20.2 Configuring the Firewall to Allow NFS Traffic

Next, the firewall needs to be configured to allow NFS traffic. If the Uncomplicated Firewall is enabled, run the following command to add a rule to allow NFS traffic:

# ufw allow nfs

If, on the other hand, you are using firewalld, run the following firewall-cmd commands where <zone> is replaced by the appropriate zone for your firewall and system configuration:

# firewall-cmd --zone=<zone> --permanent --add-service=mountd

# firewall-cmd --zone=<zone> --permanent --add-service=nfs

# firewall-cmd --zone=<zone> --permanent --add-service=rpc-bind

# firewall-cmd --reload

20.3 Specifying the Folders to be Shared

Now that NFS is running and the firewall has been configured, we need to specify which parts of the Ubuntu file system may be accessed by remote Linux or UNIX systems. These settings can be declared in the /etc/exports file, which must be modified to export the directories for remote access via NFS. The syntax for an export line in this file is as follows:

<export> <host1>(<options>) <host2>(<options>)...

In the above line, <export> is replaced by the directory to be exported, <host1> is the name or IP address of the system to which access is being granted, and <options> represents the restrictions that are to be imposed on that access (read-only, read-write, etc.). Multiple host and options entries may be placed on the same line if required. For example, the following line grants read-only permission to the /datafiles directory to a host with the IP address 192.168.2.38:

/datafiles 192.168.2.38(ro,no_subtree_check)

The use of wildcards is permitted to apply an export to multiple hosts. For example, the following line permits read-write access to /home/demo to all external hosts:

/home/demo *(rw,no_subtree_check)

While most Linux distributions default to the recommended no_subtree_check setting, the Ubuntu implementation of NFS requires that either the no_subtree_check or subtree_check is included in all export directives.

For this chapter, we will configure the /etc/exports file as follows:

/tmp *(rw,sync,no_subtree_check)

/vol1 192.168.86.42(ro,sync,no_subtree_check)

Once configured, the table of exported file systems maintained by the NFS server needs to be updated with the latest /etc/exports settings using the exportfs command as follows:

# exportfs -a

It is also possible to view the current share settings from the command line using the exportfs tool:

# exportfs

The above command will generate the following output:

/vol1 192.168.86.42

/tmp <world>

20.4 Accessing Shared Folders

The shared folders may be accessed from a client system by mounting them manually from the command line. However, before attempting to mount a remote NFS folder, the nfs-common package must first be installed on the client system:

# apt install nfs-common

To mount a remote folder from the command line, open a terminal window and create a directory where you would like the remote shared folder to be mounted:

$ mkdir /home/demo/tmp

Next, enter the command to mount the remote folder using either the IP address or hostname of the remote NFS server, for example:

$ sudo mount -t nfs 192.168.86.24:/tmp /home/demo/tmp

The remote /tmp folder will then be mounted on the local system. Once mounted, the /home/demo/tmp folder will contain the remote folder and all its contents.

Options may also be specified when mounting a remote NFS filesystem. The following command, for example, mounts the same folder but configures it to be read-only:

$ sudo mount -t nfs -o ro 192.168.86.24:/tmp /home/demo/tmp

20.5 Mounting an NFS Filesystem on System Startup

It is also possible to configure an Ubuntu system to automatically mount a remote file system each time it starts up by editing the /etc/fstab file. When loaded into an editor, it will likely resemble the following:

/dev/disk/by-id/dm-uuid-LVM-Qv7p2RxcHOSG6RjnkgR21xkhaCQ9NC / ext4 defaults 0 1

# /boot was on /dev/nvme0n1p2 during curtin installation

/dev/disk/by-uuid/aa49b362-6c42-49a6-98ba-7a256a96b4b8 /boot ext4 defaults 0 1

# /boot/efi was on /dev/nvme0n1p1 during curtin installation

/dev/disk/by-uuid/576B-B5F5 /boot/efi vfat defaults 0 1

To mount, for example, a folder with the path /tmp, which resides on a system with the IP address 192.168.86.24 in the local folder with the path /home/demo/tmp (note that this folder must already exist), add the following line to the /etc/fstab file:

192.168.86.24:/tmp /home/demo/tmp nfs rw 0 0

Next time the system reboots, the /tmp folder on the remote system will be mounted on the local /home/demo/tmp mount point. All the files in the remote folder can then be accessed as if they reside on the local hard disk drive.

20.6 Unmounting an NFS Mount Point

Once a remote file system is mounted using NFS, it can be unmounted using the umount command with the local mount point as the command-line argument. The following command, for example, will unmount our example filesystem mount point:

$ sudo umount /home/demo/tmp

20.7 Accessing NFS Filesystems in Cockpit

In addition to mounting a remote NFS file system on a client using the command line, it is also possible to perform mount operations from within the Cockpit web interface. Assuming that Cockpit has been installed and configured on the client system, log into the Cockpit interface from within a web browser and select the Storage option from the left-hand navigation panel. If the Storage option is not listed, the cockpit-storaged package will need to be installed:

# apt install cockpit-storaged

# systemctl restart cockpit.socket

Once the Cockpit service has restarted, log back into the Cockpit interface, at which point the Storage option should now be visible.

Once selected, the main storage page will include a section listing any currently mounted NFS file systems, as illustrated in [Figure 20-1](#NFS_File_Sharing.xhtml__idTextAnchor336):

![](image/rhel_cockpit_nfs.jpg)

Figure 20-1

To mount a remote filesystem, click on the ‘+’ button highlighted above and enter information about the remote NFS server and file system share together with the local mount point and any necessary options into the resulting dialog before clicking on the Add button:

![](image/rhel_cockpit_nfs_new.jpg)

Figure 20-2

To modify, unmount or remove an NFS filesystem share, select the corresponding mount in the NFS Mounts list ([Figure 20-1](#NFS_File_Sharing.xhtml__idTextAnchor336) above) to display the page shown in [Figure 20-3](#NFS_File_Sharing.xhtml__idTextAnchor337) below:

![](image/rhel_cockpit_nfs_modify.jpg)

Figure 20-3

Within this screen, perform tasks such as changing the server or mount points or unmounting the file system. For example, the Remove option unmounts the file system and deletes the entry from the /etc/fstab file so that it does not re-mount the next time the system reboots.

20.8 Summary

The Network File System (NFS) is a client/server-based system, originally developed by Sun Microsystems, which provides a way for Linux and Unix systems to share filesystems over a network. NFS allows a client system to access and (subject to permissions) modify files located on a remote server as though those files are stored on a local filesystem. This chapter has provided an overview of NFS and outlined the options for configuring client and server systems using the command line or the Cockpit web interface.

21\. Sharing Files between Ubuntu 23.04 and Windows with Samba

Although Linux has made some inroads into the desktop market, its origins and future are very much server based. It is unsurprising, therefore, that Ubuntu can act as a file server. It is also common for Ubuntu and Windows systems to be used side by side in networked environments. Therefore, it is a common requirement that files on an Ubuntu system be accessible to Linux, UNIX, and Windows-based systems over network connections. Similarly, shared folders and printers residing on Windows systems may also need to be accessible from Ubuntu-based systems.

Windows systems share resources such as file systems and printers using the Server Message Block (SMB) protocol. For an Ubuntu system to serve such resources over a network to a Windows system and vice versa, it must support SMB. This is achieved using a technology called Samba. In addition to providing integration between Linux and Windows systems, Samba may also provide folder sharing between Linux systems (as an alternative to NFS covered in the previous chapter).

In this chapter, we will look at the steps necessary to share file system resources and printers on an Ubuntu system with remote Windows and Linux systems and to access Windows resources from Ubuntu.

21.1 Accessing Windows Resources from the GNOME Desktop

Before getting into more details of Samba sharing, it is worth noting that if all you want to do is access Windows shared folders from within the GNOME desktop, then support is already provided within the GNOME Files application. The Files application is located in the dash as highlighted in [Figure 21-1](#Samba_File_Sharing.xhtml__idTextAnchor342):

![](image/ubuntu_files_icon.jpg)

Figure 21-1

Once launched, select the Other Locations option in the left-hand navigation panel, followed by the Windows Network icon in the main panel to browse available Windows resources:

![](image/ubuntu_files_windows_network.jpg)

Figure 21-2

21.2 Samba and Samba Client

Samba allows both Ubuntu resources to be shared with Windows systems and Windows resources to be shared with Ubuntu systems. Ubuntu accesses Windows resources using the Samba client. On the other hand, Ubuntu resources are shared with Windows systems by installing and configuring the Samba service.

21.3 Installing Samba on Ubuntu

The default settings used during the Ubuntu installation do not typically install the necessary Samba packages. Unless you specifically requested that Samba be installed, it is unlikely that you have Samba installed on your system. To check whether Samba is installed, open a terminal window and run the following command and check for the [installed] indicator for each package:

# apt -qq list samba-common samba smbclient

Any missing packages can be installed using the apt  command-line tool:

# apt install samba-common samba smbclient

21.4 Configuring the Ubuntu Firewall to Enable Samba

Next, the firewall protecting the Ubuntu system must be configured to allow Samba traffic. If you are using the Uncomplicated Firewall (ufw) run the following command:

# ufw allow samba

Alternatively, if you are using firewalld, run the firewall-cmd command as follows:

# firewall-cmd --permanent --add-port={139/tcp,445/tcp}

# firewall-cmd --reload

Before starting the Samba service, some configuration steps are necessary to define how the Ubuntu system will appear to Windows systems and the resources to be shared with remote clients. Most configuration tasks occur within the /etc/samba/smb.conf file.

21.5 Configuring the smb.conf File

Samba is a highly flexible and configurable system that provides many options for controlling how resources are shared on Windows networks. Unfortunately, this flexibility can lead to the sense that Samba is overly complex. In reality, however, the typical installation does not need many configuration options, and the learning curve to set up a basic configuration is relatively short.

For this chapter, we will look at joining an Ubuntu system to a Windows workgroup and setting up a directory as a shared resource that a specific user can access. This is a configuration known as a standalone Samba server. More advanced configurations, such as integrating Samba within an Active Directory environment, are also available, though these are outside the scope of this book.

The first step in configuring Samba is to edit the /etc/samba/smb.conf file.

21.5.1 Configuring the [global] Section

The smb.conf file is divided into sections. The first section is the [global] section, where settings that apply to the entire Samba configuration can be specified. While these settings are global, each option may be overridden within other configuration file sections.

The first task is defining the Windows workgroup name on which the Ubuntu resources will be shared. This is controlled via the workgroup = directive of the [global] section, which by default is configured as follows:

workgroup = WORKGROUP

Begin by changing this to the actual name of the workgroup if necessary.

In addition to the workgroup setting, the other settings indicate that this is a standalone server on which user passwords will protect the shared resources. Before moving on to configuring the resources to be shared, other parameters also need to be added to the [global] section as follows:

[global]

.

.

        netbios name = LinuxServer

The “netbios name” property specifies the name by which the server will be visible to other systems on the network.

21.5.2 Configuring a Shared Resource

The next step is configuring the shared resources (in other words, the resources that will be accessible from other systems on the Windows network). To achieve this, the section is given a name by which it will be referred when shared. For example, if we plan to share the /sampleshare directory of our Ubuntu system, we might entitle the section [sampleshare]. In this section, a variety of configuration options are possible. For this example, however, we will define the directory that is to be shared, indicate that the directory is both browsable and writable, and declare the resource public so that guest users can gain access:

[sampleshare]

        comment = Example Samba share

        path = /sampleshare

        browseable = Yes

        public = yes

        writable = yes

To restrict access to specific users, the “valid users” property may be used, for example:

valid users = demo, bobyoung, marcewing

21.5.3 Removing Unnecessary Shares

The smb.conf file is pre-configured with sections for sharing printers and the home folders of the users on the system. If these resources do not need to be shared, the corresponding sections can be commented out so that Samba ignores them. In the following example, the [homes] section has been commented out:

.

.

#[homes]

# comment = Home Directories

# valid users = %S, %D%w%S

# browseable = No

# read only = No

# inherit acls = Yes

.

.

21.6 Creating a Samba User

Any user that requires access to a Samba shared resource must be configured as a Samba User and assigned a password. This task is achieved using the smbpasswd command-line tool. Consider, for example, that a user named demo is required to be able to access the /sampleshare directory of our Ubuntu system from a Windows system. To fulfill this requirement, we must add demo as a Samba user as follows:

# smbpasswd -a demo

New SMB password:

Retype new SMB password:

Added user demo.

Now that we have completed the configuration of an elementary Samba server, it is time to test our configuration file and then start the Samba services.

21.7 Testing the smb.conf File

The settings in the smb.conf file may be checked for errors using the testparm command-line tool as follows:

# testparm

Load smb config files from /etc/samba/smb.conf

Loaded services file OK.

Weak crypto is allowed

Server role: ROLE_STANDALONE

Press enter to see a dump of your service definitions

# Global parameters

[global]

log file = /var/log/samba/%m.log

netbios name = LINUXSERVER

printcap name = cups

security = USER

wins support = Yes

idmap config * : backend = tdb

cups options = raw

[sampleshare]

comment = Example Samba share

guest ok = Yes

path = /sampleshare

read only = No

[homes]

browseable = No

comment = Home Directories

inherit acls = Yes

read only = No

valid users = %S %D%w%S

[printers]

browseable = No

comment = All Printers

create mask = 0600

path = /var/tmp

printable = Yes

.

.

21.8 Starting the Samba and NetBIOS Name Services

For an Ubuntu server to operate within a Windows network, the Samba (SMB) and NetBIOS nameservice (NMB) services must be started. Optionally, also enable the services so that they start each time the system boots:

# systemctl enable smbd nmbd

# systemctl start smbd nmbd

Before attempting to connect from a Windows system, use the smbclient utility to verify that the share is configured:

# smbclient -U demo -L localhost

Password for [WORKGROUP\demo]:

Sharename Type Comment

--------- ---- -------

sampleshare Disk Example Samba share

print$ Disk Printer Drivers

IPC$ IPC IPC Service (demoserver server (Samba, Ubuntu))

demo Disk Home Directories

HP_OfficeJet_Pro_9020_series_9F6907 Printer HP_OfficeJet_Pro_9020_series

21.9 Accessing Samba Shares

Now that the Samba resources are configured and the services are running, it is time to access the shared resource from a Windows system. On a suitable Windows system on the same workgroup as the Ubuntu system, open Windows Explorer and right-click on the Network entry in the side panel to display the menu shown in [Figure 21-3](#Samba_File_Sharing.xhtml__idTextAnchor356):

![](image/windows_map_ubuntu_drive.jpg)

Figure 21-3

Select the Map network drive... menu option to display the dialog illustrated in [Figure 21-4](#Samba_File_Sharing.xhtml__idTextAnchor357):

![](image/windows_map_ubuntu_drive_folder.jpg)

Figure 21-4

Select a drive letter and enter the path to a samba share. For example, assuming that the server name is LinuxServer and the samba user name is demo, the path to the user’s home folder would be as follows:

\\LINUXSERVER\demo

Enable the Connect using different credentials checkbox and click finish. When the network credentials dialog appears, enter the Samba user name and the password that was assigned earlier using the smbpasswd command:

![](image/windows_map_ubuntu_drive_credentials.jpg)

Figure 21-5

After the connection is established, a new Windows Explorer dialog will appear containing the contents of the shared Ubuntu folder:

![](image/windows_mapped_ubuntu_drive.jpg)

Figure 21-6

21.10 Accessing Windows Shares from Ubuntu

As previously mentioned, Samba is a two-way street, allowing not only Windows systems to access files and printers hosted on an Ubuntu system but also allowing the Ubuntu system to access shared resources on Windows systems. This is achieved using the samba-client package, installed at this chapter’s start. If it is not currently installed, install it from a terminal window as follows:

# apt install smbclient

Shared resources on a Windows system can be accessed from the Ubuntu desktop using the Files application or the command-line prompt using the smbclient and mount tools. The steps in this section assume that the Windows system has enabled appropriate network-sharing settings.

To access any shared resources on a Windows system using the GNOME desktop, launch the Files application and select the Other Locations option. This will display the screen shown in [Figure 21-7](#Samba_File_Sharing.xhtml__idTextAnchor359) below, including an icon for the Windows Network (if one is detected):

![](image/rhel_8_connect_to_windows_share.jpg)

Figure 21-7

Selecting the Windows Network option will display the Windows systems detected on the network and allow access to any shared resources.

![](image/rhel_8_files_windows_10_share.jpg)

Figure 21-8

Alternatively, the Connect to Server option may be used to connect to a specific system. Note that the name or IP address of the remote system must be prefixed by smb:// and may be followed by the path to a specific shared resource, for example:

smb://WinServer/Documents

Without a desktop environment, a remote Windows share may be mounted from the command line using the mount command and specifying the cifs filesystem type. The following command, for example, mounts a share named Documents located on a Windows system named WinServer at a local mount point named /winfiles:

# mount -t cifs //WinServer/Documents /winfiles -o user=demo

21.11 Summary

In this chapter, we have looked at how to configure an Ubuntu system to act as both a Samba client and server, allowing the sharing of resources with Windows systems. Topics covered included the installation of Samba client and server packages and configuring Samba as a standalone server. In addition, the basic concepts of SELinux were introduced together with the steps to provide Samba access to a shared resource.

22\. An Overview of Virtualization Techniques

Virtualization is the ability to run multiple operating systems simultaneously on a single computer system. While not necessarily a new concept, Virtualization has come to prominence in recent years because it provides a way to fully utilize the CPU and resource capacity of a server system while providing stability (in that if one virtualized guest system crashes, the host and any other guest systems continue to run).

Virtualization is also helpful in trying out different operating systems without configuring dual boot environments. For example, you can run Windows in a virtual machine without re-partitioning the disk, shut down Ubuntu, and boot from Windows. Instead, you start up a virtualized version of Windows as a guest operating system. Similarly, virtualization allows you to run other Linux distributions within an Ubuntu system, providing concurrent access to both operating systems.

When deciding on the best approach to implementing virtualization, clearly understanding the different virtualization solutions currently available is essential. Therefore, this chapter’s purpose is to describe in general terms the virtualization techniques in common use today.

22.1 Guest Operating System Virtualization

Guest OS virtualization, also called application-based virtualization, is the most straightforward concept to understand. In this scenario, the physical host computer runs a standard unmodified operating system such as Windows, Linux, UNIX, or macOS. Running on this operating system is a virtualization application that executes in much the same way as any other application, such as a word processor or spreadsheet, would run on the system. Within this virtualization application, one or more virtual machines are created to run the guest operating systems on the host computer.

The virtualization application is responsible for starting, stopping, and managing each virtual machine and essentially controlling access to physical hardware resources on behalf of the individual virtual machines. The virtualization application also engages in a process known as binary rewriting, which involves scanning the instruction stream of the executing guest system and replacing any privileged instructions with safe emulations. This makes the guest system think it is running directly on the system hardware rather than in a virtual machine within an application.

The following figure illustrates guest OS-based virtualization:

![](image/guest_os_virtualization.jpg)

Figure 22-1

As outlined in the above diagram, the guest operating systems operate in virtual machines within the virtualization application, which, in turn, runs on top of the host operating system in the same way as any other application. The multiple layers of abstraction between the guest operating systems and the underlying host hardware are not conducive to high levels of virtual machine performance. However, this technique has the advantage that no changes are necessary to host or guest operating systems, and no special CPU hardware virtualization support is required.

22.2 Hypervisor Virtualization

In hypervisor virtualization, the task of a hypervisor is to handle resource and memory allocation for the virtual machines and provide interfaces for higher-level administration and monitoring tools. Hypervisor-based solutions are categorized as being either Type-1 or Type-2\.

Type-2 hypervisors (sometimes called hosted hypervisors) are installed as software applications that run on top of the host operating system, providing virtualization capabilities by coordinating access to resources such as the CPU, memory, and network for guest virtual machines. Figure 21-2 illustrates the typical architecture of a system using Type-2 hypervisor virtualization:

![](image/type-2_hypervisor_virtualization.jpg)

Figure 22-2

To understand how Type-1 hypervisors work, it helps to understand Intel x86 processor architecture. The x86 family of CPUs provides a range of protection levels known as rings in which code can execute. Ring 0 has the highest level privilege, and it is in this ring that the operating system kernel normally runs. Code executing in ring 0 is said to be running in system space, kernel mode, or supervisor mode. All other code, such as applications running on the operating system, operate in less privileged rings, typically ring 3.

In contrast to Type-2 hypervisors, Type-1 hypervisors (also referred to as metal or native hypervisors) run directly on the hardware of the host system in ring 0\. With the hypervisor occupying ring 0 of the CPU, the kernels for any guest operating systems running on the system must run in less privileged CPU rings. Unfortunately, most operating system kernels are written explicitly to run in ring 0 because they need to perform tasks only available in that ring, such as the ability to execute privileged CPU instructions and directly manipulate memory. Several different solutions to this problem have been devised in recent years, each of which is described below:

22.2.1 Paravirtualization

Under paravirtualization, the kernel of the guest operating system is modified specifically to run on the hypervisor. This typically involves replacing privileged operations that only run in ring 0 of the CPU with calls to the hypervisor (known as hypercalls). The hypervisor, in turn, performs the task on behalf of the guest kernel. Unfortunately, this typically limits support to open-source operating systems such as Linux, which may be freely altered, and proprietary operating systems where the owners have agreed to make the necessary code modifications to target a specific hypervisor. These issues notwithstanding, the ability of the guest kernel to communicate directly with the hypervisor results in greater performance levels than other virtualization approaches.

22.2.2 Full Virtualization

Full virtualization provides support for unmodified guest operating systems. The term unmodified refers to operating system kernels that have not been altered to run on a hypervisor and, therefore, still execute privileged operations as though running in ring 0 of the CPU. In this scenario, the hypervisor provides CPU emulation to handle and modify privileged and protected CPU operations made by unmodified guest operating system kernels. Unfortunately, this emulation process requires both time and system resources to operate, resulting in inferior performance levels when compared to those provided by paravirtualization.

22.2.3 Hardware Virtualization

Hardware virtualization leverages virtualization features built into the latest generations of CPUs from both Intel and AMD. These technologies, called Intel VT and AMD-V, respectively, provide extensions necessary to run unmodified guest virtual machines without the overheads inherent in full virtualization CPU emulation. In very simplistic terms, these processors provide an additional privilege mode (ring -1) above ring 0 in which the hypervisor can operate, thereby leaving ring 0 available for unmodified guest operating systems.

The following figure illustrates the Type-1 hypervisor approach to virtualization:

![](image/type-1_hypervisor_virtualization.jpg)

Figure 22-3

As outlined in the above illustration, in addition to the virtual machines, an administrative operating system or management console also runs on top of the hypervisor allowing the virtual machines to be managed by a system administrator.

22.3 Virtual Machine Networking

Virtual machines will invariably need to be connected to a network to be of any practical use. One option is for the guest to be connected to a virtual network running within the host computer’s operating system. In this configuration, any virtual machines on the virtual network can see each other, but Network Address Translation (NAT) provides access to the external network. When using the virtual network and NAT, each virtual machine is represented on the external network (the network to which the host is connected) using the IP address of the host system. This is the default behavior for KVM virtualization on Ubuntu and generally requires no additional configuration. Typically, a single virtual network is created by default, represented by the name default and the device virbr0.

For guests to appear as individual and independent systems on the external network (i.e., with their own IP addresses), they must be configured to share a physical network interface on the host. The quickest way to achieve this is to configure the virtual machine to use the “direct connection” network configuration option (also called MacVTap), which will provide the guest system with an IP address on the same network as the host. Unfortunately, while this gives the virtual machine access to other systems on the network, it is not possible to establish a connection between the guest and the host when using the MacVTap driver.

A better option is to configure a network bridge interface on the host system to which the guests can connect. This provides the guest with an IP address on the external network while also allowing the guest and host to communicate, a topic covered in the chapter entitled [“Creating an Ubuntu 23.04 KVM Networked Bridge Interface”](#KVM_Network_Bridge.xhtml__idTextAnchor407).

22.4 Summary

Virtualization is the ability to run multiple guest operating systems within a single host operating system. Several approaches to virtualization have been developed, including a guest operating system and hypervisor virtualization. Hypervisor virtualization falls into two categories known as Type-1 and Type-2\. Type-2 virtualization solutions are categorized as paravirtualization, full virtualization, and hardware virtualization, the latter using special virtualization features of some Intel and AMD processor models.

Virtual machine guest operating systems have several options in terms of networking, including NAT, direct connection (MacVTap), and network bridge configurations.

23\. Installing KVM Virtualization on Ubuntu 23.04

Earlier versions of Ubuntu provided two virtualization platforms: Kernel-based Virtual Machine (KVM) and Xen. In recent releases, support for Xen has been removed, leaving KVM as the only bundled virtualization option supplied with Ubuntu. In addition to KVM, third-party solutions are available in products such as VMware and Oracle VirtualBox. Since KVM is supplied with Ubuntu, however, this virtualization solution will be covered in this and subsequent chapters.

Before plunging into installing and running KVM, it is worth discussing how it fits into the various types of virtualization outlined in the previous chapter.

23.1 An Overview of KVM

KVM is categorized as a Type-1 hypervisor virtualization solution that implements full virtualization with support for unmodified guest operating systems using Intel VT and AMD-V hardware virtualization support.

KVM differs from many other Type-1 solutions in that it turns the host Linux operating system into the hypervisor, allowing bare metal virtualization to be implemented while running a complete, enterprise-level host operating system.

23.2 KVM Hardware Requirements

Before proceeding with this chapter, we must discuss the hardware requirements for running virtual machines within a KVM environment. First and foremost, KVM virtualization is only available on certain processor types. As previously discussed, these processors must include either Intel VT or AMD-V technology.

To check for virtualization support, run the lscpu command in a terminal window:

# lscpu | grep Virtualization:

If the system contains a CPU with Intel VT support, the above command will provide the following output:

Virtualization: VT-x

Alternatively, the following output will be displayed when a CPU with AMD-V support is detected:

Virtualization: AMD-V

If the CPU does not support virtualization, no output will be displayed by the above lscpu command.

Note that while the above commands only report whether the processor supports the respective feature, it does not indicate whether it is currently enabled in the BIOS. This is because, in practice, virtualization support is typically disabled by default in the BIOS of most systems. Therefore, you should check your BIOS settings to ensure the appropriate virtualization technology is enabled before proceeding with this tutorial.

Unlike a dual-booting environment, a virtualized environment involves running two or more complete operating systems concurrently on a single computer system. This means the system must have enough physical memory, disk space, and CPU processing power to comfortably accommodate all these systems in parallel. Therefore, before beginning the configuration and installation process, check on the minimum system requirements for both Ubuntu and your chosen guest operating systems and verify that your host system has sufficient resources to handle the requirements of both systems.

23.3 Preparing Ubuntu for KVM Virtualization

Unlike Xen, it is not necessary to run a special version of the kernel to support KVM. As a result, KVM support is already available for use with the standard kernel via installing a KVM kernel module, thereby negating the need to install and boot from a special kernel.

To avoid conflicts, however, if a Xen-enabled kernel is currently running on the system, reboot the system and select a non-Xen kernel from the boot menu before proceeding with the remainder of this chapter.

The tools required to set up and maintain a KVM-based virtualized system are only installed by default if selected explicitly during the Ubuntu operating system installation process. To install the KVM tools from the command prompt, execute the following command in a terminal window:

# apt install qemu-kvm libvirt-clients libvirt-daemon-system bridge-utils

If you have access to a graphical desktop environment, the virt-manager package is also recommended:

# apt install virt-manager

23.4 Verifying the KVM Installation

It is worthwhile checking that the KVM installation worked correctly before moving forward. When KVM is installed and running, two modules will have been loaded into the kernel. The presence or otherwise of these modules can be verified in a terminal window by running the lsmod command:

# lsmod | grep kvm

Assuming that the installation was successful, the above command should generate output similar to the following:

kvm_intel 438272 0

kvm 1138688 21 kvm_intel

Note that if the system contains an AMD processor, the kvm module will likely read kvm_amd rather than kvm_intel.

The installation process should also have configured the libvirtd daemon to run in the background. Once again, using a terminal window, run the following command to ensure libvirtd is running:

# systemctl status libvirtd

● libvirtd.service - Virtualization daemon

     Loaded: loaded (/lib/systemd/system/libvirtd.service; enabled; vendor pres>

     Active: active (running) since Wed 2023-07-19 11:15:13 EDT; 21h ago

If the process is not running, start it as follows:

# systemctl enable --now libvirtd

# systemctl start libvirtd

If the desktop environment is available, run the virt-manager tool by selecting Activities and entering “virt” into the search box. When the Virtual Machine Manager icon appears, click it to launch it. When loaded, the manager should appear as illustrated in the following figure:

![](image/ubuntu_virt-manager.jpg)

Figure 23-1

If the QEMU/KVM entry is not listed, select the File -> Add Connection menu option and, in the resulting dialog, select the QEMU/KVM Hypervisor before clicking on the Connect button:

![](image/ubuntu_virt-manager_add_connection.jpg)

Figure 23-2

If the manager is not currently connected to the virtualization processes, right-click on the entry listed and select Connect from the popup menu.

23.5 Summary

KVM is a Type-1 hypervisor virtualization solution that implements full virtualization with support for unmodified guest operating systems using Intel VT and AMD-V hardware virtualization support. It is the default virtualization solution bundled with Ubuntu and can be installed quickly and easily on any Ubuntu system with appropriate processor support. With KVM support installed and enabled, the following chapters will outline some options for installing and managing virtual machines on an Ubuntu host.

24. Creating KVM Virtual Machines on Ubuntu 23.04 using Cockpit

KVM-based virtual machines can easily be configured on Ubuntu using the virt-install command-line tool, the virt-manager GUI tool, or the Virtual Machines module of the Cockpit web console. This chapter will use Cockpit to install an operating system as a KVM guest on an Ubuntu host. The chapter titled [“Creating KVM Virtual Machines on Ubuntu 23.04 using virt-manager”](#KVM_virt-manager.xhtml__idTextAnchor389) will cover using the virt-manager tool to create new virtual machines.

The next chapter, [“Creating KVM Virtual Machines with virt-install and virsh”](#KVM_Create_VM_Command-line.xhtml__idTextAnchor400)  will cover the command-line approach to virtual machine creation.

24.1 Installing the Cockpit Virtual Machines Module

The virtual machines module may not be included in a standard Cockpit installation by default. Assuming that Cockpit is installed and configured, the virtual machines module may be installed as follows:

# apt install cockpit-machines

Once installed, the Virtual Machines option (marked A in [Figure 24-1](#KVM_Create_VM.xhtml__idTextAnchor377)) will appear in the navigation panel the next time you log into the Cockpit interface:

![](image/cockpit_virtual_machines.jpg)

Figure 24-1

24.2 Creating a Virtual Machine in Cockpit

To create a virtual machine in Cockpit, click the Create VM button marked B in [Figure 24-1](#KVM_Create_VM.xhtml__idTextAnchor377) to display the creation dialog.

Within the dialog, enter a name for the machine and choose whether the installation media is in the form of an ISO accessible via a URL or a local filesystem path, or select the vendor and operating system type information for the guest request and choose the Download an OS option to have the installation image downloaded automatically during the installation process.

Also, specify the size of the virtual disk drive to be used for the operating system installation and the amount of memory to be allocated to the virtual machine:

![](image/ubuntu_cockpit_create_vm.jpg)

Figure 24-2

Click on the Create and edit button to build the virtual machine. After the creation process is complete, select the new VM from the list to display the configuration details, as shown in [Figure 24-3](#KVM_Create_VM.xhtml__idTextAnchor380):

![](image/rhel_cockpit_vm_overview.jpg)

Figure 24-3

As described in [“An Overview of Virtualization Techniques”](#Virtualization_Overview.xhtml__idTextAnchor361) KVM provides virtual machines with several options in terms of network configuration. To view and change the network settings of a virtual machine, scroll down to the Network interfaces section of the VM Overview screen and click the Edit button:

![](image/ubuntu_cockpit_vm_network_interfaces.jpg)

Figure 24-4

In the resulting dialog, the Network Type menu may be used to change the type of network connection, for example, from Virtual network (NAT) to direct attachment (MacVTap) or Bridge to LAN.

24.3 Starting the Installation

To start the new virtual machine and install the guest operating system from the designated installation media, click the Install button at the top of the overview page. Cockpit will start the virtual machine and update Console view where the guest OS screen will appear:

![](image/ubuntu_cockpit_vm_running.jpg)

Figure 24-5

If the installation fails, check the message to see if an error occurred when opening the installation image. This usually occurs because the QEMU emulator runs as a user named qemu, which does not have access to the directory in which the ISO installation image is located. To resolve this issue, open a terminal window (or connect with SSH if the system is remote), change directory to the location of the ISO image file, and add the libvirt-qemu user to the access control list (ACL) of the parent directory as follows:

# cd /path/to/iso/directory

# setfacl -m u:libvirt-qemu:x ..

After making this change, check the setting as follows:

# getfacl ..

# file: ..

# owner: demo

# group: demo

user::rwx

user:libvirt-qemu:--x

group::r-x

mask::r-x

other::---

Once these changes have been made, click the Install button again to complete the installation.

To complete the installation, interact with the screen in the Consoles view just as you would if you were installing the operating system on physical hardware. If the console is too small to accommodate the entire guest operating system screen, click the Expand button in the top right-hand corner.

It is also possible to connect with and display the graphical console for the VM from outside the Cockpit browser session using the virt-viewer tool. To install virt-viewer on an Ubuntu system, run the following command:

# apt install virt-viewer

The virt-viewer tool is also available for Windows systems and can be downloaded from the following URL:

[https://virt-manager.org/download/](https://virt-manager.org/download/)

To connect with a virtual machine running on the local host, run virt-viewer and select the virtual machine to which you wish to connect from the resulting dialog:

![](image/ubuntu-virt-viewer_vm_list.jpg)

Figure 24-6

The above command will list system-based virtual machines. To list and access session-based guests, launch virt-viewer as follows:

$ virt-viewer --connect qemu:///session

Alternatively, it is also possible to specify the virtual machine name and bypass the selection dialog entirely, for example:

# virt-viewer demo-vm-guest

To connect a virt-viewer instance to a virtual machine running on a remote host using SSH, the following command can be used:

$ virt-viewer --connect qemu+ssh://<user>@<host>/system <guest name>

For example:

$ virt-viewer --connect qemu+ssh://root@192.168.1.122/system demo_vm_guest

When using this technique, it is important to note that you will be prompted twice for the user password before the connection is fully established.

Once the virtual machine has been created, the Cockpit interface can monitor the machine and perform tasks such as rebooting, shutting down, or deleting the guest system. An option is also included on the Disks panel to add disks to the virtual machine configuration.

24.4 Working with Storage Volumes and Storage Pools

When a virtual machine is created, it will usually have at least one virtual disk drive. The images that represent these virtual disk drives are stored in storage pools. A storage pool can be an existing directory on a local filesystem, a filesystem partition, a physical disk device, Logical Volume Management (LVM) volume group, or even a remote network file system (NFS).

Each storage pool is divided into one or more storage volumes. Storage volumes are typically individual image files, each representing a single virtual disk drive, but they can also take the form of physical disk partitions, entire disk drives, or LVM volume groups.

When a virtual machine was created using the previous steps, a default storage pool was created to store virtual machine images. This default storage pool occupies space on the root filesystem and can be reviewed from within the Cockpit Virtual Machine interface by selecting the Storage Pools option at the top of the panel marked C in [Figure 24-1](#KVM_Create_VM.xhtml__idTextAnchor377) above.

When selected, the screen shown in [Figure 24-7](#KVM_Create_VM.xhtml__idTextAnchor384) below will appear containing a list of storage pools currently configured on the system:

![](image/rhel_cockpit_vm_storage_pools.jpg)

Figure 24-7

In the above example, the default storage pool is located on the root filesystem and stores the virtual machine image in the /var/lib/libvirtd/images directory. To view the storage volumes contained within the pool, select the Storage Volumes tab highlighted in [Figure 24-8](#KVM_Create_VM.xhtml__idTextAnchor385):

![](image/cockpit_virtual_machines_storage_pools.jpg)

Figure 24-8

In the case of the demo guest, the storage volume takes the form of an image file named demo-vm-guest.qcow2. In addition, the pool also includes a storage volume containing the installation ISO image. To find out which storage volume a particular virtual machine uses, return to the main Virtual Machine Cockpit screen, select the virtual machine, and scroll to the Disks panel, as shown in [Figure 24-9](#KVM_Create_VM.xhtml__idTextAnchor386):

![](image/ubuntu_cockpit_vm_disks.jpg)

Figure 24-9

Although using the default storage pool is acceptable for testing purposes and early experimentation, it is recommended that additional pools be created for general virtualization use. To create a new storage pool, display the Storage Pools screen within Cockpit and click on the Create storage pool button to display the dialog shown in [Figure 24-10](#KVM_Create_VM.xhtml__idTextAnchor387):

![](image/rhel_cockpit_vm_create_pool.jpg)

Figure 24-10

In the above example, a new storage pool is being created named MyPool using a file system partition mounted as /MyPool within the local filesystem (the topic of disk drives, partitions, and mount points is covered later in the chapter entitled [“Adding a New Disk Drive to an Ubuntu 23.04 System”](#Adding_New_DIsk.xhtml__idTextAnchor494)). Once created, the pool will be listed within the Cockpit storage pool screen and can contain storage volumes as new virtual machines are created.

24.5 Summary

This chapter has outlined using the Cockpit web-based interface to create and manage KVM-based virtual machines. The Cockpit interface has the advantage of not requiring access to a desktop environment running on the host system. An alternative option is using the virt-manager graphical tool outlined in the next chapter.

25\. Creating KVM Virtual Machines on Ubuntu 23.04 using virt-manager

The previous chapter explored how to create KVM virtual machines on Ubuntu using the Cockpit web tool. With the caveat that virt-manager may one day be discontinued once the Virtual Machines Cockpit extension is fully implemented, this chapter will cover using this tool to create new virtual machines.

25.1 Starting the Virtual Machine Manager

If you have not already done so, install the virt-manager package as follows:

# apt install virt-manager

Next, launch Virtual Machine Manager from the command line in a terminal window by running virt-manager. Once loaded, the virtual machine manager will prompt for the password of the currently active user before displaying the following screen:

![](image/ubuntu_virt-manager1.jpg)

Figure 25-1

The main screen lists the current virtual machines running on the system.

By default, the manager should be connected to the system libvirtd instance. If it is not, connect to the host system by right-clicking on the entry in the list and selecting Connect from the popup menu.

To manage session-based virtual machines, select the File -> Add Connection... menu option to display the dialog shown in [Figure 25-2](#KVM_virt-manager.xhtml__idTextAnchor393):

![](image/ubuntu_virt-manager_add_connection1.jpg)

Figure 25-2

Select QEMU/KVM user session from the Hypervisor menu and click the Connect button within this dialog. On returning to the main virt-manager screen, the QEMU/KVM session should now be listed as shown in [Figure 25-1](#KVM_virt-manager.xhtml__idTextAnchor392) above.

To create a virtual system, click on the new virtual machine button (the far left button in the toolbar) to display the first screen of the New VM wizard. In the Name field, enter a suitably descriptive name for the virtual system. On this screen, also select the location of the media from which the guest operating system will be installed. This can either be a CD or DVD drive, an ISO image file accessible to the local host, a network install using HTTP, FTP, NFS, or PXE, or the disk image from an existing virtual machine:

![](image/ubuntu_virt-manager_iso.jpg)

Figure 25-3

25.2 Configuring the KVM Virtual System

Clicking Forward will display a screen seeking additional information about the installation process. The displayed screen and information required will depend on selections made on the initial screen. For example, if a CD, DVD, or ISO is selected, this screen will ask for the specific location of the ISO file or physical media device. This screen also attempts to identify the type and version of the guest operating system (for example, the Windows version or Linux distribution) based on the specified installation media. If it is unable to do so, turn off the Automatically detect from installation media/source option, type in the first few characters of the operating system name, and select an option from the list of possible matches:

![](image/ubuntu_virt-manager_iso_selected.jpg)

Figure 25-4

Once these settings are complete, click the Forward button to configure CPU and memory settings. The optimal settings will depend on the number of CPUs and amount of physical memory present in the host, together with the requirements of other applications and virtual machines that will run in parallel with the new virtual machine:

![](image/ubuntu_virt-manager_memory.jpg)

Figure 25-5

On the next screen, options are available to create an image disk of a specified size, select a pre-existing volume, or create a storage volume of a specified format (raw, vmdk, ISO, etc.). Unless you have a specific need to use a particular format (for example, you might need to use vmdk to migrate to a VMware-based virtualization environment at a later date) or need to use a dedicated disk or partition, it is generally adequate to specify a size on this screen:

![](image/ubuntu_virt-manager_storage.jpg)

Figure 25-6

If the default settings are used here, the virtual machine will use a storage volume within the default storage pool for the virtual disk drive. To use the custom “MyPool” storage pool created in the preceding chapter, enable the Select or create custom storage option before clicking the Manage... button.

In the storage volume dialog, select the MyPool entry in the left-hand panel, followed by the + button in the main panel to create a new storage volume:

![](image/ubuntu_virt-manager_select_pool.jpg)

Figure 25-7

Note that the + button in the bottom left-hand corner of the dialog may also be used to create new storage pools as an alternative to using the Cockpit interface.

In the configuration screen ([Figure 25-8](#KVM_virt-manager.xhtml__idTextAnchor395)), name the storage volume, select the volume size, and click on the Finish button to create the volume and assign it to the virtual machine:

![](image/ubuntu_virt_manager_volume.jpg)

Figure 25-8

Once these settings are configured, select the new volume and click the Choose Volume button. Then, click the Forward button once more. The final screen displays a summary of the configuration. Review the information displayed. Advanced options are also available to change the virtual network configuration for the guest, as shown in [Figure 25-9](#KVM_virt-manager.xhtml__idTextAnchor396):

![](image/ubuntu_virt_manager_finish.jpg)

Figure 25-9

25.3 Starting the KVM Virtual Machine

Click on the Finish button to begin the creation process. The virtualization manager will create the disk and configure the virtual machine before starting the guest system. Finally, the new virtual machine will appear in the main virt-manager window with the status set to Running as illustrated in [Figure 25-10](#KVM_virt-manager.xhtml__idTextAnchor398):

![](image/ubuntu_virt_manager_vm_running.jpg)

Figure 25-10

By default, the console for the virtual machine should appear in the virtual machine viewer window. To view the console of the running machine at any future time, ensure that it is selected in the virtual machine list and select the Open button from the toolbar. The virtual machine viewer should be ready for the installation process to begin:

![](image/ubuntu_virt-manager_guest_console.jpg)

Figure 25-11

From now on, follow the installation instructions to install the guest OS in the KVM virtual machine.

25.4 Summary

There are several ways to create new KVM-based virtual machines on an Ubuntu host system. This chapter uses the virt-manager graphical tool to create, configure, and run a guest operating system, including creating a new storage volume. With these basics covered, the next chapter will cover the creation of virtual machines from the command line.

26\. Creating KVM Virtual Machines with virt-install and virsh

In the previous chapters, we explored the creation of KVM guest operating systems on an Ubuntu host using Cockpit and the virt-manager graphical tool. This chapter will focus on creating KVM-based virtual machines using the virt-install and virsh command-line tools. These tools provide all the capabilities of the virt-manager and Cockpit options with the added advantage of being used within scripts to automate virtual machine creation. In addition, the virsh command allows virtual machines to be created based on a specification contained within a configuration file.

The virt-install tool is supplied to allow new virtual machines to be created by providing a list of command-line options. This chapter assumes that the necessary KVM tools are installed. Read the chapter [“Installing KVM Virtualization on Ubuntu 23.04”](#KVM_Installation.xhtml__idTextAnchor369)  for details on these requirements.

26.1 Running virt-install to build a KVM Guest System

The virt-install utility accepts a wide range of command-line arguments that provide configuration information related to the virtual machine being created. Some command-line options are mandatory (expressly, name, memory, and disk storage must be provided), while others are optional.

At a minimum, a virt-install command will typically need the following arguments:

•--name - The name to be assigned to the virtual machine.

•--memory - The amount of memory allocated to the virtual machine.

•--disk - The name and location of an image file for storage for the virtual machine. This file will be created by virt-install during the virtual machine creation unless the --import option is specified to indicate an existing image file is to be used.

•--cdrom or --location - Specifies the local path or the URL of a remote ISO image containing the installation media for the guest operating system.

A summary of all the arguments available for use when using virt-install can be found in the man page:

$ man virt-install

26.2 An Example Ubuntu virt-install Command

With reference to the above command-line argument list, we can now look at an example command-line construct using the virt-install tool.

Note that to display the virtual machine and complete the installation, a virt-viewer instance must be connected to the virtual machine after the virt-install utility starts it. By default, virt-install will attempt to launch virt-viewer automatically once the virtual machine starts running. However, if virt-viewer is unavailable, virt-install will wait until a virt-viewer connection is established. For example, the virt-viewer session may be running locally on the host system if it has a graphical desktop, or a connection may be established from a remote client as outlined in the chapter entitled [“Creating KVM Virtual Machines on Ubuntu 23.04 using virt-manager”](#KVM_virt-manager.xhtml__idTextAnchor389).

The following command creates a new KVM virtual machine configured to run a Ubuntu guest using KVM para-virtualization. It creates a new 10GB disk image, assigns 2048MB of RAM to the virtual machine, and configures a virtual CD device for the installation media ISO image:

# virt-install --name demo_vm_guest --memory 2048 --disk path=/tmp/demo_vm_guest.img,size=10 --network network=default --cdrom /home/demo/iso/ubuntu-23.04-desktop-amd64.iso

As the creation process runs, the virt-install command will display status updates of the creation progress:

Starting install...

Allocating 'demo_vm_guest.img' | 10 GB 00:00:01

Running graphical console command: virt-viewer --connect qemu:///system --wait demo_vm_guest

Once the guest system has been created, the virt-viewer screen will appear containing the guest operating system installer loaded from the specified installation media:

![](image/ubuntu_virt-install_running.jpg)

Figure 26-1

From this point, follow the standard installation procedure for the guest operating system.

26.3 Starting and Stopping a Virtual Machine from the Command-Line

Having created the virtual machine from the command line, it stands to reason that you may also need to start it from the command line in the future. This can be achieved using the virsh command-line utility, referencing the name assigned to the virtual machine during creation. For example:

# virsh start demo_vm_guest

Similarly, the virtual machine may be sent a shutdown signal as follows:

# virsh shutdown demo_vm_guest

Suppose the virtual machine fails to respond to the shutdown signal and does not begin a graceful shutdown. In that case, the virtual machine may be destroyed (with the attendant risks of data loss) using the destroy directive:

# virsh destroy demo_vm_guest

26.4 Creating a Virtual Machine from a Configuration File

The virsh create command can take as an argument the name of a configuration file on which to base the creation of a new virtual machine. The configuration file uses XML format. The easiest way to create a configuration file is to dump out the configuration of an existing virtual machine and modify it for the new one. This can be achieved using the virsh dumpxml command. For example, the following command outputs the configuration data for a virtual machine domain named demo_vm_guest to a file named demo_vm_guest.xml:

# virsh dumpxml demo_vm_guest > demo_vm_guest.xml

Once the file has been generated, load it into an editor to review and change the settings for the new virtual machine.

At the very least, the <name>, <uuid>, and image file path <source file> must be changed to avoid conflict with the virtual machine from which the configuration was taken. In the case of the UUID, this line can be deleted from the file.

The virtualization type, memory allocation, and number of CPUs, to name but a few options, may also be changed if required. Once the file has been modified, the new virtual machine may be created as follows:

# virsh create demo_vm_guest.xml

26.5 Summary

KVM provides the virt-install and virsh command-line tools as a quick and efficient alternative to using the Cockpit and virt-manager tools to create and manage virtual machine instances. These tools have the advantage that they can be used from within scripts to automate the creation and management of virtual machines. The virsh command also includes the option to create VM instances from XML-based configuration files.

27\. Creating an Ubuntu 23.04 KVM Networked Bridge Interface

By default, the KVM virtualization environment on Ubuntu creates a virtual network to which virtual machines may connect. It is also possible to configure a direct connection using a MacVTap driver. However, as outlined in the chapter entitled [“An Overview of Virtualization Techniques”](#Virtualization_Overview.xhtml__idTextAnchor361), this approach does not allow the host and guest systems to communicate.

This chapter will cover the steps involved in creating a network bridge on Ubuntu, enabling guest systems to share one or more of the host system’s physical network connections while still allowing the guest and host systems to communicate.

In the remainder of this chapter, we will explain how to configure an Ubuntu network bridge for KVM-based guest operating systems.

27.1 Getting the Current Network Manager Settings

A network bridge can be created using the NetworkManager command-line interface tool (nmcli). The NetworkManager is installed and enabled by default on Ubuntu systems and is responsible for detecting and connecting to network devices and providing an interface for managing networking configurations.

A list of current network connections on the host system can be displayed as follows:

# nmcli con show

NAME UUID TYPE DEVICE

Wired connection 1 daae7adc-2a52-3fa0-9085-25748531e1b6 ethernet eno1

virbr0 299e0d95-4f39-4e65-aace-c7abbd8b018d bridge virbr0

vnet2 bcb3cd6e-dae4-4545-b98b-e8f90c86dadb tun vnet2

The above output shows that the host has an Ethernet network connection established via a device named eno1 and the default bridge interface named virbr0, which provides access to the NAT-based virtual network to which KVM guest systems are connected by default.

Similarly, the following command can be used to identify the devices (both virtual and physical) that are currently configured on the system:

# nmcli device show

GENERAL.DEVICE: eno1

GENERAL.TYPE: ethernet

GENERAL.HWADDR: 00:23:24:52:52:57

GENERAL.MTU: 1500

GENERAL.STATE: 100 (connected)

GENERAL.CONNECTION: Wired connection 1

GENERAL.CON-PATH: /org/freedesktop/NetworkManager/ActiveC>

WIRED-PROPERTIES.CARRIER: on

IP4.ADDRESS[1]: 192.168.86.39/24

IP4.GATEWAY: 192.168.86.1

IP4.ROUTE[1]: dst = 169.254.0.0/16, nh = 0.0.0.0, mt >

IP4.ROUTE[2]: dst = 192.168.86.0/24, nh = 0.0.0.0, mt>

IP4.ROUTE[3]: dst = 0.0.0.0/0, nh = 192.168.86.1, mt >

IP4.DNS[1]: 192.168.86.1

IP4.DOMAIN[1]: lan

IP6.ADDRESS[1]: fda8:b48c:1079:0:5f:670e:a693:9ae2/64

IP6.ADDRESS[2]: fda8:b48c:1079:0:c734:89bd:8384:992d/64

IP6.ADDRESS[3]: fda8:b48c:1079:0:ec7b:35d8:8253:3739/64

IP6.ADDRESS[4]: fe80::1e40:b04c:3de4:5fe0/64

IP6.GATEWAY: --

IP6.ROUTE[1]: dst = fda8:b48c:1079::/64, nh = ::, mt >

IP6.ROUTE[2]: dst = fe80::/64, nh = ::, mt = 1024

IP6.ROUTE[3]: dst = fd56:6a14:af59:1::/64, nh = fe80:>

GENERAL.DEVICE: virbr0

GENERAL.TYPE: bridge

GENERAL.HWADDR: 52:54:00:00:A8:CA

GENERAL.MTU: 1500

GENERAL.STATE: 100 (connected (externally))

GENERAL.CONNECTION: virbr0

GENERAL.CON-PATH: /org/freedesktop/NetworkManager/ActiveC>

IP4.ADDRESS[1]: 192.168.122.1/24

IP4.GATEWAY: --

IP4.ROUTE[1]: dst = 192.168.122.0/24, nh = 0.0.0.0, m>

IP6.GATEWAY: --

.

.

The above partial output indicates that the host system on which the command was executed contains a physical Ethernet device (eno1) and a virtual bridge (virbr0).

The virsh command may also be used to list the virtual networks currently configured on the system:

# virsh net-list --all

 Name State Autostart Persistent

----------------------------------------------------------

 default active yes yes

Currently, the only virtual network present is the default network provided by virbr0\. Now that some basic information about the current network configuration has been obtained, the next step is to create a network bridge connected to the physical network device (in this case, eno1).

27.2 Creating a Network Manager Bridge from the Command-Line

The first step in creating the network bridge is adding a new connection to the configuration. This can be achieved using the nmcli tool, specifying that the connection is to be a bridge and providing names for both the connection and the interface:

# nmcli con add ifname br0 type bridge con-name br0

Once the connection has been added, a bridge slave interface needs to be established between physical device eno1 (the slave) and the bridge connection br0 (the master) as follows:

# nmcli con add type bridge-slave ifname eno1 master br0

At this point, the NetworkManager connection list should read as follows:

# nmcli con show

br0 8680c281-6d49-4f76-93b1-902c42514ca5 bridge br0

Wired connection 1 126ab0e8-d4d3-3326-bd5e-1fea169c5635 ethernet eno1

virbr0 556042d4-2e5d-45fe-9c78-a24259e07265 bridge virbr0

bridge-slave-eno1 e6ba8ead-8fa9-4434-a884-d39225ecda20 ethernet --

The next step is to start up the bridge interface. If the steps to configure the bridge are being performed over a network connection (i.e., via SSH) this step can be problematic because the current "Wired connection 1" connection must be closed down before the bridge connection can be brought up. This means the current connection will be lost before the bridge connection can be enabled to replace it, potentially leaving the remote host unreachable.

If you are accessing the host system remotely, this problem can be avoided by creating a shell script to perform the network changes. This will ensure that the bridge interface is enabled after the ”Wired connection 1” interface is brought down, allowing you to reconnect to the host after the changes are complete. Begin by creating a shell script file named bridge.sh containing the following commands:

#!/bin/bash

nmcli con down "Wired connection 1"

nmcli con up br0

Once the script has been created, execute it as follows:

# sh ./bridge.sh

When the script executes, the connection will be lost when the ”Wired connection 1” connection is brought down. After waiting a few seconds, however, it should be possible to reconnect to the host once the br0 connection has been activated. Note that in some cases, the bridge interface may be assigned a different IP address than the one previously assigned to the system. Keep this in mind while attempting to reconnect via ssh.

If you are working locally on the host, the two nmcli commands can be run within a terminal window without any risk of losing connectivity:

# nmcli con down "Wired connection 1"

# nmcli con up br0

Once the bridge is up and running, the connection list should now include both the bridge and the bridge-slave connections:

# nmcli con show

NAME UUID TYPE DEVICE

br0 8680c281-6d49-4f76-93b1-902c42514ca5 bridge br0

virbr0 556042d4-2e5d-45fe-9c78-a24259e07265 bridge virbr0

bridge-slave-eno1 e6ba8ead-8fa9-4434-a884-d39225ecda20 ethernet eno1

Wired connection 1 126ab0e8-d4d3-3326-bd5e-1fea169c5635 ethernet --

Note that the ”Wired connection 1” connection is still listed but is no longer active. To exclude inactive connections from the list, use the --active flag when requesting the list:

# nmcli con show --active

NAME UUID TYPE DEVICE

br0 8680c281-6d49-4f76-93b1-902c42514ca5 bridge br0

virbr0 556042d4-2e5d-45fe-9c78-a24259e07265 bridge virbr0

bridge-slave-eno1 e6ba8ead-8fa9-4434-a884-d39225ecda20 ethernet eno1

27.3 Declaring the KVM Bridged Network

At this point, the bridge connection is on the system but is not visible to the KVM environment. Running the virsh command should still list the default network as being the only available network option:

# virsh net-list --all

 Name State Autostart Persistent

----------------------------------------------------------

 default active yes yes

Before a virtual machine can use the bridge, it must be declared and added to the KVM network configuration. This involves the creation of a definition file and, once again, using the virsh command-line tool.

Begin by creating a definition file for the bridge network named bridge.xml that reads as follows:

<network>

  <name>br0</name>

  <forward mode="bridge"/>

  <bridge name="br0" />

</network>

Next, use the file to define the new network:

# virsh net-define ./bridge.xml

Once the network has been defined, start it and, if required, configure it to autostart each time the system reboots:

# virsh net-start br0

# virsh net-autostart br0

Once again, list the networks to verify that the bridge network is now accessible within the KVM environment:

# virsh net-list --all

 Name State Autostart Persistent

----------------------------------------------------------

 br0 active yes yes

 default active yes yes

27.4 Using a Bridge Network in a Virtual Machine

To create a virtual machine that uses the bridge network, use the virt-install --network option and specify the br0 bridge name. For example:

# virt-install --name demo_vm_guest --memory 1024 --disk path=/tmp/demo_vm_guest.img,size=10 --network network=br0 --cdrom /home/demo/ubuntu-23.04-desktop-amd64.iso

When the guest operating system runs, it will appear on the same physical network as the host system and will no longer be on the NAT-based virtual network.

The bridge may also be selected for virtual machines within the Cockpit interface by editing the virtual machine, locating the Network interfaces section, and clicking the Edit button as highlighted in [Figure 27-1](#KVM_Network_Bridge.xhtml__idTextAnchor412) below:

![](image/ubuntu_cockpit_edit_network.jpg)

Figure 27-1

Within the resulting interface settings dialog, change the Interface type menu to Bridge to LAN and set the Source to br0 as shown in [Figure 27-2](#KVM_Network_Bridge.xhtml__idTextAnchor413):

![](image/cockpit_kvm_bridge.jpg)

Figure 27-2

Similarly, when creating a new virtual machine using the virt-manager tool, the bridge will be available within the Network selection menu:

![](image/ubuntu_virt-manager_bridge.jpg)

Figure 27-3

To modify an existing virtual machine so that it uses the bridge, use the virsh edit command. This command loads the XML definition file into an editor where changes can be made and saved:

# virsh edit GuestName

By default, the file will be loaded into the vi editor. To use a different editor, change the $EDITOR environment variable, for example:

# export EDITOR=gedit

To change from the default virtual network, locate the <interface> section of the file, which will read as follows for a NAT-based configuration:

<interface type='network'>

      <mac address='<your mac address here>'/>

      <source network='default'/>

      <model type='virtio'/>

      <address type='pci' domain='0x0000' bus='0x01' slot='0x00' function='0x0'/>

</interface>

Alternatively, if the virtual machine was using a direct connection, the entry may read as follows:

<interface type='direct'>

      <mac address='<your mac address here>'/>

      <source dev='eno1' mode='vepa'/>

      <model type='virtio'/>

      <address type='pci' domain='0x0000' bus='0x01' slot='0x00' function='0x0'/>

To use the bridge, change the source network property to read as follows before saving the file:

<interface type='network'>

      <mac address='<your mac address here>'/>

      <source network='br0'/>

      <model type='virtio'/>

      <address type='pci' domain='0x0000' bus='0x01' slot='0x00' function='0x0'/>

</interface>

If the virtual machine is already running, the change will not take effect until it is restarted.

27.5 Creating a Bridge Network using nm-connection-editor

If either local or remote desktop access is available on the host system, much of the bridge configuration process can be performed using the nm-connection-editor graphical tool. To use this tool, open a Terminal window within the desktop and enter the following command:

# nm-connection-editor

When the tool has loaded, the window shown in [Figure 27-4](#KVM_Network_Bridge.xhtml__idTextAnchor415) will appear, listing the currently configured network connections (essentially the same output as that generated by the nmcli con show command):

![](image/ubuntu_nm-connection_editor_home.jpg)

Figure 27-4

To create a new connection, click on the ‘+’ button in the window’s bottom left-hand corner. Then, from the resulting dialog ([Figure 27-5](#KVM_Network_Bridge.xhtml__idTextAnchor416)), select the Bridge option from the menu:

![](image/ubuntu_new_bridge.jpg)

Figure 27-5

With the bridge option selected, click the Create button to proceed to the bridge configuration screen. Begin by changing both the connection and interface name fields to br0 before clicking on the Add button located to the right of the Bridge connections list, as highlighted in [Figure 27-6](#KVM_Network_Bridge.xhtml__idTextAnchor417):

![](image/ubuntu_edit_bridge.jpg)

Figure 27-6

From the connection type dialog ([Figure 27-7](#KVM_Network_Bridge.xhtml__idTextAnchor418)), change the menu setting to Ethernet before clicking on the Create button:

![](image/ubuntu_new_ethernet.jpg)

Figure 27-7

Another dialog will now appear in which the bridge slave connection needs to be configured. Within this dialog, select the physical network to which the bridge is to connect (for example, eno1) from the Device menu:

![](image/ubuntu_edit_ethernet.jpg)

Figure 27-8

Click on the Save button to apply the changes and return to the Editing br0 dialog (as illustrated in [Figure 27-6](#KVM_Network_Bridge.xhtml__idTextAnchor417) above). Within this dialog, click on the Save button to create the bridge. On returning to the main window, the new bridge and slave connections should now be listed:

![](image/ubuntu_br0_ready.jpg)

Figure 27-9

All that remains is to bring down the original ”Wired connection 1” connection and bring up the br0 connection using the steps outlined in the previous chapter (remembering to perform these steps in a shell script if the host is being accessed remotely):

# nmcli con down "Wired connection 1"

# nmcli con up br0

It will also be necessary, as it was when creating the bridge using the command-line tool, to add this bridge to the KVM network configuration. To do so, repeat the steps outlined in the [“Declaring the KVM Bridged Network”](#KVM_Network_Bridge.xhtml__idTextAnchor410) section above. Once this step has been taken, the bridge is ready to be used by guest virtual machines.

27.6 Summary

By default, KVM virtual machines are connected to a virtual network that uses NAT to provide access to the network to which the host system is connected. If the guests are required to appear on the network with their own IP addresses, they need to be configured to share the physical network interface of the host system. This chapter outlines that this can be achieved using the nmcli or nm-connection-editor tools to create a networked bridge interface.

28\. Managing KVM using the virsh Command-Line Tool

In previous chapters, we have covered the installation and configuration of KVM-based guest operating systems on Ubuntu. This chapter explores additional areas of the virsh tool that have not been covered in previous chapters and how it may be used to manage KVM-based guest operating systems from the command line.

28.1 The virsh Shell and Command-Line

The virsh tool is both a command-line tool and an interactive shell environment. When used in the command-line mode, the command is issued at the command prompt with sets of arguments appropriate to the task.

To use the options as command-line arguments, use them at a terminal command prompt, as shown in the following example:

# virsh <option>

The virsh tool, when used in shell mode, provides an interactive environment from which to issue sequences of commands.

To run commands in the virsh shell, run the following command:

# virsh

Welcome to virsh, the virtualization interactive terminal.

Type: 'help' for help with commands

       'quit' to quit

virsh #

At the virsh # prompt, enter the options you wish to run. The following virsh session, for example, lists the current virtual machines, starts a virtual machine named FedoraVM, and then obtains another listing to verify the VM is running:

# virsh

Welcome to virsh, the virtualization interactive terminal.

Type: 'help' for help with commands

       'quit' to quit

virsh # list

 Id Name State

----------------------------------------------------

 8 RHEL9VM running

 9 CentOS9VM running

virsh # start FedoraVM

Domain FedoraVM started

virsh # list

 Id Name State

----------------------------------------------------

 8 RHEL9VM running

 9 CentOS9VM running

10 FedoraVM running

virsh#

The virsh tool supports a wide range of commands, a complete listing of which may be obtained using the help option:

# virsh help

Additional details on the syntax for each command may be obtained by specifying the command after the help directive:

# virsh help restore

  NAME

    restore - restore a domain from a saved state in a file

  SYNOPSIS

    restore <file> [--bypass-cache] [--xml <string>] [--running] [--paused]

  DESCRIPTION

    Restore a domain.

  OPTIONS

    [--file] <string> the state to restore

    --bypass-cache avoid file system cache when restoring

    --xml <string> filename containing updated XML for the target

    --running restore domain into running state

    --paused restore domain into paused state

In the remainder of this chapter, we will look at some of these commands in more detail.

28.2 Listing Guest System Status

The status of the guest systems on an Ubuntu virtualization host may be viewed at any time using the list option of the virsh tool. For example:

# virsh list

The above command will display output containing a line for each guest similar to the following:

virsh # list

 Id Name State

----------------------------------------------------

 8 RHEL9VM running

 9 CentOS9VM running

10 FedoraVM running

28.3 Starting a Guest System

A guest operating system can be started using the virsh tool combined with the start option followed by the name of the guest operating system to be launched. For example:

# virsh start myGuestOS

28.4 Shutting Down a Guest System

The shutdown option of the virsh tool, as the name suggests, is used to shut down a guest operating system:

# virsh shutdown guestName

Note that the shutdown option allows the guest operating system to perform an orderly shutdown when it receives the instruction. To instantly stop a guest operating system, the destroy option may be used (with the risk of file system damage and data loss):

# virsh destroy guestName

28.5 Suspending and Resuming a Guest System

A guest system can be suspended and resumed using the virsh tool’s suspend and resume options. For example, to suspend a specific system:

# virsh suspend guestName

Similarly, to resume the paused system:

# virsh resume guestName

A suspended session will be lost if the host system is rebooted. Also, be aware that a suspended system continues to reside in memory. Therefore, to save a session such that it no longer takes up memory and can be restored to its exact state (even after a reboot), it is necessary to save and restore the guest.

28.6 Saving and Restoring Guest Systems

A running guest operating system can be saved and restored using the virsh utility. When saved, the current status of the guest operating system is written to disk and removed from system memory. A saved system may subsequently be restored at any time (including after a host system reboot).

To save a guest:

# virsh save guestName path_to_save_file

To restore a saved guest operating system session:

# virsh restore path_to_save_file

28.7 Rebooting a Guest System

To reboot a guest operating system:

# virsh reboot guestName

28.8 Configuring the Memory Assigned to a Guest OS

To configure the memory assigned to a guest OS, use the setmem option of the virsh command. For example, the following command reduces the memory allocated to a guest system to 256MB:

# virsh setmem guestName 256

Note that acceptable memory settings must fall within the memory available to the current Domain. This may be increased using the setmaxmem option.

28.9 Summary

The virsh tool provides various options for creating, monitoring, and managing guest virtual machines. As outlined in this chapter, the tool can be used in either command-line or interactive modes.

29\. An Introduction to Linux Containers

The preceding chapters covered the concept of virtualization, emphasizing creating and managing virtual machines using KVM. This chapter will introduce a related technology in the form of Linux Containers. While there are some similarities between virtual machines and containers, key differences will be outlined in this chapter, along with an introduction to the concepts and advantages of Linux Containers. The chapter will also introduce some Ubuntu container management tools. Once the basics of containers have been covered in this chapter, the next chapter will work through some practical examples of creating and running containers on Ubuntu.

29.1 Linux Containers and Kernel Sharing

In simple terms, Linux containers are a lightweight alternative to virtualization. A virtual machine contains and runs the entire guest operating system in a virtualized environment. The virtual machine, in turn, runs on top of an environment such as a hypervisor that manages access to the physical resources of the host system.

Containers work by using a concept referred to as kernel sharing, which takes advantage of the architectural design of Linux and UNIX-based operating systems.

To understand how kernel sharing and containers work, it helps first to understand the two main components of Linux or UNIX operating systems. At the core of the operating system is the kernel. In simple terms, the kernel handles all the interactions between the operating system and the physical hardware. The second key component is the root file system which contains all the libraries, files, and utilities necessary for the operating system to function. Taking advantage of this structure, containers each have their own root file system but share the host operating system’s kernel. This structure is illustrated in the architectural diagram in [Figure 29-1](#Containers_Overview.xhtml__idTextAnchor433) below.

This type of resource sharing is made possible by the ability of the kernel to dynamically change the current root file system (a concept known as change root or chroot) to a different root file system without having to reboot the entire system. Linux containers are essentially an extension of this capability combined with a container runtime, the responsibility of which is to provide an interface for executing and managing the containers on the host system. Several container runtimes are available, including Docker, lxd, containerd, and CRI-O.

![](image/linux_container_diagram.jpg)

Figure 29-1

29.2 Container Uses and Advantages

The main advantage of containers is that they require considerably less resource overhead than virtualization allowing many container instances to be run simultaneously on a single server. They can be started and stopped rapidly and efficiently in response to demand levels. In addition, containers run natively on the host system providing a level of performance that a virtual machine cannot match.

Containers are also highly portable and can be easily migrated between systems. Combined with a container management system such as Docker, OpenShift, and Kubernetes, it is possible to deploy and manage containers on a vast scale spanning multiple servers and cloud platforms, potentially running thousands of containers.

Containers are frequently used to create lightweight execution environments for applications. In this scenario, each container provides an isolated environment containing the application together with all of the runtime and supporting files required by that application to run. The container can then be deployed to any other compatible host system that supports container execution and runs without any concerns that the target system may not have the necessary runtime configuration for the application - all of the application’s dependencies are already in the container.

Containers are also helpful when bridging the gap between development and production environments. By performing development and QA work in containers, they can be passed to production and launched safely because the applications run in the same container environments in which they were developed and tested.

Containers also promote a modular approach to deploying large and complex solutions. Instead of developing applications as single monolithic entities, containers can be used to design applications as groups of interacting modules, each running in a separate container.

One possible drawback of containers is that the guest operating systems must be compatible with the shared kernel version. It is not, for example, possible to run Microsoft Windows in a container on a Linux system. Nor is it possible for a Linux guest system designed for the 2.6 version of the kernel to share a 2.4 version kernel. These requirements are not, however, what containers were designed for. Rather than being seen as limitations, these restrictions should be considered some of the key advantages of containers in providing a simple, scalable, and reliable deployment platform.

29.3 Ubuntu Container Tools

Ubuntu provides several tools for creating, inspecting, and managing containers. The main tools are as follows:

•buildah – A command-line tool for building container images.

•podman – A command-line based container runtime and management tool. Performs tasks such as downloading container images from remote registries and inspecting, starting, and stopping images.

•skopeo – A command-line utility used to convert container images, copy images between registries and inspect images stored in registries without downloading them.

•runc – A lightweight container runtime for launching and running containers from the command line.

•OpenShift – An enterprise-level container application management platform consisting of command-line and web-based tools.

All of the above tools comply with the Open Container Initiative (OCI), a set of specifications designed to ensure that containers conform to the same standards between competing tools and platforms.

29.4 The Ubuntu Docker Registry

Although Ubuntu is provided with a set of tools designed to be used in place of those provided by Docker, those tools still need access to Ubuntu images for use when building containers. For this purpose, the Ubuntu team maintains a set of Ubuntu container images within the Docker Hub. The Docker Hub is an online container registry made of multiple repositories, each containing a wide range of container images available for download when building containers. The images within a repository are each assigned a repository tag (for example, 21.04, 20.10, 23.04, latest etc.) which can be referenced when performing an image download. The following, for example, is the URL of the Ubuntu 23.04 image contained within the Docker Hub:

docker://docker.io/library/ubuntu:23.04

In addition to downloading (referred to as “pulling” in container terminology) container images from Docker and other third party hosts registries, you can also use registries to store your own images. This can be achieved either by hosting your own registry, or by making use of existing services such as those provided by Docker, Amazon AWS, Google Cloud, Microsoft Azure and IBM Cloud to name a few of the many options.

29.5 Container Networking

By default, containers are connected to a network using a Container Networking Interface (CNI) bridged network stack. In the bridged configuration, all the containers running on a server belong to the same subnet and, as such, can communicate with each other. The containers are also connected to the external network by bridging the host system’s network connection. Similarly, the host can access the containers via a virtual network interface (usually named podman0) which will have been created as part of the container tool installation.

29.6 Summary

Linux Containers offer a lightweight alternative to virtualization and take advantage of the structure of the Linux and Unix operating systems. Linux Containers share the host operating system’s kernel, with each container having its own root file system containing the files, libraries, and applications. As a result, containers are highly efficient and scalable and provide an ideal platform for building and deploying modular enterprise-level solutions. In addition, several tools and platforms are available for building, deploying, and managing containers, including third-party solutions and those provided with Ubuntu.

30\. Working with Containers on Ubuntu

Now that the basics of Linux Containers have been covered in the previous chapter, this chapter will demonstrate how to create and manage containers using the Podman, Skopeo, and Buildah tools on Ubuntu. It is intended that by the end of this chapter, you will have a clearer understanding of how to create and manage containers on Ubuntu and will have gained a knowledge foundation on which to continue exploring the power of Linux Containers.

30.1 Installing the Container Tools

Before starting with containers, the first step is to install all of the container tools outlined in the previous chapter using the following commands:

# apt install curl

# . /etc/os-release

# sh -c "echo 'deb https://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/xUbuntu_${VERSION_ID}/ /' > /etc/apt/sources.list.d/devel:kubic:libcontainers:stable.list"

# curl -L https://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/xUbuntu_${VERSION_ID}/Release.key | sudo apt-key add -

# apt update

# apt install podman skopeo buildah

30.2 Pulling a Container Image

For this example, the most recent Ubuntu release will be pulled from the registry. Before pulling an image, however, information about the image repository can be obtained using the skopeo tool, for example:

$ skopeo inspect docker://docker.io/ubuntu

{

    "Name": "docker.io/library/ubuntu",

    "Digest": "sha256:bec5a2727be7fff3d308193cfde3491f8fba1a2ba392b7546b43a051853a341d",

    "RepoTags": [

        "10.04",

        "12.04.5",

        "12.04",

        "12.10",

        "13.04",

        "13.10",

        "14.04.1",

        "14.04.2",

        "14.04.3",

        "14.04.4",

        "14.04.5",

        "14.04",

        "14.10",

        "15.04",

.

.

    ],

    "Created": "2023-06-28T08:42:50.42500211Z",

    "DockerVersion": "20.10.21",

    "Labels": {

        "org.opencontainers.image.ref.name": "ubuntu",

        "org.opencontainers.image.version": "22.04"

    },

    "Architecture": "arm64",

    "Os": "linux",

    "Layers": [

        "sha256:5af00eab97847634d0b3b8a5933f52ca8378f5f30a2949279d682de1e210d78b"

    ],

    "Env": [

        "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"

    ]

}

For example, to pull the latest Ubuntu image:

$ podman pull docker://docker.io/ubuntu:latest

Trying to pull docker.io/library/ubuntu:latest...

Getting image source signatures

Copying blob 5af00eab9784 done

Copying config 37f7489146 done

Writing manifest to image destination

Storing signatures

37f74891464b2067aacbde60d9e2888e002af047a0d5dfc0b06b701928e0b473

Verify that the image has been stored by asking podman to list all local images:

$ podman images

REPOSITORY TAG IMAGE ID CREATED SIZE

docker.io/library/ubuntu latest 4e5021d210f6 3 weeks ago 66.6 MB

Details about a local image may be obtained by running the podman inspect command:

$ podman inspect ubuntu:latest

This command should output the same information as the skopeo command performed on the remote image earlier in this chapter.

30.3 Running the Image in a Container

The image pulled from the registry is a fully operational image that is ready to run in a container without modification. To run the image, use the podman run command. In this case, the –rm option will be specified to indicate that we want to run the image in a container, execute one command and then have the container exit. In this case, the cat tool will be used to output the content of the /etc/passwd file located on the container root filesystem:

$ podman run --rm ubuntu:latest cat /etc/passwd

root:x:0:0:root:/root:/bin/bash

daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin

bin:x:2:2:bin:/bin:/usr/sbin/nologin

sys:x:3:3:sys:/dev:/usr/sbin/nologin

sync:x:4:65534:sync:/bin:/bin/sync

games:x:5:60:games:/usr/games:/usr/sbin/nologin

man:x:6:12:man:/var/cache/man:/usr/sbin/nologin

lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin

mail:x:8:8:mail:/var/mail:/usr/sbin/nologin

news:x:9:9:news:/var/spool/news:/usr/sbin/nologin

uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin

proxy:x:13:13:proxy:/bin:/usr/sbin/nologin

www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin

backup:x:34:34:backup:/var/backups:/usr/sbin/nologin

list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin

irc:x:39:39:ircd:/var/run/ircd:/usr/sbin/nologin

gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/usr/sbin/nologin

nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin

_apt:x:100:65534::/nonexistent:/usr/sbin/nologin

Compare the content of the /etc/passwd file within the container with the /etc/passwd file on the host system and note that it lacks all of the additional users that are present on the host confirming that the cat command was executed within the container environment. Also note that the container started, ran the command and exited all within a matter of seconds. Compare this to the amount of time it takes to start a full operating system, perform a task, and shutdown a virtual machine, and you begin to appreciate the speed and efficiency of containers.

To launch a container, keep it running, and access the shell, the following command can be used:

$ podman run --name=mycontainer -it ubuntu:latest /bin/bash

root@4b49ddeb2987:/#

In this case, an additional command-line option has been used to assign the name “mycontainer” to the container. Though optional, this makes the container easier to recognize and reference as an alternative to using the automatically generated container ID.

While the container is running, run podman in a different terminal window to see the status of all containers on the system

$ podman ps -a

CONTAINER ID IMAGE COMMAND CREATED STATUS PORTS NAMES

4b49ddeb2987 docker.io/library/ubuntu:latest /bin/bash About a minute ago Up About a minute ago mycontainer

To execute a command in a running container from the host, simply use the podman exec command, referencing the name of the running container and the command to be executed. The following command, for example, starts up a second bash session in the container named mycontainer:

$ podman exec -it mycontainer /bin/bash

root@4b49ddeb2987:/#

Note that though the above example referenced the container name the same result can be achieved using the container ID as listed by the podman ps -a command:

$ podman exec -it 4b49ddeb2987 /bin/bash

root@4b49ddeb2987:/#

Alternatively, the podman attach command will also attach to a running container and access the shell prompt:

$ podman attach mycontainer

root@4b49ddeb2987:/#

Once the container is up and running, any additional configuration changes can be made, and packages installed just like any other Ubuntu system.

30.4 Managing a Container

Once launched, a container will continue to run until it is stopped via podman, or the command that was launched when the container was run exits. Running the following command on the host, for example, will cause the container to exit:

$ podman stop mycontainer

Alternatively, pressing the Ctrl-D keyboard sequence within the last remaining bash shell of the container would cause both the shell and container to exit. Once it has exited, the status of the container will change accordingly:

$ podman ps -a

CONTAINER ID IMAGE COMMAND CREATED STATUS PORTS NAMES

4b49ddeb2987 docker.io/library/ubuntu:latest /bin/bash 6 minutes ago Exited (127) About a minute ago mycontainer

Although the container is no longer running, it still exists and contains all of the changes that were made to the configuration and file system. If you installed packages, made configuration changes or added files, these changes will persist within “mycontainer”. To verify this, simply restart the container as follows:

$ podman start mycontainer

After starting the container, use the podman exec command once again to execute commands within the container as outlined previously. For example, to once again gain access to a shell prompt:

$ podman exec -it mycontainer /bin/bash

A running container may also be paused and resumed using the podman pause and unpause commands as follows:

$ podman pause mycontainer

$ podman unpause mycontainer

30.5 Saving a Container to an Image

Once the container guest system is configured to your requirements there is a good chance that you will want to create and run more than one container of this particular type. To do this, the container needs to be saved as an image to local storage so that it can be used as the basis for additional container instances. This is achieved using the podman commit command combined with the name or ID of the container and the name by which the image will be stored, for example:

$ podman commit mycontainer myubuntu_image

Once the image has been saved, check that it now appears in the list of images in the local repository:

$ podman images

REPOSITORY TAG IMAGE ID CREATED SIZE

localhost/myubuntu_image latest 8ad685d49482 47 seconds ago 66.6 MB

docker.io/library/ubuntu latest 4e5021d210f6 3 weeks ago 66.6 MB

The saved image can now be used to create additional containers identical to the original:

$ podman run --name=mycontainer2 -it localhost/myubuntu_image /bin/bash

30.6 Removing an Image from Local Storage

To remove an image from local storage once it is no longer needed, simply run the podman rmi command, referencing either the image name or ID as output by the podman images command. For example, to remove the image named myubuntu_image created in the previous section, run podman as follows:

$ podman rmi localhost/myubuntu_image

Note before an image can be removed, any containers based on that image must first be removed.

30.7 Removing Containers

Even when a container has exited or been stopped, it still exists and can be restarted at any time. If a container is no longer needed, it can be deleted using the podman rm command as follows after the container has been stopped:

# podman rm mycontainer2

30.8 Building a Container with Buildah

Buildah allows new containers to be built either from existing containers, an image or entirely from scratch. Buildah also includes the ability to mount the file system of a container so that it can be accessed and modified from the host.

The following buildah command, for example, will build a container from the Ubuntu Base image (if the image has not already been pulled from the registry, buildah will download it before creating the container):

$ buildah from docker://docker.io/library/ubuntu:latest

The result of running this command will be a container named ubuntu-working-container that is ready to run:

$ buildah run ubuntu-working-container cat /etc/passwd

30.9 Summary

This chapter has worked through the creation and management of Linux Containers on Ubuntu using the podman, skopeo and buildah tools.

31. Setting Up an Ubuntu 23.04 Web Server

The Apache web server is among the many packages that make up the Ubuntu operating system. The scalability and resilience of Ubuntu make it an ideal platform for hosting even the most heavily trafficked websites.

This chapter will explain how to configure an Ubuntu system using Apache to act as a web server, including secure (HTTPS) and insecure (HTTP) configurations.

31.1 Requirements for Configuring an Ubuntu Web Server

To set up your own website, you need a computer (or cloud server instance), an operating system, a web server, a domain name, a name server, and an IP address.

As previously mentioned, Ubuntu supports the Apache web server, which can easily be installed once the operating system is up and running. In addition, a domain name can be registered with any domain name registration service.

If you are running Ubuntu on a cloud instance, the IP address assigned by the provider will be listed in the server overview information. However, if you are hosting your own server and your internet service provider (ISP) has assigned a static IP address, you must associate your domain with that address. This is achieved using a name server, and all domain registration services will provide this service.

If you do not have a static IP address (i.e., your ISP provides you with a dynamic address that changes frequently), you can use one of several free Dynamic DNS (DDNS or DynDNS for short) services to map your dynamic IP address to your domain name.

Once you have configured your domain name and your name server, the next step is to install and configure your web server.

31.2 Installing the Apache Web Server Packages

The current release of Ubuntu typically does not install the Apache web server by default. To check whether the server is already installed, run the following command:

# apt -qq list apache2

If apt generates output similar to the following, the apache server is already installed:

apache2/lunar,now 2.4.55-1ubuntu2 amd64 [installed]

If the apt output does not list the package or include the [installed] status, run the following command at the command prompt to perform the Apache installation:

# apt install apache2

31.3 Configuring the Firewall

Before starting and testing the Apache webserver, the firewall will need to be modified to allow the web server to communicate with the outside world. By default, the HTTP and HTTPS protocols use ports 80 and 443 respectively so, depending on which protocols are being used, either one or both of these ports will need to be opened. If your Ubuntu system is being protected by the Uncomplicated Firewall, the following command can be used to enable only insecure web traffic (HTTP):

# ufw allow Apache

To enable only secure (HTTPS) traffic:

# ufw allow 'Apache Secure'

Alternatively, enable both secure and insecure web traffic as follows:

# ufw allow 'Apache Full'

If you are using firewalld, the following commands can be used to open the HTTP and HTTPS ports. When opening the ports, be sure to specify the firewall zone that applies to the internet-facing network connection:

# firewall-cmd --permanent --zone=<zone> --add-port=80/tcp

# firewall-cmd --permanent --zone=<zone> --add-port=443/tcp

After opening the necessary ports, be sure to reload the firewall settings:

# firewall-cmd --reload

On cloud-hosted servers, enabling the appropriate port for the server instance within the cloud console may also be necessary. Check the documentation for the cloud provider for steps to do this.

31.4 Port Forwarding

Suppose the Ubuntu system hosting the web server sits on a network protected by a firewall (another computer running a firewall, router, or wireless base station containing built-in firewall protection). In that case, you must configure the firewall to forward ports 80 and 443 to your web server system. The mechanism for performing this differs between firewalls and devices, so check your documentation to find out how to configure port forwarding.

31.5 Starting the Apache Web Server

Once the Apache server is installed and the firewall configured, the next step is to verify that the server is running and start it if necessary.

To check the status of the Apache service from the command line, enter the following at the command prompt:

# systemctl status apache2

If the above command indicates that the apache2 service is not running, it can be launched from the command line as follows:

# systemctl start apache2

If you would like the Apache httpd service to start automatically when the system boots, run the following command:

# systemctl enable apache2

31.6 Testing the Web Server

Once the installation is complete, the next step is verifying the web server is running.

If you have access (either locally or remotely) to the desktop environment of the server, start up a web browser and enter http://127.0.0.1 in the address bar (127.0.0.1 is the loop-back network address that tells the system to connect to the local machine). If everything is set up correctly, the browser should load the test page shown in [Figure 31-1](#Web_Server.xhtml__idTextAnchor470):

![](image/ubuntu_website.jpg)

Figure 31-1

If the desktop environment is unavailable, connect either from another system on the same local network as the server, or use the external IP address assigned to the system if it is hosted remotely.

31.7 Configuring the Apache Web Server for Your Domain

The next step in setting up your web server is configuring it for your domain name. To configure the web server, begin by changing directory to  /etc/apache2, which, in turn, contains several files and sub-directories. The main configuration file is named apache2.conf and serves as the central point for organizing the modular configuration files located in the sub-directories. For example, the apache2.conf file includes a line to import the configuration settings declared in the files located in the sites-enabled folder:

# Include the virtual host configurations:

IncludeOptional sites-enabled/*.conf

Similarly, the apache2.conf file imports the ports.conf file, which defines the ports on which the Apache server listens for network traffic.

To configure a website domain on Ubuntu, begin by changing directory to /etc/apache2. In this directory, you will find two sub-directories, sites-available and sites-enabled. Change directory into sites-available. In this directory you will find a default file which may be used as a template for your own site.

Copy the default file to a new file with a name that matches your domain name. For example:

# cp 000-default.conf myexample.conf

Edit your myexample.com file using your favorite editor where it will appear as follows:

<VirtualHost *:80>

        # The ServerName directive sets the request scheme, hostname and port that

# the server uses to identify itself. This is used when creating

# redirection URLs. In the context of virtual hosts, the ServerName

        # specifies what hostname must appear in the request’s Host: header to

# match this virtual host. For the default virtual host (this file) this

        # value is not decisive as it is used as a last resort host regardless.

        # However, you must set it for any further virtual host explicitly.

        #ServerName www.example.com

        ServerAdmin webmaster@localhost

        DocumentRoot /var/www/html

        # Available loglevels: trace8, ..., trace1, debug, info, notice, warn,

        # error, crit, alert, emerg.

        # It is also possible to configure the loglevel for particular

        # modules, e.g.

        #LogLevel info ssl:warn

        ErrorLog ${APACHE_LOG_DIR}/error.log

        CustomLog ${APACHE_LOG_DIR}/access.log combined

        # For most configuration files from conf-available/, which are

        # enabled or disabled at a global level, it is possible to

# include a line for only one particular virtual host. For example the

        # following line enables the CGI configuration for this host only

        # after it has been globally disabled with “a2disconf”.

        #Include conf-available/serve-cgi-bin.conf

</VirtualHost>

The ServerAdmin directive defines an administrative email address for people wishing to contact the webmaster for your site. Change this to an appropriate email address where you can be contacted:

ServerAdmin webmaster@myexample.com

Next, the ServerName directive needs to be uncommented (in other words remove the ‘#’ character prefix) and defined so that the web server knows which virtual host this configuration file refers to:

ServerName myexample.com

In the next stage, we need to define where the website files are going to be located using the DocumentRoot directive. The tradition is to use /var/www/domain-name:

DocumentRoot /var/www/myexample.com

Having completed the changes, we now need to enable the site as follows:

# a2ensite myexample.conf

This command creates a symbolic link from the myexample.conf file in the sites-available directory to the sites-enabled folder.

With the site enabled, run the following command to disable the default test site:

# a2dissite 000-default.conf

Next, create the /var/www/myexample.com directory and place an index.html file in it. For example:

<html>

<title>Sample Web Page</title>

<body>

Welcome to MyExample.com

</body>

</html>

With these changes made, run the apache2ctl command to check the configuration files for errors:

# apache2ctl configtest

Syntax OK

If no errors are reported, reload the Apache web server to make sure it picks up our new settings:

# systemctl reload apache2

Finally, check that the server configuration works by opening a browser window and navigating to the site using the domain name instead of the IP address. The web page that loads should be the one defined in the index.html file created above.

31.8 The Basics of a Secure Website

The web server and website created in this chapter use the HTTP protocol on port 80 and, as such, are considered to be insecure. The problem is that the traffic between the web server and the client (typically a user’s web browser) is transmitted in clear text. In other words, the data is unencrypted and susceptible to interception. While not a problem for general web browsing, this is a severe weakness when performing tasks such as logging into websites or transferring sensitive information such as identity or credit card details.

These days, websites are expected to use HTTPS, which uses either Secure Socket Layer (SSL) or Transport Layer Security (TLS) to establish secure, encrypted communication between a web server and a client. This security is established through the use of public, private, and session encryption together with certificates.

To support HTTPS, a website must have a certificate issued by a trusted authority known as a Certificate Authority (CA). When a browser connects to a secure website, the web server sends back a copy of the website’s SSL certificate, which also contains a copy of the site’s public key. The browser then validates the authenticity of the certificate with trusted certificate authorities.

If the certificate is valid, the browser uses the public key sent by the server to encrypt a session key and pass it to the server. The server decrypts the session key using the private key to send an encrypted acknowledgment to the browser. Once this process is complete, the browser and server use the session key to encrypt all subsequent data transmissions until the session ends.

31.9 Configuring Apache for HTTPS

By default, the Apache server does not include the necessary module to implement a secure HTTPS website. The first step, therefore, is to enable the Apache mod_ssl module on the server system as follows:

# a2enmod ssl

Restart apache2 after the installation completes to load the new module into the Apache server:

# systemctl restart apache2

Check that the module has loaded into the server using the following command:

# apache2ctl -M | grep ssl_module

 ssl_module (shared)

Once the ssl module is installed, repeat the steps from the previous section of this chapter to create a configuration file for the website, this time using the sites-available/default-ssl.conf file as the template for the site configuration file.

Assuming the module is installed, the next step is to generate an SSL certificate for the website.

31.10 Obtaining an SSL Certificate

The certificate for a website must be obtained from a Certificate Authority. Several options are available at a range of prices. By far the best option, however, is to obtain a free certificate from Let’s Encrypt at the following URL:

[https://letsencrypt.org/](https://letsencrypt.org/)

Obtaining a certificate from Let’s Encrypt involves installing and running the Certbot tool. This tool will scan the Apache configuration files on the server and provides the option to generate certificates for any virtual hosts configured on the system. It will then generate the certificate and add virtual host entries to the Apache configuration for the corresponding websites.

Follow the steps on the Let’s Encrypt website to download and install Certbot on your Ubuntu system, then run the certbot tool as follows to generate and install the certificate:

# certbot --apache

After requesting an email address and seeking terms of service acceptance, Certbot will list the domains found in the httpd.conf file and allow the selection of one or more sites for which a certificate will be installed. Certbot will then perform some checks before obtaining and installing the certificate on the system:

Which names would you like to activate HTTPS for?

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

1: www.myexample.com

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

Select the appropriate numbers separated by commas and/or spaces, or leave input

blank to select all options shown (Enter ‘c’ to cancel): 1

Obtaining a new certificate

Performing the following challenges:

http-01 challenge for www.myexample.com

Waiting for verification...

Cleaning up challenges

Created an SSL vhost at /etc/httpd/conf/httpd-le-ssl.conf

Deploying Certificate to VirtualHost /etc/httpd/conf/httpd-le-ssl.conf

Enabling site /etc/httpd/conf/httpd-le-ssl.conf by adding Include to root configuration

Certbot will also create a new file named myexample-le-ssl.conf in the /etc/apache2/sites-available directory containing a secure virtual host entry for each domain name for which a certificate has been generated and enabled the site so that a link to the file is made in the /etc/apache2/sites-enabled directory. These entries will be similar to the following:

<IfModule mod_ssl.c>

<VirtualHost *:443>

    ServerAdmin feedback@myexample.com

    ServerName www.myexample.com

    DocumentRoot /var/www/myexample

    ErrorLog logs/myexample_error_log

    CustomLog logs/myexample_access_log combined

SSLCertificateFile /etc/letsencrypt/live/www.myexample.com/fullchain.pem

SSLCertificateKeyFile /etc/letsencrypt/live/www.myexample.com/privkey.pem

Include /etc/letsencrypt/options-ssl-apache.conf

</VirtualHost>

</IfModule>

Finally, Certbot will ask whether the server should redirect future HTTP web requests to HTTPS. In other words, if a user attempts to access http://www.myexample.com, the web server will redirect the user to https://www.myexample.com:

Please choose whether or not to redirect HTTP traffic to HTTPS, removing HTTP access.

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

1: No redirect - Make no further changes to the webserver configuration.

2: Redirect - Make all requests redirect to secure HTTPS access. Choose this for

new sites, or if you’re confident your site works on HTTPS. You can undo this

change by editing your web server’s configuration.

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

Select the appropriate number [1-2] then [enter] (press ‘c’ to cancel): 2

If you are currently testing the HTTPS configuration and would like to keep the HTTP version live until later, select the No redirect option. Otherwise, redirecting to HTTPS is generally recommended.

Once the certificate has been installed, test it in a browser at the following URL (replacing myexample.com with your own domain name):

[https://www.ssllabs.com/ssltest/analyze.html?d=www.myexample.com](https://www.ssllabs.com/ssltest/analyze.html?d=www.myexample.com)

If the certificate configuration is successful, the SSL Labs report will provide a high rating, as shown in [Figure 31-2](#Web_Server.xhtml__idTextAnchor475):

![](image/rhel_8_ssl_labs_report.jpg)

Figure 31-2

As a final test, open a browser window and navigate to your domain using the https:// prefix. The page should load as before, and the browser should indicate that the connection between the browser and server is secure (usually indicated by a padlock icon in the address bar, which can be clicked for additional information):

![](image/ubuntu_secure_site.jpg)

Figure 31-3

31.11 Summary

An Ubuntu system can host websites by installing the Apache web server. Insecure (HTTP) and secure (HTTPS) websites can be deployed on Ubuntu. Secure websites use either Secure Socket Layer (SSL) or Transport Layer Security (TLS) to establish encrypted communication between the web server and client through public, private, and session encryption, together with a certificate issued by a trusted Certificate Authority.

32. Configuring an Ubuntu 23.04 Postfix Email Server

Along with acting as a web server, email is one of the primary uses of an Ubuntu system, particularly in business environments. Given the importance and popularity of email, it is surprising to some people to find out how complex the email structure is on a Linux system. This complexity can often be overwhelming to the Ubuntu newcomer.

The good news is that much of the complexity is there to allow experienced email administrators to implement complicated configurations for large-scale enterprise installations. However, for most Linux administrators, setting up a basic email system is relatively straightforward so that users can send and receive electronic mail.

This chapter of Ubuntu Essentials will explain the basics of Linux-based email configuration and step through configuring a basic email environment. To provide the essentials, we will leave the complexities of the email system for more advanced books on the subject.

32.1 The Structure of the Email System

Several components make up a complete email system. Below is a brief description of each one:

32.1.1 Mail User Agent

The typical user will likely be most familiar with this part of the system. The Mail User Agent (MUA), or mail client, is the application that is used to write, send and read email messages. Anyone who has written and sent a message on any computer has used a Mail User Agent of one type or another.

Typical Graphical MUAs on Linux are Evolution, Thunderbird, and KMail. For those who prefer a text-based mail client, there are also the more traditional Pine and mail tools.

32.1.2 Mail Transfer Agent

The Mail Transfer Agent (MTA) is the part of the email system that transfers email messages from one computer to another (either on the same local network or over the internet to a remote system). Once configured correctly, most users will only directly interact with their chosen MTA if they wish to re-configure it. Many MTA choices are available for Linux, including Sendmail, Postfix, Fetchmail, Qmail, and Exim.

32.1.3 Mail Delivery Agent

Another part of the infrastructure typically hidden from the user, the Mail Delivery Agent (MDA), sits in the background and performs filtering of the email messages between the Mail Transfer Agent and the mail client (MUA). The most popular form of MDA is a spam filter to remove all unwanted email messages from the system before they reach the inbox of the user’s mail client (MUA). Popular MDAs are Spamassassin and Procmail. It is important to note that some Mail User Agent applications (such as Evolution, Thunderbird, and KMail) include their own MDA filtering. Others, such as Pine and Basla, do not. This can be a source of confusion for the Linux beginner.

32.1.4 SMTP

SMTP is an acronym for Simple Mail Transport Protocol. The email systems use this protocol to transfer mail messages from one server to another. This protocol is the communication language that the MTAs use to talk to each other and transfer messages back and forth.

32.1.5 SMTP Relay

SMTP Relay is a protocol that allows an external SMTP server to send emails instead of hosting a local SMTP server. This will typically involve using a service such as Mailjet, SendGrid, or MailGun. These services avoid configuring and maintaining your own SMTP server and often provide additional benefits such as analytics.

32.2 Configuring an Ubuntu Email Server

Many systems use the Sendmail MTA to transfer email messages; on many Linux distributions, this is the default Mail Transfer Agent. Unfortunately, Sendmail is a complex system that can be difficult for beginners and experienced users to understand and configure. It is also falling from favor because it is considered slower at processing email messages than many of the more recent MTAs available.

Many system administrators are now using Postfix or Qmail to handle email. Both are faster and easier to configure than Sendmail.

For this chapter, therefore, we will look at Postfix as an MTA because of its simplicity and popularity. However, if you prefer to use Sendmail, many books specialize in the subject and will do the subject much more justice than we can in this chapter.

As a first step, this chapter will cover configuring an Ubuntu system to act as a full email server. Later in the chapter, the steps to use an SMTP Relay service will also be covered.

32.3 Postfix Pre-Installation Steps

The first step before installing Postfix is to ensure that Sendmail is not already running on your system. You can check for this using the following command:

# systemctl status sendmail

If sendmail is not installed, the tool will display a message similar to the following:

Unit sendmail.service could not be found.

If sendmail is running on your system, it is necessary to stop it before installing and configuring Postfix. To stop sendmail, run the following command:

# systemctl stop sendmail

The next step is to ensure that sendmail does not get restarted automatically when the system is rebooted:

# systemctl disable sendmail

Sendmail is now switched off and configured to not auto-start when the system is booted. Optionally, to altogether remove sendmail from the system, run the following command:

# apt remove sendmail

32.4 Firewall/Router Configuration

Since sending and receiving email messages involves network connections, the firewall must be configured to allow SMTP traffic. If firewalld is active, use the firewall-cmd tool will as follows:

# firewall-cmd --permanent --add-service=smtp

Alternatively, if ufw is enabled, configure it to allow SMTP traffic using the following command:

# ufw allow Postfix

It will also be essential to configure any other firewall or router between the server and the internet to allow connections on ports 25, 143, and 587 and, if necessary, to configure port forwarding for those ports to the corresponding ports on the email server.

With these initial steps completed, we can now install Postfix.

32.5 Installing Postfix on Ubuntu

By default, the Ubuntu installation process installs postfix for most configurations. To verify if postfix is already installed, use the following apt command:

# apt -qq list postfix

If apt reports that postfix is not installed, it may be installed as follows:

# apt install postfix

The apt tool will download and install postfix and configure a special postfix user in the /etc/passwd file.

32.6 Configuring Postfix

The main configuration settings for postfix are located in the /etc/postfix/main.cf file. The /etc/postfix directory contains a template file named main.cf.proto that you can use as the basis for your mail system configuration. Many resources on the internet provide detailed information on postfix, so this section will focus on the basic options required to get email up and running. Even though the apt installation set up some basic configuration options, it tends to miss some settings and guess incorrectly for others, so carefully review the main.cf file.

The key options in the main.cf file are as follows:

myhostname = mta1.domain.com

mydomain = domain.com

myorigin = $mydomain

mydestination = $myhostname, localhost.$mydomain, localhost, $mydomain

inet_interfaces = $myhostname

mynetworks = subnet

Other settings will have either been set up for you by the installation process or are only needed if you are feeling adventurous and want to configure a more sophisticated email system.

The format of myhostname is host.domain.extension. If, for example, your Linux system is named MyLinuxHost and your internet domain is MyDomain.com you would set the myhostname option as follows:

myhostname = mylinuxhost.mydomain.com

The mydomain setting is just the domain part of the above setting. For example:

mydomain = mydomain.com

The myorigin setting defines the name of the domain from which the output email appears to come from when it arrives in the recipient’s inbox and should be set to your domain name:

myorigin = $mydomain

One of the most crucial parameters, mydestination relates to incoming messages and declares the domains for which this server is the final delivery destination. Any incoming email messages addressed to a domain name, not on this list will be considered a relay request which, subject to the mynetworks setting (outlined below), will typically result in a delivery failure.

The inet_interfaces setting defines the network interfaces on the system via which postfix is permitted to receive email and is generally set to all:

inet_interfaces = all

The mynetworks setting defines which external systems are trusted to use the server as an SMTP relay. Possible values for this setting are as follows:

•host - Only the local system is trusted. Attempts by all external clients to use the server as a relay will be rejected.

•subnet - Only systems on the same network subnet can use the server as a relay. If, for example, the server has an IP address of 192.168.1.29, a client system with an IP address of 192.168.1.30 could use the server as a relay.

•class - Any systems within the same IP address class (A, B, and C) may use the server as a relay.

Trusted IP addresses may be defined manually by specifying subnets, address ranges, or referencing pattern files. The following example declares the local host and the subnet 192.168.0.0 as trusted IP addresses:

mynetworks = 192.168.0.0/24, 127.0.0.0/8

For this example, set the property to subnet so that any other systems on the same local network as the server can send email via SMTP relay. In contrast, external systems are prevented from doing so:

mynetworks = subnet

32.7 Configuring DNS MX Records

When you register and configure your domain name with a registrar, several default values will have been configured in the DNS settings. One of these is the so-called Mail Exchanger (MX) record. This record defines where emails addressed to your domain should be sent and is usually set by default to a mail server provided by your registrar. If you are hosting your own mail server, the MX record should be set to your domain or the IP address of your mail server. The steps to make this change will depend on your domain registrar but generally involves editing the DNS information for the domain and either adding or editing an existing MX record so that it points to your email server.

32.8 Starting Postfix on an Ubuntu System

Once the /etc/postfix/main.cf file is configured with the correct settings, it is now time to start up postfix. This can be achieved from the command line as follows:

# systemctl start postfix

If postfix was already running, make sure the configuration changes are loaded using the following command:

# systemctl reload postfix

To configure postfix to start automatically at system startup, run the following command:

# systemctl enable postfix

The postfix process should now start up. The best way to verify everything works is to check your mail log. This is typically in the /var/log/maillog file and should now contain an entry resembling the following output:

Mar 25 11:21:48 demo-server postfix/postfix-script[5377]: starting the Postfix mail system

Mar 25 11:21:48 demo-server postfix/master[5379]: daemon started -- version 3.3.1, configuration /etc/postfix

As long as no error messages have been logged, you have successfully installed and started postfix and are ready to test the postfix configuration.

32.9 Testing Postfix

An easy way to test the postfix configuration is to send email messages between local users on the system. To perform a quick test, use the mail tool as follows (where name and mydomain are replaced by the name of a user on the system and your domain name, respectively):

# mail name@mydomain.com

When prompted, enter a subject for the email message and then type the message body text. To send the email message, press Ctrl-D. For example:

# mail demo@mydomain.com

Subject: Test email message

This is a test message.

EOT

If the mail tool is not available, it can be installed as follows:

# apt install mailutils

Rerun the mail command, this time as the other user, and verify that the message was sent and received:

$ mail

"/var/mail/demo": 1 message 1 new

>N 1 demo Wed Apr 15 15:30 13/475 Test email message

?

Check the log file (/var/log/maillog) for errors if the message does not appear. Successful mail delivery will appear in the log file as follows:

Mar 25 13:41:37 demo-server postfix/pickup[7153]: 94FAF61E8F4A: uid=0 from=<root>

Mar 25 13:41:37 demo-server postfix/cleanup[7498]: 94FAF61E8F4A: message-id=<20190325174137.94FAF61E8F4A@demo-server.mydomain.com>

Mar 25 13:41:37 demo-server postfix/qmgr[7154]: 94FAF61E8F4A: from=<root@mydomain.com>, size=450, nrcpt=1 (queue active)

Mar 25 13:41:37 demo-server postfix/local[7500]: 94FAF61E8F4A: to=<neil@mydomain.com>, relay=local, delay=0.12, delays=0.09/0.01/0/0.02, dsn=2.0.0, status=sent (delivered to mailbox)

Mar 25 13:41:37 demo-server postfix/qmgr[7154]: 94FAF61E8F4A: removed

Once the local email is working, try sending an email to an external address (such as a GMail account). Also, test that incoming mail works by sending an email from an external account to a user on your domain. In each case, check the /var/log/mail.log file for explanations of any errors.

32.10 Sending Mail via an SMTP Relay Server

An SMTP Relay service is an alternative to configuring a mail server to handle outgoing email messages. As previously discussed, several services are available, most of which can be found by performing a web search for “SMTP Relay Service”. Most of these services will require you to verify your domain in some way and will provide MX records with which to update your DNS settings. You will also be provided with a username and password, which must be added to the postfix configuration. The remainder of this section assumes that postfix is installed on your system and that all of the initial steps required by your chosen SMTP Relay provider have been completed.

Begin by editing the /etc/postfix/main.cf file and configure the myhostname parameter with your domain name:

myhostname = mydomain.com

Next, create a new file in /etc/postfix named sasl_passwd and add a line containing the mail server host provided by the relay service and the user name and password. For example:

[smtp.myprovider.com]:587 neil@mydomain.com:mypassword

Note that port 587 has also been specified in the above entry. Without this setting, postfix will default to using port 25, which is blocked by default by most SMTP relay service providers.

With the password file created, use the postmap utility to generate the hash database containing the mail credentials:

# postmap /etc/postfix/sasl_passwd

Before proceeding, take some additional steps to secure your postfix credentials:

# chown root:root /etc/postfix/sasl_passwd /etc/postfix/sasl_passwd.db

# chmod 0600 /etc/postfix/sasl_passwd /etc/postfix/sasl_passwd.db

Edit the main.cf file once again and add an entry to specify the relay server:

relayhost = [smtp.myprovider.com]:587

Remaining within the main.cf file, add the following lines to configure the authentication settings for the SMTP server:

smtp_use_tls = yes

smtp_sasl_auth_enable = yes

smtp_sasl_password_maps = hash:/etc/postfix/sasl_passwd

smtp_tls_CAfile = /etc/ssl/certs/ca-bundle.crt

smtp_sasl_security_options = noanonymous

smtp_sasl_tls_security_options = noanonymous

Finally, restart the postfix service:

# systemctl restart postfix

Once the service has restarted, try sending and receiving mail using either the mail tool or your preferred mail client.

32.11 Summary

A complete, end-to-end email system consists of a Mail User Agent (MUA), Mail Transfer Agent (MTA), Mail Delivery Agent (MDA), and the SMTP protocol. Ubuntu provides several options in terms of MTA solutions, one of the more popular being Postfix. This chapter has outlined how to install, configure and test postfix on an Ubuntu system to act as a mail server and send and receive email using a third-party SMTP relay server.

33. Adding a New Disk Drive to an Ubuntu 23.04 System

One of the first problems users and system administrators encounter is that systems need more disk space to store data. Fortunately, disk space is now one of the cheapest IT commodities. In this and the next chapter, we will look at configuring Ubuntu to use the space provided when a new physical or virtual disk drive is installed.

33.1 Mounted File Systems or Logical Volumes

There are two ways to configure a new disk drive on an Ubuntu system. One straightforward method is to create one or more Linux partitions on the new drive, create Linux file systems on those partitions and then mount them at specific mount points to be accessed. This approach will be covered in this chapter.

Another approach is adding new space to an existing volume group or creating a new one. When Ubuntu is installed, a volume group named is created. Within this volume group are three logical volumes named root, home, and swap, used to store the / and /home file systems and swap partitions, respectively. We can increase the disk space available to the existing logical volumes by configuring the new disk as part of a volume group. For example, using this approach, we can increase the size of the /home file system by allocating some or all of the space on the new disk to the home volume. This topic will be discussed in detail in [“Adding a New Disk to an Ubuntu 23.04 Volume Group and Logical Volume”](#Volume_Groups.xhtml__idTextAnchor506).

33.2 Finding the New Hard Drive

This tutorial assumes that a new physical or virtual hard drive has been installed and is visible to the operating system. Once added, the operating system should automatically detect the new drive. Typically, the disk drives in a system are assigned device names beginning hd, sd, or nvme, followed by a letter to indicate the device number. The first device might be /dev/sda, the second /dev/sdb, etc.

The following is the output from a typical system with only one disk drive connected to a SATA controller:

# ls /dev/sd*

/dev/sda /dev/sda1 /dev/sda2

This shows that the disk drive represented by /dev/sda is divided into two partitions, represented by /dev/sda1 and /dev/sda2.

The following output is from the same system after a second hard disk drive has been installed:

# ls /dev/sd*

/dev/sda /dev/sda1 /dev/sda2 /dev/sdb

The new hard drive has been assigned to the device file /dev/sdb. The drive has no partitions shown (because we have yet to create any).

At this point, we can create partitions and file systems on the new drive and mount them for access or add the disk as a physical volume as part of a volume group. To perform the former continue with this chapter; otherwise, read [“Adding a New Disk to an Ubuntu 23.04 Volume Group and Logical Volume”](#Volume_Groups.xhtml__idTextAnchor506) for details on configuring Logical Volumes.

33.3 Creating Linux Partitions

The next step is to create one or more Linux partitions on the new disk drive. This is achieved using the fdisk utility, which takes as a command-line argument the device to be partitioned:

# fdisk /dev/sdb

Welcome to fdisk (util-linux 2.37.4).

Changes will remain in memory only, until you decide to write them.

Be careful before using the write command.

Device does not contain a recognized partition table.

Created a new DOS disklabel with disk identifier 0x64d68d00.

Command (m for help):

To view the current partitions on the disk, enter the p command:

Command (m for help): p

Disk /dev/sdb: 14.46 GiB, 15525216256 bytes, 30322688 sectors

Disk model: USB 2.0 FD

Units: sectors of 1 * 512 = 512 bytes

Sector size (logical/physical): 512 bytes / 512 bytes

I/O size (minimum/optimal): 512 bytes / 512 bytes

Disklabel type: dos

Disk identifier: 0x64d68d00

As we can see from the above fdisk output, the disk currently has no partitions because it was previously unused. The next step is to create a new partition on the disk, a task which is performed by entering n (for a new partition) and p (for a primary partition):

Command (m for help): n

Partition type

   p primary (0 primary, 0 extended, 4 free)

   e extended (container for logical partitions)

Select (default p): p

Partition number (1-4, default 1):

In this example, we only plan to create one partition, which will be partition 1\. Next, we need to specify where the partition will begin and end. Since this is the first partition, we need it to start at the first available sector, and since we want to use the entire disk, we specify the last sector as the end. Note that if you wish to create multiple partitions, you can specify the size of each partition by sectors, bytes, kilobytes, or megabytes:

Partition number (1-4, default 1): 1

First sector (2048-30322687, default 2048):

Last sector, +/-sectors or +/-size{K,M,G,T,P} (2048-30322687, default 30322687):

Created a new partition 1 of type 'Linux' and of size 14.5 GiB.

Command (m for help):

Now that we have specified the partition, we need to write it to the disk using the w command:

Command (m for help): w

The partition table has been altered.

Calling ioctl() to re-read partition table.

Syncing disks.

If we now look at the devices again, we will see that the new partition is visible as /dev/sdb1:

# ls /dev/sd*

/dev/sda /dev/sda1 /dev/sda2 /dev/sdb /dev/sdb1

The next step is to create a file system on our new partition.

33.4 Creating a File System on an Ubuntu Disk Partition

We now have a new disk installed, it is visible to Ubuntu, and we have configured a Linux partition on the disk. The next step is to create a Linux file system on the partition so that the operating system can use it to store files and data. The easiest way to create a file system on a partition is to use the mkfs.xfs utility:

# apt install xfsprogs

# umount /dev/sdb1

# mkfs.xfs -f /dev/sdb1

meta-data=/dev/sdb1 isize=512 agcount=4, agsize=947520 blks

         = sectsz=512 attr=2, projid32bit=1

         = crc=1 finobt=1, sparse=1, rmapbt=0

         = reflink=1 bigtime=1 inobtcount=1

data = bsize=4096 blocks=3790080, imaxpct=25

         = sunit=0 swidth=0 blks

naming =version 2 bsize=4096 ascii-ci=0, ftype=1

log =internal log bsize=4096 blocks=2560, version=2

         = sectsz=512 sunit=0 blks, lazy-count=1

realtime =none extsz=4096 blocks=0, rtextents=0

In this case, we have created an XFS file system. XFS is a high-performance file system that is the default filesystem type on Ubuntu and includes several advantages in terms of parallel I/O performance and the use of journaling.

33.5 An Overview of Journaled File Systems

A journaling filesystem keeps a journal or log of the changes being made to the filesystem during disk writing that can be used to rapidly reconstruct corruptions that may occur due to events such as a system crash or power outage.

There are several advantages to using a journaling file system. First, the size and volume of data stored on disk drives have grown exponentially over the years. The problem with a non-journaled file system is that following a crash, the fsck (filesystem consistency check) utility has to be run. The fsck utility will scan the entire filesystem validating all entries and ensuring that blocks are allocated and referenced correctly. It will attempt to fix the problem if it finds a corrupt entry. The issues here are two-fold. First, the fsck utility will not always be able to repair the damage, and you will end up with data in the lost+found directory. An application uses this data, but the system no longer knows where it was referenced from. The other problem is the issue of time. Completing the fsck process on an extensive file system can take a long time, potentially leading to unacceptable downtime.

On the other hand, a journaled file system records information in a log area on a disk (the journal and log do not need to be on the same device) during each write. This is essentially an “intent to commit” data to the filesystem. The amount of information logged is configurable and ranges from not logging anything to logging what is known as the “metadata” (i.e., ownership, date stamp information, etc.) to logging the “metadata” and the data blocks that are to be written to the file. Once the log is updated, the system writes the actual data to the appropriate filesystem areas and marks an entry to say the data is committed.

After a crash, the filesystem can quickly be brought back online using the journal log, thereby reducing what could take minutes using fsck to seconds with the added advantage that there is considerably less chance of data loss or corruption.

33.6 Mounting a File System

Now that we have created a new file system on the Linux partition of our new disk drive, we need to mount it to be accessible and usable. To do this, we need to create a mount point. A mount point is simply a directory or folder into which the file system will be mounted. For this example, we will create a /backup directory to match our file system label (although these values don’t need to match):

# mkdir /backup

The file system may then be manually mounted using the mount command:

# mount /dev/sdb1 /backup

Running the mount command with no arguments shows us all currently mounted file systems (including our new file system):

# mount

proc on /proc type proc (rw,nosuid,nodev,noexec,relatime)

sysfs on /sys type sysfs (rw,nosuid,nodev,noexec,relatime,seclabel)

.

.

/dev/sdb1 on /backup type xfs (rw,relatime,seclabel,attr2,inode64,logbufs=8,logbsize=32k,noquota)

33.7 Configuring Ubuntu to Mount a File System Automatically

To set up the system so that the new file system is automatically mounted at boot time, an entry needs to be added to the /etc/fstab file. The format for an fstab entry is as follows:

<device> <dir> <type> <options> <dump> <fsck>

These entries can be summarized as follows:

•<device> - The device on which the filesystem will be mounted.

•<dir> - The directory that is to act as the mount point for the filesystem.

•<type> - The filesystem type (xfs, ext4 etc.)

•<options> - Additional filesystem mount options, for example, making the filesystem read-only or controlling whether any user can mount the filesystem. Run man mount to review a complete list of options. Setting this value to defaults will use the default settings for the filesystem (rw, suid, dev, exec, auto, nouser, async).

•<dump> - Dictates whether the content of the filesystem is to be included in any backups performed by the dump utility. This setting is rarely used and can be disabled with a 0 value.

•<fsck> - Whether the filesystem is checked by fsck after a system crash and the order in which filesystems are to be checked. For journaled filesystems such as XFS this should be set to 0 to indicate that the check is not required.

The following example shows a fstab entry to automount our /backup partition on the /dev/sdb1 partition:

/dev/sdb1 /backup xfs defaults 0 0

The /backup filesystem will now automount each time the system restarts.

33.8 Adding a Disk Using Cockpit

In addition to working with storage using the command-line utilities outlined in this chapter, it is also possible to configure a new storage device using the Cockpit web console. To view the current storage configuration, log into the Cockpit console and select the Storage option as shown in [Figure 33-1](#Adding_New_DIsk.xhtml__idTextAnchor503):

![](image/centos_cockpit_storage1.jpg)

Figure 33-1

To locate the newly added storage, scroll to the bottom of the Storage page until the Drives section comes into view (note that the Drives section may also be located in the top right-hand corner of the screen):

![](image/cockpit_drives.jpg)

Figure 33-2

In the case of the above figure, the new drive is the 15.5 GB drive. Select the new drive to display the Drive screen as shown in [Figure 33-3](#Adding_New_DIsk.xhtml__idTextAnchor504):

![](image/cockpit_drive_details.jpg)

Figure 33-3

Click on the Create partition button and use the dialog to specify how much space will be allocated to this partition, the filesystem type (XFS is recommended), and an optional label, filesystem mount point, and mount options. Note that additional partitions may be added to the drive if this new partition does not use all the available space. To change settings such as whether the filesystem is read-only or mounted at boot time, change the settings in the Mount options section:

![](image/cockpit_drive_create_partition.jpg)

Figure 33-4

Once the settings have been selected, click the Create partition button to commit the change. Upon completion of the creation process, the new partition will be added to the disk, the corresponding filesystem will be created and mounted at the designated mount point, and appropriate changes will be made to the /etc/fstab file.

33.9 Summary

This chapter has covered adding a physical or virtual disk drive to an existing Ubuntu system. This is a relatively simple process of ensuring the new drive has been detected by the operating system, creating one or more partitions on the drive, and then making filesystems on those partitions. Although several filesystem types are available on Ubuntu, XFS is generally recommended. Once the filesystems are ready, they can be mounted using the mount command. So that the newly created filesystems mount automatically on system startup, additions can be made to the /etc/fstab configuration file.

34. Adding a New Disk to an Ubuntu 23.04 Volume Group and Logical Volume

In the previous chapter, we looked at adding a new disk drive to an Ubuntu system, creating a partition and file system, and then mounting that file system to access the disk. An alternative to creating fixed partitions and file systems is to use Logical Volume Management (LVM) to create logical disks comprising space from one or more physical or virtual disks or partitions. The advantage of using LVM is that space can be added to or removed from logical volumes without spreading data over multiple file systems.

Let us take, for example, the root (/) file system of an Ubuntu-based server. Without LVM, this file system would be created with a specific size when the operating system is installed. If a new disk drive is installed, there is no way to allocate any of that space to the / file system. The only option would be to create new file systems on the new disk and mount them at particular mount points. In this scenario, you would have plenty of space on the new file system, but the / file system would still be nearly full. The only option would be to move files onto the new file system. With LVM, the new disk (or part thereof) can be assigned to the logical volume containing the home file system, thereby dynamically extending the space available.

In this chapter, we will look at the steps necessary to add new disk space to both a volume group and a logical volume to add additional space to the home file system of an Ubuntu system.

34.1 An Overview of Logical Volume Management (LVM)

LVM provides a flexible and high-level approach to managing disk space. Instead of each disk drive being split into partitions of fixed sizes onto which fixed-size file systems are created, LVM provides a way to group disk space into logical volumes that can be easily resized and moved. In addition, LVM allows administrators to carefully control disk space assigned to different groups of users by allocating distinct volume groups or logical volumes to those users. When the space initially allocated to the volume is exhausted, the administrator can add more space without moving the user files to a different file system.

LVM consists of the following components:

34.1.1 Volume Group (VG)

The Volume Group is the high-level container with one or more logical and physical volumes.

34.1.2 Physical Volume (PV)

A physical volume represents a storage device such as a disk drive or other storage media.

34.1.3 Logical Volume (LV)

A logical volume is equivalent to a disk partition and, as with a disk partition, can contain a file system.

34.1.4 Physical Extent (PE)

Each physical volume (PV) is divided into equal size blocks known as physical extents.

34.1.5 Logical Extent (LE)

Each logical volume (LV) is divided into equal size blocks called logical extents.

Suppose we are creating a new volume group called VolGroup001\. This volume group needs physical disk space to function, so we allocate three disk partitions /dev/sda1, /dev/sdb1, and /dev/sdb2. These become physical volumes in VolGroup001\. We would then create a logical volume called LogVol001 within the volume group comprising the three physical volumes.

If we run out of space in LogVol001, we add more disk partitions as physical volumes and assign them to the volume group and logical volume.

34.2 Getting Information about Logical Volumes

As an example of using LVM with Ubuntu, we will work through an example of adding space to the / file system of a standard Ubuntu installation. Anticipating the need for flexibility in the sizing of the root partition, Ubuntu sets up the / file system as a logical volume (called ubuntu_lv) within a volume group called ubuntu-vg. Before making any changes to the LVM setup, however, it is essential first to gather information.

Running the mount command will output information about a range of mount points, including the following entry for the home filesystem:

/dev/mapper/ubuntu--vg-ubuntu--lv on / type ext4 (rw,relatime)

Information about the volume group can be obtained using the vgdisplay command:

# vgdisplay

  --- Volume group ---

  VG Name ubuntu-vg

  System ID

  Format lvm2

  Metadata Areas 1

  Metadata Sequence No 2

  VG Access read/write

  VG Status resizable

  MAX LV 0

  Cur LV 1

  Open LV 1

  Max PV 0

  Cur PV 1

  Act PV 1

  VG Size <295.04 GiB

  PE Size 4.00 MiB

  Total PE 75529

  Alloc PE / Size 75529 / <295.04 GiB

  Free PE / Size 0 / 0

  VG UUID IIGC9W-1UBx-fajE-SMoK-rUdn-qw8E-0omd5P

As we can see in the above example, the ubuntu-vg volume group has a physical extent size of 4.00MiB and has a total of 295.04GB available for allocation to logical volumes. Currently, 75529 physical extents are allocated, equaling the total capacity. Therefore, we must add one or more physical volumes to increase the space allocated to any logical volumes in the ubuntu-vg volume group. The vgs tool is also helpful for displaying a quick overview of the space available in the volume groups on a system:

# vgs

  VG #PV #LV #SN Attr VSize VFree

  ubuntu-vg 1 1 0 wz--n- <295.04g 0

Information about logical volumes in a volume group may similarly be obtained using the lvdisplay command:

# lvdisplay

  --- Logical volume ---

  LV Path /dev/ubuntu-vg/ubuntu-lv

  LV Name ubuntu-lv

  VG Name ubuntu-vg

  LV UUID DaPi0C-vwvy-UudI-aUJQ-mFqx-rIhZ-rT7uHH

  LV Write Access read/write

  LV Creation host, time ubuntu, 2023-07-26 15:42:23 -0400

  LV Status available

  # open 1

  LV Size <295.04 GiB

  Current LE 75529

  Segments 1

  Allocation inherit

  Read ahead sectors auto

  - currently set to 256

  Block device 253:0

As shown in the above example, 295.04 GiB of the space in volume group ubuntu-vg is allocated to logical volume ubuntu-lv (for the / file system).

Now that we know what space is being used, it is often helpful to understand which devices are providing the space (in other words, which devices are being used as physical volumes). To obtain this information, we need to run the pvdisplay command:

# pvdisplay

  --- Physical volume ---

  PV Name /dev/sda3

  VG Name ubuntu-vg

  PV Size <295.04 GiB / not usable 4.00 MiB

  Allocatable yes (but full)

  PE Size 4.00 MiB

  Total PE 75529

  Free PE 0

  Allocated PE 75529

  PV UUID mdde89-ZZS8-6ila-qoZy-ofLp-zxEq-dhifen

Clearly, the space controlled by logical volume ubuntu-vg is provided via a physical volume located on /dev/sda2.

Now that we know more about our LVM configuration, we can add space to the volume group and the logical volume contained within.

34.3 Adding Additional Space to a Volume Group from the Command-Line

Just as with the previous steps to gather information about the current Logical Volume Management configuration of an Ubuntu system, changes to this configuration can be made from the command line.

In the remainder of this chapter, we will assume that a new disk has been added to the system and that the operating system sees it as /dev/sdb. We shall also assume this is a new disk with no existing partitions. If existing partitions are present, they should be backed up, and then the partitions should be deleted from the disk using the fdisk utility. For example, assuming a device represented by /dev/sdb containing two partitions as follows:

# fdisk -l /dev/sdb

Disk /dev/sdb: 14.46 GiB, 15525216256 bytes, 30322688 sectors

Disk model: USB 2.0 FD

Units: sectors of 1 * 512 = 512 bytes

Sector size (logical/physical): 512 bytes / 512 bytes

I/O size (minimum/optimal): 512 bytes / 512 bytes

Disklabel type: dos

Disk identifier: 0x4c33060b

Device Boot Start End Sectors Size Id Type

/dev/sdb1 2048 30322687 30320640 14.5G 83 Linux

Once any filesystems on these partitions have been unmounted, they can be deleted as follows:

# fdisk /dev/sdb

Welcome to fdisk (util-linux 2.37.4).

Changes will remain in memory only, until you decide to write them.

Be careful before using the write command.

Command (m for help): d

Selected partition 1

Partition 1 has been deleted.

Command (m for help): w

The partition table has been altered.

Calling ioctl() to re-read partition table.

Syncing disks.

Before moving to the next step, remove any entries in the /etc/fstab file for these filesystems so that the system does not attempt to mount them on the next reboot.

Once the disk is ready, the next step is to convert this disk into a physical volume using the pvcreate command (also wiping the dos signature if one exists):

# pvcreate /dev/sdb

WARNING: dos signature detected on /dev/sdb at offset 510\. Wipe it? [y/n]: y

  Wiping dos signature on /dev/sdb.

  Physical volume "/dev/sdb" successfully created.

If the creation fails with a message that reads “Device /dev/<device> excluded by a filter”, it may be necessary to wipe the disk using the wipefs command before creating the physical volume:

# wipefs -a /dev/sdb

/dev/sdb: 8 bytes were erased at offset 0x00000200 (gpt): 45 46 49 20 50 41 52 54

/dev/sdb: 8 bytes were erased at offset 0x1fffffe00 (gpt): 45 46 49 20 50 41 52 54

/dev/sdb: 2 bytes were erased at offset 0x000001fe (PMBR): 55 aa

/dev/sdb: calling ioctl to re-read partition table: Success

With the physical volume created, we now need to add it to the volume group (in this case, ubuntu-vg) using the vgextend command:

# vgextend ubuntu-vg /dev/sdb

  Volume group "ubuntu-vg" successfully extended

The new physical volume has now been added to the volume group and is ready to be allocated to a logical volume. To do this, we run the lvextend tool providing the size by which we wish to extend the volume. In this case, we want to extend the size of the root  logical volume by 14 GB. Note that we need to provide the path to the logical volume, which can be obtained from the lvdisplay command (in this case, /dev/ubuntu-vg/ubuntu-lv):

# lvextend -L+14G /dev/ubuntu-vg/ubuntu-lv

  Size of logical volume ubuntu-vg/ubuntu-lv changed from <295.04 GiB (75529 extents) to <309.04 GiB (79113 extents).

  Logical volume ubuntu-vg/ubuntu-lv successfully resized.

The last step is to resize the file system residing on the logical volume to use the additional space. The way this is performed will depend on the filesystem type, which can be identified using the following df command and checking the Type column:

# df -T /

Filesystem Type 1K-blocks Used Available Use% Mounted

/dev/mapper/ubuntu--vg-ubuntu--lv ext4 303396024 22139044 265772260 8% /

If / is formatted using the XFS filesystem, it can be resized using the xfs_growfs utility:

# xfs_growfs /

If, on the other hand, the filesystem is of type ext2, ext3, or ext4, the resize2fs utility should be used instead when performing the filesystem resize:

# resize2fs /dev/ubuntu-vg/ubuntu-lv

Once the resize completes, the file system will have been extended to use the additional space provided by the new disk drive. All this has been achieved without moving a single file or restarting the server. As far as users on the system are concerned, nothing has changed (except that there is now more disk space).

34.4 Summary

Volume groups and logical volumes provide an abstract layer on top of the physical storage devices on an Ubuntu system to provide a flexible way to allocate the space provided by multiple disk drives. This allows disk space allocations to be made and changed dynamically without the need to repartition disk drives and move data between filesystems. This chapter has outlined the basic concepts of volume groups and logical and physical volumes while demonstrating how to manage these using command-line tools.

35\. Adding and Managing Ubuntu Swap Space

An important part of maintaining the performance of an Ubuntu system involves ensuring that adequate swap space is available comparable to the memory demands placed on the system. The goal of this chapter, therefore, is to provide an overview of swap management on Ubuntu.

35.1 What is Swap Space?

Computer systems have a finite amount of physical memory that is made available to the operating system. When the operating system begins to approach the limit of the available memory, it frees up space by writing memory pages to disk. When the operating system requires any of those pages, they are subsequently read back into memory. The area of the disk allocated for this task is referred to as swap space.

35.2 Recommended Swap Space for Ubuntu

The amount of swap recommended for Ubuntu depends on a number of factors including the amount of memory in the system, the workload imposed on that memory and whether the system is required to support hibernation. The current guidelines for Ubuntu swap space are as follows:

| Amount of installed RAM | Recommended swap space | Recommended swap space if hibernation enabled |
| 1GB | 1GB | 2GB |
| 2GB | 1GB | 3GB |
| 3GB | 2GB | 5GB |
| 4GB | 2GB | 6GB |
| 5GB | 2GB | 7GB |
| 6GB | 2GB | 8GB |
| 8GB | 3GB | 11GB |
| 12GB | 3GB | 15GB |
| 16GB | 4GB | 32GB |
| 24GB | 5GB | 48GB |

Table 35-1

For systems with memory configurations exceeding 24GB refer to the following web page for swap space guidelines:

[https://help.ubuntu.com/community/SwapFaq](https://help.ubuntu.com/community/SwapFaq%20)

When a system enters hibernation, the current system state is written to the hard disk, and the host machine is powered off. When the machine is subsequently powered on, the state of the system is restored from the hard disk drive. This differs from suspension, where the system state is stored in RAM. The machine then enters a sleep state whereby power is maintained to the system RAM while other devices are shut down.

35.3 Identifying Current Swap Space Usage

The current amount of swap used by an Ubuntu system may be identified in a number of ways. One option is to output the /proc/swaps file:

# cat /proc/swaps

Filename Type Size Used Priority

/swap.img file 3778556 836928 -2

Alternatively, the swapon command may be used:

# swapon

NAME TYPE SIZE USED PRIO

/swap.img file 3.6G 817.3M -2

To view the amount of swap space relative to the overall available RAM, the free command may be used:

# free

           total used free shared buff/cache available

Mem: 3779672 2554028 451216 809132 1839908 1225644

Swap: 3778556 836928 2941628

35.4 Adding a Swap File to an Ubuntu System

Additional swap may be added to the system by creating a file and assigning it as swap. Begin by creating the swap file using the dd command. The size of the file can be changed by adjusting the count= variable. The following command-line, for example, creates a 2.0 GB file:

# dd if=/dev/zero of=/newswap bs=1024 count=2000000

2000000+0 records in

2000000+0 records out

2048000000 bytes (2.0 GB, 1.9 GiB) copied, 3.62697 s, 565 MB/s

Before converting the file to a swap file, it is important to make sure the file has secure permissions set:

# chmod 0600 /newswap

Once a suitable file has been created, it needs to be converted into a swap file using the mkswap command:

# mkswap /newswap

Setting up swapspace version 1, size = 1.9 GiB (2047995904 bytes)

no label, UUID=4ffc238d-7fde-4367-bd98-c5c46407e535

With the swap file created and configured it can be added to the system in real-time using the swapon utility:

# swapon /newswap

Re-running swapon should now report that the new file is now being used as swap:

# swapon

NAME TYPE SIZE USED PRIO

/swap.img file 3.6G 832.5M -2

/newswap file 1.9G 0B -3

The swap space may be removed dynamically by using the swapoff utility as follows:

# swapoff /newswap

Finally, modify the /etc/fstab file to automatically add the new swap at system boot time by adding the following line:

/newswap swap swap defaults 0 0

35.5 Adding Swap as a Partition

As an alternative to designating a file as swap space, entire disk partitions may also be designated as swap. The steps to achieve this are largely the same as those for adding a swap file. Before allocating a partition to swap, however, make sure that any existing data on the corresponding filesystem is either backed up or no longer needed and that the filesystem has been unmounted.

Assuming that a partition exists on a disk drive represented by /dev/sdb1, for example, the first step would be to convert this into a swap partition, once again using the mkswap utility:

# mkswap /dev/sdb1

mkswap: /dev/sdb1: warning: wiping old xfs signature.

Setting up swapspace version 1, size = 8 GiB (8587833344 bytes)

no label, UUID=a899c8ec-c410-4569-ba18-ddea03370c7f

Next, add the new partition to the system swap and verify that it has indeed been added:

# swapon /dev/sdb1

# swapon

NAME TYPE SIZE USED PRIO

/swap.img file 3.6G 832.5M -2

/dev/sdb1 partition 8G 0B -3

Once again, the /etc/fstab file may be modified to automatically add the swap partition at boot time as follows:

/dev/sdb1 swap swap defaults 0 0

35.6 Adding Space to an Ubuntu LVM Swap Volume

On systems using Logical Volume Management with swap configured as a logical volume, an alternative to adding swap via file or disk partition is to extend the logical volume used for the swap space.

The first step is to identify the current amount of swap available and the volume group and logical volume used for the swap space using the lvdisplay utility (for more information on LVM, refer to the chapter entitled [“Adding a New Disk to an Ubuntu 23.04 Volume Group and Logical Volume”](#Volume_Groups.xhtml__idTextAnchor506)):

# lvdisplay

.

.

  --- Logical volume ---

  LV Path /dev/ubuntu-vg/swap_1

  LV Name swap_1

  VG Name ubuntu-vg

  LV UUID nJPip0-Q6dx-Mfe3-4Aao-gWAa-swDk-7ZiPdP

  LV Write Access read/write

  LV Creation host, time ubuntu, 2020-01-13 13:16:18 -0500

  LV Status available

  # open 2

  LV Size 5.00 GiB

  Current LE 1280

  Segments 1

  Allocation inherit

  Read ahead sectors auto

  - currently set to 256

  Block device 253:1

Clearly, the swap resides on a logical volume named swap_1 which is part of the volume group named ubuntu-vg. The next step is to verify if there is any space available on the volume group that can be allocated to the swap volume:

# vgs

  VG #PV #LV #SN Attr VSize VFree

  ubuntu-vg 2 3 0 wz--n- 197.66g <22.00g

If the amount of space available is sufficient to meet additional swap requirements, turn off the swap and extend the swap logical volume to use as much of the available space as needed to meet the system’s swap requirements:

# lvextend -L+8GB /dev/ubuntu-vg/swap_1

    Logical volume ubuntu_vg/swap_1 successfully resized.

Next, reformat the swap volume and turn the swap back on:

# mkswap /dev/ubuntu-vg/swap_1

mkswap: /dev/ubuntu-vg/swap_1: warning: wiping old swap signature.

Setting up swapspace version 1, size = 12 GiB (12754874368 bytes)

no label, UUID=241a4818-e51c-4b8c-9bc9-1697fc2ce26e

# swapon /dev/ubuntu-vg/swap_1

Having made the changes, check that the swap space has increased:

# swapon

NAME TYPE SIZE USED PRIO

/dev/dm-1 partition 12G 0B -2

35.7 Adding Swap Space to the Volume Group

In the above section, we extended the swap logical volume to use space that was already available in the volume group. If no space is available in the volume group, then it will need to be added before the swap can be extended.

Begin by checking the status of the volume group:

# vgs

  VG #PV #LV #SN Attr VSize VFree

  ubuntu-vg 1 2 0 wz--n- <73.75g 0

The above output indicates that no space is available within the volume group. Suppose, however, that we have a requirement to add 8 GB to the swap on the system. Clearly, this will require the addition of more space to the volume group. For the purposes of this example, it will be assumed that a disk that is 8 GB in size and represented by /dev/sdb is available for addition to the volume group. The first step is to turn this partition into a physical volume:

# pvcreate /dev/sdb

  Physical volume "/dev/sdb" successfully created.

If the creation fails with a message similar to “Device /dev/sdb excluded by a filter”, it may be necessary to wipe the disk before creating the physical volume:

# wipefs -a /dev/sdb

/dev/sdb: 8 bytes were erased at offset 0x00000200 (gpt): 45 46 49 20 50 41 52 54

/dev/sdb: 8 bytes were erased at offset 0x1fffffe00 (gpt): 45 46 49 20 50 41 52 54

/dev/sdb: 2 bytes were erased at offset 0x000001fe (PMBR): 55 aa

/dev/sdb: calling ioctl to re-read partition table: Success

Next, the volume group needs to be extended to use this additional physical volume:

# vgextend ubuntu-vg /dev/sdb

  Volume group "ubuntu-vg" successfully extended

At this point the vgs command should report the addition of the 10 GB of space to the volume group:

# vgs

  VG #PV #LV #SN Attr VSize VFree

  ubuntu-vg 2 2 0 wz--n- 83.74g <10.00g

Now that the additional space is available in the volume group, the swap logical volume may be extended to utilize the space. First, turn off the swap using the swapoff utility:

# swapoff /dev/ubuntu-vg/swap_1

Next, extend the logical volume to use the new space:

# lvextend -L+9.7GB /dev/ubuntu-vg/swap_1

  Rounding size to boundary between physical extents: 9.70 GiB.

  Size of logical volume ubuntu-vg/swap_1 changed from 980.00 MiB (245 extents) to 10.66 GiB (2729 extents).

  Logical volume ubuntu-vg/swap_1 successfully resized.

Re-create the swap on the logical volume:

# mkswap /dev/ubuntu-vg/swap_1

mkswap: /dev/ubuntu-vg/swap_1: warning: wiping old swap signature.

Setting up swapspace version 1, size = 10.7 GiB (11446251520 bytes)

no label, UUID=447fb9e5-5473-4f2c-96f8-839b1457d3ed

Next, turn swap back on:

# swapon /dev/ubuntu-vg/swap_1

Finally, use the  swapon command to verify the addition of the swap space to the system:

# swapon

NAME TYPE SIZE USED PRIO

/dev/dm-1 partition 10.7G 0B -2

35.8 Summary

Swap space is a vital component of just about any operating system in terms of handling situations where memory resources become constrained. By swapping out areas of memory to disk, the system is able to continue to function and meet the needs of the processes and applications running on it.

Ubuntu has a set of guidelines recommending the amount of disk-based swap space that should be allocated depending on the amount of RAM installed in the system. In situations where these recommendations prove to be insufficient, additional swap space can be added to the system, typically without the need to reboot. As outlined in this chapter, swap space can be added in the form of a file, disk or disk partition or by extending existing logical volumes that have been configured as swap space.

36\. Ubuntu 23.04 System and Process Monitoring

An essential part of running and administering an Ubuntu system involves monitoring the overall system health regarding memory, swap, storage, and processor usage. This includes knowing how to inspect and manage the system and user processes running in the background. This chapter will outline some tools and utilities that can be used to monitor system resources and processes on an Ubuntu system.

36.1 Managing Processes

Even when an Ubuntu system appears idle, many system processes will run silently in the background to keep the operating system functioning. For example, when you execute a command or launch an app, user processes are started, running until the associated task is completed.

To obtain a list of active user processes you are currently running within the context of a single terminal or command-prompt session, use the ps command as follows:

$ ps

  PID TTY TIME CMD

10395 pts/1 00:00:00 bash

13218 pts/1 00:00:00 ps

The output from the ps command shows that two user processes are running within the context of the current terminal window or command prompt session, the bash shell into which the command was entered and the ps command itself.

To list all active processes running for the current user, use the ps command with the -a flag. This command will list all running processes that are associated with the user regardless of where they are running (for example, processes running in other terminal windows):

$ ps -a

    PID TTY TIME CMD

   5442 tty2 00:00:00 gnome-session-b

   6350 pts/0 00:00:00 sudo

   6354 pts/0 00:00:00 su

   6355 pts/0 00:00:00 bash

   9849 pts/2 00:00:00 nano

   9850 pts/1 00:00:00 ps

As shown in the above output, the user is running processes related to the GNOME desktop, the shell session, the nano text editor, and the ps command.

To list the processes for a specific user, run ps with the -u flag followed by the user name:

# ps -u john

  PID TTY TIME CMD

914 ? 00:00:00 systemd

915 ? 00:00:00 (sd-pam)

970 ? 00:00:00 gnome-keyring-d

  974 tty1 00:00:00 gdm-x-session

.

.

Note that each process is assigned a unique process ID which can be used to stop the process by sending it a termination (TERM) signal via the kill command. For example:

$ kill 13217

The advantage of ending a process with the TERM signal is that it allows the process to exit gracefully, potentially saving any data that might otherwise be lost.

If the standard termination signal does not terminate the process, repeat the kill command with the -9 option. This command sends a KILL signal which should cause even frozen processes to exit but does not give the process a chance to exit gracefully, possibly resulting in data loss:

$ kill -9 13217

To list all of the processes running on a system (including all user and system processes), execute the following command:

$ ps -ax

    PID TTY STAT TIME COMMAND

1 ? Ss 0:22 /usr/lib/systemd/systemd rhgb --switched-root

2 ? S 0:00 [kthreadd]

3 ? I< 0:00 [rcu_gp]

4 ? I< 0:00 [rcu_par_gp]

5 ? I< 0:00 [netns]

To list all processes and include information about process ownership, CPU, and memory use, execute the ps command with the -aux option:

$ ps -aux

USER PID %CPU %MEM VSZ RSS TTY STAT START TIME COMMAND

root 2 0.0 0.0 0 0 ? S 09:59 0:00 [kthreadd]

root 3 0.0 0.0 0 0 ? I< 09:59 0:00 [rcu_gp]

root 4 0.0 0.0 0 0 ? I< 09:59 0:00 [rcu_par_gp]

root 5 0.0 0.0 0 0 ? I< 09:59 0:00 [netns]

root 7 0.0 0.0 0 0 ? I< 09:59 0:00 [kworker/0:0H-events_highpri]

root 9 0.0 0.0 0 0 ? I< 09:59 0:00 [kworker/0:1H-events_highpri]

.

.

demo 9788 0.1 1.4 763248 50480 ? Ssl 15:05 0:00 /usr/libexec/gnome-terminal-serv

demo 9814 0.0 0.1 224108 5664 pts/2 Ss 15:05 0:00 bash

demo 9849 0.0 0.0 222412 3588 pts/2 S+ 15:06 0:00 nano

demo 9873 0.0 0.1 233416 6280 pts/1 R+ 15:08 0:00 ps -aux

A Linux process can start its own sub-processes (referred to as spawning), resulting in a hierarchical parent-child relationship between processes. To view the process tree, use the ps command and include the -H option. Below is part of the tree output for a ps -aH command execution:

$ ps -aH

    PID TTY TIME CMD

  10036 pts/3 00:00:00 ps

   6350 pts/0 00:00:00 sudo

   6354 pts/0 00:00:00 su

   6355 pts/0 00:00:00 bash

   5442 tty2 00:00:00 gnome-session-b

Process information may also be viewed via the System Monitor tool from the GNOME desktop. This tool can either be launched by searching for “System Monitor” within the desktop environment or from the command line as follows:

$ gnome-system-monitor

Once the System Monitor has launched, select the Processes button located in the toolbar to list the processes running on the system, as shown in [Figure 36-1](#System_and_Process_Monitoring.xhtml__idTextAnchor527) below:

![](image/ubuntu_system_monitor.jpg)

Figure 36-1

To change the processes listed (for example, to list all processes or just your own processes), use the menu as illustrated in [Figure 36-2](#System_and_Process_Monitoring.xhtml__idTextAnchor528):

![](image/ubuntu_system_monitor_menu.jpg)

Figure 36-2

To filter the list of processes, click on the search button in the title bar and enter the process name into the search field:

![](image/ubuntu_system-monitor_search.jpg)

Figure 36-3

To display additional information about a specific process, select it from the list and click on the button located in the bottom right-hand corner (marked A in [Figure 36-4](#System_and_Process_Monitoring.xhtml__idTextAnchor530)) of the dialog:

![](image/ubuntu_system_monitor_details.jpg)

Figure 36-4

A dialog similar to that marked B in the above figure will appear when the button is clicked. Select a process from the list and click the End Process button (C) to terminate it.

To monitor CPU, memory, swap, and network usage, click on the Resources button in the title bar to display the screen shown in [Figure 36-5](#System_and_Process_Monitoring.xhtml__idTextAnchor531):

![](image/ubuntu_system_monitor_resources.jpg)

Figure 36-5

Similarly, a summary of storage space used on the system can be viewed by selecting the File Systems toolbar button:

![](image/ubuntu_system_monitor_filesystems.jpg)

Figure 36-6

36.2 Real-time System Monitoring with top

As the chapter “An Overview of the Cockpit Web Interface” outlined, the Cockpit web interface can perform basic system monitoring. The previous section also explained how the GNOME System Monitor tool could be used to monitor processes and system resources. This chapter also explored how the ps command can provide a snapshot of the processes running on an Ubuntu system. However, the ps command does not provide a real-time view of the processes and resource usage on the system. The top command is an ideal tool for real-time monitoring of system resources and processes from the command prompt.

When running, top will list the processes running on the system ranked by system resource usage (with the most demanding process in the top position). The upper section of the screen displays memory and swap usage information together with CPU data for all CPU cores. All of this output is constantly updated, allowing the system to be monitored in real-time:

![](image/top_running.jpg)

Figure 36-7

To limit the information displayed to the processes belonging to a specific user, start top with the -u option followed by the user name:

$ top -u john

For a complete listing of the features available in top, press the keyboard ‘h’ key or refer to the man page:

$ man top

36.3 Command-Line Disk and Swap Space Monitoring

Disk space can be monitored from within Cockpit and using the GNOME System Monitor. To identify disk usage from the command line, however, the df command provides a helpful and quick overview:

To review current swap space and memory usage, run the free command:

# free

              total used free shared buff/cache available

Mem: 3823720 879916 1561108 226220 1382696 2476300

To continuously monitor memory and swap levels, use the free command with the -s option, specifying the delay in seconds between each update (keeping in mind that the top tool may provide a better way to view this data in real-time):

$ free -s 1

Mem: 3823720 879472 1561532 226220 1382716 2476744

Swap: 2097148 0 2097148

              total used free shared buff/cache available

Mem: 3823720 879140 1559940 228144 1384640 2475152

Swap: 2097148 0 2097148

.

.

To monitor disk I/O from the command line, consider using the iotop command, which can be installed as follows:

# apt install iotop

Once installed and executed (iotop must be run with system administrator privileges), the tool will display a real-time list of disk I/O on a per-process basis:

![](image/iotop_running.jpg)

Figure 36-8

36.4 Summary

Even a system that appears to be doing nothing will have many system processes running in the background. Activities performed by users on the system will result in additional processes being started. Processes can also spawn their own child processes. Each process will use some system resources, including memory, swap space, processor cycles, disk storage, and network bandwidth. This chapter has explored a set of tools that can be used to monitor both process and system resources on a running system and, when necessary, kill errant processes that may be impacting the performance of a system.

Index

Symbols

! [79](#Shell_Overview.xhtml__idIndexMarker111)

#! [83](#Shell_Overview.xhtml__idIndexMarker158)

>> [81](#Shell_Overview.xhtml__idIndexMarker126)

| [81](#Shell_Overview.xhtml__idIndexMarker132)

$DISPLAY variable [170](#X11_Forwarding.xhtml__idIndexMarker461)

.bashrc [83](#Shell_Overview.xhtml__idIndexMarker149)

/etc/exports [176](#NFS_File_Sharing.xhtml__idIndexMarker476)

/etc/fstab [37](#Ubuntu_Installation_Dual_Boot.xhtml__idIndexMarker058), [41](#Reclaim_Windows_Partition.xhtml__idIndexMarker062), [177](#NFS_File_Sharing.xhtml__idIndexMarker480), [179](#NFS_File_Sharing.xhtml__idIndexMarker487), [267](#Adding_New_DIsk.xhtml__idIndexMarker772)

/etc/gdm/custom.conf [170](#X11_Forwarding.xhtml__idIndexMarker453)

/etc/group [87](#User_Management.xhtml__idIndexMarker176)

/etc/httpd [247](#Web_Server.xhtml__idIndexMarker701)

/etc/passwd [87](#User_Management.xhtml__idIndexMarker175)

/etc/samba/smb.conf [182](#Samba_File_Sharing.xhtml__idIndexMarker494)

/etc/shadow [87](#User_Management.xhtml__idIndexMarker177)

/etc/sshd_config [170](#X11_Forwarding.xhtml__idIndexMarker455)

/etc/ssh/sshd_config.d [170](#X11_Forwarding.xhtml__idIndexMarker456)

/etc/sudoers [87](#User_Management.xhtml__idIndexMarker174)

/etc/systemd/system [98](#Systemd_Targets_and_States.xhtml__idIndexMarker199)

/home [85](#User_Management.xhtml__idIndexMarker164)

/proc/swaps file [278](#Ubuntu_Swap_Space.xhtml__idIndexMarker810)

.requires [98](#Systemd_Targets_and_States.xhtml__idIndexMarker201)

.ssh [154](#SSH_Authentication.xhtml__idIndexMarker414), [155](#SSH_Authentication.xhtml__idIndexMarker421)

/usr/lib/systemd/system [98](#Systemd_Targets_and_States.xhtml__idIndexMarker200)

/var/log/maillog [260](#Postfix_Setup.xhtml__idIndexMarker752)

.wants [98](#Systemd_Targets_and_States.xhtml__idIndexMarker198)

A

access control list [203](#KVM_Create_VM.xhtml__idIndexMarker593)

ACL [203](#KVM_Create_VM.xhtml__idIndexMarker594)

Advanced Package Tool [101](#Ubuntu_Package_Management.xhtml__idIndexMarker206)

AIX [7](#Red_Hat_History.xhtml__idIndexMarker016)

alias [81](#Shell_Overview.xhtml__idIndexMarker138)

Aliases [81](#Shell_Overview.xhtml__idIndexMarker136)

AMD-V [194](#Virtualization_Overview.xhtml__idIndexMarker561)

Andrew S. Tanenbaum [7](#Red_Hat_History.xhtml__idIndexMarker022)

Apache

mod_ssl [250](#Web_Server.xhtml__idIndexMarker715)

Apache web server [245](#Web_Server.xhtml__idIndexMarker690)

apt [101](#Ubuntu_Package_Management.xhtml__idIndexMarker207)

edit-sources [102](#Ubuntu_Package_Management.xhtml__idIndexMarker218)

install [104](#Ubuntu_Package_Management.xhtml__idIndexMarker224)

package management [104](#Ubuntu_Package_Management.xhtml__idIndexMarker222)

purge [104](#Ubuntu_Package_Management.xhtml__idIndexMarker226)

remove [104](#Ubuntu_Package_Management.xhtml__idIndexMarker225)

search [105](#Ubuntu_Package_Management.xhtml__idIndexMarker228)

show [105](#Ubuntu_Package_Management.xhtml__idIndexMarker230)

sources list [102](#Ubuntu_Package_Management.xhtml__idIndexMarker216)

update [104](#Ubuntu_Package_Management.xhtml__idIndexMarker223)

upgrade [106](#Ubuntu_Package_Management.xhtml__idIndexMarker232)

apt-file [105](#Ubuntu_Package_Management.xhtml__idIndexMarker229)

apt list [104](#Ubuntu_Package_Management.xhtml__idIndexMarker227)

authorized_keys file [158](#SSH_Authentication.xhtml__idIndexMarker433)

B

Bash

scripts [83](#Shell_Overview.xhtml__idIndexMarker151)

Bash shell [77](#Shell_Overview.xhtml__idIndexMarker094)

aliases [81](#Shell_Overview.xhtml__idIndexMarker135)

.bashrc [83](#Shell_Overview.xhtml__idIndexMarker150)

chmod [84](#Shell_Overview.xhtml__idIndexMarker161)

command-line editing [78](#Shell_Overview.xhtml__idIndexMarker108)

do loops [83](#Shell_Overview.xhtml__idIndexMarker155)

echo [82](#Shell_Overview.xhtml__idIndexMarker147)

environment variables [82](#Shell_Overview.xhtml__idIndexMarker139)

filename completion [80](#Shell_Overview.xhtml__idIndexMarker117)

Filename shorthand [80](#Shell_Overview.xhtml__idIndexMarker112)

for loop [83](#Shell_Overview.xhtml__idIndexMarker153)

history [79](#Shell_Overview.xhtml__idIndexMarker109)

HOME [82](#Shell_Overview.xhtml__idIndexMarker144)

input and output redirection [80](#Shell_Overview.xhtml__idIndexMarker120)

PATH [82](#Shell_Overview.xhtml__idIndexMarker142)

path completion [80](#Shell_Overview.xhtml__idIndexMarker118)

pipes [81](#Shell_Overview.xhtml__idIndexMarker129)

sh [84](#Shell_Overview.xhtml__idIndexMarker159)

stderr [81](#Shell_Overview.xhtml__idIndexMarker127)

stdin [80](#Shell_Overview.xhtml__idIndexMarker124)

stdout [80](#Shell_Overview.xhtml__idIndexMarker122)

basic.target [94](#Systemd_Targets_and_States.xhtml__idIndexMarker190)

Bell Labs [77](#Shell_Overview.xhtml__idIndexMarker098)

Boot Menu

editing [45](#Reclaim_Windows_Partition.xhtml__idIndexMarker067)

Bourne Again SHell [77](#Shell_Overview.xhtml__idIndexMarker101)

Bourne shell [77](#Shell_Overview.xhtml__idIndexMarker099)

Brian Fox [77](#Shell_Overview.xhtml__idIndexMarker102)

buildah [237](#Containers_Overview.xhtml__idIndexMarker652)

C

CA [250](#Web_Server.xhtml__idIndexMarker713)

Canonical Ltd [7](#Red_Hat_History.xhtml__idIndexMarker010), [8](#Red_Hat_History.xhtml__idIndexMarker033)

cat [80](#Shell_Overview.xhtml__idIndexMarker114)

CentOS

history of [7](#Red_Hat_History.xhtml__idIndexMarker006)

certbot [251](#Web_Server.xhtml__idIndexMarker720)

Certificate Authority [250](#Web_Server.xhtml__idIndexMarker712)

change root [235](#Containers_Overview.xhtml__idIndexMarker642)

chmod [84](#Shell_Overview.xhtml__idIndexMarker162)

chroot [235](#Containers_Overview.xhtml__idIndexMarker643)

cifs filesystem [189](#Samba_File_Sharing.xhtml__idIndexMarker535)

CNI [238](#Containers_Overview.xhtml__idIndexMarker665)

Cockpit [98](#Systemd_Targets_and_States.xhtml__idIndexMarker202)

accessing [66](#Ubuntu_Cockpit_Overview.xhtml__idIndexMarker080)

account management [70](#Ubuntu_Cockpit_Overview.xhtml__idIndexMarker085)

applications [71](#Ubuntu_Cockpit_Overview.xhtml__idIndexMarker087)

cockpit-machines [201](#KVM_Create_VM.xhtml__idIndexMarker589)

cockpit-storaged [178](#NFS_File_Sharing.xhtml__idIndexMarker485)

create VM [201](#KVM_Create_VM.xhtml__idIndexMarker590)

Drives [268](#Adding_New_DIsk.xhtml__idIndexMarker775)

enabling [66](#Ubuntu_Cockpit_Overview.xhtml__idIndexMarker076)

extensions [65](#Ubuntu_Cockpit_Overview.xhtml__idIndexMarker075), [71](#Ubuntu_Cockpit_Overview.xhtml__idIndexMarker088)

installing [66](#Ubuntu_Cockpit_Overview.xhtml__idIndexMarker077)

logs [68](#Ubuntu_Cockpit_Overview.xhtml__idIndexMarker082)

Multiple Servers [73](#Ubuntu_Cockpit_Overview.xhtml__idIndexMarker092)

networking [69](#Ubuntu_Cockpit_Overview.xhtml__idIndexMarker084)

NFS [177](#NFS_File_Sharing.xhtml__idIndexMarker483)

overview [65](#Ubuntu_Cockpit_Overview.xhtml__idIndexMarker074)

persistent metrics [74](#Ubuntu_Cockpit_Overview.xhtml__idIndexMarker093)

port [66](#Ubuntu_Cockpit_Overview.xhtml__idIndexMarker079)

select bridge [225](#KVM_Network_Bridge.xhtml__idIndexMarker623)

services [71](#Ubuntu_Cockpit_Overview.xhtml__idIndexMarker086), [98](#Systemd_Targets_and_States.xhtml__idIndexMarker203)

storage [69](#Ubuntu_Cockpit_Overview.xhtml__idIndexMarker083), [267](#Adding_New_DIsk.xhtml__idIndexMarker774)

system [67](#Ubuntu_Cockpit_Overview.xhtml__idIndexMarker081)

systemd [98](#Systemd_Targets_and_States.xhtml__idIndexMarker204)

terminal access [73](#Ubuntu_Cockpit_Overview.xhtml__idIndexMarker091)

user management [87](#User_Management.xhtml__idIndexMarker178)

virtual machines [72](#Ubuntu_Cockpit_Overview.xhtml__idIndexMarker090)

cockpit-machines [201](#KVM_Create_VM.xhtml__idIndexMarker588)

cockpit.socket [66](#Ubuntu_Cockpit_Overview.xhtml__idIndexMarker078)

cockpit-storaged [178](#NFS_File_Sharing.xhtml__idIndexMarker486)

Compressed X11 Forwarding [171](#X11_Forwarding.xhtml__idIndexMarker467)

Connection Profiles [122](#Network_Management.xhtml__idIndexMarker278)

containerd [235](#Containers_Overview.xhtml__idIndexMarker646)

Container Networking Interface [238](#Containers_Overview.xhtml__idIndexMarker664)

Containers

overview [235](#Containers_Overview.xhtml__idIndexMarker641)

pull image [239](#Ubuntu_Container_Tutorial.xhtml__idIndexMarker671)

running image [241](#Ubuntu_Container_Tutorial.xhtml__idIndexMarker674)

save to image [243](#Ubuntu_Container_Tutorial.xhtml__idIndexMarker682)

CRI-O [235](#Containers_Overview.xhtml__idIndexMarker647)

C shell [77](#Shell_Overview.xhtml__idIndexMarker100)

D

daemon [93](#Systemd_Targets_and_States.xhtml__idIndexMarker184)

David Korn [77](#Shell_Overview.xhtml__idIndexMarker097)

dd [11](#Ubuntu_Installation_Clean_Disk.xhtml__idIndexMarker050), [278](#Ubuntu_Swap_Space.xhtml__idIndexMarker814)

DDNS [245](#Web_Server.xhtml__idIndexMarker694)

Debian [8](#Red_Hat_History.xhtml__idIndexMarker032)

default.target [96](#Systemd_Targets_and_States.xhtml__idIndexMarker195)

df [276](#Volume_Groups.xhtml__idIndexMarker799), [288](#System_and_Process_Monitoring.xhtml__idIndexMarker841)

disk drive

detecting [263](#Adding_New_DIsk.xhtml__idIndexMarker758)

disk I/O [289](#System_and_Process_Monitoring.xhtml__idIndexMarker845)

Disk partition

formatting [44](#Reclaim_Windows_Partition.xhtml__idIndexMarker064)

disk usage [288](#System_and_Process_Monitoring.xhtml__idIndexMarker840)

diskutil [12](#Ubuntu_Installation_Clean_Disk.xhtml__idIndexMarker052)

DISPLAY variable [170](#X11_Forwarding.xhtml__idIndexMarker462)

dmesg [11](#Ubuntu_Installation_Clean_Disk.xhtml__idIndexMarker047)

DNS [130](#Firewall_Basics.xhtml__idIndexMarker315)

DNS MX Records [259](#Postfix_Setup.xhtml__idIndexMarker747)

Docker [235](#Containers_Overview.xhtml__idIndexMarker644), [236](#Containers_Overview.xhtml__idIndexMarker649)

do loops [83](#Shell_Overview.xhtml__idIndexMarker156)

Domain Name Server [130](#Firewall_Basics.xhtml__idIndexMarker316)

dual boot [41](#Reclaim_Windows_Partition.xhtml__idIndexMarker059)

Dynamic DNS [245](#Web_Server.xhtml__idIndexMarker693)

DynDNS [245](#Web_Server.xhtml__idIndexMarker695)

E

echo [82](#Shell_Overview.xhtml__idIndexMarker148)

Email Server [255](#Postfix_Setup.xhtml__idIndexMarker725)

env [82](#Shell_Overview.xhtml__idIndexMarker141)

Environment Variables [82](#Shell_Overview.xhtml__idIndexMarker140)

Errata [5](#Introduction.xhtml__idIndexMarker005)

Exim [255](#Postfix_Setup.xhtml__idIndexMarker733)

export [82](#Shell_Overview.xhtml__idIndexMarker146)

exportfs [176](#NFS_File_Sharing.xhtml__idIndexMarker477)

ext2 [276](#Volume_Groups.xhtml__idIndexMarker802)

ext3 [276](#Volume_Groups.xhtml__idIndexMarker803)

ext4 [276](#Volume_Groups.xhtml__idIndexMarker804)

F

fdisk [41](#Reclaim_Windows_Partition.xhtml__idIndexMarker063), [264](#Adding_New_DIsk.xhtml__idIndexMarker762), [274](#Volume_Groups.xhtml__idIndexMarker793)

create partition [264](#Adding_New_DIsk.xhtml__idIndexMarker763)

list partitions [264](#Adding_New_DIsk.xhtml__idIndexMarker761)

Fedora Media Writer [13](#Ubuntu_Installation_Clean_Disk.xhtml__idIndexMarker053)

Fetchmail [255](#Postfix_Setup.xhtml__idIndexMarker732)

Filename Shorthand [80](#Shell_Overview.xhtml__idIndexMarker113)

File System

creating [265](#Adding_New_DIsk.xhtml__idIndexMarker764)

mounting [266](#Adding_New_DIsk.xhtml__idIndexMarker770)

File Transfer (Control) [129](#Firewall_Basics.xhtml__idIndexMarker306)

File Transfer Protocol (Data) [129](#Firewall_Basics.xhtml__idIndexMarker301)

findmnt [11](#Ubuntu_Installation_Clean_Disk.xhtml__idIndexMarker048)

firewall

gufw [133](#Ubuntu_ufw_Firewall.xhtml__idIndexMarker342)

ufw [133](#Ubuntu_ufw_Firewall.xhtml__idIndexMarker341)

Firewall

overview [127](#Firewall_Basics.xhtml__idIndexMarker285), [143](#Ubuntu_Firewall_Configuration.xhtml__idIndexMarker364)

web server settings [246](#Web_Server.xhtml__idIndexMarker697)

firewall-cmd [129](#Firewall_Basics.xhtml__idIndexMarker297), [146](#Ubuntu_Firewall_Configuration.xhtml__idIndexMarker378)

mail settings [257](#Postfix_Setup.xhtml__idIndexMarker742)

NFS settings [175](#NFS_File_Sharing.xhtml__idIndexMarker475)

firewall-config [150](#Ubuntu_Firewall_Configuration.xhtml__idIndexMarker403)

firewalld

default zone [146](#Ubuntu_Firewall_Configuration.xhtml__idIndexMarker383)

display zone information [146](#Ubuntu_Firewall_Configuration.xhtml__idIndexMarker385)

firewall-cmd [146](#Ubuntu_Firewall_Configuration.xhtml__idIndexMarker377)

firewall-config [150](#Ubuntu_Firewall_Configuration.xhtml__idIndexMarker402)

ICMP rules [149](#Ubuntu_Firewall_Configuration.xhtml__idIndexMarker398)

interfaces [143](#Ubuntu_Firewall_Configuration.xhtml__idIndexMarker369), [145](#Ubuntu_Firewall_Configuration.xhtml__idIndexMarker372)

list services [147](#Ubuntu_Firewall_Configuration.xhtml__idIndexMarker387)

overview [143](#Ubuntu_Firewall_Configuration.xhtml__idIndexMarker365)

permanent settings [146](#Ubuntu_Firewall_Configuration.xhtml__idIndexMarker380)

port forwarding [149](#Ubuntu_Firewall_Configuration.xhtml__idIndexMarker399)

port rules [147](#Ubuntu_Firewall_Configuration.xhtml__idIndexMarker389), [148](#Ubuntu_Firewall_Configuration.xhtml__idIndexMarker393)

ports [143](#Ubuntu_Firewall_Configuration.xhtml__idIndexMarker367), [145](#Ubuntu_Firewall_Configuration.xhtml__idIndexMarker374)

reload [146](#Ubuntu_Firewall_Configuration.xhtml__idIndexMarker381)

runtime settings [146](#Ubuntu_Firewall_Configuration.xhtml__idIndexMarker379)

services [143](#Ubuntu_Firewall_Configuration.xhtml__idIndexMarker368)

status [145](#Ubuntu_Firewall_Configuration.xhtml__idIndexMarker375)

zone creation [148](#Ubuntu_Firewall_Configuration.xhtml__idIndexMarker395)

zone/interface assignments [148](#Ubuntu_Firewall_Configuration.xhtml__idIndexMarker397)

zones [143](#Ubuntu_Firewall_Configuration.xhtml__idIndexMarker370)

zone services [147](#Ubuntu_Firewall_Configuration.xhtml__idIndexMarker391)

for [83](#Shell_Overview.xhtml__idIndexMarker154)

ForwardX11Trusted [171](#X11_Forwarding.xhtml__idIndexMarker465)

FQDN [130](#Firewall_Basics.xhtml__idIndexMarker317)

free [278](#Ubuntu_Swap_Space.xhtml__idIndexMarker812)

-s flag [288](#System_and_Process_Monitoring.xhtml__idIndexMarker842)

Free Software Foundation [8](#Red_Hat_History.xhtml__idIndexMarker027)

fsck [266](#Adding_New_DIsk.xhtml__idIndexMarker768)

fstab [177](#NFS_File_Sharing.xhtml__idIndexMarker481), [267](#Adding_New_DIsk.xhtml__idIndexMarker773)

FTP [127](#Firewall_Basics.xhtml__idIndexMarker289), [129](#Firewall_Basics.xhtml__idIndexMarker300)

Full Virtualization [194](#Virtualization_Overview.xhtml__idIndexMarker555)

G

GDM [21](#Ubuntu_Installation_Clean_Disk.xhtml__idIndexMarker055)

gedit [171](#X11_Forwarding.xhtml__idIndexMarker463)

getfacl [203](#KVM_Create_VM.xhtml__idIndexMarker596)

GNOME 3 [51](#Ubuntu_GNOME_Desktop.xhtml__idIndexMarker073)

GNOME desktop

installing [51](#Ubuntu_GNOME_Desktop.xhtml__idIndexMarker069)

GNOME Desktop [51](#Ubuntu_GNOME_Desktop.xhtml__idIndexMarker068)

installation [51](#Ubuntu_GNOME_Desktop.xhtml__idIndexMarker071)

starting [51](#Ubuntu_GNOME_Desktop.xhtml__idIndexMarker070)

GNOME Display Manager [21](#Ubuntu_Installation_Clean_Disk.xhtml__idIndexMarker054)

gnome-system-monitor [285](#System_and_Process_Monitoring.xhtml__idIndexMarker837)

GNU/Linux [8](#Red_Hat_History.xhtml__idIndexMarker028)

GNU project [8](#Red_Hat_History.xhtml__idIndexMarker040)

graphical.target [94](#Systemd_Targets_and_States.xhtml__idIndexMarker188)

groupadd [86](#User_Management.xhtml__idIndexMarker168)

groupdel [86](#User_Management.xhtml__idIndexMarker170)

groups [86](#User_Management.xhtml__idIndexMarker171)

Guest OS virtualization [191](#Virtualization_Overview.xhtml__idIndexMarker538)

gufw [133](#Ubuntu_ufw_Firewall.xhtml__idIndexMarker343)

adding simple rules [137](#Ubuntu_ufw_Firewall.xhtml__idIndexMarker354)

advanced rules [138](#Ubuntu_ufw_Firewall.xhtml__idIndexMarker355)

allow [136](#Ubuntu_ufw_Firewall.xhtml__idIndexMarker350)

deny [136](#Ubuntu_ufw_Firewall.xhtml__idIndexMarker351)

enabling [133](#Ubuntu_ufw_Firewall.xhtml__idIndexMarker346)

installing [133](#Ubuntu_ufw_Firewall.xhtml__idIndexMarker345)

limit [137](#Ubuntu_ufw_Firewall.xhtml__idIndexMarker353)

preconfigured rules [136](#Ubuntu_ufw_Firewall.xhtml__idIndexMarker349)

profiles [134](#Ubuntu_ufw_Firewall.xhtml__idIndexMarker348)

reject [137](#Ubuntu_ufw_Firewall.xhtml__idIndexMarker352)

running [133](#Ubuntu_ufw_Firewall.xhtml__idIndexMarker347)

H

Hardware Virtualization [194](#Virtualization_Overview.xhtml__idIndexMarker558)

Hewlett-Packard [7](#Red_Hat_History.xhtml__idIndexMarker017)

hibernation [278](#Ubuntu_Swap_Space.xhtml__idIndexMarker808)

history [78](#Shell_Overview.xhtml__idIndexMarker105), [79](#Shell_Overview.xhtml__idIndexMarker110)

HOME [82](#Shell_Overview.xhtml__idIndexMarker145)

HP-UX [7](#Red_Hat_History.xhtml__idIndexMarker018)

HTTP [131](#Firewall_Basics.xhtml__idIndexMarker320), [249](#Web_Server.xhtml__idIndexMarker705)

httpd.conf [251](#Web_Server.xhtml__idIndexMarker721)

httpd-le-ssl.conf [251](#Web_Server.xhtml__idIndexMarker722)

HTTPS [127](#Firewall_Basics.xhtml__idIndexMarker288), [132](#Firewall_Basics.xhtml__idIndexMarker334), [250](#Web_Server.xhtml__idIndexMarker706)

hypercalls [193](#Virtualization_Overview.xhtml__idIndexMarker551)

Hypertext Text Transfer Protocol [131](#Firewall_Basics.xhtml__idIndexMarker321)

Hypertext Transfer Protocol Secure [132](#Firewall_Basics.xhtml__idIndexMarker335)

Hypervisor [192](#Virtualization_Overview.xhtml__idIndexMarker545)

hypercalls [193](#Virtualization_Overview.xhtml__idIndexMarker553)

type-1 [192](#Virtualization_Overview.xhtml__idIndexMarker544)

type-2 [192](#Virtualization_Overview.xhtml__idIndexMarker543)

Hypervisor Virtualization [192](#Virtualization_Overview.xhtml__idIndexMarker540)

I

Ian Murdoch [8](#Red_Hat_History.xhtml__idIndexMarker030)

IBM [7](#Red_Hat_History.xhtml__idIndexMarker015)

id_rsa file [154](#SSH_Authentication.xhtml__idIndexMarker415), [155](#SSH_Authentication.xhtml__idIndexMarker420), [157](#SSH_Authentication.xhtml__idIndexMarker430)

id_rsa.pub file [154](#SSH_Authentication.xhtml__idIndexMarker416), [158](#SSH_Authentication.xhtml__idIndexMarker431)

if statements [83](#Shell_Overview.xhtml__idIndexMarker157)

IMAP [130](#Firewall_Basics.xhtml__idIndexMarker314)

IMAP4 [131](#Firewall_Basics.xhtml__idIndexMarker329)

Input and Output Redirection [80](#Shell_Overview.xhtml__idIndexMarker121)

Installation

clean disk [9](#Ubuntu_Installation_Clean_Disk.xhtml__idIndexMarker041)

Intel VT [194](#Virtualization_Overview.xhtml__idIndexMarker562)

Intel x86

Rings [193](#Virtualization_Overview.xhtml__idIndexMarker546)

Internet Message Access Protocol, Version 4 [131](#Firewall_Basics.xhtml__idIndexMarker330)

internet service provider [245](#Web_Server.xhtml__idIndexMarker691)

I/O redirection [81](#Shell_Overview.xhtml__idIndexMarker131)

iotop [289](#System_and_Process_Monitoring.xhtml__idIndexMarker844)

installing [289](#System_and_Process_Monitoring.xhtml__idIndexMarker843)

iptables [127](#Firewall_Basics.xhtml__idIndexMarker286), [129](#Firewall_Basics.xhtml__idIndexMarker296), [143](#Ubuntu_Firewall_Configuration.xhtml__idIndexMarker366)

rules [128](#Firewall_Basics.xhtml__idIndexMarker294)

tool [128](#Firewall_Basics.xhtml__idIndexMarker295)

ip tool [120](#Network_Management.xhtml__idIndexMarker271)

ISO image

write to USB drive [11](#Ubuntu_Installation_Clean_Disk.xhtml__idIndexMarker044)

ISP [245](#Web_Server.xhtml__idIndexMarker692)

J

Journaled File Systems [266](#Adding_New_DIsk.xhtml__idIndexMarker767)

K

Kerberos [131](#Firewall_Basics.xhtml__idIndexMarker331)

kernel [7](#Red_Hat_History.xhtml__idIndexMarker023)

kill [284](#System_and_Process_Monitoring.xhtml__idIndexMarker829)

-9 flag [284](#System_and_Process_Monitoring.xhtml__idIndexMarker832)

KMail [255](#Postfix_Setup.xhtml__idIndexMarker728)

Korn shell [77](#Shell_Overview.xhtml__idIndexMarker096)

Kubernetes [236](#Containers_Overview.xhtml__idIndexMarker651)

KVM

hardware requirements [197](#KVM_Installation.xhtml__idIndexMarker573)

installation [198](#KVM_Installation.xhtml__idIndexMarker575)

overview [197](#KVM_Installation.xhtml__idIndexMarker572)

virt-manager [198](#KVM_Installation.xhtml__idIndexMarker579)

kvm_amd [198](#KVM_Installation.xhtml__idIndexMarker582)

kvm_intel [198](#KVM_Installation.xhtml__idIndexMarker583)

KVM virtualization [195](#Virtualization_Overview.xhtml__idIndexMarker567)

L

LE [272](#Volume_Groups.xhtml__idIndexMarker787)

Let’s Encrypt [250](#Web_Server.xhtml__idIndexMarker719)

libvirtd [209](#KVM_virt-manager.xhtml__idIndexMarker602)

libvirtd daemon [199](#KVM_Installation.xhtml__idIndexMarker584)

Linus Torvalds [7](#Red_Hat_History.xhtml__idIndexMarker024)

Linux Containers. See Containers

Logical Extent [272](#Volume_Groups.xhtml__idIndexMarker786)

Logical Volume [272](#Volume_Groups.xhtml__idIndexMarker782)

Logical Volume Management [271](#Volume_Groups.xhtml__idIndexMarker776)

loopback interface [119](#Network_Management.xhtml__idIndexMarker269)

lost+found [266](#Adding_New_DIsk.xhtml__idIndexMarker769)

ls [78](#Shell_Overview.xhtml__idIndexMarker103), [81](#Shell_Overview.xhtml__idIndexMarker137)

lscpu [197](#KVM_Installation.xhtml__idIndexMarker574)

lsmod [198](#KVM_Installation.xhtml__idIndexMarker581)

LV [272](#Volume_Groups.xhtml__idIndexMarker783)

lvdisplay [273](#Volume_Groups.xhtml__idIndexMarker791), [275](#Volume_Groups.xhtml__idIndexMarker798), [280](#Ubuntu_Swap_Space.xhtml__idIndexMarker820)

lvextend [275](#Volume_Groups.xhtml__idIndexMarker797)

LVM [271](#Volume_Groups.xhtml__idIndexMarker777)

lxd [235](#Containers_Overview.xhtml__idIndexMarker645)

M

macOS

writing ISO to USB drive [12](#Ubuntu_Installation_Clean_Disk.xhtml__idIndexMarker051)

MacVTap [195](#Virtualization_Overview.xhtml__idIndexMarker569)

Mail Delivery Agent [255](#Postfix_Setup.xhtml__idIndexMarker734)

Mail Exchanger [259](#Postfix_Setup.xhtml__idIndexMarker748)

Mail Transfer Agent [255](#Postfix_Setup.xhtml__idIndexMarker729)

Mail User Agent [255](#Postfix_Setup.xhtml__idIndexMarker726)

main.cf [257](#Postfix_Setup.xhtml__idIndexMarker746)

man [78](#Shell_Overview.xhtml__idIndexMarker106)

Mark Shuttleworth [7](#Red_Hat_History.xhtml__idIndexMarker011), [8](#Red_Hat_History.xhtml__idIndexMarker031)

Martin Hellman [153](#SSH_Authentication.xhtml__idIndexMarker408)

MDA [255](#Postfix_Setup.xhtml__idIndexMarker735)

MINIX [7](#Red_Hat_History.xhtml__idIndexMarker021)

mkfs.xfs [44](#Reclaim_Windows_Partition.xhtml__idIndexMarker065), [265](#Adding_New_DIsk.xhtml__idIndexMarker765)

mkswap [278](#Ubuntu_Swap_Space.xhtml__idIndexMarker815), [279](#Ubuntu_Swap_Space.xhtml__idIndexMarker818)

mod_ssl [250](#Web_Server.xhtml__idIndexMarker716)

mount [36](#Ubuntu_Installation_Dual_Boot.xhtml__idIndexMarker057), [177](#NFS_File_Sharing.xhtml__idIndexMarker479), [188](#Samba_File_Sharing.xhtml__idIndexMarker534), [266](#Adding_New_DIsk.xhtml__idIndexMarker771), [272](#Volume_Groups.xhtml__idIndexMarker788)

MTA [255](#Postfix_Setup.xhtml__idIndexMarker730)

MUA [255](#Postfix_Setup.xhtml__idIndexMarker727)

multi-user.target [94](#Systemd_Targets_and_States.xhtml__idIndexMarker187)

MX [259](#Postfix_Setup.xhtml__idIndexMarker749)

N

NAT [195](#Virtualization_Overview.xhtml__idIndexMarker565), [203](#KVM_Create_VM.xhtml__idIndexMarker592)

NetBIOS [185](#Samba_File_Sharing.xhtml__idIndexMarker527)

NetBIOS nameservice [185](#Samba_File_Sharing.xhtml__idIndexMarker529)

Network Address Translation [195](#Virtualization_Overview.xhtml__idIndexMarker564)

Networked Bridge Interface [221](#KVM_Network_Bridge.xhtml__idIndexMarker616)

Network File System [132](#Firewall_Basics.xhtml__idIndexMarker339)

NetworkManager

Connection Profiles [122](#Network_Management.xhtml__idIndexMarker277)

enabling [118](#Network_Management.xhtml__idIndexMarker264)

installing [118](#Network_Management.xhtml__idIndexMarker265)

permissions [126](#Network_Management.xhtml__idIndexMarker284)

Network News Transfer Protocol [131](#Firewall_Basics.xhtml__idIndexMarker325)

Network Time Protocol [131](#Firewall_Basics.xhtml__idIndexMarker328)

NFS [132](#Firewall_Basics.xhtml__idIndexMarker338)

Cockpit [177](#NFS_File_Sharing.xhtml__idIndexMarker484)

firewall settings [175](#NFS_File_Sharing.xhtml__idIndexMarker473)

nfs-utils [176](#NFS_File_Sharing.xhtml__idIndexMarker478)

NMB [185](#Samba_File_Sharing.xhtml__idIndexMarker528)

nmcli [117](#Network_Management.xhtml__idIndexMarker261), [223](#KVM_Network_Bridge.xhtml__idIndexMarker620)

activate connection [121](#Network_Management.xhtml__idIndexMarker275)

add bridge [223](#KVM_Network_Bridge.xhtml__idIndexMarker619)

add connections [123](#Network_Management.xhtml__idIndexMarker281)

command line options [118](#Network_Management.xhtml__idIndexMarker266)

deactivate connection [121](#Network_Management.xhtml__idIndexMarker274)

delete connection [123](#Network_Management.xhtml__idIndexMarker280)

device status [119](#Network_Management.xhtml__idIndexMarker268)

general status [119](#Network_Management.xhtml__idIndexMarker267)

interactive [124](#Network_Management.xhtml__idIndexMarker282)

modify connection [122](#Network_Management.xhtml__idIndexMarker276)

permissions [126](#Network_Management.xhtml__idIndexMarker283)

reload [122](#Network_Management.xhtml__idIndexMarker279)

show connections [120](#Network_Management.xhtml__idIndexMarker270)

switch connection [121](#Network_Management.xhtml__idIndexMarker272)

wifi scan [121](#Network_Management.xhtml__idIndexMarker273)

nm-connection-editor [117](#Network_Management.xhtml__idIndexMarker263)

create bridge [227](#KVM_Network_Bridge.xhtml__idIndexMarker626)

nmtui [117](#Network_Management.xhtml__idIndexMarker262)

NNTP [131](#Firewall_Basics.xhtml__idIndexMarker324)

NTP [131](#Firewall_Basics.xhtml__idIndexMarker327)

nvme [263](#Adding_New_DIsk.xhtml__idIndexMarker759)

O

OCI [237](#Containers_Overview.xhtml__idIndexMarker658)

Open Container Initiative [237](#Containers_Overview.xhtml__idIndexMarker657)

OpenShift [236](#Containers_Overview.xhtml__idIndexMarker650), [237](#Containers_Overview.xhtml__idIndexMarker656)

OSI stack [131](#Firewall_Basics.xhtml__idIndexMarker326)

P

Paravirtualization [193](#Virtualization_Overview.xhtml__idIndexMarker550), [194](#Virtualization_Overview.xhtml__idIndexMarker556)

Partition

mounting [44](#Reclaim_Windows_Partition.xhtml__idIndexMarker066)

passwd [85](#User_Management.xhtml__idIndexMarker166)

PATH [82](#Shell_Overview.xhtml__idIndexMarker143)

Path Completion [80](#Shell_Overview.xhtml__idIndexMarker119)

PE [272](#Volume_Groups.xhtml__idIndexMarker785)

Physical Extent [272](#Volume_Groups.xhtml__idIndexMarker784)

Physical Volume [272](#Volume_Groups.xhtml__idIndexMarker780)

Pipes [81](#Shell_Overview.xhtml__idIndexMarker130)

podman [237](#Containers_Overview.xhtml__idIndexMarker653)

attach [242](#Ubuntu_Container_Tutorial.xhtml__idIndexMarker677)

exec [241](#Ubuntu_Container_Tutorial.xhtml__idIndexMarker675)

list images [240](#Ubuntu_Container_Tutorial.xhtml__idIndexMarker673)

pause [243](#Ubuntu_Container_Tutorial.xhtml__idIndexMarker681)

ps -a [242](#Ubuntu_Container_Tutorial.xhtml__idIndexMarker676)

rm [243](#Ubuntu_Container_Tutorial.xhtml__idIndexMarker688)

start [242](#Ubuntu_Container_Tutorial.xhtml__idIndexMarker679)

unpause [243](#Ubuntu_Container_Tutorial.xhtml__idIndexMarker680)

POP3 [131](#Firewall_Basics.xhtml__idIndexMarker322)

Port Forwarding [149](#Ubuntu_Firewall_Configuration.xhtml__idIndexMarker400), [246](#Web_Server.xhtml__idIndexMarker699)

Ports

securing [127](#Firewall_Basics.xhtml__idIndexMarker292)

Postfix [255](#Postfix_Setup.xhtml__idIndexMarker724), [256](#Postfix_Setup.xhtml__idIndexMarker739)

configuring [257](#Postfix_Setup.xhtml__idIndexMarker744)

installing [257](#Postfix_Setup.xhtml__idIndexMarker743)

main.cf [257](#Postfix_Setup.xhtml__idIndexMarker745)

postmap [261](#Postfix_Setup.xhtml__idIndexMarker756)

sasl_passwd [260](#Postfix_Setup.xhtml__idIndexMarker754)

starting [259](#Postfix_Setup.xhtml__idIndexMarker750)

testing [259](#Postfix_Setup.xhtml__idIndexMarker751)

postmap [261](#Postfix_Setup.xhtml__idIndexMarker757)

Post Office Protocol [131](#Firewall_Basics.xhtml__idIndexMarker323)

poweroff.target [93](#Systemd_Targets_and_States.xhtml__idIndexMarker185)

PowerShell [157](#SSH_Authentication.xhtml__idIndexMarker429)

Preboot Execution Environment [10](#Ubuntu_Installation_Clean_Disk.xhtml__idIndexMarker042)

private key [153](#SSH_Authentication.xhtml__idIndexMarker410)

ps [81](#Shell_Overview.xhtml__idIndexMarker133), [283](#System_and_Process_Monitoring.xhtml__idIndexMarker826)

-a flag [283](#System_and_Process_Monitoring.xhtml__idIndexMarker827)

-aux flags [284](#System_and_Process_Monitoring.xhtml__idIndexMarker833)

-H flag [285](#System_and_Process_Monitoring.xhtml__idIndexMarker835)

TERM signal [284](#System_and_Process_Monitoring.xhtml__idIndexMarker830)

-u flag [283](#System_and_Process_Monitoring.xhtml__idIndexMarker828)

public key [153](#SSH_Authentication.xhtml__idIndexMarker409)

public key encryption [153](#SSH_Authentication.xhtml__idIndexMarker406)

PuTTY [159](#SSH_Authentication.xhtml__idIndexMarker434)

X11 Forwarding [172](#X11_Forwarding.xhtml__idIndexMarker471)

PuTTYgen [159](#SSH_Authentication.xhtml__idIndexMarker435)

PuTTY Key Generator [159](#SSH_Authentication.xhtml__idIndexMarker436)

PV [272](#Volume_Groups.xhtml__idIndexMarker781)

pvcreate [275](#Volume_Groups.xhtml__idIndexMarker794)

pvdisplay [274](#Volume_Groups.xhtml__idIndexMarker792)

pwd [78](#Shell_Overview.xhtml__idIndexMarker107)

PXE [10](#Ubuntu_Installation_Clean_Disk.xhtml__idIndexMarker043), [210](#KVM_virt-manager.xhtml__idIndexMarker605)

Q

QEMU [210](#KVM_virt-manager.xhtml__idIndexMarker603)

QEMU/KVM Hypervisor [199](#KVM_Installation.xhtml__idIndexMarker586)

Qmail [256](#Postfix_Setup.xhtml__idIndexMarker740)

R

reboot.target [94](#Systemd_Targets_and_States.xhtml__idIndexMarker189)

Red Hat, Inc. [7](#Red_Hat_History.xhtml__idIndexMarker012)

Remmina Desktop Client [165](#Ubuntu_Remote_Desktop_Access.xhtml__idIndexMarker443)

Remote Desktop Access [163](#Ubuntu_Remote_Desktop_Access.xhtml__idIndexMarker437), [164](#Ubuntu_Remote_Desktop_Access.xhtml__idIndexMarker439)

enabling [164](#Ubuntu_Remote_Desktop_Access.xhtml__idIndexMarker442)

secure vs. insecure [163](#Ubuntu_Remote_Desktop_Access.xhtml__idIndexMarker438)

Repositories [101](#Ubuntu_Package_Management.xhtml__idIndexMarker205)

disabling [102](#Ubuntu_Package_Management.xhtml__idIndexMarker219)

main [101](#Ubuntu_Package_Management.xhtml__idIndexMarker209)

managing [102](#Ubuntu_Package_Management.xhtml__idIndexMarker220)

multiverse [102](#Ubuntu_Package_Management.xhtml__idIndexMarker214)

restricted [101](#Ubuntu_Package_Management.xhtml__idIndexMarker211)

sources list [102](#Ubuntu_Package_Management.xhtml__idIndexMarker215)

universe [101](#Ubuntu_Package_Management.xhtml__idIndexMarker213)

rescue.target [93](#Systemd_Targets_and_States.xhtml__idIndexMarker186)

resize2fs [276](#Volume_Groups.xhtml__idIndexMarker806)

RFC 3339 [114](#Snap_Package_Management.xhtml__idIndexMarker254)

Richard Stallman [8](#Red_Hat_History.xhtml__idIndexMarker025)

rlogin [130](#Firewall_Basics.xhtml__idIndexMarker310)

root user [1](#Introduction.xhtml__idIndexMarker001)

rsh [130](#Firewall_Basics.xhtml__idIndexMarker309)

runc [237](#Containers_Overview.xhtml__idIndexMarker655)

S

Samba [175](#NFS_File_Sharing.xhtml__idIndexMarker472), [182](#Samba_File_Sharing.xhtml__idIndexMarker490)

add user [184](#Samba_File_Sharing.xhtml__idIndexMarker519)

firewall settings [182](#Samba_File_Sharing.xhtml__idIndexMarker493)

installing [182](#Samba_File_Sharing.xhtml__idIndexMarker492)

NetBIOS [185](#Samba_File_Sharing.xhtml__idIndexMarker526)

smbclient [185](#Samba_File_Sharing.xhtml__idIndexMarker530), [188](#Samba_File_Sharing.xhtml__idIndexMarker532)

smb.conf [182](#Samba_File_Sharing.xhtml__idIndexMarker495)

smbpasswd [184](#Samba_File_Sharing.xhtml__idIndexMarker520)

testparm [185](#Samba_File_Sharing.xhtml__idIndexMarker525)

Samba Client [182](#Samba_File_Sharing.xhtml__idIndexMarker491)

sasl_passwd [260](#Postfix_Setup.xhtml__idIndexMarker755)

SATA [263](#Adding_New_DIsk.xhtml__idIndexMarker760)

Secure File Transfer Protocol [129](#Firewall_Basics.xhtml__idIndexMarker303)

Secure Shell [130](#Firewall_Basics.xhtml__idIndexMarker308), [153](#SSH_Authentication.xhtml__idIndexMarker404)

Secure Socket Layer [250](#Web_Server.xhtml__idIndexMarker708)

Secure Sockets Layer [132](#Firewall_Basics.xhtml__idIndexMarker336)

Sendmail [255](#Postfix_Setup.xhtml__idIndexMarker731), [256](#Postfix_Setup.xhtml__idIndexMarker741)

Server Message Block [181](#Samba_File_Sharing.xhtml__idIndexMarker488)

Services

securing [127](#Firewall_Basics.xhtml__idIndexMarker293)

setfacl [203](#KVM_Create_VM.xhtml__idIndexMarker595)

Settings App [89](#User_Management.xhtml__idIndexMarker180)

users [89](#User_Management.xhtml__idIndexMarker179)

SFTP [129](#Firewall_Basics.xhtml__idIndexMarker304)

sh [84](#Shell_Overview.xhtml__idIndexMarker160)

Shell Scripts [83](#Shell_Overview.xhtml__idIndexMarker152)

Simple Mail Transfer Protocol [130](#Firewall_Basics.xhtml__idIndexMarker313)

Simple Mail Transport Protocol [256](#Postfix_Setup.xhtml__idIndexMarker737)

Simple Network Management Protocol [132](#Firewall_Basics.xhtml__idIndexMarker333)

skopeo [237](#Containers_Overview.xhtml__idIndexMarker654), [239](#Ubuntu_Container_Tutorial.xhtml__idIndexMarker672)

get image info [239](#Ubuntu_Container_Tutorial.xhtml__idIndexMarker670)

SMB [181](#Samba_File_Sharing.xhtml__idIndexMarker489)

smbclient [185](#Samba_File_Sharing.xhtml__idIndexMarker531), [188](#Samba_File_Sharing.xhtml__idIndexMarker533)

smb.conf [182](#Samba_File_Sharing.xhtml__idIndexMarker496)

testing [184](#Samba_File_Sharing.xhtml__idIndexMarker524)

testparm [184](#Samba_File_Sharing.xhtml__idIndexMarker523)

smbpasswd [184](#Samba_File_Sharing.xhtml__idIndexMarker521)

SMTP [127](#Firewall_Basics.xhtml__idIndexMarker291), [130](#Firewall_Basics.xhtml__idIndexMarker312), [256](#Postfix_Setup.xhtml__idIndexMarker736)

SMTP Relay [256](#Postfix_Setup.xhtml__idIndexMarker738), [260](#Postfix_Setup.xhtml__idIndexMarker753)

snap

channels [112](#Snap_Package_Management.xhtml__idIndexMarker245)

commands [110](#Snap_Package_Management.xhtml__idIndexMarker239)

disable [115](#Snap_Package_Management.xhtml__idIndexMarker256)

enable [115](#Snap_Package_Management.xhtml__idIndexMarker257)

find [110](#Snap_Package_Management.xhtml__idIndexMarker240)

info [110](#Snap_Package_Management.xhtml__idIndexMarker241), [113](#Snap_Package_Management.xhtml__idIndexMarker247)

install [112](#Snap_Package_Management.xhtml__idIndexMarker243)

list [111](#Snap_Package_Management.xhtml__idIndexMarker242)

logs [115](#Snap_Package_Management.xhtml__idIndexMarker260)

overview [109](#Snap_Package_Management.xhtml__idIndexMarker237)

packages [109](#Snap_Package_Management.xhtml__idIndexMarker238)

refresh [113](#Snap_Package_Management.xhtml__idIndexMarker248)

refresh.hold [113](#Snap_Package_Management.xhtml__idIndexMarker251)

refresh.metered [113](#Snap_Package_Management.xhtml__idIndexMarker250)

refresh.retain [113](#Snap_Package_Management.xhtml__idIndexMarker249)

refresh.timer [113](#Snap_Package_Management.xhtml__idIndexMarker252)

remove [112](#Snap_Package_Management.xhtml__idIndexMarker244)

services [115](#Snap_Package_Management.xhtml__idIndexMarker255)

set system [114](#Snap_Package_Management.xhtml__idIndexMarker253)

start [115](#Snap_Package_Management.xhtml__idIndexMarker259)

stop [115](#Snap_Package_Management.xhtml__idIndexMarker258)

switch [112](#Snap_Package_Management.xhtml__idIndexMarker246)

SNMP [132](#Firewall_Basics.xhtml__idIndexMarker332)

sockets.target [94](#Systemd_Targets_and_States.xhtml__idIndexMarker191)

Solaris [7](#Red_Hat_History.xhtml__idIndexMarker020)

sources.list file [102](#Ubuntu_Package_Management.xhtml__idIndexMarker217)

spawning [285](#System_and_Process_Monitoring.xhtml__idIndexMarker834)

ssh

-C flag [171](#X11_Forwarding.xhtml__idIndexMarker468)

X11 Forwarding [170](#X11_Forwarding.xhtml__idIndexMarker459)

-X flag [170](#X11_Forwarding.xhtml__idIndexMarker460)

SSH [127](#Firewall_Basics.xhtml__idIndexMarker290), [130](#Firewall_Basics.xhtml__idIndexMarker307), [153](#SSH_Authentication.xhtml__idIndexMarker405)

Microsoft Windows [157](#SSH_Authentication.xhtml__idIndexMarker426)

Multiple Keys [156](#SSH_Authentication.xhtml__idIndexMarker425)

ssh client [155](#SSH_Authentication.xhtml__idIndexMarker419)

ssh-copy-id [155](#SSH_Authentication.xhtml__idIndexMarker418), [158](#SSH_Authentication.xhtml__idIndexMarker432)

sshd_config.d [170](#X11_Forwarding.xhtml__idIndexMarker457)

sshd_config.d directory [156](#SSH_Authentication.xhtml__idIndexMarker423)

sshd_config file [156](#SSH_Authentication.xhtml__idIndexMarker422)

sshd service [156](#SSH_Authentication.xhtml__idIndexMarker424)

ssh-keygen [154](#SSH_Authentication.xhtml__idIndexMarker417)

SSH Service

installing [154](#SSH_Authentication.xhtml__idIndexMarker411)

starting [154](#SSH_Authentication.xhtml__idIndexMarker412)

SSL [132](#Firewall_Basics.xhtml__idIndexMarker337), [250](#Web_Server.xhtml__idIndexMarker709)

SSL certificate [250](#Web_Server.xhtml__idIndexMarker714)

SSL Labs [252](#Web_Server.xhtml__idIndexMarker723)

stderr [81](#Shell_Overview.xhtml__idIndexMarker128)

stdin [80](#Shell_Overview.xhtml__idIndexMarker125)

stdout [80](#Shell_Overview.xhtml__idIndexMarker123)

storage devices

identify [11](#Ubuntu_Installation_Clean_Disk.xhtml__idIndexMarker046)

Storage Pools [205](#KVM_Create_VM.xhtml__idIndexMarker600)

Storage Volumes [205](#KVM_Create_VM.xhtml__idIndexMarker599)

su - command [1](#Introduction.xhtml__idIndexMarker002)

sudo [2](#Introduction.xhtml__idIndexMarker003)

wheel group [86](#User_Management.xhtml__idIndexMarker172)

SunOS [7](#Red_Hat_History.xhtml__idIndexMarker019)

Superuser [1](#Introduction.xhtml__idIndexMarker000)

swapoff [279](#Ubuntu_Swap_Space.xhtml__idIndexMarker816)

swapoff u [281](#Ubuntu_Swap_Space.xhtml__idIndexMarker822)

swapon [278](#Ubuntu_Swap_Space.xhtml__idIndexMarker811), [282](#Ubuntu_Swap_Space.xhtml__idIndexMarker823)

swap space

add partition [279](#Ubuntu_Swap_Space.xhtml__idIndexMarker817)

add swap file [278](#Ubuntu_Swap_Space.xhtml__idIndexMarker813)

add to volume group [281](#Ubuntu_Swap_Space.xhtml__idIndexMarker821)

current usage [278](#Ubuntu_Swap_Space.xhtml__idIndexMarker809)

extend logical swap volume [279](#Ubuntu_Swap_Space.xhtml__idIndexMarker819)

recommended [277](#Ubuntu_Swap_Space.xhtml__idIndexMarker807)

system

units [96](#Systemd_Targets_and_States.xhtml__idIndexMarker197)

unit types [96](#Systemd_Targets_and_States.xhtml__idIndexMarker196)

systemctl [95](#Systemd_Targets_and_States.xhtml__idIndexMarker194)

systemd [93](#Systemd_Targets_and_States.xhtml__idIndexMarker182)

services [93](#Systemd_Targets_and_States.xhtml__idIndexMarker183)

targets [93](#Systemd_Targets_and_States.xhtml__idIndexMarker181)

System Monitor [285](#System_and_Process_Monitoring.xhtml__idIndexMarker836)

system processes [283](#System_and_Process_Monitoring.xhtml__idIndexMarker824)

T

TCP/IP [127](#Firewall_Basics.xhtml__idIndexMarker287)

Well-Known Ports [129](#Firewall_Basics.xhtml__idIndexMarker298)

Telnet [130](#Firewall_Basics.xhtml__idIndexMarker311)

Terminal window [2](#Introduction.xhtml__idIndexMarker004)

TERM signal [284](#System_and_Process_Monitoring.xhtml__idIndexMarker831)

testparm

smb.conf [184](#Samba_File_Sharing.xhtml__idIndexMarker522)

TFTP [130](#Firewall_Basics.xhtml__idIndexMarker318)

TLS [250](#Web_Server.xhtml__idIndexMarker711)

top [287](#System_and_Process_Monitoring.xhtml__idIndexMarker838)

-u flag [288](#System_and_Process_Monitoring.xhtml__idIndexMarker839)

Transport Layer Security [250](#Web_Server.xhtml__idIndexMarker710)

Trivial File Transfer Protocol [130](#Firewall_Basics.xhtml__idIndexMarker319)

Trusted X11 Forwarding [171](#X11_Forwarding.xhtml__idIndexMarker464)

Type-1 hypervisors [193](#Virtualization_Overview.xhtml__idIndexMarker549)

Type-2 hypervisors [193](#Virtualization_Overview.xhtml__idIndexMarker548)

U

Ubuntu

history of [8](#Red_Hat_History.xhtml__idIndexMarker029)

meaning [8](#Red_Hat_History.xhtml__idIndexMarker034)

UDP [129](#Firewall_Basics.xhtml__idIndexMarker302)

ufw [133](#Ubuntu_ufw_Firewall.xhtml__idIndexMarker344), [139](#Ubuntu_ufw_Firewall.xhtml__idIndexMarker356)

command-line options [139](#Ubuntu_ufw_Firewall.xhtml__idIndexMarker360)

disabling [139](#Ubuntu_ufw_Firewall.xhtml__idIndexMarker358)

enabling [139](#Ubuntu_ufw_Firewall.xhtml__idIndexMarker357)

logging [141](#Ubuntu_ufw_Firewall.xhtml__idIndexMarker361)

reload [141](#Ubuntu_ufw_Firewall.xhtml__idIndexMarker362)

resetting [141](#Ubuntu_ufw_Firewall.xhtml__idIndexMarker363)

status [139](#Ubuntu_ufw_Firewall.xhtml__idIndexMarker359)

umount [11](#Ubuntu_Installation_Clean_Disk.xhtml__idIndexMarker049), [177](#NFS_File_Sharing.xhtml__idIndexMarker482)

Uncomplicated Firewall [133](#Ubuntu_ufw_Firewall.xhtml__idIndexMarker340)

UNIX [7](#Red_Hat_History.xhtml__idIndexMarker014), [77](#Shell_Overview.xhtml__idIndexMarker095)

origins of [7](#Red_Hat_History.xhtml__idIndexMarker013)

update-manager [102](#Ubuntu_Package_Management.xhtml__idIndexMarker221)

Updates [105](#Ubuntu_Package_Management.xhtml__idIndexMarker231)

automatic [106](#Ubuntu_Package_Management.xhtml__idIndexMarker233)

USB drive

device name [11](#Ubuntu_Installation_Clean_Disk.xhtml__idIndexMarker045)

userdel [85](#User_Management.xhtml__idIndexMarker167)

usermod [86](#User_Management.xhtml__idIndexMarker169)

user processes [283](#System_and_Process_Monitoring.xhtml__idIndexMarker825)

Users and Groups [85](#User_Management.xhtml__idIndexMarker163)

V

VcXsrv [171](#X11_Forwarding.xhtml__idIndexMarker469)

VG [271](#Volume_Groups.xhtml__idIndexMarker779)

vgdisplay [272](#Volume_Groups.xhtml__idIndexMarker789)

vgextend [275](#Volume_Groups.xhtml__idIndexMarker796)

vgs [273](#Volume_Groups.xhtml__idIndexMarker790)

Vino [164](#Ubuntu_Remote_Desktop_Access.xhtml__idIndexMarker440)

installing [164](#Ubuntu_Remote_Desktop_Access.xhtml__idIndexMarker441)

virbr0 [221](#KVM_Network_Bridge.xhtml__idIndexMarker617), [222](#KVM_Network_Bridge.xhtml__idIndexMarker618)

virsh [217](#KVM_Create_VM_Command-line.xhtml__idIndexMarker609), [219](#KVM_Create_VM_Command-line.xhtml__idIndexMarker611), [224](#KVM_Network_Bridge.xhtml__idIndexMarker621), [231](#KVM_virsh_Management.xhtml__idIndexMarker627)

destroy [219](#KVM_Create_VM_Command-line.xhtml__idIndexMarker614), [233](#KVM_virsh_Management.xhtml__idIndexMarker633)

dumpxml [219](#KVM_Create_VM_Command-line.xhtml__idIndexMarker615)

edit [226](#KVM_Network_Bridge.xhtml__idIndexMarker625)

help [232](#KVM_virsh_Management.xhtml__idIndexMarker629)

list [232](#KVM_virsh_Management.xhtml__idIndexMarker630)

reboot [234](#KVM_virsh_Management.xhtml__idIndexMarker638)

restore [233](#KVM_virsh_Management.xhtml__idIndexMarker637)

resume [233](#KVM_virsh_Management.xhtml__idIndexMarker634)

save [233](#KVM_virsh_Management.xhtml__idIndexMarker636)

setmem [234](#KVM_virsh_Management.xhtml__idIndexMarker640)

setmemmax [234](#KVM_virsh_Management.xhtml__idIndexMarker639)

shell [231](#KVM_virsh_Management.xhtml__idIndexMarker628)

shutdown [219](#KVM_Create_VM_Command-line.xhtml__idIndexMarker613), [233](#KVM_virsh_Management.xhtml__idIndexMarker632)

start [219](#KVM_Create_VM_Command-line.xhtml__idIndexMarker612), [233](#KVM_virsh_Management.xhtml__idIndexMarker631)

suspend [233](#KVM_virsh_Management.xhtml__idIndexMarker635)

virt-install [201](#KVM_Create_VM.xhtml__idIndexMarker587), [217](#KVM_Create_VM_Command-line.xhtml__idIndexMarker608), [225](#KVM_Network_Bridge.xhtml__idIndexMarker622)

virt-manager [198](#KVM_Installation.xhtml__idIndexMarker580), [209](#KVM_virt-manager.xhtml__idIndexMarker601), [225](#KVM_Network_Bridge.xhtml__idIndexMarker624)

installation [198](#KVM_Installation.xhtml__idIndexMarker577)

New VM wizard [210](#KVM_virt-manager.xhtml__idIndexMarker604)

storage pools [212](#KVM_virt-manager.xhtml__idIndexMarker607)

VirtualBox [197](#KVM_Installation.xhtml__idIndexMarker571)

Virtualization [191](#Virtualization_Overview.xhtml__idIndexMarker537)

AMD-V [194](#Virtualization_Overview.xhtml__idIndexMarker560)

full [194](#Virtualization_Overview.xhtml__idIndexMarker554)

guest [191](#Virtualization_Overview.xhtml__idIndexMarker536)

hardware [194](#Virtualization_Overview.xhtml__idIndexMarker557)

hypercalls [193](#Virtualization_Overview.xhtml__idIndexMarker552)

hypervisor [192](#Virtualization_Overview.xhtml__idIndexMarker539)

Intel VT [194](#Virtualization_Overview.xhtml__idIndexMarker559)

KVM virtualization [195](#Virtualization_Overview.xhtml__idIndexMarker566)

MacVTap [195](#Virtualization_Overview.xhtml__idIndexMarker568)

Type-1 [192](#Virtualization_Overview.xhtml__idIndexMarker542)

Type-2 [192](#Virtualization_Overview.xhtml__idIndexMarker541)

virt-manager [198](#KVM_Installation.xhtml__idIndexMarker578)

Virtual Machine Networking [195](#Virtualization_Overview.xhtml__idIndexMarker563)

virt-viewer [204](#KVM_Create_VM.xhtml__idIndexMarker598), [217](#KVM_Create_VM_Command-line.xhtml__idIndexMarker610)

vmdk [211](#KVM_virt-manager.xhtml__idIndexMarker606)

VMware [197](#KVM_Installation.xhtml__idIndexMarker570)

Volume Group [271](#Volume_Groups.xhtml__idIndexMarker778)

W

Wayland [169](#X11_Forwarding.xhtml__idIndexMarker452)

WaylandEnable [170](#X11_Forwarding.xhtml__idIndexMarker454)

wc [81](#Shell_Overview.xhtml__idIndexMarker134)

Web Server [245](#Web_Server.xhtml__idIndexMarker689)

testing [247](#Web_Server.xhtml__idIndexMarker700)

Well-Known Ports [129](#Firewall_Basics.xhtml__idIndexMarker299)

wheel group [86](#User_Management.xhtml__idIndexMarker173)

which [78](#Shell_Overview.xhtml__idIndexMarker104)

Whitfield Diffie [153](#SSH_Authentication.xhtml__idIndexMarker407)

wildcard character [80](#Shell_Overview.xhtml__idIndexMarker116)

wildcards [80](#Shell_Overview.xhtml__idIndexMarker115)

Windows partition

filesystem access [36](#Ubuntu_Installation_Dual_Boot.xhtml__idIndexMarker056)

reclaiming [41](#Reclaim_Windows_Partition.xhtml__idIndexMarker060)

unmounting [41](#Reclaim_Windows_Partition.xhtml__idIndexMarker061)

Windows PowerShell [157](#SSH_Authentication.xhtml__idIndexMarker428)

wipefs [275](#Volume_Groups.xhtml__idIndexMarker795)

X

X11 Forwarding [169](#X11_Forwarding.xhtml__idIndexMarker449)

compressed [171](#X11_Forwarding.xhtml__idIndexMarker466)

X11Forwarding [170](#X11_Forwarding.xhtml__idIndexMarker458)

x86 family [193](#Virtualization_Overview.xhtml__idIndexMarker547)

Xen [198](#KVM_Installation.xhtml__idIndexMarker576)

XFS file system [265](#Adding_New_DIsk.xhtml__idIndexMarker766)

XFS filesystem [276](#Volume_Groups.xhtml__idIndexMarker800)

xfs_growfs [276](#Volume_Groups.xhtml__idIndexMarker801)

XLaunch [171](#X11_Forwarding.xhtml__idIndexMarker470)

X.org [169](#X11_Forwarding.xhtml__idIndexMarker451)

X Window System [169](#X11_Forwarding.xhtml__idIndexMarker450)