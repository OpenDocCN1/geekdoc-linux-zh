![](images/00002.jpeg)

Linux For Beginners

The Ultimate Guide to Linux Command Line, Linux Programming and Linux Operating System

Table of Content

[Introduction](#part0000_split_002.html_intro)

[Chapter 1 – History Highlights](#part0000_split_003.html_ch1)

[Chapter 2 – Installing Linux](#part0000_split_007.html_ch2)

[Chapter 3 – The Shell](#part0000_split_017.html_ch3)

[Chapter 4 – File Globbing](#part0000_split_024.html_ch4)

[Chapter 5 - User Management](#part0000_split_027.html_ch5)

[Chapter 6 - Linux Tips and Tricks](#part0000_split_033.html_ch6)

[Chapter 7 - Vi Editor](#part0000_split_040.html_ch7)

[Conclusion](#part0000_split_047.html_conclusion)

Introduction

This book is for all computer userseager to learn or consolidate bases acquired in the field.
As you will know when reading this book, there are different distributions of the Linux kernel. In this book we will focus a little more on the Redhat distribution because we consider it as the easier one to install and use. In the following chapters, important methods and Linux administration commands are presented and detailed.

A lot of computer users tend to avoid Linux for its “complexity” and “sophistication”. This book is specially written and tailored to prove those people are wrong.

This book really popularizes and simplifies the Linux operating system and its usage while following a good methodology. Linux for beginners covers all the important facets which all beginners should know about. I am asking you to imagine yourself using this great OS without having any difficulties or fogginess about it.

Reading and understanding this book will make it happen.In the beginning we will explore Linux history and genesis so we can have a clear vision and be methodological. Then, we will learn and understand how to install the system knowing the necessary equipments and devices needed to have an operational OS running.

We will also learn about the shell which is very important and all the relative commands. And of course we must not forget about command lines which are really useful and commonly used. File globbing will be covered too; it’s really indispensable for Linux beginners to know about.

Then we will hit user’s management and authenticating which will certainly help you secure data and manage access rights for all users. By the end, just to make it complete and really useful for Linux learners and beginners, we included some very important Linux tips and talked about the Vi editor which is really an interesting thing to know about.

Chapter 1 – History Highlights

In this chapter we will explore and learn about our OS history which is very important. Also, once you are done reading it, you will know about a lot of general information indispensable for Linux beginners.

## History and genesis of Linux

Linus B.Torvalds is behind this entirely free OS. In the early 90s, Linus wanted to develop his own OSand present it as his graduation project. He was intended to develop a UNIX version that runs on a 80386 type architecture.Minixwasthe first UNIX clone running on PC, written by Andrew Tanenbaum. Linus Torvalds then decided to expand the possibilities of Minix, creating what would become Linux. Amused by this initiative, many people contributed to help Linus Torvalds to complete this system, so that in 1992 a first version of the system was launched with almost no bug.

With the increasing number of developers working on this system, it has been able to integrate quickly free redevelopments of tools present in commercial UNIX systems. New tools for Linux now appear at breakneck speed.

The originality of this system lies in the fact that Linux was not developed for commercial purposes. Indeed no line of code has been copied from the original UNIX systems (Linux, in fact draws on many commercial UNIX versions: UNIX System V). So everyone, since its inception, is free to use but also to improve it.

Although Linux was initially designed to run on PC, it has now been developedand adapted to many other platforms such as SPARC stations, Macintosh,and even platforms such as personal assistants (PDA), even videogame consoles!

## 
Core concepts and distribution

Linux is built around a kernel responsible for taking care of the equipment. We call distribution assembling a set of software around a Linux kernel to provide a turnkey system. The kernel of a distribution can be updated to allow for the inclusion of recent material; however this operation consisting in rebuilding the kernel is difficult because it requires a certain level of knowledge of the system and equipment. The kernel recompilation is reserved for specialists or users willing to make them unusable system to learn.

Most distributions also provide a graphical installation of their own and a package management system to automatically install software by managing dependencies (software under Linux is sometimes linked to external libraries or rely on other software).

Each distribution has its advantages and disadvantages. Indeed if some are more suited to beginners and offer advanced graphics interfaces, others prefer the security or scalability. The best known distributions are:

- The RedHat distribution

- The Debian distribution

- The SuSe distribution

- The Knoppix distribution

- Slackware

- The Mageia distribution.

## System features

Linux is an operating system similar to UNIX systems that can run on different hardware platforms: x86 (that is to say based platforms Intel, AMD, etc.), Sparc, PowerPC, Alpha, ARM, etc. So the Linux system can operate both on personal computers as game consoles or personal assistants!

Linux is therefore a multi-platform system. It is also multi-user (several people can simultaneously work on the same computer), but also multi-task (several applications can be run simultaneously without any of them affects the other) and multiprocessor.
Linux is considered a reliable, robust and powerful. It is also capable of operating with very few resources on low end computers very few powerful.

The Linux system has the following advantages in particular:

- Support for Internet standards, that is to say, TCP/IP protocols, the groupof Internetprotocols. Linux is a free way to create a local network to connect to the Internet and to set up a server.

- More security due to its sourcecode’s transparency and the responsiveness of the community during the vulnerabilities advertisements.

- A partitioning of memory space and disk space coupled with a sharp rights management to manage large numbers of users with minimal risk.

- A fully configurable nucleus depending on the hardware of the machine on which the system is installed to maximize performance.

Chapter 2 –Installing Linux

This chapter is really useful since it covers a lot important details and proposes the best solutions for Linux beginners.

## Necessary material

Linux does not require the latest computer with minimal configuration:

- a 386SX processor minimum

- 4MB of memory (8MB recommended)

- a hard disk controller and a disk with free 20MB (100MB recommended) (Linux is able in practice to operate from a single disk)

- a CD-ROM

Regarding appendices devices, common hardware components on the market will have much more chance of being supported by Linux...

## Prerequisite

Linux can be installed in addition to the operating system already installed on your machine. Make sure before you start installing the file system is healthy by using a program such as scandisk or chkdsk to verify the integrity of the reader, because Linux makes use of much more muscular than the DOS disk e.g.

## Installation Phases

Installing Linux is done in several phases to implement a file system supported by Linux (ext2fs) on one or several dedicated partitions and then to proceed with the installation itself, finally configure the kernel before booting from disc, the steps are the following:

- creating floppy disks

- system boot from the diskette

- creating the primary partition of the hard drive

- creation of the swap partition

- creation of the file system

- Linux Installation

- Kernel Configuration

- system reboot

## Creating boot and root disks

Through floppy disks to boot the system with minimal Linux kernel we will be able to install Linux. These disks will be created using a program to copy image files (all data to put on floppy disks) on a disk. These disks are two in number:

- Boot disk: containing a Linux kernel for booting the system

- Root disk: contains the installation software

The image file to be chosen in each case depends on the configuration of your system, it will be called:

- scsi, in the case of a SCSI CD-ROM drive

- sbpcd, in the case of a Panasonic CD-ROM drive or connected to a Sound Blaster Pro

- nec260, in the case of a CD-ROM Nec 260

- Mitsumi, in the case of a CD-ROM Mitsumi

- cdu31a, in the case of a CD-ROM or Sony cdu31 CDU33a

- cdu535, in the case of a CD-ROM or Sony CDU531 CDU535

It only remains for you for each of the two image files (boot and root) totype in the directory containing the proper image file "\rawrite", the program will ask you the name of the image file (scsi for example), then the drive (a:)

You can optionally create an additional disk for later use (e.g. if you plan to buy a SCSI card while you have an IDE CD-ROM drive ...).

## Booting from the boot disk

Once the disks created, restart the computer taking care to place the boot disk in drive a :.

After displaying some messages the system displays the line: "boot", press enter to proceed.The system then calls the root disk.

## Creating Partitions

To use Linux, you need to create a partition (preferably larger than 900MB to install all options) using the "Linux Ext2" file system and (optionally) a swap partition (virtual memory, that is, i.e. a part of the disk used in case of lack of memory) of tens of MBs.

Creating partitions can be done in different ways:

Under a Microsoft system before booting the system with the diskette boot:

- In Windows 9x, the software Partition Magic 4 makes it very easy to create ext2fs and swap partitions without losing data on the disk

- Under MS-DOS, with the fdisk software supplied as standard, which is more ergonomic than his colleague of the same name supplied with Linux

- There’salsoa DOS utility called fips. It allows performing operations on partitions.

On Linux, after starting the system. Next distributing the installation procedure is different:

- with Slackware type distributions you will need to enter the commands manually, that is to say format, partition, create the file system and installsuccessively

- withRedHat type distributions, these operations are automated, you will answer questions ...

When creating partitions, you will surely be asked the type of the previous partitions

Follow these steps:

- type 82 for the secondary memory

- type 83 for the main partition

- The primary partition must be within the range of the disc between the first and 1023àme cylinder!

- Note on a paper the size (in blocks) of the main partition and of the swap partition on a paper because this helps later

## Creating the file system

Under certain distributions you will be asked to create a file system before launching the installation (this is not the case, among other things, distributions RedHat 5.2 and Mandrake 6.0, for which all the following operations are automated through menus).

When you have created the main partition and the secondary memory partition (swap partition), this is to activate the secondary memory and create the file system of the root partition.

Activating the secondary memory is done with the command:

<<mkswap -c partition size>>

For example, for a secondary memory using 10000 blocks on the second partition of the second disc (hdb2) command would be:

<<mkswap -c / dev / hdb2 11000>>

Then the “swapon” command to launch it

The creation of ext2 file system is done through the following command:

<<mke2fs -c partition size>>

for example:

<<mke2fs -c / dev / hda2 202137 >>

Installing RedHat

The RedHat distribution is currently one of the most acclaimed distributions given that the installation procedure is quite simple. In fact, this procedure simply asks you to make choices from a drop-down list for your main devices and for choices related to language or packages needed to be installed. Here are the different steps to be followed:

- Choice of language: choose the language in which the installation procedure will be

- Choice of keyboard

- Choice of installation support: If your Linux distribution is on CD, choose CD-ROM, otherwise, choose the Hard drive if the copy is downloaded.

- Choice of installation style: if it is an update of a previous system or a full install

- Type of installation: The system allows you to choose between workstation, server or customized. You have every interest to opt for custom configuration that will leave you more flexibility

- Choice of SCSI adapters: If you have a SCSI adapter, you should answer yes. The system will detect your hardware. If ever this automatic search is unsuccessful, you can simply enter a line of parameters enabling it to know what kind of SCSI adapter in question, as well as knowing his IRQ and memory address. One Card "AHA1520" to address 0x140 and IRQ 10 will be located in the command line: = aha152x 0x140,10

- Hard diskpartitioning: RedHat allows you to partition your disk at this level of the installation (if you have not done it previously) and leaves you the choice between disk druid and fdisk

- choose the hard drive: the software lets you choose from a list the hard disk on which to create the partitions

-Unnecessary partitionsRemoval: under fdisk using the "d" key you can delete unnecessary partitions (be careful not to delete your Windows partitions!)

-Creating Linux partitions: the “n” button and the “p” button will allow you to create root and swap partitions, and all other partitions you may need. U The first cylinder number of the partition and its size (in MB) will be required

-Change the partition type: with the key “t” you canallocate the type 82 to the swap partition, and type 83 to the Linux partitions ...

-fdisk output: by pressing the “q” key you exit fdisk abandoning the changes. By pressing the button “w” you save the changes before leaving

- Selecting mount points: a screen offers several partitions, at this point you need to select the one you would like to use and name them one by one, that is to say, specify the mount point. The root is mandatory, it is the master partition and must be named /. Each partition that you wish to use under Linux must be assigned a mount point (/home for example, or /mnt/dos for your DOS partition, if you want it to be mounted automatically after installation

- Selecting the swap partition: the system naturally asks you to select the partition that will be used as secondary memory

- Formatting partitions: you must select all new partitions that you have created. Be careful not to format partitions containing data!

- Choice of packages: this option requires you to simply select from a list, what to install

- Installing / copying packages: installs the system one by one all the required packages. This operation can be very long! (Up to half an hour ...)

- Network configuration: these computers with a network card (not a modem)

- Choice of the clock: Choose appropriate clock to your country

- Choice of start-up services: you can select from a list the services that will be activated at each start.

- choice of printer: a series of questions will allow you to configure your printer by choosing it from a list and specifying the port on which it is connected

- the password input: password You will be asked for the super user account (root), that is to say, a user who has all rights

Once you have completed all these steps, the computer will restart and you will be faced with a prompt indicating LILO: just type Linux to boot under Linux and dos to go to your DOS partition, on which is Windows 9 xs, DOS or other...

When booting under Linux and entering your super user name (root) and password, you willneed to install a graphical interface which will be friendlier than the console (text mode).

## Installing XFree86

XFree86 is a graphical interface under Linux (XWindow is the interface of the UNIX stations). To configure XFree86, just type "XF86Setup" in the command line, in capital letters. A screen appears asking you for information on your screen and to be paid the display. A graphical window then appears in which you have tabs to configure each of the hardware in your computer.

So we must first configure the mouse which is mostly a Microsoft mouse type (PS / 2 or if it is connected to a special port) on COM1 (or COM2).

The keyboard is generally not to change, be careful with the settings of the video card since they will directly impact the display, causing an unstable display on error (screen flickers for example).

Once all input parameters are good, you quit the setup program and return the command line under the console.Just type "startx" to start X-Window.

Chapter 3 –The Shell

In this chapter we will learn about a very important concept. You will find a lot of important details to know about the shell which will help you evolve during your self-study.

## Introduction to the shell

The interface between the operating system and the useris the command interpreter, hence its name "shell".

![http://i.stack.imgur.com/Znlqz.jpg](images/00001.jpeg)

The shell is thus responsible for making through the operating system and the user thanks to command lines entered by the latter. Its role is therefore to read command lines, interpret their meanings, execute them, and then returns the result to the outputs.

The shell is thus an executable file responsible for interpreting orders, transmitting them to the system and sending the result in return. There is a wide range of different shells; the most common being sh (called "Bourne shell"), bash ("Bourne again shell"), csh ("C Shell"), Tcsh ("Tenex C shell"), ksh ("Korn shell") and zsh ("Zero shell"). Their name is usually the name of the executable.

Each user has a default shell, which will be launched at the opening of a command prompt. The default shell is specified in the configuration file /etc/passwd in the last field of the line corresponding to the user. It is possible to change the shell in a session by simply executing the corresponding file, here’s an example:

/Bin/bash

## Command prompt (prompt)

The shell is initialized by reading its overall configuration (in a file in the /etc/), followed by reading the user-specific configuration (in a hidden file whose name starts with a dot, located in the directory user base, that is to say /home/username/. Configuration file), then displays a command prompt as follows:

Machine:/directory/current$

By default in most shells the prompt consists of the name of the machine,followed by a colon (:), the current directory, then a character indicating user type logged on:

- A normal user is indicated with a "$" 

- The administrator, called "root" is indicated with a hash"#"

## Command line concept

A command line is a character string consisting of a command corresponding to an executable system or a shell command and the Optional arguments (parameters):

ls –al /home/j/

In the above command, lsis the name of the command, -al and /home/jimmy/ are arguments. Arguments beginning with - are called options.

For each order there are usually a number of options available which can be detailed by typing the following commands:

command--help

command -?

man command

## Standard input-output

When executing a command, a process is created.This will then open three flows:

- Stdin: where the process will read the input data. It’s called standard input. By default stdin is the keyboard. STDIN is identified by the number 0.

- Stdout: where the process will write the output data. It’s called standard output. By default stdin corresponds to the screen; STDOUT is identified by the number 1.

- Stderr: where the process will write error messages. It’s called standard error. Default is stderr on the screen. STDERR is identified by the number 2.

By default when executing a program, the data is read from the keyboard and the program sends its output and errors on the screen, but it is possible to read data from any device to input or from a file and send the output to a display device, a file, etc.

## Redirects

Linux, like any Unix-like system, has mechanisms to redirect the standard input-output to files.

Thus, the use of the character ">" redirectsthe standard of a command to the left output to the file locatedto the right:

ls -al /home/jf/> test.txt

echo "test"> /etc/myconfigurationfile

The following command is equivalent to copying files:

cat file1>file2

Redirection ">" aims to create a new file. So if a file with same name existed, it is overwritten. The following command simply creates an empty file:

> File

The use of a double character ">>" concatenatesstandard output to the file, that is to say, add the output after the file without overwriting it.

Similarly, the "<" character indicates a standard input’sredirection. The next command sends the foo.txt file content as input to the cat command, whose sole purpose is to display the content on the standard output (useless but trainer example):

cat<foo.txt

Finally the use of redirection "<<" can be read on standard inputuntil the chain to the right is encountered. Thus, the following example willread the standard input until the word STOP is encountered, and then will display the result:

cat<< STOP

## Communicating tubes (pipes)

The pipes are a specific communication mechanism to all UNIX systems. A pipe, symbolized by a vertical bar ("|" character), is used to assign the standard output of one command to the standard input of another, such as a pipe for communicating the standard input of a command with the standard output of another.

So in the following example, the standard output of the ls -al command is sent out on the program responsible for sorting the result in alphabetical order:

ls -al | sort

It is possible in this way to chain a number of commands through successive pipes. In the following example the command displays all files in the current directory, selects the lines containing the word "zip" (using the grep command)and counts the total number of lines:

ls -l | grep zip | wc -l

Chapter 4 –File Globbing

This chapter is one of the most important ones since it covers a very interesting topic. Knowing about files hierarchy in Linux is indispensable. We will also learn about the main shell commands which are commonly used.

## The hierarchy of files in Linux

To ensure portability and compatibility, a Linux system conformsthe single standard FHS (File Hierarchy Standard). The base hierarchy is as follows:

|  |  |  | the root, it contains the main directories |
| bin |  |  | contains essential executables to the system used by all users (for example, ls, rm, cp, chmod, mount, ...) |
| /boot |  |  | contains files that allow Linux to start |
| /dev |  |  | contains the devices entry points |
| /etc |  |  | contains commands and files needed to the system administrator (group, passwd,ld.so.conf,inittab,...) |
|  | /etc/X11 |  | contains the specific files for the configuration of X |
|  | /etc/opt |  | contains the specific configuration files to applications installed in /opt |
| /home |  |  | Personal Directory users |
| /lib |  |  | contains shared libraries essential to the system during startup |
| /mnt |  |  | contains temporary mount points partitions (CD-ROM, floppy disk, ...) |
| /opt |  |  | contains additional application packages |
| /root |  |  | root directory administrator |
| /sbin |  |  | contains the essential binary system (egadduser) |
| /tmp |  |  | contains temporary files |
| /usr |  |  | secondary hierarchy |
|  | /usr/X11R6 |  | this directory is reserved for system X version 11 release 6 |
|  | /usr/X386 |  | used before by X version 5, that is a symlink to / usr / X11R6 |
|  | /usr/bin |  | contains the majority of binary files and user commands |
|  | /usr/include |  | contains the header files for C and C ++ programs |
|  | /usr/lib |  | contains most of the system shared libraries |
|  | /usr/local |  | contains data about installed programs on the local machine by the root |
|  |  | /usr/local/bin | binaries of local programs |
|  |  | /usr/local/games | binaries of local games |
|  |  | /usr/local/include | local C and C ++ header files |
|  |  | /usr/local/lib | Local Shared Libraries |
|  |  | /usr/local/sbin | Local binary system |
|  |  | /usr/local/share | autonomous hierarchy |
|  |  | /usr/local/src | local source files |
|  | /usr/sbin |  | contains non-essential binaries to the system reserved for system administrator |
|  | /usr/share |  | Reserved for non-dependent data architecture |
|  | /usr/src |  | contains source code files |
| /var |  |  | contains variable data |

## Table of main Linux Shell commands

| Command | Description | equivalent DOS |
| Ls | Lists the contents of a directory | dir |
| Cd | Changes the directory | cd |
| cd .. | Parent directory | cd.. |
| Mkdir | Creates a new directory | md |
| Rmdir | Removes a directory | deltree |
| Cp | File Copy | copy, xcopy |
| Mv | File displacement | move |
| Rm | deletes the file | del |
| Passwd | changes the user's password |  |
| Cat | displays the file's contents | type |
| More | displays the file content with pauses | more |
| man apropos | help for the requested command | help |
| Lpr | prints the requested file | print |
| Chmod | changes the attribute of a filechmodxxx filexxx = User-Group-Others where x is an integer 1 < x<7Read = 4, Write = 2, Execution = 1x = Read + Write + Run0 means no permissions1 means execution permission2 means writing permission3 means writing and execution permission4 means readingpermission5 means reading and execution permission6 means reading and writing permission7 means all permissions |  |
| Chfn | Changes personal information viewed with finger |  |
| Chsh | changes the shell : chsh user shell_location |  |
| Finger | Lists online users |  |
| traceroute | traces the path between the local machine and the remote machine |  |
| [ftp](http://www.commentcamarche.net/contents/531-protocoles#FTP)[machine] [port]getputquit | file transfer between the local machine and the target machinerecovers a filesends a filequits the FTP session |  |
| telnet [machine] | performs a telnet |  |
| Talk | Permits talking to a connected user (talk user) |  |
| Mesg | authorizes or not the talk commandmesg n: Prevents reception of talk messagesmesg y: Authorizestalk messages reception |  |
| Logout | Disconnects |  |

Chapter 5 - User Management

This chapter is also very important because it covers all the details about authentication and user management. It also covers a lot of useful information which you will certainly find very helpful as we advance more in our journey.

First step of the administrator

When several persons have access to a system, you need the system administrator manages users. For this, the common commands and files to configure must be known.

Important files to know are:

/etc/passwd

/etc/group

## The /etc/passwd file

The /etc/passwd file contains all the user information (login, password ...). Only the super user (root) must be able to change it. We must therefore change the rights of this file so that it is read-only for other users.

This file has a special format for identifying each user; each line has the following format:

Account Name: Password: User number: groupnumber: Comment: directory: startup program

Sevenfields are explained and separated by the character ":":

- The account name of the user

- User’s password (encrypted of course)

- The integer identifying the user for the operating system (UID = User ID, user ID)

- The integer that identifies the user group (GID = Group ID, group ID)

- The comment in which one can find information on the user or simply its real name

- Where the connection directoryis located after connecting to the system

- The command is executed after the connection to the system (that is often a shell)

Here’s an example of a passwd file:

| root:x:0:0:root:/root:/bin/bash |
| bin:x:1:1:bin:/bin:/bin/bash |
| daemon:x:2:2:daemon:/sbin:/bin/bash |
| news:x:9:13:News system:/etc/news:/bin/bash |
| uucp:x:10:14::/var/lib/uucp/taylor_config:/bin/bash |
| cquoi:x:500:100:Cool......:/home/cquoi:/bin/bash |

It is veryimportant to note that in this filethe passwordsareencrypted.

It is therefore useless to edit and replace the field password by directly typing the password that only leads to the blocking of the account. When a user connects, the login program compares the password typed by the user (once encrypted) to that in the passwd file. If they are different, the connection cannot be established. To prohibit use, simply replace the encrypted password by a star: "*".

The account access may possibly be open with empty password field. In this case, anyone wanting to connect with this account can do so. To change the password of an account with the passwd command, you must be either system administrator or account owner (the system will then prompt the user to enter the old password before asking 2 times to enter the new password).

UID: identifier (unique) to each user account. The numbers ‘0’ to ‘99’ are reserved for frequently own accounts.Numbers greater than ‘100’ are reserved for these users.

GID: group ID. The default group’s number is 50\. In connection withaccess rights to files, this identifier is used. This question tells you if your system has more than one user group. (You will then have to worry about the /etc/group).

It is possible to modify the commands interpreter from the Shell. To do this, use the chsh or passwd -s command. Linux then looks in the /etc/shells file the program you have specified. Only orders present in this file will be accepted and will replace the current value of the startup program field. These restrictions do not apply to the superuser account.

Make sure the permissions of the /etc/passwdfile are the same as for the file /etc/shells. The root can be called names other than root. To change this, just replace the name of the root account with the one you desire.

If an account’s identifier (UID) is zero, it means that it’s a privileged one.

The /etc/group file

The /etc/group contains a list of users belonging to different groups. Indeed, when many users can access the system, they are frequently combined in different groups each with their own access rights to files and directories.

It consists of various fields separated by ":":

Group Name: Specialfield: Group number: member1, member 2

The special field is frequently blank.

The group number id the field that links the /etc/group and /etc/passwd files.

Here is an example /etc/group:

| root:x:0:root |
| bin:x:1:root,bin,daemon |
| daemon:x:2: |
| tty:x:5: |
| disk:x:6: |
| lp:x:7: |
| wwwadmin:x:8: |
| kmem:x:9: |
| wheel:x:10: |
| mail:x:12:cyrus |
| news:x:13:news |

-When using the ls command with the -l option, the group number is displayed with the user number who owns the file (or directory). This unique number corresponds to a unique group name (often 8 characters max.).

-The same user can appear in several groups. When connecting to the system it belongs to the group specified in the /etc/passwd (GID field). This may change with the newgrp command. Access rights to files are then defined.

-The File protections must prevent editing by non-privileged users.

- To add a group, the administrator can edit the /etc/group using a text editor. He also can use the addgroup or groupadd command (not always present). In the first case, he will only have the row corresponding to the groups to add. For example, the line: admin:: 56: ccm

- To add a user to a group, simply edit the /etc/group and add the name at the end of the line separating the name of the members by a comma.

- To delete a group, simply edit the /etc/group and delete the corresponding line. But beware, do not forget to change the /etc/passwd numbers (GID) of the deleted group, if users belonged to it. It is also essential to look for files and directories of this group to change (in the opposite case files and directories may be inaccessible).

## Customizing the shell

The /etc/profile configures the Shell. It concerns all users.

Firstly it includes Shell’s variables such asPATH,OPENWINHOME...

Then, the type of terminal and the TERM variable are accordingly defined. One part is dedicated to the prompt; finally a last one allows defining colors of the ls command.

In Linux boot, it's nice to have the lighted keypad, which is not the case by default.

There are therefore a few lines that need to be added to the /etc/profile:

| INITTY=/dev/tty[1-7] |
| for tty in $INITTY; |
| do setleds -D +num< $tty |
| Done |

When connected to the Shell, the first thing that appears is the prompt; it can be configured to suit the user.

If the administrator wants to have a prompt that is called: "Hello #", he only needs to edit the /etc/profile. It contains a variable called PS1\. All lines related to this variable must then be preceded by a hash: #. It is then to add the line PS1 = 'Hello #'.

All there’s left to do is to save and log in again. Then we can see the changes.

Tip: leave a blank after the prompt to improve readability. It is also possible to use variables in the prompt (for example to display the time or name of the machine ...):

| \d | to add the date (English format) |
| \t | to add the time (HH: MM: SS) |
| \u | to add the user's name |
| \r | for a newline |
| \w | to add the full path of the current directory |
| \W | to add the current directory |
| \h | to add the name of the machine |

The color can also be changed. For this, use the PS1 variable like this: PS1 = '\[\033 [color_number] wanted_prompt\033[0m]'

The color number will be taken from the following list:

| Black | 0;30 |
| Red | 0;31 |
| Green | 0;32 |
| Brown | 0;33 |
| Blue | 0;34 |
| Purple | 0;35 |
| Cyan | 0;36 |
| Light Gray | 0;37 |
| Gray | 1;30 |
| Pink | 1;31 |
| Light green | 1;32 |
| Light brown | 1;33 |
| Light blue | 1;34 |
| Light purple | 1;35 |
| Light cyan | 1;36 |
| White | 1;37 |

An example showing the time followed by the user-name in red:

PS1 = '\ t \ [\ 033 [0; 31m] \ u \ 033 [0m]'

Chapter 6 - Linux Tips and Tricks

Just to make it complete, this chapter includes several interesting and really useful tips.

## Mounting a CD-ROM

To mount a CD-ROM on Linux you must login as system administrator, i.e. with the login "root".

Then just mount the drive, that is to say "hang" the contents of the CD-ROM drive in a directory (most of the time /mnt/cdrom/) by typing this command:

Mount -t iso9660 /dev/cdrom/mnt/cdrom

Do not forget to demount the drive with the command

Umount /mnt/cdrom

## Mount a DOS partition

It is possible for Linux to access MS-DOS partitions by mounting them in the UNIX file system. To mount the /dev/hda1 just type:

mount -t msdos/dev/hda1/mnt/hd

Do not forget to demount the partition

umount /mnt/hd

## Mount a floppy drive

In the same way as for the MS-DOS partition, you can mount a floppy disk drive and access the data on a formatted disk in DOS with the command:

mount -t msdos/dev/fd0/mnt/fd

Do not forget to remove the floppy drive

umount /mnt/fd.

## Restart the computer

To correctly restart the computer, just use the command "shutdown". The key sequence <CTRL><ALT><DEL> has on most Linux distributions programmed to match the shutdown command.

For a quick restart simply type in "shutdown -r now".

## The SCSI controller forced recognition

When controllers have no bios they are generally not detected by Linux, in which case it must force the detection by typing prompt LILO:

Boot: linux tmx8xx = <IRQ>, <address>

tmx8xx represents a TMC-8xx controller, if you have another you need to know its designation. IRQ represents the interruption of the controller and "address" the address of the shared memory.

## Making an Alias

First of all what is an alias?

This is a shortcut command to run in another it may also extend to other concepts; an alias can be a shortcut to an email.

The commands under Linux to mount a device are (as you saw above heavy typing.

So instead of typing the command:

"Mount -t iso9660/dev/cdrom/mnt/cdrom"

type:

aliascdrom = "mount -t iso9660/dev/cdrom/mnt/cdrom '

Now just type "cdrom" to mount the device

However, you may ask yourself, why should I type this command if I have to declare it every time I reset the system?

To avoid that, edit the file "/etc/bashrc" and add the line:

aliascdrom = "mount -t iso9660/dev/cdrom/mnt/cdrom '

Chapter 7 - Vi Editor

Text editors are commonly used under Linux. In this chapter we learn about a widespread one.

## Introduction to Vi

Vi is one of the most popular text editors under Unix systems (with Emacs and pico) Despite its very limited ergonomics. In Linux there is a free version of Vi called Vim (Vi Improved). Vi (pronounced vee-eye) is an editor entirely in text mode, which means that each action is done using text commands. This editor although inconvenient at first sight is very powerful and can be very useful in case of operation of the GUI.

The syntax to launch Vi is as follows:

Vifile_name

After opening the file, it is possible to move using cursors, and the h, j, k and l (in case the keyboard does not possess arrow cursors).

## The Vi modes

Vi has 3 modes of operation:

-Normal mode: the one in which you are opening the file.

It allows you to type commands.

- The insert mode: This mode allows you to insert characters you type in the document. To switch to insert mode, simply press the Insert key on your keyboard, or, if the i key

- Replacement mode: This mode allows you to replace the existing text with the text that you type. Simply press again r to enter replace mode, and press the Esc key to return to normal mode.

## The basic commands

| Command | Description |
| :q | Quit the editor (without saving) |
| :q! | Forces the editor to quit without saving (even if changes were made to the document) |
| :wq | Saves the document and quits the editor |
| :filename | Saves the document under the specified name |

## The editing commands

| Command | Description |
| X | Deletes the current character under the cursor |
| Dd | Deletes the current line under the cursor |
| Dxd | Deletes x lines from the one currently under the cursor |
| Nx | Delete n characters from the one currently under the cursor |
| x>> | Indent x lines to the right from the one currently under the cursor |
| x<< | Indent x lines to the left from the one currently under the cursor |

## Search and replace

To find a word in a document, simply (in normal mode) type / followed by the search string, then confirm with the enter key.

It is then possible to go from occurrence to occurrence with the n button.

To replace a character string with another on a line, there is a very powerful command in Vi using regular expressions with the following syntax:

:S/string_to_be_replaced/new_string/

It is possible to generalize to the entire document with the following syntax:

:%S/string_to_be_replaced/new_string/

## The copy-paste and cut-paste

It is possible in Vi to copy and paste a selection of lines. To do this, just type the following command to copy n lines:

nyy

By way of example,here’s a command allowing to copy 16 lines in the buffer:

16yy

To paste the selection, just type the letter p.

Cutting and pasting n lines is similarly done with the command:

Ndd

Then p to paste!

Conclusion

A beautiful journey has come to an end at this level. But, we surly now have all the tools and skills to begin using and enjoying this powerful operating system. As you have witnessed, this book covers several interesting areas about Linux. At the beginning we started talking about Linux history and genesis so we can have a clear vision and be methodological. Then, we learnt and understood how to install the system knowing the necessary equipments and devices needed to have an operational OS running. We also learnt about the shell which is very important and all the relative commands. And of course we must not forget about command lines which are really useful and commonly used. Fileglobbingwas covered too; it’s indispensable for Linux beginners to know.User’s management and authenticating will certainly help you secure data and manage access rights for all users. By the end, just to make it complete and really useful for Linux learners and beginners, we included some very important Linux tips and talked about the Vi editor which is really an interesting thing to know. All that is left to say is that I wish you prosperity, all the best and good luck, achieving your objectives and being closer to your personal achievements.