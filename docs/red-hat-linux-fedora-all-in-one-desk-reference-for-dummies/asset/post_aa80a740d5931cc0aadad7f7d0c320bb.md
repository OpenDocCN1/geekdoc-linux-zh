
- A class is a Perl module that provides the methods to work with the object.
- A method is a Perl subroutine that expects the object reference as the first argument.

Object implementers have to follow certain rules and provide certain methods in a module that represents a class. However, you really don't need to know much about an object's implementation to use it in your Perl program. For practical purposes, all you need to know are the steps you have to follow when you use an object.

## Creating and accessing Perl objects

An especially useful Perl object is the Shell object, which is implemented by the Perl module Shell.pm. That module comes with the Perl distribution and is in the /usr/lib/perl5/5.8.1 directory (for Perl version 5.8.1).

As the name implies, the Shell object is meant for running shell commands from within Perl scripts. You can create a Shell object and have it execute commands.

To use the Shell object, follow these general steps:

1. Place the following line to include the Shell module in your program:

```
use Shell;
```

You must include this line before you create a Shell object.

2. To create a Shell object, use the following syntax:

```
my $sh = Shell->new;
```

where $sh is the reference to the Shell object.

3. Run Linux commands by using the Shell object and capture any outputs by saving to an appropriate variable. For example, to save the directory listing of the /usr/lib/perl5/5.8.0 directory in an array named @modules, write the following:

```
@modules = $sh->ls("/usr/lib/perl5/5.8.0/*.pm");
```

Then you can work with this array of Perl module filenames (that's what *.pm files are) any way you want. For example, to simply go through the array and print each string out, use the following while loop:

```
while(@modules)
{
  $mod = shift @modules;
  # Do whatever you want with the module name
  print $mod;
}
```

How do you know which methods to call and in what order to call them? You have to read the object's documentation before you can use the object. The method names and the sequences of method invocation depend on what the object does.

## Using the English module

Perl includes several special variables with strange names, such as $_ (for the default argument) and $! (for error messages corresponding to the last error). When you read a program, it can be difficult to guess what a special variable means. The result is that you may end up avoiding a special variable that could be useful in your program.

As a helpful gesture, Perl 5 provides the English module (English.pm), which enables you to use understandable names for various special variables in Perl. To use the English module, include the following line in your Perl program:

```
use English;
```

After that, you can refer to $_ as $ARG and $! as $ERRNO (these "English" names can still be a bit cryptic, but they're definitely better than the punctuation marks).

The following program uses the English module — and prints a few interesting variables:

```
#!/usr/bin/perl -w
# File: english.pl

use English;
print "Perl executable = $EXECUTABLE_NAME\n";
print "Script name = $PROGRAM_NAME\n";
```

Run this script with the following command:

```
./english.pl
```

When I run this script on Red Hat Linux, here's what I get as output:

```
Perl executable = /usr/bin/perl
Script name = ./english.pl
```

The English module is handy because it lets you write Perl scripts in which you can refer to special variables by meaningful names. To learn more about the Perl special variables and their English names, type man perlvar in a terminal window — or, better yet, point your Web browser to

```
http://www.perldoc.com/perl5.8.0/pod/perlvar.html
```

## Appendix: About the DVD

### In This Appendix

- System requirements
- DVD installation instructions
- What you'll find on the DVD
- Troubleshooting

### System Requirements

Make sure that your computer meets the minimum system requirements shown in the following list. If your computer doesn't match up to most of these requirements, you may have problems using the software and files on the DVD.

- A PC with a 133 MHz Pentium-class processor (400 MHz Pentium II or better recommended for graphical mode)
- At least 64MB of total RAM installed on your computer for text mode and 128MB for graphical mode; for best performance, we recommend at least 256MB for graphical mode
- A DVD-ROM drive (if you have only a CD-ROM drive, use the included coupon to order Red Hat Linux on CD-ROMs)
- A graphics card and a monitor capable of displaying at least 256 colors
- A sound card
- Ethernet network interface card (NIC) or modem with a speed of at least 56 Kbps
- At least 650MB of free space on your hard disk for a minimal installation; 2.6GB recommended for a workstation class installation

### DVD Installation Instructions

Installing Red Hat Linux from the DVD can be tricky, as some hardware on your PC is not supported by Red Hat Linux. Nevertheless, Red Hat Linux on the companion DVD already supports such a wide variety of hardware, so chances are good that all your PC's peripherals probably are supported.

To install Red Hat Linux from the companion DVD, follow these steps. (For the latest and greatest information, please refer to the README file located at the root of the DVD-ROM.)

1. **Gather information about your PC's hardware, such as graphics card, network card, and SCSI card, before you install Linux.**
2. **Use a partitioning program such as PartitionMagic or the FIPS program to create room on your hard disk for Red Hat Linux.**
   Skip this step if you plan to use Red Hat Linux as the sole operating system on your PC or if you plan to install it on an empty second hard disk.
3. **If your PC cannot boot from the DVD drive, create a Red Hat Linux boot disk.**
4. **Boot your PC with the DVD or by using the Red Hat Linux boot disk.**
   This step automatically runs the Red Hat Linux installation program. From this point on, respond to the questions and choices in a number of windows as the Red Hat installation program takes you through the steps. Here are some of the key installation steps:
   - Identify any SCSI adapters installed on your PC.
   - Prepare the hard disk partitions for Red Hat Linux. If you have created space by reducing the size of an existing DOS partition, this step enables you to create the partitions for Red Hat Linux.
   - Configure the Ethernet network, if any. You may have to specify parameters, such as the IP address and host name for your Red Hat Linux system.
   - Specify the local time zone and set the root password.
   - Install a boot loader program on your hard disk so that you can boot Red Hat Linux when you power up your PC after shutting it down.
   - Select the specific software packages that you want to install, such as the X Window System and the GNOME or KDE graphical desktop.
   - Configure the X Window System and enable the graphical login screen so that when you boot your Linux system, it displays a login dialog box and goes directly into the GNOME or KDE graphical desktop after successful login.

To install specific packages from the DVD to your hard drive, follow these steps:

1. **Log in as root.**
2. **Insert the DVD into your computer's DVD drive.**
3. **If you are using GNOME or KDE GUI, wait for the DVD to mount. Otherwise, open a terminal window and at the command prompt type**

```
mount /mnt/cdrom
```

4. Choose Main Menu: System Settings: Add/Remove Applications.

The Add and Remove Software utility starts and gathers information about the status of packages installed on your system. After it sorts through the information about all the installed packages, the utility displays a list of all the packages. The left side of the window has two large buttons — Install Software and Remove Software. By default the Install Software button is selected.

5. To install any uninstalled package, click the Install hyperlink next to that package.

A dialog box appears with details regarding what you're about to install and how much disk space the new packages require.

6. Click Install Packages to install the selected package.

7. To remove the DVD from your DVD drive, type the following command at the command prompt:

```
umount /mnt/cdrom
```

### What You'll Find on the DVD

This section provides a summary of the software and other goodies you find on the DVD. If you need help with installing the items provided on the DVD, refer back to the installation instructions in the preceding section.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_838_0.png)

Shareware programs are fully functional, free, trial versions of copyrighted programs. If you like particular programs, register with their authors for a nominal fee and receive licenses, enhanced versions, and technical support. Freeware programs are free, copyrighted games, applications, and utilities. You can copy them to as many PCs as you like — for free — but they offer no tech support. GNU software is governed by its own license, which is included in the folder of the GNU software. There are no restrictions on distribution of GNU software. See the GNU license at the root of the DVD for details. Trial, demo, or evaluation versions of software are usually limited by time or functionality (such as not letting you save a project after you create it).

You can find the following software on the DVD (for info on the directory organization of a DVD, refer to the README file located at the root of the DVD):

- Linux kernel 2.4.22 with driver modules for major PC hardware configurations, including IDE/EIDE and SCSI drives, PCMCIA devices, and CD drives and DVD drives
- A complete set of installation and configuration tools for setting up devices and services
