![](Images/cover00429.jpeg)

Express Guide

Oracle LINUX 8

Shiv Kumar Goyal

Preface

Let us starts journey with Oracle Linux. This book covers installation, file system structure, network, LVM, Repository Structure, NTP, Log management and many other aspects of Oracle Linux. The structure of the book is very simple and easy to follow.

Thanks

Shiv Kumar Goyal

Contents

[Introduction](#part0007.xhtml__Toc103419597)

[Support Life Cycle of oracle Linux](#part0008.xhtml__Toc103419598)

[Installation Media Preparation](#part0010.xhtml__Toc103419599)

[Installation Steps](#part0011.xhtml__Toc103419600)

[Exploring the Desktop Components](#part0015.xhtml__Toc103419601)

[Exploring Command line](#part0016.xhtml__Toc103419602)

[Exploring File System](#part0019.xhtml__Toc103419603)

[Networking](#part0021.xhtml__Toc103419604)

[Local file systems](#part0026.xhtml__Toc103419605)

[Exploring Network File Systems](#part0029.xhtml__Toc103419606)

[Disk Partitions](#part0031.xhtml__Toc103419607)

[Management of local file system](#part0034.xhtml__Toc103419608)

[Logical Volume Management](#part0036.xhtml__Toc103419609)

[Software Management](#part0039.xhtml__Toc103419610)

[Software Repositories](#part0047.xhtml__Toc103419611)

[Service Management System](#part0052.xhtml__Toc103419612)

[Users and Groups](#part0055.xhtml__Toc103419613)

[Exploring SU and SUDO](#part0059.xhtml__Toc103419614)

[Exploring File and Directory Permissions](#part0061.xhtml__Toc103419615)

[Network Time Protocol](#part0067.xhtml__Toc103419616)

[Exploring Secure Shell - SSH](#part0067.xhtml__Toc103419617)

[Secure System with Firewall](#part0068.xhtml__Toc103419618)

[Exploring Cockpit](#part0070.xhtml__Toc103419619)

[Logs management](#part0071.xhtml__Toc103419620)

[Understanding Processes](#part0072.xhtml__Toc103419621)

[Monitoring Your System](#part0075.xhtml__Toc103419622)

[Automating your System](#part0080.xhtml__Toc103419623)

[Resetting forgotten root password](#part0081.xhtml__Toc103419624)

Chapter 1  

# Introduction

Linux is an open source project started by Linus Torvalds in 1991\. It is Unix like operating system. There are thousands of Linux distributions in the market, broadly classified on their root distribution for example CentOS, Oracle and Scientific Linux are based on Red hat which in further based on Fedora Linux. Fedora Linux is community project sponsored by Red Hat.

Free V/s Paid

Linux although is open source project but there are two types of Linux distribution available in the market, one is free and other one is paid. Free is self-explanatory you do not have to pay anything. In case of any problem, you can take help from volunteers working for Linux community. However, this type of support is not time bond. So companies who uses mission critical Linux servers and desktop computers prefers paid type of Linux distributions where they pay fixed amount as subscription and support fee. These paid Linux distribution companies keeps teams of Linux experts to provide support and fixes. 

Oracle Linux follow middle path, it is free to use and update but support is paid. Oracle Linux distribution is derived from source code of RedHat. Oracle Linux is functionally and binary compatible with Red hat enterprise Linux. Oracle Linux generally removes Red hat’s branding and artwork. After merger of Redhat with IBM, Centos linux which was free alternative of Redhat is no more available. Only product available from Centos is Centos stream which is rolling release. The customers that use to prefer Centos as free alternative of Redhat Linux now reluctant to use Centos in production environment. Oracle provides simple script to migrate your current Centos environment to Oracle Linux.

Platform supported.

Oracle Linux Version 8 installation images are available for following platforms:-

| Image | Platform Supported |
| x86_64 | Intel and AMD  64 Bit |
| aarch64 | ARM 64 Bit |

Types of images

Standard installation image is in the form of ISO image only, however, you can also get Cloud image, Container image and Vagrant image.

Chapter 2  

# Support Life Cycle of oracle Linux

As mentioned earlier you can opt for support of Oracle Linux if you are using the Oracle Linux in mission critical system, the life cycle of Oracle Linux support is following

| Releases | General Availability | Premier Support Ends | ExtendedSupport Ends | Sustaining Support Ends |
| Linux 3 | Oct 2003 | Oct 2011 | Not Available | Indefinite |
| Linux 4 | Feb 2005 | Feb 2013 | Not Available | Indefinite |
| Linux 5 | Jun 2007 | Jun 2017 | Nov 2020 | Indefinite |
| Linux 6 | Feb 2011 | Mar 2021 | Jun 2024 | Indefinite |
| Linux 7 | Jul 2014 | Jul 2024 | Not Available | Indefinite |
| Linux 8 | Jul 2019 | Jul 2029 | Not Available | Indefinite |

Type of support

Oracle provides two types of paid support for Oracle Linux. The difference between the two type of support according to oracle site is bellow

| Feature | Basic Support | Premier Support |
| 24x7 telephone and online support | Yes | Yes |
| Access to enhancements, updates, and errata | Yes | Yes |
| Oracle Enterprise Manager for Linux Management | Yes | Yes |
| Spacewalk support | Yes | Yes |
| High availability with Oracle Clusterware | Yes | Yes |
| Comprehensive tracing with DTrace | Yes | Yes |
| Oracle Linux load balancer | Yes | Yes |
| Oracle Container runtime for Docker | Yes | Yes |
| Oracle Linux Virtualization Manager | No | Yes |
| Ksplice | No | Yes |
| Oracle Linux Automation Manager | No | Yes |
| Oracle Cloud Native Environment like Kubernetes | No | Yes |
| Gluster Storage | No | Yes |
| Access to Oracle Linux software collections | No | Yes |
| Corosync and Pacemaker support | No | Yes |
| Premier backports | No | Yes |
| Lifetime sustaining support | No | Yes |

Chapter 3  

# Installation Media Preparation

Oracle Linux downloads are available in several forms:

| Format | Description |
| ISO images | Installation Media for x86_64 and Arm |
| Vagrant | For Vagrant Boxes |
| Container images | for x86_64 and Arm |
| GitHub Container Registry |  |
| Docker Hub | Docker images |
| Virtual machine templates | .ova format templates |
| Raspberry Pi 4 and Raspberry Pi 3 | for Arm |

In this book, we will cover only Intel platform installation. To download image of Oracle Linux follow these steps :-

1 Go to oracle site https://yum.oracle.com/oracle-linux-isos.html

2 ![](Images/image00331.jpeg)Select the version and platform in our case it is x86_64 under Full ISO

Verifying the download

Download the checksum file from bellow site

![](Images/image00332.jpeg)[https://linux.oracle.com/security/gpg/](https://linux.oracle.com/security/gpg/)

if you have downloaded the image on Microsoft windows machine. Open the powershell prompt and give following command :-

Syntax

get-filehash path for isofile

Example

![](Images/image00333.jpeg)PS C:\> get-filehash D:\Download\OracleLinux-R8-U4-x86_64-dvd.iso

Now open the checksum file and compare the output of the get-filehash command output.

Media preparation

To prepare USB media for installation on physical machine use following steps.

1.  Download Fedora live USB creator from the Fedora Linux site.

![](Images/image00334.jpeg)[https://getfedora.org/fmw/FedoraMediaWriter-win32-latest.exe](https://getfedora.org/fmw/FedoraMediaWriter-win32-latest.exe)

2.  Double click the downloaded file and follow the installation steps.
3.  ![](Images/image00335.jpeg)Select Custom Image

4.  Select the downloaded ISO file of Oracle Linux and press Open.

5.  ![](Images/image00336.jpeg)![](Images/image00337.jpeg)Select the USB device and press Write to Disk.
6.  Wait to finish and press Close.
7.  Unplug the USB from the windows system.

![](Images/image00338.jpeg) Now installation media is ready to use.

Chapter 4  

# Installation Steps

In this chapter, we will cover installation procedure. However, before proceeding for installation it is advisable to check the hardware compatibility of your server/ PC at Oracle Linux internet sites.

Oracle Linux in its release notes specify the minimum configuration for its installation but it recommended to have at least following configuration for optimal performance of the system

*   4 GB or more RAM.
*   Intel Core I3 or better processor.
*   60GB of Hard disk
*   16GB of USB disk for installation media

Note: it is possible to complete the installation with less resources depending upon your requirement and environment.

Installation Basics

Oracle Linux uses Anaconda installer for installation. Installation of Oracle Linux can be done in following ways:-

*   Quick install
*   Customized GUI install
*   Kickstart automated install

Partitioning

Oracle Linux supports three type of partitioned devices

*   Standard partition
*   LVM
*   LVM thin

Standard Partition

For boot, BIOS boot and EFI system partition only standard partition can be used.

LVM

LVM partition scheme allows flexibility and performance benefit. When you choose LVM partition during the installation, if no volume group currently exists on the system, the installation creates one automatically.

LVM thin

LVM thin uses storage pool which allows thin provisioning of the storage.

File system Supported

*   XFS
*   ext4, ext3, ext2
*   swap
*   BIOS boot
*   EFI system partition

XFS

XFS is a high performance file system that supports up to 500 TB of single file system. It is the default file system for Oracle Linux 8.

Ext3 and Ext4

Ext3 and Ext4 are known as Journal file systems. Journaling keep track of changes not yet committed to the file system which allows easy file system recovery in case of abrupt system power off. 

EXT2 is the standard file system used in the older versions of Linux.

Swap

It is a virtual memory present on hard disk. When system does not have enough RAM to operate, then it transfers some portion of the memory data in to swap space.

BIOS boot

Partition required for GPT.

EFI

Boot device for GPT on UEFI system.

Recommended partition scheme

| Partition | Details |
| /boot | 1 GB and no LVM. |
| / | root partition recommended size 10GB. |
| /home | 2GB minimum (optional) |
| /swap | Equal to more than RAM in some cases it should be double of system memory. |

Booting your machine

To start installation process of Oracle Linux you have to boot your system with installation media.

For virtual machine like VM in VMware infrastructure, you can use ISO image directly. Just attach the ISO image and boot the machine.

For physical server, plug in the Oracle Linux USB installation media created earlier.

Switch on the server and press key to change boot order to use USB as boot device (refer the hardware manual of the machine for boot manger key like F11 for some dell servers).

Installation Procedure

1.  ![](Images/image00339.jpeg)From the boot menu, select Install Oracle Linux 8 and press the ENTER key.
2.  ![](Images/image00340.jpeg)Select your language and location. Click Continue.
3.  Next screen is installation summary, which shows all installation options with default values. 
4.  ![](Images/image00341.jpeg)![](Images/image00342.jpeg)From the installation summary screen select Time & Date. Click your current location on the map.

The system will change the date, time and time zone accordingly. Change date, time format from 24 hours to AM/PM, if required. Press Done.

5.  ![](Images/image00343.jpeg)Select Installation Destination. From the Local Standard Disks pane, select the target disk. Click Done to use the default setting for Automatic partitioning.

Note: if you have specific file system requirement you can select Custom option.

6.  On network configuration screen. Change the Host Name to fully qualified host name and press Apply.
7.  Press Configure.

8.  ![](Images/image00344.jpeg)![](Images/image00345.jpeg)Make sure that the Connect automatically with priority is selected.
9.  Select IPV4 Settings tab to configure static IP address.

10.  On the IPV4 Tab change following: -

1 Change Method to Manual from drop down menu.

2 Press Add button.

3 Provide IP address

4 Provide Net mask

5 Provide gateway.

6 Add DNS

7 ![](Images/image00346.jpeg)Press Save.

11.  Click Done to accept the changes.
12.  ![](Images/image00347.jpeg)On the Installation Summary screen press Root Password.
13.  Set root password and press Done.
14.  Select User Creation on Installation Summary window.
15.  ![](Images/image00348.jpeg)On the Create User screen, provide Full name, user name and password for new user. Select Make user administrator if you want this user to be administrator.    

![](Images/image00349.jpeg)

16.  Press Begin Installation on Installation summary window. It will start installation process.
17.  ![](Images/image00350.jpeg)On Completion of installation process press Reboot System.

18.  ![](Images/image00351.jpeg)After reboot, on Initial Setup Screen press Licence Information.
19.  ![](Images/image00352.jpeg)On the Licence information screen, select I accept licence agreement. Press Done. 
20.  ![](Images/image00353.jpeg)Press Finish installation.

21.  On the Login screen, select Not listed.
22.  ![](Images/image00354.jpeg)![](Images/image00355.jpeg)Write root and press Next.
23.  Provide password for root user. The same password you selected at the time of installation. Press Sign In. ![](Images/image00356.jpeg)

24.  On the Welcome screen press Next.

![](Images/image00357.jpeg)

25.  On the Typing Screen, press Next.
26.  On Privacy Screen, press Next.
27.  ![](Images/image00358.jpeg)Press Skip on Online Account screen
28.  Press Start using Oracle Linux server
29.  Press X Button to close the help screen.

This concludes our Oracle Linux 8 installation.

Chapter 5  

# ![](Images/image00359.jpeg)Exploring the Desktop Components

On Server with GUI, GNOME is the default desktop. GNOME provide easy to use GUI experience. In this chapter we will explore desktop interfaces.

TOP BAR

The top bar has four main sections.

![](Images/image00360.jpeg) 

*   Activities
*   Application menu
*   Clock
*   System Menu

![](Images/image00361.jpeg)System Menu

Right corner of the bar has power, speaker network, battery and Bluetooth icons. Click any of these icons to open System menu. System menu allows you to adjust speaker and microphone volume. This menu also give you option to adjust network and Bluetooth settings. You will find quick links for system settings, Lock screen and Shutdown Menu.

Clock

In the center of the bar, there is clock and by default, it shows day of the week and current time in 24-hour format. If you want, you can change the time format in the system settings. Click clock to open dialog box with calendar on the right side and any task notification on the left side.

![](Images/image00362.jpeg)

Activities

On the left side of the top bar is the Activities button. Click on this button to open overview screen. You can use Super key (also known as Windows key) on your keyboard to open Activities overview. Activities Screen provides following items

*   Search Bar.
*   ![](Images/image00363.jpeg)Windows Peak View.
*   Workspaces

Search Bar

One of the main item of Activities overview screen is search bar. With search bar you can search applications, documents, settings, calendar events etc. on your computer. For example, if you write calculator in the search bar it will show calculator application.

![](Images/image00364.jpeg)Click the icon to open the calculator application.

Windows Peak View

![](Images/image00365.jpeg)Second item of Activity overview is peek view of all running applications. Click the desired application window to switch application. To close any running application window, hover over the window and click X button.  

![](Images/image00366.jpeg)Workspaces

Left side of the Activities overview screen shows the list of workspaces. Workspaces are virtual desktops for better windows management. You can create multiple workspaces. Workspaces are meant to reduce mess on the single desktop and make the desktop easier to navigate.

Click on the workspace to switch workspace. To move the application to different workspace just drag the running application to new workspace.

Dash

![](Images/image00367.jpeg)![](Images/image00368.jpeg)On the left side of the desktop you will find the Dash bar. The Dash provides access to your favourite and running applications. Click the application icon on the dash bar to open the application. The small dot at the bottom of icon indicates running application. Click on any running application icon brings most recent window of the application.

Right click on the icon to open context menu. From this menu you can open new window or pick any window of a running application. You can also add or remove any application to favourites from this menu.

Grid

![](Images/image00369.jpeg)At the bottom of the dash bar there is grid icon. Click on this icon shows the list of all and frequently used applications. The icons are in grid format, from the bottom of the grid you can switch between all applications and frequently used applications. The list of applications can span multiple pages, to navigate to next page use scroll (centre) wheel of mouse or click the dots on the right side of the grid.

Some applications in the grid are contained in the application folder. Click application folder to list the grid of all containing applications.

![](Images/image00370.jpeg)

![](Images/image00371.jpeg)Application menu

Located beside the Activities button, application menu shows the name of the active application. Also provides other options specific to the active application. 

System settings

![](Images/image00372.jpeg)![](Images/image00373.jpeg)Click on system setting icon in the system menu will open settings windows for system and hardware. Setting screen has two panes, left pane shows the list of settings and right pane provides the description of the selected setting. You can scroll the list of settings with mouse’s scroll wheel. Suppose you want to change the background of your desktop. Click background in the left pane and select the wallpaper from the list of available wallpapers in the right pane.

Top bar of the system setting tool also houses search button. Search button offers you to search anything related to settings. Suppose you want to look for date and time settings, just press search button and write date. The system will show you list of items related to date in the left pane.

 ![](Images/image00374.jpeg)Log out

After finishing your task, it is good practice to logout from the system. The logout option closes all running application started by the user in the current session. To logout as current user press user name from the system menu. From the sub menu press Log Out. On the confirmation popup press logout again.

Lock screen

![](Images/image00375.jpeg)When you are away from your machine for short period of time it is recommended to lock your screen so that nobody can use your computer in your absence. When system screen is in lock state, all the running application will continue to run. To log back, provide your login password to unlock the screen. System also locks the screen automatically, if you leave your computer for a specific time period.

To lock the screen manually, click the system menu on the right side of the top bar, click Lock icon.

To unlock, press ENTER key on the locked screen and provide your password.

![](Images/image00376.jpeg)Power off or Restart

To shutdown or reboot the server through GUI, click the system menu on the right side of the top bar, click Power Off button. At the dialog box, press the button you want.

![](Images/image00377.jpeg)

Windows

Gnome uses windows to display your running applications. This is one of the ways to do multitasking. Whenever you launch any application, it opens in a new window. In this section, we will explore windows operations.

List windows

To show all the running windows just click Activities button. From the list of windows press left button of mouse to select any window.

Switch window

You can switch the window using keyboard, press Super key + TAB to open windows switcher. Hold Super key, release and press TAB key to cycle between open windows.  

![](Images/image00378.jpeg)Please note: Super key is an alternative name for the Windows key when using Linux.

Maximize and unmaximize a window

You can maximize a window to view its content on whole desktop and unmaximize or restore down a window to restore it to its normal size.

Maximize the Window

To maximize a window, press and hold left button of mouse at title bar of the window to grab the window title bar, now drag it to the top bar. Other way to maximize, is to double click left button of mouse on the title bar of window. To maximize a window using the keyboard press Alt + F10.

Unmaximize window

To restore a window to its normal size grab the window title bar and drag away from the top bar or just double click title bar of window.  Press Alt + F10 on the key board to unmaximize the windows using keyboard.

Tile Windows (Snap Windows)

![](Images/image00379.jpeg)To copy files or to compare content of two windows you can place two windows side-by-side. In Microsoft windows, this feature is known as windows Snap. To snap window to left side press Super + left Arrow and to snap window right side of screen select the window, press Super + right arrow key on the keyboard. To snap window using mouse, grab the title of window and drag it to the left or right side until half of the screen is highlighted.

Switch workspaces

![](Images/image00380.jpeg)Workspaces are virtual desktops. It is like having more than one monitors virtually on same desktop. If you are working on several applications at same time, workspace is good option to organize them. To move one application from current workspace to another workspace, press Activities to view the list of windows and workspaces. Grab the title of widow and move to new workspace from the list of workspaces on right side of screen.

To move to a workspace, Click Activities and select the workspace or press Super + Page Down and Super + Page Up on your keyboard.

Chapter 6  

# Exploring Command line

In the last chapter we have discussed Graphical user interface but Linux is known for command line. As command line provides more power and flexibility. A command line interface (CLI) is a text-based user interface (UI) used to manage Linux. In this chapter we will discuss various ways to access the command line interface. But before going ahead with command line we should know some basics of command line.

Bash

Bourne-Again Shell, bash is Linux shell that provides interface to the user to input commands and present output as its result. You have choice of multiple shells on the Linux like Korn, C shell and Z shell etc, but bash is the default shell available in the Oracle Linux. However, you can use other shells also if required.  Bash shell can be used in two ways, interactive and in the script also known as shell script.

Shell basics

When you enter any command on the terminal it has three parts

Command option argument

Example

cp -R /test/1anty.text /home/f1/.

Here cp is command

-R is option, there can be multiple options in the same command.

Rest is the argument. there can be multiple arguments depending on the command.

Virtual Consoles

Terminal is the device to input commands. Bash uses terminal to interact with user. Terminal term came from Unix display devices. Oracle Linux provides 6 virtual consoles with default installation. These terminals provide virtually independent shell environment while working on the server. Virtual console provides another way to access shell. You can change virtual terminal by pressing Alt + Ctrl + function keys on your keyboard. First terminal start at F1 key through F6 key on your keyboard. Suppose you want change to terminal 3 press Ctrl + Alt + F3 key.  If you have installed Server with GUI, then first two Virtual consoles will be graphical user interface available with Ctrl + Alt + F1 and Ctrl +Alt + F2 key rest of the four virtual consoles can be assessed using Ctrl + Alt keys up to f6. ![](Images/image00381.jpeg)

Gnome Terminal

Gnome terminal is a terminal emulator for GNOME Desktop environment. It provides terminal environment in the GUI environment.

Open GNOME terminal

Press Activities, write terminal in search bar and click on terminal icon

![](Images/image00382.jpeg)

Shortcuts

Following are some basic shortcuts which can be used on the bash shell.

| Keyboard Shortcut | Task |
| Ctrl +a | Moves the cursor to the beginning of the command prompt |
| Ctrl + e | Moves the  cursor to the end of the command prompt |
| Ctrl + u | Clear the current line |
| Middle mouse button click | Paste the highlighted text |
| Tab | Completes the command |
| Up / Down Keys | Show history of commands |
| Ctrl +c | Terminate the current process |
| Ctrl + z | Suspends the foreground process |
| Ctrl + d | Close terminal™ |

Commands

Let’s explore some basic and important command

Tab Completion

One of the main high light of the bash shell is the tab completion. When you press tab after partially written command system automatically completes the command. if more than one command is available with same string then it will show the list of commands. Not only commands it also completes the name of files.

Example

hostna<tab>

cat /etc/grou<tab>

history

To list the previously used command

Example

history

Count number of lines of line

wc -l

date

Print or change the system data and time.

Syntax

date

To check date

To set date

date -s "24 feb 2017 19:00"

echo

Print text on the terminal

Syntax

echo text

Example

echo hello

Accessing Terminal remotely

So far we accessed the terminal on the server locally normally servers are in the datacentres and you may have limited access to the server. Therefore, we usually access the Linux servers remotely. In this section will learn how to access the Linux terminal remotely on your Linux or Window PC.

To access the server remotely we require two pieces of software one on the server other on the client. The most common tools to access the Linux server remotely are :-

*   telnet
*   ssh

Telnet

Telnet is old software that transfers data in plain format, hence it is not safe to use. Due to safety concerns, telnet is not available by default on the server. If you have specific requirement you can still install it and use it.

Install telnet Server

yum install telnet-server

Start telnet server

systemctl start telnet.socket

Enable telnet server

systemctl enable telnet.socket

On the remote machine

Install telnet client

yum install telnet

Run client to connect

Syntax

telnet IP_address port

Example

telnet 192.168.0.1 8080

ssh

ssh is the modern software for accessing terminal remotely. It transfers data in the encrypted format therefore safe to use even on the less secure network. Ssh has two parts, sshd which is the server daemon that runs on the server and ssh client which runs on the client PC.

Check status of ssh server

systemctl status sshd  

Access terminal on Linux client

If you are using Ubuntu or oracle as Linux client PC you can access terminal with following procedure:-

Open Terminal on the Linux client.

On the command window.

ssh user@ip_address_of_the_server

Example

ssh root@192.168.100.47

Enter password for the user.

Access terminal on MS Windows

To access the terminal on windows machine you require a third party software known as putty. The putty is the free software. You can download the software from the putty site:-

1 Open site

https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html

![](Images/image00383.jpeg)

2 On this site select 64 bit msi windows installer to download. 

3 Install the downloaded software.

![](Images/image00384.jpeg)After installation

![](Images/image00385.jpeg)Open up PuTTY on your host system, and in the field for Host Name (or IP address) type the IP address of your server and press open.

![](Images/image00386.jpeg)First time you will get Security Alert , press Yes.

On the terminal screen write username and press Enter key

Provide password and press Enter key.

Save session

To save the session:-.

1 Write the IP address in the IP address input box.

2 Make sure ssh is selected 

3 Write the name of session in the saved sessions input box.

4 ![](Images/image00387.jpeg)Press Save button.

Open the saved session

To connect the server using putty session.

1 Open Putty

2 Select the session.

3 Press Load

4 Press Open.

Chapter 7  

# Exploring File System

In this chapter will look into briefly in to file system structure. Like almost all Linux distributions Oracle Linux has following filesystem structure.

![](Images/image00388.jpeg)

| Directory | Description |
| / | Top directory, all other directories are sub directories of root file system. |
| /bin | This directory is link(shortcut) to /usr/bin containing executable files. |
| /boot | Files for system boot. |
| /drv | Device driver files. |
| /etc | Configuration files. |
| /home | Users home directory other than root user. |
| /lib | Libraries. |
| /lib64 | 64 bit libraries |
| /media | Mount point for external storage devices. |
| /mnt | Mount point for user mounts. |
| /opt | Third party software. |
| /proc | Temp directory for all running process. |
| /root | Home directory of root user. |
| /run | Temp file system used by running process. |
| /sbin | Symbolic link to /usr/sbin directory for system executable files. |
| /srv | Services related data. |
| /sys | Symbolic link to the kernel source tree. |
| /tmp | Temporary files. |
| /usr | Binary files of the users. |
| /var | Variable files like logs. |

What is path

Path is the location of the file or directory. Path can be relative or absolute.

Relative v/s absolute path

There are two type of directory representation, relative and absolute path.

Relative path

Relative path is defined as path related to the current directory. Suppose you are in /home directory and want to change directory to  /home/user1. You can use relative path and give command  cd user1

Absolute path

An absolute path is defined as the specifying the location of a file or directory starting from the root (/) directory. Suppose you are in  /var directory and want to change directory to  /home/user1. You can use absolute path and give command  cd /home/user1.

File and directory operations

In this section we will discuss few file and directory operation.

Create empty file

Syntax

touch filename

Example

touch abc.txt

Add text to end of the file

Syntax

echo “text” >> filename

example

echo “this is test” >> abc.txt

Create directory

mkdir directoryname

Example

mkdir /example

it will create example directory in the root directory

Change directory

Syntax

cd directory_name

Example

cd /example 

Display file content

cat

Syntax

cat file_name

Example

cat abc.txt

To view the content of file page wise

more

Paging through text one screen full at a time.

Syntax

more filename

Example

more /etc/hosts     

less

Less is a program similar to more, but it allows backward and forward movement in the file.

Syntax

less filename

Example

less /etc/hosts 

head

Print the first 10 lines of a file to the standard output. You can also specify number of line to show.

Syntax

head option file

Example

head -20 /etc/passwd

Show first 20 lines of passwd file  

tail

Print the last 10 lines of a file to standard output. You can also specify number of lines to show.

Syntax

tail option file

Example

tail -20 /var/log/logfile

it will show last 20 lines

Use tail to monitor file continuously

tail -f /var/log/logfile 

It will show end of growing file. Ctrl +c to interrupt

Copy files and directory

Copy file

Syntax

cp filename target_dir

Example

cp abc.txt /home/user1/.

Copy multiple files

Syntax

cp * /target-location/.

Example

cp *.txt /home/user/.

This will copy all files with txt extension to /home/user1 directory

Prompt before any overwrite

cp –i /home /home1

Forcefully copy files

cp –f /tmp/abc.txt /backup/.

Do not overwrite an existing file, silently do nothing instead.

cp -n * /backup/.

Copy directory

Syntax

cp -R source_dir target_dir

Example

cp -R user1 user2

copy user1 directory to user2

Removing file and directory

Remove file

To remove file or directory you can use rm command

Syntax

rm file_name

Example

rm abc.txt

To remove a directory and all its contents, including any subdirectories and files

rm -r /example

use this command very carefully, can cause data lose

Remove directory

Syntax

rmdir directory

Example

rmdir /example

List file and directories

ls

Lists the names of files and directories

Syntax

ls -<options>

Long listing

ls -l

shows list of files or directories with size, modified date, modified time and its permission.

Show also hidden files and directories

ls -la

Show human readable format

ls -lh

mv

mv command is used to move file from one location to other location. You can also use mv command to rename the file without moving it.

To move file

Syntax

mv filename destination_directory

Example

mv a.txt /tmp/. 

It will move a.txt file from current directory to /tmp directory

To rename

Syntax

mv filename newfilename

Example

mv a.txt b.txt

grep

Searches for a String from one or more files. Display each line which has string.

Syntax

grep string file

Example

grep '127.0.0.1' /etc/hosts

diff

Compares two files.

Syntax

diff First_file  Second_file

Example

diff abc.txt bbc.txt

file

Determine file type

Syntax

file file_name

Example

file bbc.txt

Linking files and directories

Link is the like short cut in Windows which point to the original file. There are two types of links

*   Hard link
*   Soft link

Both hard and soft link are short cut to file. Soft link can exit in different file system where as hard link can exist only in the same file system. When you remove original file soft link will stop working whereas there will be no effect on hard link. The reason is that, in case of hard link both original file and hard link is pointing to same inode.

Create Soft link

Syntax

ln -s /source/file_name /target/file_name

Example

ln -s /home/admin/abc.txt /abc1.txt

Create hard link

Syntax

ln file_name /target/file_name

Example

ln /home/admin/abc.txt /home/admin/abc1.txt

Chapter 8  

# Networking  

In this chapter we will discuss networking part. There mainly two types of networks :

Non-IP network

Non-IP network make use of transport layers for communication. One of the example of Non-IP network is InfiniBand.

IP Network

IP network is the network which uses IP address to communicate. Each device which is part of IP network should have IP address. IP Network is most common type of the network type. Home, offices and internet mostly use IP network. 

For IP Network you have option to select address assignment mechanism. Two types of IP address mechanisms are available.

Static

Static IP address is manual mode of IP address assignment to devices. In case of static IP addressing, IP address remain same over the time, unless you change it. This type of IP addressing is mainly used on small networks or shared devices like Servers, printer etc where you want same IP address every time.

Dynamic IP Address:

Dynamic IP address configuration is an automatic configuration of addresses. It uses DHCP server to get the IP address for your device. When you configure DHCP server you allocate range of IP addresses to be assigned to the clients. When you start the device it connects to the DHCP server to get the IP address. Every time you start your device you may get different IP address, unless you reserve an IP address based on MAC address of the device. Dynamic IP configuration is ideal for large organizations where it is not possible to remember the address assigned to each device. But DHCP is not ideal solution for servers and printers where you want same IP address every time.

Configuring Network

By default, Oracle Linux 8 uses NetworkManager to configure and manage network connections. To use NetworkManager for configuring network interfaces, use one of the following tools:

| nmtui | Text based User Interface to manage network. This tool is very useful in non GUI environment. |
| GNOME Networkmanager | Graphical Tool for network management . |
| nmcli | Command line tool.  |

Device naming convention

The interface name starts with a two-character prefix based on the type of interface:

| Type of device | Prefix |
| Ethernet | en |
| wireless | wl |
| wireless wide area network | ww |

To keep the deice name persistent the Oracle Linux uses following convention for Ethernet devices:-

| Type of device | Device Name |
| For Onboard devices | enoX where X is the device number |
| For PCIe devices | ensX where X is the device number |
| For Multi-port devices | enpZsX where Z is the physical port number and X is the device number |
| Traditional Naming | ethX  where X is the device number |

Traditional naming convention ethX was used for network devices in the older versions of Linux. The new naming convention provides following benefits:-

1 Stable interface names across reboots.

2 Stable interface names even after hardware addition and removal.

Benefits of using NetworkManager

1 Synchronized and updated network status for all applications.

2 Easier network management.

3 Variety of tools for network management.

4 Easy and flexible Wi-Fi network management.

Network manager scripts

By default, NetworkManager executes scripts in the /etc/NetworkManager/dispatcher.d directory or subdirectories in alphabetical order in response to network events. Each script should be an executable file owned by root.

Using traditional scripts

By default Oracle Linux 8 use NetworkManger for network management, however, if required you can still use the deprecated network scripts to manage network configuration instead NetworkManager.

To install the scripts:  

yum install network-scripts

nmtui

nmtui is Text Based Interface (TUI) tool for configuring networking. This tool is very helpful in network management on the system without GUI.

To start nmtui

nmtui

Set Static IP address using nmtui

In this example we will set static IP address. 

1.  Start nmtui
2.  ![](Images/image00389.jpeg)Select Edit a connection.
3.  ![](Images/image00390.jpeg)Select the connection profile from the list and press Edit.
4.  On the Edit Connection screen, press SPACE BAR key at IPv4 configuration.
5.  Select Manual.
6.  Press TAB and select Show.
7.  Provide IP Address, Netmask, gateway and DNS in respective fields.
8.  ![](Images/image00391.jpeg)![](Images/image00392.jpeg)Scroll down and make sure Automatically connect radio button is selected.
9.  Press OK.
10.  Select Back .
11.  ![](Images/image00393.jpeg)Select Activate the connection, and press Enter.
12.  Select the connection from the list, and press Enter to activate the connection. If connection is already activated, then deactivate and activate to make changes effective.
13.  Select Back.
14.  Select Quit.

Commands nmtui

Set hostname using nmtui

Syntax

nmtui hostname new_hostname

Example

nmtui hostname Server2

nmcli

nmcli is a command-line tool for managing network. nmcli can be used to create, display, edit, delete, activate, and deactivate network connections. nmcli is a very useful tool to control and display network device status.

Listing network devices and their status

Syntax

nmcli device

![](Images/image00394.jpeg)Example

Device detailed information

nmcli device show

List connections

nmcli connection show

Activate Connection

Syntax

nmcli connection up connection_name

Example

nmcli connection up ens35

Deactivate Connection

Syntax

nmcli connection down connection_name

Example

nmcli connection down ens35

Change networking status

Syntax

nmcli networking on/off

Example

nmcli networking off 

Show hostname

nmcli general hostname

Wifi network management

Listing available WiFi APs

nmcli device wifi list

Connecting to password protected Wifi network

Syntax

nmcli device wifi connect "SSID" password "password"

Example

nmcli device wifi connect "mynetwork" password "pa$$w0rd"

GNOME GUI network manager

Network can be controlled in GUI mode in two places either from top bar system menu or under settings.

Connecting Wireless connection.

You will see Wi-Fi icon at the top bar of your desktop if system is connected to wireless network, otherwise follow the bellow procedure to connect to your home or office wireless network:-

1.  Click System Menu.
2.  Click Wireless not connected to expand collapsed menu.
3.  ![](Images/image00395.jpeg)Click Select  Network.
4.  New screen will open with all available networks. Select your Wi-Fi network name. Press Connect.
5.  ![](Images/image00396.jpeg)![](Images/image00397.jpeg)If network is password protected, at password prompt, provide password and press Connect.
6.  Now your network is connected and top bar will show Wi-Fi icon.

Change Wi-Fi Password

If for some reasons you had changed the Wi-Fi network password on your Wi-Fi router, you have to set the same password in your system also otherwise, it will not connect next time.

1.  Click System menu.
2.  Click wireless Connected to open sub menu.
3.  Click Change settings.
4.  From the list of available networks select your network and press gear icon next to it.
5.  In security setting change password and press ok.

Wired network

Connecting wired network is easy, just plug the network cable to your computer. The system will automatically configure the system for available network. As soon as the system is connected to the wired network, system indicator shows at the top bar.

Manual Wired network configuration.

Most of the time wired network settings are automatic, but in some cases you have to set IP address manually. This type of configuration is known as static IP address configuration.

To configure static IP address:-

1.  Open System Menu.
2.  ![](Images/image00398.jpeg)Click Wired Connected and select Wire Settings.
3.  It will bring Network settings windows.
4.  Click gear icon.

![](Images/image00399.jpeg)

5.  Wired profile dialog box will open.
6.  In the Details tab make sure Connect automatically is ticked.
7.  ![](Images/image00400.jpeg)Click IPv4 tab.

1 Click Manual radio button.

2 Provide IP address.

3 Enter Netmask,

4 Enter Gateway.

5 DNS

8.  Press Apply.

Name Resolution

Whenever you write hostname instead of IP address to connect Linux host, you have followingoptions to resolve hostname to IP address.

*   Local file i.e. /etc/hosts

*   DNS server
*   NIS

Local file (/etc/hosts)

/etc/hosts is file which stores hostname to IP address mapping. It provides ability to resolve hostname without using DNS server. We generally use this file if we are connecting to limited number of hosts due scope or security reason. Downside of using this file is that in case of IP address change, administrator has to change this file on all servers or PCs .

Format

IP_address hostname aliases

Example

127.0.0.1 server1 localhost

31::1 server1 localhost

192.168.228.129 server1server1.example.com

DNS

A DNS server is a central repository that contains a database of IP addresses and their associated hostnames. Whenever any client wants to resolve hostname to IP address instead of using its local file it sends request to DNS server. If IP Address of some client changes you just have to update the DNS entry. You can have multiple DNS server in one organization. To redirect your request for hostname resolution Oracle Linux uses  /etc/resolve.conf file. By default, NetworkManager on Oracle Linux 8 dynamically updates the  /etc/resolv.conf file. However, depending on your requirement you can disable DNS processing by NetworkManager.

Teaming

Teaming allows you to group multiple physical Ethernet network adapters into one logical adapter. This logical network adapter provides higher throughput or redundancy.

Modes for Teaming

| Round-robin | In this mode, data is transmitted across all ports in turn. |
| Broadcast | Here data is transmitted across all ports. |
| Load-balance | Traffic is distributed across all NICs. |
| Active-backup | Where one link or port is activated as the rest are reserved as a backup. This is used for failover to provide redundancy. |
| LACP | Uses 802.3ad protocol for link aggregation |

Install teaming packages

yum install teamd NetworkManager-team

Create active backup team adapter

Example

nmcli connection add type team con-name bond0 ifname bond0 config '{"runner": {"name": "activebackup"}}'

Important Network Commands

Show IP address

ip addr show

Show Link status

![](Images/image00401.jpeg)ip link show

The highlighted text shows the link state.

Show routing table

ip route

Check network reachability

Syntax

ping ipaddress/hostname

Example

ping 192.110.22.121

Check and change host name

The name of the computer in Linux is known as hostname. To change the hostname, you can use  hostnamectl command.

Display current hostname

hostnamectl

Change hostname

Syntax

hostnamectl set-hostname newname

Example

hostnamectl set-hostname myhost1 

If you are interested in changing IP address manually using command line, try  nmcli command. Check  nmcli-examples command for more information.

dig

DNS lookups and displays result

Syntax

dig hostname

Example

dig microsoft.com

telnet

To connect destination host:port. You can also use telnet command to test host and port reachability.

Syntax

telnet hostname port

Example

telnet myserver1 8080

nslookup

Query Internet domain name servers.

Syntax

nslookup hostname

Example

nslookup microsoft.com

scp

Copy files from one host to other host over the network in secure manner.

Syntax

scp filename user@targetserver:/path

Example

scp ast.txt user1@server2:/home/user1

ssh

For secure login to target server.

Syntax

ssh user@targethost

Example

ssh user1@server2

nmap

Checks the opened port on the server.

Syntax

nmap hostname

Example

nmap cloudflare.com

Chapter 9  

# Local file systems

File system controls how data is stored and retrieved in the Operating system. File system is way to organize data on the storage. Oracle Linux 8 supports different type file system for local data storage. We will discuss two major file systems.

*   XFS
*   EXT4

XFS

XFS is high performance file system developed by Silicon Graphics, Inc (SGI) in 1993\. XFS is the default file system for Oracle Linux 8\. it is journaling file system which means recovery of the file system is seamless in case of abrupt system failure. XFS is also capable of storing large files and big file systems. XFS can be extended and defragmented in mounted state.

EXT4

EXT file system has long history. ext4 is the fourth generation of the ext file system family. It is also a journaling file system.  Ext4 drivers can read and write both ext3 and ext2 file system. It can support file system size up to 50 TiB. Being a legacy file system ext4 file system is supported by almost all applications on Linux.  

Commands for XFS file system management

Create XFS file system

Syntax

mkfs.xfs devicename

Example

mkfs.xfs /dev/sda01

Resize XFS file system

You can only extend the file system and can not reduce it. To grow XFS file system use:-

Syntax

xfs_growfs device_name 

Command

This command will extend xfs file system to maximum limit of the device.

xfs_growfs /dev/sda01 

-D takes argument number as file system blocks.

xfs_growfs /dev/sda01 -D 200

Repair XFS file system

Syntax

xfs_repair -n device_name

Example

xfs_repair -n /dev/sda01

Ext4 file system management Commands

Create ext4 filesystem

Syntax

mkfs.ext4 /dev/device_name

Example

mkfs.ext4 /dev/sd01

Label the partition

Syntax

e4label device_name new_label

Example

e2label /dev/sda01 data01

Resize

you can expand ext4 file system while it is mounted.  Shrink require ext4 file system has to be unmounted.

Syntax

Resize2fs device_name new_size

Example

Resize2fs /dev/sda01

if you do not specify size this command will extend the file system to maximum limit of the device.

To change the file system to specific size

resize2fs /dev/sda01 5G

Chapter 10  

# Exploring Network File Systems 

In the previous chapter we had discussed local file systems, however to share data over the network remote file system comes in to the picture. Network file system requires extra layer above local file system in order to share and mount over the network. Network file system can be used by multiple users at same time. Once mounted it behaves like local file system on remote machine. In this chapter, we will walk through commonly used remote file system on Oracle Linux 8. 

NFS

NFS is a file sharing file system, which works on server client basis. The file systems which are shared on server can be mounted on client over the network. NFS File system is very popular file system sharing protocol among Unix and Linux systems. Oracle Linux server support both NFS Server and client. NFS on Linux is very useful for cross platform files and folders sharing. NFS is also widely used protocol on Network Attached Storage NAS systems also. Currently there are four versions of NFS and each versions has further releases, like version 4 has 4.2:-

NFS V1

NFS V2

NFS V3

NFS V4

Where NFS V3 and NFS V4 are more recent version of NFS. In Oracle Linux 8, NFS over UDP is no longer supported. NFSV4 has added advantage of working through firewall and works on TCP. In Oracle Linux 8, the default NFS version is 4.2 which features support for Access Control Lists (ACLs), server-side copy and sparse files. Oracle Linux 8 support only version 3 and version 4 of NFS, version1 and version 2 is no more supported by Oracle Linux version 8.

Installing NFS

Install packages

yum install nfs-utils

After installation, enable the service to start automatically after reboot.

systemctl enable nfs-server.service

Start the service

systemctl start nfs-server.service

this command will start other services required by the NFS such as nfsd, nfs-idmapd, rpcbind, rpc.mountd, lockd, rpc.rquotad, rpc.statd and rpc.idmapd.

Now check the status of service

systemctl status nfs-server.service

The important files for NFS server are

| File Name | Purpose |
| /etc/nfs.conf | main configuration file for the NFS daemons and tools. |
| /etc/nfsmount.conf | Global configuration file for NFS mounts.  |
| /etc/exports | File for NFS server export table |

/etc/exports files options

| rw | allows both read and write access on the file system. |
| sync | this option by default tell NFS server to reply to requests only after the last changes have been committed.  |
| all_squash | Map all UIDs and GIDs to the anonymous user. Useful for public FTP directory |
| root_squash | Map  requests  from  client UID/GID  0  to  the  anonymous UID/GID. |
| no_subtree_check | This option disables subtree checking |

Export directory

In this example we will create two directories and export these directory for clients to mount .

mkdir /accounts

mkdir /hrms

Edit the /etc/exports file

vi /etc/exports

Add following entries

/account 10.101.11.0/24(rw,sync)

/hrms*(rw.sync)

in this example first line exports the NFS share to specific network IP range. Second line shares hrms directory to everybody.

Export the directory

exportfs -a

List the exported directories

export -s

Add the firewall rule

firewall-cmd --permanent --add-service=rpc-bind

firewall-cmd --permanent --add-service=mountd

firewall-cmd --permanent --add-service=nfs

Reload the filewall configuration

firewall-cmd --reload

Check the firewall configuration

firewall-cmd --list-all|grep nfs

Configure NFS on client

Install the package if it is not already there.

yum install nfs-utils nfs4-acl-tools

Create directory for mount

mkdir /myhrms

Mount the file system

mount -t nfs 192.168.115.128:/hrms /myhrms 

Configure file system to mount automatic on boot using  /etc/fstab file

echo "192.168.115.128:/hrms  /myhrms  nfs  defaults 0 0" >>/etc/fstab

Samba or CIF

Samba is a free and open source protocol that allows files to be sharing across Linux and windows machine.

In this chapter we will see how use to Oracle Linux 8 server as smb client. We will use the shared folder from Window machine on Oracle Linux Linux machine.

Install required packages

yum install cifs-utils

Mount the shared folder

Syntax

mount -t cifs -o username=user //servername/sharename /Local_mount_point/

Example

mount -t cifs – username=user1 //192.168.115.129/shared /mnt

This command will prompt for windows password

Chapter 11  

# Disk Partitions

Disk partitioning is a way to create separate region on the storage which can be managed independently. Partitions have following benefits: -

1 Running more than one OS on your system.

2 Data and application space segregation.

3 Minimize corruption risk.

4 Improve performance.   

Partition Table

A partition has partition table where it stores partition’s beginning and end. It also stores the code that is used during start-up, if a partition is bootable. You have option to setup disk as MBR (Master Boot Record) or GPT (GUID Partition Table). In this section, we will explain what difference between two is.

Master Boot Record (MBR)

The MBR partition was introduced in 1983 with DOS 2.0 also Known as Master Boot Record. As it very old partition scheme it provides the maximum compatibility. It not only support x64 but also conventional x86-based computers. Due to old architecture of MBR, it has many limitations. First one, it limits the maximum addressable storage space of a partitioned disk up to 2 TB, which is a big barrier for new disks which can store more than 2TB and specially with RAID where partition can be pooled capacity of several disks. Another limitation is, MBR disks support only four primary partitions. If you want more than four partitions then you have to make one of your primary partitions as extended partition and create logical partitions inside it. 

GUID Partition Table (GPT)

To overcome limitations of MBR and bring new features like security of partitions, GPT was introduced in late 1990s. Unlike MBR, GPT does not support x86 systems. GPT uses UEFI instead of BIOS. Each GPT Partition has Globally Unique Identifier or GUID which is unique random number. GPT has no limitation in the case of maximum number of partitions as it allows nearly unlimited number of partitions, only limited by OS limitations, like Oracle Linux 8 allows up to 128 partitions. For redundancy GPT disks uses primary and backup partition tables. For integrity, it uses CRC32 field.

Although GPT brings many advantages, but MBR is still the most compatible and widely used partition schema. 

In this chapter we will learn to create, delete, and modify various types of disk partitions.

There are couple of utilities for partition management .

*   Parted
*   fdisk

Parted

Parted is command line tool that can manage partition tables.

Display partition layout

Syntax

parted -l

This command will display partition layout of all block devices 

To display partition table of specific block device

Syntax

parted device print

Example

parted /dev/sda print

Use parted interactively 

Enter parted command with device name. Suppose new disk is sdb

parted /dev/sdb

it will start the interactive session.

Create partition table on a disk

Start parted

Syntax

parted device_name

Where device name is disk name

Example 

parted /dev/sda

Create partition

Syntax

mkpart part-type name fs-type start end

Where

| part-type | can be primary, logical, or extended for MBR partition table. |
| name | partition name required for GPT partition tables. |
| fs-type | can be xfs, ext2, ext3, ext4, fat16, fat32, hfs, hfs+, linux-swap, ntfs, or reiserfs. The fs-type parameter is optional because parted does not create the file system on the partition. |
| start and end | are sizes that determine the starting and ending points of the partition. Size suffixes, such as MiB, GiB, or TiB. The default size megabytes. |

Example

(parted) mkpart primary xfs 1 5GiB 

List the partition using print command

(parted) print                                                           

Model: VMware, VMware Virtual S (scsi)

Disk /dev/sdb: 10.7GB

Sector size (logical/physical): 512B/512B

Partition Table: msdos

Disk Flags:

Number  Start   End     Size    Type     File system  Flags

1      1049kB  5369MB  5368MB  primary  xfs          lba

use quit command to exit parted

(parted) quit                                                            

Information: You may need to update /etc/fstab.

Remove partition using parted

In the parted interactive session select the

parted device

Example

parted /dev/sdb

Display the current partition table

(parted) print                                                           

Model: VMware, VMware Virtual S (scsi)

Disk /dev/sdb: 10.7GB

Sector size (logical/physical): 512B/512B

Partition Table: msdos

Disk Flags:

Number  Start   End     Size    Type     File system  Flags

1      1049kB  5370MB  5369MB  primary               lvm

2      5370MB  7000MB  1631MB  primary  ext2       lba

Remove the partition with rm command and select the partition number

(parted) rm                                                              

Partition number? 2                                                      

(parted)          

Create partition using fdisk

Syntax

fdisk device

In this example we will create 5GB partition on device sdb

fdisk /dev/sdb

1 On interactive prompt give n command to create new partition.

2 Enter partition type p for primary and e for extended.

3 Select the partition number. Press enter to select default.  

4 Press enter to use default start point

5 Enter size in MB, GB and KB like for 5 GB write +5G

6 Use p command to print the partitions

7 Optionally if you required to change filesystem type using t command and press L to list the filesystem type with IDs . Enter the id like 83 for Linux and 8e for Linux LVM.

8 Use w command to write the changes.

Command (m for help): n

Partition type

   p   primary (0 primary, 0 extended, 4 free)

   e   extended (container for logical partitions)

Select (default p): p

Partition number (1-4, default 1):

First sector (2048-20971519, default 2048):

Last sector, +sectors or +size{K,M,G,T,P} (2048-20971519, default 20971519): +5G

Created a new partition 1 of type 'Linux' and of size 5 GiB.

Command (m for help): p

Disk /dev/sdb: 10 GiB, 10737418240 bytes, 20971520 sectors

Geometry: 255 heads, 63 sectors/track, 1305 cylinders

Units: sectors of 1 * 512 = 512 bytes

Sector size (logical/physical): 512 bytes / 512 bytes

I/O size (minimum/optimal): 512 bytes / 512 bytes

Disklabel type: dos

Disk identifier: 0x08dd22da

Device     Boot Start      End  Sectors Size Id Type

/dev/sdb1        2048 10487807 10485760   5G 83 Linux

Command (m for help): t

Selected partition 1

Hex code (type L to list all codes): L

Hex code (type L to list all codes): 8e

Changed type of partition 'Linux' to 'Linux LVM'.

Command (m for help): w

The partition table has been altered.

Calling ioctl() to re-read partition table.

Syncing disks.

Remove partition

Start fdisk with device name

fdisk /dev/sdb

Print current partition table

Command (m for help): p

Disk /dev/sdb: 10 GiB, 10737418240 bytes, 20971520 sectors

Units: sectors of 1 * 512 = 512 bytes

Sector size (logical/physical): 512 bytes / 512 bytes

I/O size (minimum/optimal): 512 bytes / 512 bytes

Disklabel type: dos

Disk identifier: 0x0eacb20b

Device    Boot Start End Sectors  Size   Id   Type

/dev/sdb1   2048 10487807 10485760     5G     8e  Linux LVM

/dev/sdb2   10487808 14393343 3905536     1.9G   83  Linux

Use d command to delete partition

Command (m for help): d

Partition number (1,2, default 2): 2

Partition 2 has been deleted.                       

Chapter 12  

# Management of local file system 

In this chapter we will cover management of local file system

*   Create a file system
*   Remove a file system
*   Mount a file system
*   Unmount a file system
*   Create LVM volume groups
*   Remove LVM volume groups
*   Create logical volumes
*   Remove logical volumes

Create file system

Before creating file system you should decide which type of file system you want to create.

Create XFS filesystem

Syntax

mksfs.xfs /dev/sdb1

Example

mksfs.xfs /dev/sdb1

Create ext4

Syntax

mkfs.ext4 /dev/sdb1

Example

mkfs.ext4  /dev/sdb1

Mount file system

In Linux based systems to use file system you have to first mount the file system. Mounting require minimum two things, mount device and mount point.

Mount device

Mount device is the block device or remote filesystem which you want to use for storing data.

List all block devices

lsblk 

To mount file system you can identify the mount device by following identifiers :-

| UUID | UUID is the Universal Unique ID of the device. This is the best way to mount the device as UUID remain same. You can use   blkid command to get UUID of device. |
| Device name | Device name is hierarchical name of the device it can be like  /dev/sdb1 |
| Label | Volume label for example  LABEL=data1. You can use  e2label to check or change the label of ext file system. To set or list label of XFS file system use  xfs_admin command. |

Mount point

Mount point is the link for accessing this mount device. Mount point is the normal directory. Once mounted device becomes the part of the directory and you can access the contents of file system under this directory.  

Mount command

mount command can be used for mounting file system.

Syntax

mount -t type -o options device dir

Mount command require following parameter to mount the file system.

| type | Type of file system it can be xfs, ext4, nfs etc. |
| options | Options like  rw for read and write,  ro for read only,  loop for ISO media, |
| device | Device name. |
| dir | Mount Point. |

Example

mount -t ext4 /dev/sdb1 /mnt 

Automatic mounting

If you want to mount the filesystem to be mounted automatically on every boot you can use  /etc/fstab file.

fstab file has following format

firstsecond third fourth fifty sixth

| Field | Description |
| First | Block device or remote file system |
| Second | Mount point |
| Third | File system type |
| Fourth | Options, atleast one ro or rw. Other options aredefaults : rw, suid, dev, exec, auto, nouser, and async.noauto: do not mount automatically or with mount -a command.user:   allow a user to mount the file system.owner:  allow device owner to mount. |
| Fifth | Dump option, default is 0 for no dump. |
| Sixth | File system check priority for fsck. |

Example

/dev/mapper/cl-root/ xfsdefaults0 0

UUID=095af347-cb2c-4d50-99b6-xxx/bootext4   defaults      1 2

/dev/mapper/cl-swap swap         swapdefaults0 0

LABEL=data1/data1 ext4defaults0 0

/dev/sdb2/data2xfsdefaults0 0             

Manually mount all devices in the fstab with auto option 

mount -a

Manually mount single device in the fstab.

Syntax

mount mount_point 

No need to specify the device name.

Example

mount /data2

List all mounted file systems

mount

or

findmnt

List specific fileystems type

findmnt -t xfs

Unmounting a file system

Syntax

umount mount_point

Example

umount /data1

If you get “target is busy” error when you unmount a file system, use fuser command to list all processes using fileystem.

Syntax

fuser --mount mountpoint

Example

fuser –mount /data1

Remove file system

To delete a file system, we must first unmount it

Example

umount /dev/sda2

Then we can delete the partition from the partition table using fdisk or parted

Example

fdisk /dev/sda2

Select the option d to delete the partition

Write the changes to the partition table by selecting w.

Chapter 13  

# Logical Volume Management

LVM or Logical Volume Manager allows creation of group of disk and partitions that can be used as one disk. Creates an abstraction layer between physical devices and logical devices. The benefits of LVM are bellow

*   Flexibility: allows resize.
*   Snapshot: take point in time copy of Logical Volume.

Conventional setup of disk is bellow

| File systems | / | /opt | /home |
| Partitions | /dev/sda1 | /dev/sda2 | /dev/sda3 |
| Physical devices | /dev/sda | /dev/sdb |
|  |  |  |  |

This setup has disks then partitions and above partitions there are file systems.

LVM setup

| File systems | / | /home | /var |
| Logical Volume | /dev/sda1 | /dev/sda2 | /dev/sda3 |
| Volume Group | Vg01 |
| Physical Volume | /dev/sda | /dev/sdb |
|  |  |  |  |  |

Physical volume

Physical Volume (PV) is underlying physical storage unit. Physical storage is a block device such as a partition or whole disk. Use  pvcreate command to use the physical device as Physical Volume. If block device is a partition, then use fdisk to change the partition type to 8e (Linux LVM) before using  pvcreate command.

Create PV

Syntax

pvcreate device

Example

pvcreate /dev/sdb

If device is a partition

Change partition type as LVM

fdisk /dev/sda (Refer the partition chapter to change partition type)

now create PV

pvcreate /dev/sda3

Volume Groups

One or more physical volumes combined together to make a Volume Group (VG). Volume group is an abstract that presents underlying devices as a unified logical device with combined storage capacity of the physical volumes.

To create Physical Volume

Syntax

vgcreate vgname PV1 PV2 .. 

Example

vgcreate vg01 /dev/sdb /dev/sdc

Logical Volume

Logical Volume is logical partitioning of the volume group. Logical volume can be used for file system creation. In some cases, you can also use LV as block device.

To create LV

Syntax

lvcreate -n name -L size  VG_name

Example

lvcreate -n data_lv -L 5G vg01

File system

To create XFS filesystem on the LV

Syntax

mkfs.xfs lv_name

Example

mkfs.xfs /dev/vg01/data_lv

To create ext filename on LV

Syntax

mkfs.ext4 lv_name

Example

mkfs.ext4 /dev/vg01/data_lv

Two more terms in LVM is worth mentioning

*   Physical Extent
*   Logical Extent

Physical Extent

Storage space from Physical Volume is divided in to small unit of fixed size known as physical extent, which is smallest unit that can be allocated. P.E. size is always same for all physical volume in the same VG.

Logical extent

Mapping of PE to make up frontend of LVM. By default, one PE is generally mapped to one LE. However, you can map more than one PE to one LE in case of mirroring.

LVM management commands

PV management commands

List all PVs

pvs

Display attributes

Shows the attributes of PVs, like size, physical extent size, space etc.

pvdisplay

PV Resize

If PV is coming from storage or vitrtual storage you have option to change size of virtual device or LUN. To update LVM with the new size of physical storage.

Syntax

pvresize device

Example

![](Images/image00402.jpeg)![](Images/image00403.jpeg)![](Images/image00404.jpeg)pvresize /dev/sda

Remove PV

If for some reason the PV is no more used by LVM you can remove the PV using pvremove command

Syntax

pvremove device

Example

pvremove /dev/sda

Rescan system for PVs

pvscan scans all block devices in the system for PVs.

Syntax

pvscan --cache

VG management commands

Display summary all VGs.

Syntax

vgs

Example

[root@Server1 ~]# vgs

  VG #PV #LV #SN Attr   VSize   VFree

  cl   1   2   0 wz--n- <19.00g    0 

Display VG properties

vgdisplay displays properties of VG such as size, extents, number of physical volumes etc)

Syntax

vgdisplay

To view specific VG

Syntax

vgdisplay vgname

Example

vgdisplay vg01

Scans all the disks for VG

To scans all the disks for volume groups and rebuilds the LVM cache file use  vgscan command.

Syntax

vgscan

Adding Physical Volumes to a Volume Group

To increase the space of VG you can add additional physical volumes to an existing volume group. To extend the VG use the  vgextend command.

Syntax

vgextend vgname new_PV

Example

vgextend vg01 /dev/sdc

Use  vgscan command to rescan for VGs on the system.

Example 

[root@Server1 ~]# vgscan

Found volume group "cl" using metadata type lvm2

Remove PV from VG

To remove the physical volume from VG you can use  vgreduce command. Before reducing VG make sure there is no data on the PV.

Syntax

vgreduce vgname pv_name

Example

vgreduce vg01 /dev/sdc

Change VG

You can deactivate an active VG and vice versa using  vgchange command. VG in deactivated state can be used.

Syntax

vgchange -a n vgname

Example

vgchange -a n vg01

same way you can activate VG also.

Example

vgchange -a y vg01

Remove VG

When vg is no more required and there is no LV on the VG you can remove it.

Syntax

vgremove vgname

example

vgremove vg01

Rename VG

For some reason if you have to rename a VG

Syntax

vgrename vgname new_vgname 

Example

vgrename vg01 vg02

Moving a Volume Group to Another System

To move volume group from one system to another first you have to export the volume group from the original system and then import into the target system. The export VG command insure the removal of VG information from the system so that next time it will not complain about missing VG.

Syntax

vgexport vgname

Example

vgexport vg01

On the target machine

Syntax

vgimport vgname

Example

vgimport vg01

Logical volume

list logical volume on the system

lvs

Show the properties of the Logical volume or volumes.

lvdisplay

Remove a LV

To remove a logical volume, make sure it is not in use anymore.

Syntax

lvremove vgname/lvname

Example

lvremove vg01/lv01

Extend the file system size

in this section we will go through the practical scenario in which one the filesystem with LVM configuration is full. To extend the file system we will use following procedure:-

Check the filesystem and its LV

df -hT

Add the new disk to the system

Check if new disk is visible

lsblk

or

fdisk -l

Create PV for new disk

pvcreate /dev/sdb

Check the new PV

pvs

Extend the VG with filesystem to be extended

vgextend vg01 /dev/sdb

Extend the LV and filesystem

Use this command to increase the size of LV and filesystem over it. This command will increase the size of LV by 20 GB and also extend the respective filesystem.  

lvextend -L 20G -r vg01/lv-root

Use this command to extend the LV to use 100% free space of VG and extend the filesystem also.

lvextend -l +100%FREE -r vg01/lv-root

This concludes the LVM chapter

Chapter 14  

# Software Management

Oracle Linux distribution is based on RPM packages. Oracle Linux uses .rpm packages for installing software with rpm command. RPM package is simply a file that contains some files and information about those files. Technically speaking RPM is a file containing cpio archive and metadata about itself. RPM Header contains the metadata and this metadata is used to determine following things about the package:-

*   Description of package.
*   List of files in the package.
*   Version and release of package.
*   When and who made it.
*   Architecture supported.
*   Checksums of the files contained in the package.
*   Dependences.

Etc…

Package Management System

If you try to install single package manually you have to first install all its dependencies and keep track of versions also. To make software management easy Linux companies have developed a system known as package management system or package manager. Package management system install precompiled packages, which are in form of archives containing binaries of software, configuration files, and information about dependencies. Package management system is a collection of software tools to automate the process of installation, upgradation and removal of software packages. Software manager maintains its own database of software dependencies and version information. Package management system helps in preventing software mismatches and missing prerequisites. Oracle Linux uses YUM tool for package management.

YUM

Like other Linux distributions, Oracle Linux uses very comprehensive package management system known as YUM. Yellow dog Updater Modifier is command line tool for package management. Yum uses repositories to fetch the correct version of a particular package compatible for your system. Yum allows automatic updating of packages and dependency management. When you use yum command for installation of software, it automatically downloads package and all its dependencies from defined repositories. Oracle Linux version 8 uses YUM v4 instead to YUM v3 used in the earlier version. YUM v4 tool, which is based on the DNF technology has the following advantages :

*   Better performance
*   Support for modular content (We will discuss later about modules)
*   Stable API for integration with tooling

In Oracle Linux 8 has three application streams, each one with its own lifecycle:

*   BaseOS provides the basic operating system,
*   AppStream provides user applications,
*   CodeReady Linux Builder provides developer tools and languages.

Package management

Search package

Syntax

yum search package_name

Example

yum search httpd

Display information about package

Syntax

yum info package_name

Example

yum info httpd

List available packages

yum list available

Install packages from the default stream 

Syntax

yum install package_name

Example

yum install httpd

Install locally downloaded package

Syntax

yum localinstall package.rpm

Example

yum localinstall abc.rpm

Removing package

Syntax

yum remove package_name

Example

yum remove httpd

Update

Update specific package

Syntax

yum update package_name

Example

yum update vsftpd

Update whole system

To update the system to latest level

yum -y update

Update only security patches

yum -y update --security

This command can increase the minor release of the system., in some cases it is not required then you can use more conservative approach to security update.

yum update-minimal --security -y

CVE

Common Vulnerabilities and Exposures is a list of common identifiers for publicly known Cybersecurity vulnerabilities. Each CVE has unique ID assigned by central body.

To install specific CVE.

Syntax

yum update --cve cve-id 

Example

yum update --cve CVE-2017-1000392 

List all CVE

yum updateinfo list cves

Update advisory

Update advisory is the list of packages with bug fixes.

View update advisory

yum updateinfo list

Install specific advisory

Syntax

yum update --advisory=advisory_id

Example

yum update --advisory=RHBA-2020:0618

Remove unwanted dependencies

yum autoremove

Display package which provide specific file

Syntax

yum whatprovides filename

Example

yum whatprovides /etc/hosts

Clean yum cache

yum clean all

View History of Yum

To view all the past transactions of yum command, just use the following command.

yum history

Modules

In Oracle Linux 8 a new concept of modules has been introduced. Modules is the extension to RPM. A module is set of RPM packages that represent a component. A module typically contains application packages, its libraries, dependent packages and documentation including help files. Oracle Linux 8 can contain multiple versions of same package for example you can have two versions of python or perl. These packages have its own life cycle rather than Oracle Linux life cycle. When you install one version of module its dependencies and libraries will be automatically installed from the module. You can consider module as a virtual repository. For handling module  yum module command has been introduced. The modules has extension module after rpm like example.rpm.module.

Streams and profiles

Module Streams

Modules are available in single or multiple streams which usually represent a version of a software, providing you an option to choose what versions of packages you want to install. Module stream is like virtual repository. Each module may have a default stream which usually provides the latest or recommended version of the component. Default streams make it easy to install packages without the need to learn about modules. Modules make it possible to have multiple versions of software available to your system for installation.

Module Profiles

To simplify installation further, modules usually classified with set of specific set of packages for specific workload or user case. This list of packages is known as profile. A profile name can be anything like server, client, development, minimal install etc.

Package management using modules

List all available modules

yum module list

![](Images/image00405.jpeg)

It will show output in four columns

*   Name of the module
*   Stream
*   Profile
*   Summary

The output shows Steams and profiles with [d], [e], [x] and [i] in the stream and profile column which show the status of module’s stream and profile. Where [d] if for default, [e] for enabled [x] for disabled [i] installed. 

Display information about module

Syntax

yum module info module_name

Example

![](Images/image00406.jpeg)yum module info nodejs

Search which module provides specific package

Syntax

yum module provides package_name

Example

yum module provides php

Display information about module’s profiles

Syntax

yum module info --profile module_name

Example

yum module info --profile nodejs

Display information about specific profiles

Syntax

yum module info --profile module_name:stream

Example

yum module info --profile nodejs:12

Install package from specific stream

To install package for other stream first you have to enable that stream and then install the package

Syntax

yum module enable module_name:stream 

Example

yum module enable nodejs:12

Install module

Syntax

yum module install module_name

Example

yum module install nodejs

This will install the module from default stream

To install module of specific stream without enabling

Syntax

yum module install module_name:stream

Example

yum module install nodejs:10

Install a selected profile of the module stream

Syntax

yum module install module_name:stream/profile

Example

yum module enable --profile httpd:2.4/devel

Remove all packages from a selected stream

Syntax

yum module remove --all module_name:stream

Example

yum module remove --all nodejs:12

Remove packages of particular profile

Syntax

yum module remove module_name:stream/profile

Example

yum module remove --profile nodejs:12/minimal

Reset a module to the initial state

Syntax

yum module reset module_name

Example

yum module reset nodejs

Disable a module and all its streams

Syntax

yum module disable module_name

Example

yum module disable nodejs

RPM

Package management using rpm.

Although yum is very versatile package manager but in some situations you have to manage rpm packages manually

List all installed packages

rpm -qa

List specific installed package

Syntax

rpm -qa |grep package_name 

Example

rpm -qa |grep gzip

Install rpm package

Syntax

rpm -ihv package_name

where -i for install

-v for verbose mode

-h show progress

Example

rpm -ihv zsh-html-5.5.1-6.el8_1.2.noarch.rpm

Update already installed package

Syntax

rpm -Uhv package_name

Example

rpm -Uhv zsh-html-5.5.1-6.el8_1.2.noarch.rpm

Check the dependency of package

Syntax

rpm -qpR package_name

Example

rpm -qpR zsh-html-5.5.1-6.el8_1.2.noarch.rpm

To list all files installed by specific package

Syntax

rpm -ql package_name

Example

rpm -ql zsh-html-5.5.1-6.el8_1.2.noarch.rpm

Remove package

Syntax

rpm -ev  package_name

Example

rpm -ev zsh-html

Print information about the package before installation

Syntax

rpm -qip package.rpm

Example

rpm -qip zsh-html-5.5.1-6.el8_1.2.noarch.rpm

To rebuild the rpm database

cd /var/lib/rpm

rm __db*

rpm --rebuilddb

/usr/lib/rpm/rpmdb_verify /var/lib/rpm/Packages

Package Group

Package group contain packages that perform related tasks such as System Tools, Workstation and Minimal Install etc.

List group list

Syntax

yum grouplist

Install package group

Syntax

yum group install “Group Name”

Example

yum group install “System Tools”

Update group

Syntax

yum group install “Group Name”

Example

yum group update “System Tools”

Remove package group

Syntax

yum group remove “Group Name”

Example

yum group remove “System Tools”

Chapter 15  

# Software Repositories

A Linux repository is a storage location from where Linux updates operating system. Repositories are also used for installing new application and updating installed applications. Each repository is a collection of software hosted on a remote server or locally. Repository can be classified in to multiple branches like binaries, source codes, optional etc. 

To add new repository add entries in the /etc/yum.conf file,  however it is recommended to create separate file for each repository in the  /etc/yum.repos.d directory. The file extension for repository files should be  .repo.

The main components of repository files are

| [repository] | Each repository should have repository ID with starts the repository section |
| name=repository_name | Name of the repository |
| baseurl=repository_url | Location of the repository the location can be http , ftp or localHttp [http://path/repo](http://path/repo)FTP [ftp://path/repo](ftp://path/repo)Local file:///path/repo |
| enabled = 1 | Defines state of repository 1 for enabled and 0 for disabled |
| gpgcheck = 1 | Verify the GPG signature before installation |

![](Images/image00407.jpeg)Example

Oracle Linux Repositories

Unlike previous versions, Oracle Linux 8 comes with two main repositories.

1 BaseOS

2 Appstream

BaseOS

BaseOS is intended to provide core set of functionality and core components to OS independent to all types of installations. Which mean BaseOS repository is required for all set of installation even for headless installation.

Appstream

Appstream contains additional userspace applications, languages, databases etc. Appstream is intended for different set of workloads like http, database or file server. Appstream gets updates more frequently than BaseOS. Appstream is made up of rpm packages and modules.

Repository management commands

List all enabled repositories

yum repolist

List status of all repositories

yum repolist all

Add repository using repofile from internet

Example

yum config-manager --add-repo http://www.example.com/example.rep

Enable /Disable repository

Using repofile

You can enable or disable a repository by either editing repo file in the /et/yum.repo.d or using command  yum config-manager command.

To enable any repository using repo file.

![](Images/image00408.jpeg)open the repo file and change from enabled=0 to enabled=1\. To disable any repository, change from enabled=1 to enabled=0.

Using command

Enable any repository

Syntax

yum config-manager --set-enabled repo_name

Example

yum config-manager --set-enabled PowerTools

Disable repository

Syntax

yum config-manager --set-disabled reponame

Example

yum config-manager --set-disabled PowerTools

Clear cache after each modification

yum clean all 

Set Up a Local repository

In some cases, where internet is not available you have to create local repositories for software management. The steps for creating local repository are following: -

1.  Create directory
2.  mkdir /local_repo

3.  Mount the DVD on /mnt directory

mount /dev/cdrom /mnt

Note : your cdrom device name can be different

4.  Copy installation files to the server’s /local_repo directory

cp -r /mnt/* /local_repo

5.  Copy the repo file to /etc/yum.repos.d/ directory

cp  /local_repo/media.repo  /etc/yum.repos.d/local_repo.repo

6.  Change the permission of repo file

chmod 644 /etc/yum.repos.d/local_repo.repo

7.  Edit the configuration

vi /etc/yum.repos.d/local_repo.repo

8.  Changed file should look like below

[InstallMedia-BaseOS]

name=Oracle Linux 8 - BaseOS

metadata_expire=-1

gpgcheck=1

enabled=1

baseurl=file:///local_repo/BaseOS/

gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-oracle

[InstallMedia-AppStream]

name=Oracle Linux 8 - AppStream

metadata_expire=-1

gpgcheck=1

enabled=1

baseurl=file:///local_repo/AppStream/

gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-oracle

9.  Clean the Cache 

yum clean all

10.  List repositories

yum repolist

![](Images/image00409.jpeg)

Repository for developers

PowerTools

Powertools repository is mainly for software developers. This repository contains number of packages required for building applications from source code.

Enable

yum config-manager --set-enabled PowerTools

Third Party repositories

To install software which are not available on these three repositories due license issues or scope, you can add third-party repositories. The most common third party repositories are:-

*   EPEL
*   REMI
*   RPM Fusion

EPEL repository

EPEL or enterprise Linux repository is from fedora community containing packages which are not available from Oracle official repository due to license limitation. Most common packages are chromium, codec for audio and videos.

To add repository

yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm

Enable

yum config-manager --set-enabled epel

REMI

REMI is a free to use repository created and maintained by a Remi Collect. The REMI provides the latest versions of the PHP stack and some other software.

Install

yum -y install https://rpms.remirepo.net/enterprise/remi-release-8.rpm

Enable

yum config-manager --set-enabled remi

RPM Fusion

RPM Fusion provides proprietary multimedia software that the Oracle Linux doesn’t want to ship.

Install

yum install --nogpgcheck https://download1.rpmfusion.org/free/el/rpmfusion-free-release-8.noarch.rpm https://download1.rpmfusion.org/nonfree/el/rpmfusion-nonfree-release-8.noarch.rpm

Note: This is single line command which will add both free and non-free RPM Fusion repositories.

Chapter 16  

# Service Management System

What is service

A service is a program that runs in the background waiting to be used, or carrying out essential tasks. When system boots, it starts many services to achieve required state of the system. Suppose you want to start the system in GUI mode, system has to start all the services related to Desktop environment. Same way if you have configured the server as web server you have to start the web services during boot process. Even to do its basic tasks it requires many services to be running like network, date and time etc. Unlike regular software program that is launched by the user and closes automatically when the user log off, services can start without user intervention and may continue to run even after the user logs off. Most of the services runs in the background without the knowledge of users. Software developer can develop its own software to run as service.

Introduction to SYSTEMD

Systemd is a system and service manager for most of the Linux distributions.  Oracle Linux also uses Systemd for service management. Systemd is backward compatible with legacy SysV init scripts. The major benefits of using Systemd for service management are:-

*   Easier service management
*   Parallelized job execution at boot time
*   cgroups for better resource management.
*   On-demand activation of daemons

Important directories and files for systemd

| Directory | Description |
| /usr/lib/systemd/system/ | Systemd unit files installed programs . |
| /run/systemd/system/ | Systemd unit files created at run time. |
| /etc/systemd/system/ | Systemd unit files created for automatic start of the services. |

System units type

| Unit | Description |
| .service | For services |
| .device | For devices |
| .target | Equivalent to run level in sysv |
| .snapshot | Stores state of services |
| .swap | Encapsulate memory swap partitions or swap files. |

Commands

systemctl is the command to manage the services in Oracle Linux 8\. we will use this command to view, start, stop, enable and disable the service.

List all services

systemctl list-units --type service --all

Display status of the services

Syntax

systemctl status service_name

Example

systemctl status sshd

To check whether a service is active (running)

Syntax

systemctl is-active service_name

Example

systemctl is-active sshd

Starting and Stopping Services

Starts a service

Syntax

systemctl start service_name

Example

systemctl start httpd

Stops a service

Syntax

systemctl stop service_name

Example

systemctl stop httpd

Restart a service

Syntax

systemctl restart service_name

Example

systemctl restart httpd

Restart a service if it is running

Syntax

systemctl try-restart service_name

Example

systemctl try-restart httpd

Reloads configuration of service

Syntax

systemctl reload service_name

Example

systemctl reload httpd

Mask Service

When you mask the service it is impossible to start the service. This is very useful in disabling dangerous and unknown services.

Syntax

systemctl mask service_name

Example

systemctl mask httpd

Unmask the service

Syntax

systemctl unmask service_name

Example

systemctl unmask httpd

Using Targets (Runlevels)

Targets are basically intended to bring the server into a specific state. Many services and other units start and stop to bring the server to desired state. Multiple targets can be active at the same time.

To see all of the targets available on your system

systemctl list-unit-files --type=target

View the default target

Described in /lib/systemd/system/default.target that systemd tries to reach at boot.

systemctl get-default

To change the default target that will be used at boot

Syntax

systemctl set-default target_name

Example

systemctl set-default multi-user.target

List units tied to a target

Syntax

systemctl list-dependencies target_name

Example

systemctl list-dependencies multi-user.target

Predefined target

| Target | Discerption |
| rescue.target | Single user mode. |
| multi-user.target | Non GUI multi-user console access |
| graphical.target | A GUI session. |
| custom.target | custom defined targets. |
| emergency.target | The most minimal environment for system repair. |

Shutdown or Reboot

Shutdown using systemctl

systemctl poweroff

To reboot

systemctl reboot

To boot the server in rescue mode

systemctl rescue

Enabling and disabling services

To configure any service to start at boot time we use  systemctl enable command. This command creates link file in the /etc/systemd/system/ directory. When you disable any service systemctl removes the link file for this directory.

Configure service to start automatically

Syntax

systemctl enable service_name

Example

systemctl enable httpd

Disable service automatic start

Syntax

systemctl disable service_name

Example

systemctl disable httpd  

Checks whether a service is enabled

Syntax

systemctl is-enabled service_name

Example

systemctl is-enabled httpd

List enabled services (automatic start at boot)

systemctl list-unit-files --type service

Know more about services

Syntax

systemctl cat service_name

Example

systemctl cat httpd

or

Syntax

systemctl help service_name

Example

systemctl help httpd

Chapter 17  

# Users and Groups

User and group

A user is anyone who uses a computer or network service. A user can be ether human or an account. For better management, the users are grouped together in groups. Group is logical entity to organize users together based on their different properties, it can be either based on same department, same place or same work. Sometimes groups are just made to provide certain common facilities or right to different users. When you create a user in Oracle Linux, by default each user is given a corresponding group with the same name known as User Private Group (UPG). For user and group management you can use both command line and GUI mode.

Group provides following benefits: -

*   Easy user management
*   To share same resource with a number of users.
*   Easy permission and right assignment.

User Management Commands

Create a new user

Syntax

useradd options username

Example

useradd user3

The bellow command will create user acct1 and -c option adds description (comment) for the user

useradd -c accounts acct1

Now when you check /etc/passwd it will show like that

acct1:x:1002:1002:accounts:/home/acct1:/bin/bash

Modify user

Syntax

usermod

Example

usermod -c finance acct1

Delete user

Syntax

userdel

Example

userdel acct1

Change or display user password expiry information.

Syntax

chage options username

Example

show account aging information

chage -l user3

Change the maximum numbers to 90 for password change

chage -M 90 user3

Change user password

Syntax

passwd username

Example

To change own password

passwd

To change other user password if you have administrator rights

passwd user3

Group commands

Add group

Syntax

groupadd option groupname

Example

groupadd finance

Delete group

Syntax

groupdel option groupname

Example

groupdel finance

Modify group

Syntax

groupmod options groupname

Example

groupmod -n finance1 finance

in this example change the group name of finance to finance1

Print the groups of the user

groups

Change the group membership

Syntax

Groupmems option groupname

Example

groupmems -g finance -a apache

List all groups on the system

less /etc/groups

User ID

UID stands for user identifier. A UID is a number assigned to each user. Linux kernel identifies each user internally through its ID. UIDs are stored in the /etc/passwd file. User ID for root user is 0 and all system users id is less than 1000\. All user normal users id start from 1000 onward.

You can check this in the /etc/login.defs file

grep -E '^UID_MIN|^UID_MAX' /etc/login.defs

To view a user's list of groups, UID and GIDs

Syntax

id user_name

Example

id user2

Check own groupid and userid

id

List all normal users on the system

Now you have the minimum and maximum range of normal, to list all normal users

awk -F'[/:]' '{if ($3 >= 1000 && $3 != 65534) print $1}' /etc/passwd

/etc/passwd file

/etc/passwd file hold the list of all users on the system both system users and normal users. The format of the file is that each line represents a user. The fields in each line are separated by : (colons). The fields have following information

1 User Name

2 The encrypted password (show x, actual location of encrypted password is /etc/shadow file)

3 User ID number (UID)

4 Group ID of user (GID)

5 User full name

6 Home directory

7 ![](Images/image00410.jpeg)Login shell

List of all users on the system

awk -F':' '{ print $1}' /etc/passwd

Group ID (GID)

Groups in Linux are defined by group IDs (GIDs).  GIDs are stored in the /etc/groups file. The first 1000 GIDs are usually reserved for system use. All application groups start from 1001 onward.

/etc/group file

/etc/group is a file that defines the groups of each user. Multiple users can belong to same group. Each user name in the same group is separated with commas.  The fields have following information: -

1 Name of the group.

2 Password: Generally, password is not used, hence it is empty/blank. If it is not blank, then stores encrypted password. This is useful in implementing privileged groups.

3 Group ID (GID)

4 Users list separated by commas.

![](Images/image00411.jpeg)

Chapter 18  

# Exploring SU and SUDO

To elevate the privilege assigned to the current user you can either use su or sudo.

SU

The su command is used to switch to another user. If executed without a username, it will login as root user by default. su requires the password of the target account.

To login as specific

Syntax

su username

Example

su oracle 

when used with a hyphen (su -) assume the user environment of the target user.

Example

For root user

su -

For other user

su - oracle

sudo

sudo allows users to run programs with the security privileges of another user, by default, it uses administrator’s privileges to run commands. It is mechanism by which you can assign some administrator task to less privileged users without sharing administrator password. Unlike su which requires the password of the target account, sudo requires the password of the current user. Precede command with  sudo to execute any administrative command.

Example to run privilege command which changes system configuration

sudo yum install gzip

or change hostname

sudo hostnamectl set-hostname host2021

Run command as different user.

Syntax

sudo -u user command

Example

sudo -u user2 hostnamectl

Use sudo in interactive mode

sudo -i

Changing the sudo Configuration

Sudo stores its configuration in  /etc/sudoers file. To modify the sudo configuration, use the command  visudo command. It effectively starts the vi editor and edits as the /etc/sudoers file. The visudo command should to be executed by administrator.

The  /etc/sudoers file contains a list of users, and what commands those users can run.

user host=(users) [NOPASSWORD:]commands

Example

%operators localhost = (apache) /usr/sbin/

Wheel group

![](Images/image00412.jpeg)Oracle Linux comes with default administrator group known as wheel group if you want to assign all administrator rights to a user without sharing root password you can add that user in wheel group. But before that make sure the line in  /etc/sudoer file it is not commented out.

To add user in wheel group

usermod --append -G wheel user_name 

Example

usermod --append -G wheel user1

Note: The main difference between SU and SUDO is that in case of SU you seek root permission through switching to superuser or root user, where as in case of SUDO you seek root permission through a single command.

Chapter 19  

# Exploring File and Directory Permissions

Linux is a multi-user operating system which can be accessed by many users simultaneously. Therefore, it becomes utter necessary that users do not touch each other’s data. For security and sanity of the data and system files, the operating systems deploys different type of security system. Linux divides authorization into 2 levels.

*   Ownership
*   Permission

Ownership

Ownership defines who can access the file or directory. To represent the ownership Linux uses following symbols:

| Symbol | Description |
| u | User (owner)By default user who creates the file or directory becomes the owner of the file or directory. |
| g | Group |
| o | Other, Grants permissions to other users. Practically, it means everybody else. |

Permission

Permission defines action allowed on the file or directory. These actions are read write and execute.  There are two ways to represent the permissions:-

1 Symbol

2 Numbers

Symbols

To represent the file permissions following symbols are used:

| Symbol | Permission |
| r | Read |
| w | Write |
| x | Execute |

Execute permission for directory allows user to access the content of the directory.

Numeric representation of permissions

To view the permissions in numerical format each permission has a numeric value:-

| Number | Permission |
| 1 | Execute |
| 2 | Write |
| 4 | Read |

We use sum to represent the net permissions . 

| Sum | Symbol | Permission |
| 0 | - | No permission |
| 1 | --x | Execute permission |
| 2 | -w- | Write permission |
| 3 | -wx | Write and Execute permission |
| 4 | r-- | Read permission |
| 5 | r-x | Read and Execute permission |
| 6 | rw- | Read and Write permission |
| 7 | rwx | Read, Write and Execute permission |

![](Images/image00413.jpeg)Now let’s see how we use them practically. This is the output of  ls -l command :-

Other object types

In the above command output you can see other objects like

| Code | Object type |
| – | Regular file |
| d | Directory |
| l | Symbolic link |
| c | Character device |
| b | Block device |

Mask

Umask or user mask is the assigned default permissions when we create new file or directory.

Check umask value

umask

To change the current session umask value. 

umask 0044

To calculate the umask value just subtract the desired permissions from the default one:

777-755 = 022

To set permanently use  /etc/profile file for all users. For individual user change  ~/.profile or ~/.bashrc file.

Permissions command

chmod is the command to manage permissions

Add permission

Syntax

chmod +permssions filename

Example

chmod +x para.sh

This command will add execute permission to the file

Remove permissions

Syntax

chmod -permssions filename

Example

chmod -x para.sh

you can add or remove multiple permissions at same time

chmod +xw para.sh

Removing permissions for group

Syntax

chmod g-permission filename

Example

chmod g-xw para.sh

Remove permission for others

Syntax

chmod o-permission filename

Example

chmod o-xw para.sh

Like you can add and remove permissions for group and others at same time.

chmod go-xw para.sh

Changing permissions using numeric value

This the most popular way for changing permissions

Syntax

chmod permissions filename

Example

chmod 700 hello.txt

this will give all permissions to the user and remove all permissions from others and group.

Change ownership

chown command can be used to change the ownership of the file or directory

Change the Owner of a File

Syntax

chown username  filename

Example

chown user2 para2.sh

Change the Owner and Group of a File

Syntax

chown username:group  filename

Example

chown user2:group2 para2.sh

Change only the group

Syntax

chown :group  filename

Example

chown :user2 notes.txt

Recursively Change the file ownership

To recursively change ownership of the directory and its files

Syntax

chown -R user:group directory

Example

chown -R user2: /home/timetable

Chapter 20  

# Network Time Protocol

NTP is Network Time Protocol used to sync the time of computers. Computers worldwide use the Network Time Protocol (NTP) to synchronize their times via a hierarchy of NTP servers. The primary servers are at stratum 1 connects to stratum 0 via satellite, radio or modems. 

On Oracle Linux 8  Chrony provides implementation of NTP. Chrony is designed for systems that are often powered down or disconnected from the network like laptops. Chronyd is the daemon that runs in user space and uses chrony.conf file. The NTP has two components.

*   Server
*   Client

Clients connects to server for time synchronization. NTP provides high degree of time synchronization of computers on a network. Time synchronization is very important for logs management, login information and in some cases transaction fails if the time is not same on the two machines.

Configuring chrony on server

Install chrony package

yum install chrony

The main configuration file is  /etc/chrony.conf. Edit this file and add bellow parameters.

server Ip_of_the_stratum

Example

server 192.20.3.1

If this server is in isolated network

local stratum 10

You can restrict the usage of NTP server for a host or network

Syntax

allow network/hostIP

Example

allow 192.116.1.0/24

Save the file

Now enable and start chronyd daemon

systemctl enable chronyd

systemctl start chronyd

chronyc is a command-line program to verify the configuration. It has many options. The two main options are :-

| tracking | Displays system time information |
| sources | Displays information about current sources and other information about source. |

Verify

To verify if chrony is working

chronyc tracking

also you can use

chronyc sources

On the client

Install chrony package

yum install chrony

Edit  /etc/chrony.conf and add the IP address of the NTP server

server IP_address_NTP

Example

server  192.116.1.123

Save and close the file

Now enable and start chronyd daemon

systemctl enable chronyd

systemctl start chronyd

Configure ntpdate

The purpose of the ntpdate service is to set the clock during system boot.

Edit  /etc/ntp/step-tickers

Add entries of server IP

Example

192.116.1.123

Enable ntpdate and start

systemctl enable ntpdate

systemctl start ntpdate

Verify

chronyc sources

Chapter 21  

# Exploring Secure Shell - SSH

SSH is secure protocol for login to remote network. SSH works on server client basis on the server sshd daemon is running and on client it connects using ssh client. Openssh is an implementation of ssh on most of the Linux distribution. Oracle Linux 8 also supports openssh as ssh server.

Install openssh server

yum install sshd

Enable and start sshd daemon

systemctl start sshd

systemctl enable sshd

The main configuration file used by openssh server system-wide is /etc/ssh/sshd_config. By default, it is configured in restrictive manner. The common settings which can be changed in sshd_config file for power users and developers are following :-

X11Forwarding yes

AllowAgentForwarding yes

PermitRootLogin yes

After the modification in the configuration file stop and start the sshd service.

systemctl stop sshd

systemctl start sshd

On the client

ssh  login@server_ip

Example

ssh root@192.168.3.1

On windows machine use putty software as ssh client to connect server.

Chapter 22  

# Secure System with Firewall

Firewalld is a firewall management solution available in the Oracle Linux Linux 8\. Firewalld is frontend for the iptables packet filtering system provided by the Oracle Linux kernel. In this Chapter, we will cover how to set up a firewall for Oracle Linux server and basics of managing firewall.  firewall-cmd is the command line administrative tool for managing firewall.

Basic concepts of firewall

Zones

Zonesare groups of settings that are applied to the computer depending on where the computer is connected. Zones may contain connection settings and connection security settings. Zones defines level of protection for your computer. The zones are connected to networking interfaces or assigned a range of addresses. Predefined zones are

| Zone | Description |
| drop | least trusted zone in which only outgoing connections are possible. All inbound connections are rejected without reply. |
| block | Only outgoing connections are allowed and incoming connections are rejected with an icmp-host-prohibited message. |
| public | This setting is applied when system is connected to less secured network like direct connections to public internet. Only selected incoming connections are allowed. |
| external | Uses NAT masquerading so that your internal network remains private . |
| internal | Trusted zone both way connections are allowed. |
| dmz | Applied in DMZ or isolated computers where only confident incoming connections are allowed. |
| work | Trusted zone with more services allowed. |
| home | Trusted zone with many services are allowed. |
| trusted | Trust all of the machines in the network. |

Rule Duration

In firewalld, rules can be designated as

*   Permanent
*   Runtime.

PermanentRules will be available even after reboot .

RuntimeRules which are available only now not after reboot. 

Rule types

You can configure rules for specific

*   Program
*   Port
*   Predefined services: those service which are in the database of firewall for allowing and blocking rules.
*   Custom

Install and Enable Your Firewall service

yum install firewalld

Start

systemctl start firewalld

Enable

systemctl enable firewalld

Displaying firewall configuration

Display all zones

firewall-cmd --get-zones

Display detailed information about all zones

firewall-cmd --list-all-zones

Display information about specific zone

Syntax

firewall-cmd --zone=zone_name --list-all

Example

firewall-cmd --zone=public --list-all

Display selected zones

firewall-cmd --get-default-zone

Display Active zone

firewall-cmd --get-active-zones

Change firewall rules

Change zone of interface

Syntax

firewall-cmd --zone=zone_name --change-interface=interface_name

Example

firewall-cmd --zone=internal --change-interface=eth1

Change default zone

Syntax

firewall-cmd --set-default-zone=zone_name 

Example

firewall-cmd --set-default-zone=internal 

Change runtime rules to permanent

firewall-cmd --runtime-to-permanent

Implement permanent rules in runtime

firewall-cmd --reload

This command will reload the setting of firewall and use the permanent settings.

Allow service

First check if this service is in the list of predefined services

firewall-cmd --get-services

List the current configuration and see list of allowed services

firewall-cmd --list-services

Add

Syntax

firewall-cmd --add-service=service_name

Example

firewall-cmd --add-service=ssh

Make current configuration as permanent

firewall-cmd --runtime-to-permanent

Add service to different Zone

Syntax

firewall-cmd --add-service=service --zone=zone_name

Example

firewall-cmd --add-service=ssh --zone=public

Remove service from allowed list

Syntax

firewall-cmd --remove-service=service_name --zone=zone_name

Example

firewall-cmd --remove-service=ssh --zone=public

After this command save current configuration as permanent

firewall-cmd --runtime-to-permanent

Add port

List all allowed ports

firewall-cmd --list-ports

Add port

Syntax

firewall-cmd --add-port=port_no/port_type

Example

firewall-cmd --add-port=1191/tcp

Save current configuration as permanent

firewall-cmd --runtime-to-permanent

Working with zones

Add new zone

List all zones

firewall-cmd --list-all

View the default zone

firewall-cmd --get-default-zone

View Information about zone

Syntax

firewall-cmd --zone=zone_name --list-all

Command

firewall-cmd --zone=public --list-all

View Active Zones

firewall-cmd --get-active-zones

Stop firewall Service

systemctl stop firewalld

Disable firewall service

systemctl disable firewalld

Check the status of firewall

firewall-cmd --state

Check the permanent configuration

firewall-cmd --check-config

Reload the configuration

firewall-cmd --reload

GUI Firewall Management

You can also use graphical interface for firewall

Install firewall-config

yum install -y firewall-config

Use

![](Images/image00414.jpeg)![](Images/image00415.jpeg)Press Activities then in the search bar write  firewall and click firewall icon

The interface is self-explanatory

Changing the Firewall Settings

Changing Configuration

![](Images/image00416.jpeg)When you start the interface, by default Runtime configuration is selected from the configuration dropdown menu for immediate change in the current firewall settings, alternatively to apply the setting on next system start or firewall configuration reload, select Permanent from the drop-down list.

Change zone of Connection 

![](Images/image00417.jpeg)To configure or add connection to a zone start firewall-config, from the Options menu select Change zone of connections. It will show sub menu with list of connections available, select the desired connection from the dropdown menu. From next dropdown menu, select the Zone.

Set default zone

![](Images/image00418.jpeg)To set the default zone for new interface or change the default zone for an existing interface. First select the desired connection then select Options from the menu bar, and select Change Default Zone from the drop-down menu. Now select the require zone from the list Menu.

Configuring services

Firewall-config tool provides interface to enable and disable predefined or custom services. First, select the zone for which, service you want to configure. Next is to select or deselect the service check box. Selected check boxes are for enabled services and cleared (un-selected) check-boxes are of blocked services. 

![](Images/image00419.jpeg)

Chapter 23  

# Exploring Cockpit

Cockpit is a Web based server management tool available for Oracle Linux 8\. It is default server management tool. Cockpit is a very useful Web based GUI tool with which you can monitor and manage multiple Linux servers. Cockpit also allows you to manage networking, storage on servers, containers, virtual machines. Logs management is quite easy with cockpit.

Installation.

If Cockpit is not already installed on the system then you can install it using following command.

yum install -y cockpit

Start and enable the service

Run the following command to enable and start cockpit service.

systemctl start cockpit.socket

systemctl enable cockpit.socket

Check the status of the service

systemctl status cockpit.socket

Access Cockpit

Open web browser on your PC or on the server and type url :

https://<Your_serever_IP>:9090

Example

https://192.168.1.128:9090

If you are opening on the same server, you can use also use localhost instead IP address.

![](Images/image00420.jpeg)

Chapter 24  

# Logs management

Logs are very important part of any operating system. logs are very helpful in troubleshooting and auditing of system. Oracle Linux keeps it most of the logs in central location  /var/log directory. One of the important file is  /var/log/messages where Oracle Linux logs the kernel / core system logs.

Journalctl

Journald is the service used for collecting and storing the logs data in the Oracle Linux. This service is used to manage the system log which includes boot messages, kernel logs, syslog messages, service messages and system error messages etc. By default, it keeps all logs in the memory and store logs only in a small ring-buffer in  /run/log/journal directory. if persistent log configuration is enabled then it start storing logs under /var/log/journal directory.

Configuration file

The main configuration file for journald is /etc/systemd/journald.conf.

Change the logs to persistent

if you want save the logs permanently on your system you can configure storage variable in the configuration file to auto or persistent.

[Journal]

#Storage=auto

#Compress=yes

#Seal=yes

#SplitMode=uid

#SyncIntervalSec=5m

#RateLimitIntervalSec=30s

#RateLimitBurst=10000

---truncated ---

List the logs from the oldest entry

journalctl

List the logs from current boot

journalctl -b

List logs from yesterday

journalctl --since yesterday

List logs  by specific Process ID

Syntax

journalctl  -F _PID=PID

Example

journalctl  -F _PID=2451

View running logs

journalctl  -f

To stop the view press Ctrl + C

View specific number of recent entries

journalctl  -n10

This command will show last 10 entries

The log entries of specific priority like all errors

journalctl -p err

To view all entries with warnings

journalctl -p warning

Rsyslog

Rocket-fast Syslog Server or rsyslog is the very popular and old  processing system used by most the Linux distributions. The log files contain messages about the system, kernel, services, and applications. Oracle Linux 8 uses Rsyslog as default logging service. Journald forwards all logs to rsyslog. Rsyslog  stores all logs forwarded by journald in plain text format files under  /var/log/ directory. The main configuration file of Rsyslog is  /etc/rsyslog.conf. Configuration file contains rule lines to store log messages. It has following parameters: -

*   Facility
*   Priority
*   Actions

| Facility | Facility is process or application generating message, Using * means all facilities. |
| Priority | Priority is type of log message, codes are emerg for emergency, alert, crit for critical errors, err all errors, warn for warnings, notice, info, debug. Using * means all priority levels. |
| Action | Action decides what action must be taken for the matched rule. |

In the bellow example Facility is mail, Priority is all errors and Action is log messages to mail.err file 

![](Images/image00421.jpeg)

Rsyslog can also be used for log forwarding to central log server.

Chapter 25  

# Understanding Processes 

Any program executed by the user or system starts process or processes to accomplish the task. Each process has its own process ID. The process ID is always unique during the lifetime of the process.  There are two type of processes: -

| Foreground | A foreground process is any command or task you run directly on the terminal and wait for it to complete. Some foreground processes also require user interaction. |
| Background | Unlike foreground process shell does not wait for process to complete.  The background processes are non-interactive in the nature.  |

Daemons

These are the special processes which runs in the background and generally not effected by user login and logout. There are two types of daemons one which starts with system start others   which gets triggered by process or command.

Child and parent process

When a process starts any new process, the new process is known as child process and the process which starts the process is known as parent processes. One parent process can have multiple child processes. 

The Init process

The init process is mother of all processes. It is the first program that executes when Linux system start. Therefore, the Init process is parent process of all other processes.

The process id of the init process is always 1. 

When processes die and its child processes are still active. then these child processes are known as orphan process. The init process adapts any orphan running process in the system.

Find the process ID

As mentioned each process has its own process ID. This process ID is very important for the system, as Linux internally recognise the process with its ID. To find out the processes ID of any running program

Syntax

pidof program_name

Example

pidof systemd

Listing all processes.

Prints the processes of the current shell 

ps

List all active processes on the system

ps -e

List all process with Username

ps -eu

Show detailed process list

ps -aux

or

ps -ef

These above two commands show detailed information about the processes which includes process id and parent process ID.

Top

Top is another command to list the processes, process id and resource utilization summary.

top

![](Images/image00422.jpeg)On the top screen press q to exit

Control the processes

To stop the running process

To stop the process first check its ID

Syntax

ps -ef | grep process name

Example

ps -ef |grep http

To stop

Syntax

kill PID

Example

kill 234

Kill the process immediately forcefully without clean up

Syntax

kill -9 PID

Example

kill -9 234

Start process in background 

To start any command in the background, add ampersand mark (&)

Syntax

program &

Example

tar -xvf mytest.tar . & 

To move the running process to background press Ctrl +Z

tar -xvf mytest.tar .  

^Z

To check the background process

bg

or

jobs  

Move background process to foreground

Syntax

fg %jobid

Example

fg %2

Changing Priority of process

Every process which executes on the system has scheduling priority. Priority decides which process will run first when CPU executes the process. Processes with a higher priority will be executed before those with a lower priority. The processes with the same priority executes one after the next.

Nice and renice

You can change the priority of jobs scheduling using nice and renice commands. by default, when you start any process it start with 0 priority and you can change the priority with nice command from -20 to +19\. where -20 is the lowest priority and +19 is highest priority.  

To modify the priority of process at the time of starting use  nice command

Syntax

nice -n priority command

Example

nice -n 5 tar -xvf testdox.tar .

Change the nice value of running process

Syntax

renice -n priority -p process_id

Example

renice -n 5 -p 1235

Check the nice value of all process   

Syntax

ps -eo pid,ni,comm

Check the nice value of specific process

Syntax

ps -eo pid,ni,comm | grep command

Example

ps -eo pid,ni,comm |grep cron

Only root user can change the nice value of other user’s processes and system processes.  

Chapter 26  

# Monitoring Your System

System monitoring is vital task for system administration. System monitoring avoid the abrupt system failure and denial of services

Viewing System Processes

To List the process

ps 

Top command is multipurpose monitoring tool also can be used for processes monitoring

top

Viewing Memory Usage

The free command shows the memory snapshot including total, available and free memory

free

To display memory in GB

free -g

Viewing Block Devices

Block device in Linux is device that supports reading and writing data in fixed-size blocks. it is usually hardware device exposed to the Linux user for further use.

List available block device 

lsblk

List device UUID of Block device

blkid

Displays a list of disk partitions of selected device

Syntax

partx -s device_name

Example

partx -s /dev/sda

List currently mounted file systems in tree format 

findmnt

Orderly list of currently mounted file systems

findmnt -l

Display the list of currently mounted file systems with usage information

df

By default, df command shows the partition size in 1 kilobyte blocks, to 

Display the list in human readable format i.e. Mega Bytes and GB

df -h

Display the amount of space being used by files in a directory

du

By default, du displays the disk usage in kilobytes, to view in human readable format i.e KB, MB and GB

du -h

To view the grand total usage of the directory

du -sh

Viewing Hardware Information

Lists all PCI devices currently installed in the system

lspci

Display detailed information about all PCI devices.

lspci -v

To display more detailed information about all PCI devices.

lspci -vv

List all USB device present in the system

lsusb

List detailed information about all USB device present in the system

lsusb -v

List all pcmcia devices

lspcmcia

Display more information about PCMCIA devices

lspcmcia -v

Display information about CPUs

To view CPUs, cores , threads, vendor, family, model, etc

lscpu

or 

cat /proc/cpuinfo

The main information in this output can be

| CPU | The logical CPU number |
| CORE | The logical core of CPUs. |
| SOCKET | The logical sockets . |

Display hardware information

lshw

Display summary of hardware information

lshw -short

Display kernel information

uname -rv

Display hostname

hostname

Display Oracle Linux version

cat /etc/oracle-release

Hardware monitoring

Monitor all hardware resources like CPU, Memory and network in one screen

top command is the most used command with summary of all hardware resources information

top

CPU monitoring

To monitor CPU over committing you can use

SAR

sar command is system activity reporting tool.

Install sar command

yum install sysstat

The use sar command to monitor system

Syntax

sar time number_of_sample

Example

![](Images/image00423.jpeg)sar 2 3

Monitor memory

vmstat command can be used to view the memory and swap space usage.

Syntax

vmstat delay count

Example

vmstat 2 3

This command will take 3 samples each after 2 seconds.

Display memory summary

vmstat -s

To monitor IO devices

iostat

List open files

This command will display all open files with respective processes

lsof

You can use grep command with this command to filter the process or file.

Network

Monitor network multiple commands are there

Display all listening ports

netstat -a

Display only tcpip listening ports

netstat -at

Display all ports

netstat -tunlp

Display routing table and with default gateway

netstat -r

tcpdump

tcpdump command mostly used as network packet analyser or packets sniffer program for TCP/IP. This command analyse all network traffic pass through your computer. To use this command, you should have thorough knowledge of tcpip protocol.

Syntax

tcpdump -i interface_name

Example

tcpdump -i eth0

ss

SS utility show the network socket related information

To display all listening ports

ss -l

Display the uptime (how long the Oracle Linux system has been running)

uptime

NFS statistics 

nfsstat

to view only server side statistics

nfsstat -s

To view only client side statistics

nfsstat -c

Display information about mounted NFS file systems.

nfsstat -m

Graphical Gnome system monitor

The System Monitor application allow you to monitor the condition of the system at any instance. Moreover, you can collect valuable information about applications. It provides following information:-

*   Monitor CPU, memory, swap space and network.
*   Monitor processes and their properties
*   Control process behaviours
*   Search for open files
*   Shows disks and mounts information

Process Tab

Shows all running processes of the system with their CPU usage, memory usage, disk usage etc. Right click the process to manipulate the selected process.

![](Images/image00424.jpeg)

![](Images/image00425.jpeg)Resource Tab 

Shows all the hardware resource usage and history in graphical format.

![](Images/image00426.jpeg)Filesystem Tab

Shows mounted file system and their percentage of usage.

Chapter 27  

# Automating your System

Automation of system makes job of administrator easy and reduces the number of mistakes during repeated tasks. Linux offers scheduler for handling regular jobs.

Cron is a time-based job scheduler available in Oracle Linux to run commands at given times of intervals. Other than system wide cron table, each user can have separate cron table to execute schedules jobs.

The system wide cron table file is  /etc/crontab. /var/spool/cron/ directory contains  cron table  files for each user.

To Add or edit the cron job

crontab -e

This command will open crontab file for the user in the vi editor. you can add or change the crontab.

The format of cron file is

Minute Hour DayOfMonth Month DayOfWeek [user-name] command

Example

0 1 *  *  *     /opt/backup.sh

In this example the backup script will execute at 1 am every night.

Where * stands for every value, like * in the day of month field is for every day of month, * for the month field stands for every month and * for the day of week is for every day.   

User Access Control

As crontabs can be very harmful for the system you can control the access of users to use crontab file for scheduling jobs using /etc/cron.allow and /etc/cron.deny files. Add the username in either of the two files to allow or deny the access to the crontab. To avoid the confusion, if the cron.allow file is present in the /etc directory then cron.deny file will not be used. If both files are not present than only root user can use crontab file.

List the crontab entries

crontab -l

To delete user's crontab

crontab -r

root user can change the crontab of other users, using -u parameter

Example

crontab -u user2 -l

At

Unlike cron, which let you run a task on a regular basis at specified date and time,  at command is mostly used for scheduling adhoc jobs. The  at command is controlled by  atd daemon. To use  at command scheduling atd daemon should be in running state.

Install

yum install at

To start and enable

systemctl start atd

systemctl enable atd

Check the atd daemon state

systemctl status atd 

To add the job

at command with time and number of days from now. 

at 4pm + 3 days

This command will open the interactive at prompt to write the command or script name you want to schedule at the 4 PM 3 days later.  Press Ctrl +d key to exit at prompt.

To add the job without interactive prompt

at time -f scriptname

Example

at 4pm + 3 days -f /etc/opt/backup1.sh

To list the scheduled jobs

atq

To delete a scheduled job

atrm job_number

Example

atrm 3

Chapter 28  

# Resetting forgotten root password

To reset the unknown root password use following procedure:-

1 Reboot the machine and at GRUB menu press  e key.

2 ![](Images/image00427.jpeg)Look for line starting with Linux and move the cursor to end of the line using Ctrl+e and write  rd.break.

3 Press Ctrl + x key.

4 It will give prompt with read only root file system.

5 Remount the file system to Read into write mode

mount -o remount,rw /sysroot

6 Change the root directory

chroot /sysroot

7 Change password

passwd

8 Create file autorelabel to enable the SELinux relabeling process on the next boot.

touch /.autorelabel

9 Write  exit and press enter.

10 ![](Images/image00428.jpeg)Write  exit and press ENTER again to start the system in normal mode.