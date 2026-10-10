
## To use the `Shell` object

To use the `Shell` object, follow these general steps:

1. **Place the following line to include the `Shell` module in your program:**
   `use Shell;`
   You must include this line before you create a `Shell` object.

2. **To create a `Shell` object, use the following syntax:**
   `my $sh = Shell->new;`
   where `$sh` is the reference to the `Shell` object.

3. **Run `Linux` commands by using the `Shell` object and capture any outputs by saving to an appropriate variable.** For example, to save the directory listing of the `/usr/share/perl/5.8.6` directory in an array named `@modules`, write the following:
   ```perl
   @modules = $sh->ls("/usr/lib/perl/5.8.6/*.pm");
   ```
   Then you can work with this array of `Perl` module filenames (that’s what `*.pm` files are) any way you want. For example, to simply go through the array and print each string out, use the following `while` loop:
   ```perl
   while(@modules) {
       $mod = shift @modules;
       # Do whatever you want with the module name
       print $mod;
   }
   ```

How do you know which methods to call and in what order to call them? You have to read the object’s documentation before you can use the object. The method names and the sequences of method invocation depend on what the object does.

## Using the `English` module

`Perl` includes several special variables with strange names, such as `$_` (for the default argument) and `$!` (for error messages corresponding to the last error). When you read a program, guessing what a special variable means can be difficult. The result is that you may end up avoiding a special variable that could be useful in your program.

As a helpful gesture, `Perl` `5` provides the `English` module (`English.pm`), which enables you to use understandable names for various special variables in `Perl`. To use the `English` module, include the following line in your `Perl` program:

`use English;`

After that, you can refer to `$_` as `$ARG` and `$!` as `$ERRNO`. (These *English* names can still be a bit cryptic, but they’re definitely better than the punctuation marks.)

The following program uses the English module — and prints a few interesting variables:

```perl
#!/usr/bin/perl -w
# File: english.pl
use English;
print "Perl executable = $EXECUTABLE_NAME\n";
print "Script name = $PROGRAM_NAME\n";
```

Run this script with the following command:

`./english.pl`

When I run this script, here’s what I get as output:

```
Perl executable = /usr/bin/perl
Script name = ./english.pl
```

The English module is handy because it lets you write Perl scripts in which you can refer to special variables by meaningful names. To find out more about the Perl special variables and their English names, type **man perlvar** in a terminal window — or, better yet, point your Web browser to `perldoc.perl.org/perlvar.html`

## Appendix: About the DVD

### In This Appendix

- System requirements
- DVD installation instructions
- What you'll find on the DVD
- Troubleshooting

This book's companion DVD includes seven prominent Linux distributions — Debian GNU/Linux, Fedora Core, Knoppix, MEPIS, SUSE, Ubuntu, and Xandros Desktop OS — to get you started on your Linux journey. This appendix briefly describes the DVD and tells you how to get started with the installation.

### System Requirements

Make sure that your computer meets the minimum system requirements shown in the following list. If your computer doesn't match up to most of these requirements, you may have problems using the software and files on the DVD:

- A PC with processor running at 400 MHz or faster for graphical installation
- At least 192MB of total RAM installed on your computer for graphical installation (256MB recommended)
- At least 520MB free space on your hard drive for a minimal installation; 5GB of free space recommended if you plan to install most packages so that you can try out everything covered in this book
- A DVD-ROM drive and a CD burner (See Book 1, Chapter 2 for instructions on burning installation CDs)
- A graphics card and a monitor capable of displaying at least 256 colors
- A sound card
- Ethernet network interface card (NIC) or modem with a speed of at least 56 Kbps

### DVD Installation Instructions

To install a Linux distribution from the companion DVD, follow these steps. (Consult Book I, Chapter 2 for details.)

1. Gather information about your PC’s hardware, such as graphics card, network card, and SCSI card, before you install Linux.

2. Use a partitioning program such as PartitionMagic or the FIPS program to create room on your hard drive for Linux.
   Skip this step if you plan to use Linux as the sole operating system on your PC or if you plan to install it on an empty second hard drive.

3. Burn CDs for your distribution. (Skip this step if you are installing Fedora Core.)
   Consult Book I, Chapter 2 for instructions specific to each distribution.

4. Boot your PC with the DVD (for Fedora Core and Knoppix) or the first CD (for Debian, MEPIS, SUSE, Ubuntu, and Xandros).
   Knoppix is a Live CD distribution, so this step should get you the Knoppix desktop. For other distributions, this step runs that distribution’s installation program. From this point on, respond to the questions and choices as the installation program takes you through the steps. Here are some of the typical installation steps:
   - Prepare the hard drive partitions for Linux. If you have created space by reducing the size of an existing Windows partition, this step enables you to create the partitions for Linux.
   - Configure the Ethernet network, if any. Typically, you configure the network automatically by using DHCP.
   - Specify the local time zone and set the root password.
   - Install a boot loader program on your hard drive so that you can boot Linux when you power up your PC after shutting it down.
   - Select the specific software packages that you want to install, such as the X Window System and the GNOME or KDE graphical desktop.

### What You’ll Find on the DVD

This section provides a summary of the software and other goodies you find on the DVD. If you need help with installing the items provided on the DVD, refer back to the installation instructions in the preceding section.

![](img/792720823146d68f19fd50c99ebfce4b_798_0.png)

Shareware programs are fully functional, free, trial versions of copyrighted programs. If you like particular programs, register with their authors for a nominal fee and receive licenses, enhanced versions, and technical support.

Freeware programs are free, copyrighted games, applications, and utilities. You can copy them to as many PCs as you like - for free - but they offer no tech support.

Trial, demo, or evaluation versions of software are usually limited by time or functionality (such as not letting you save a project after you create it).

GNU software is governed by its own license, which is included in the folder of the GNU software. There are no restrictions on distribution of GNU software. See the GNU license at the root of the DVD or back of this book for details. As required by the GNU license, this book includes the source code for Fedora Core. As for the source code for Debian, Knoppix, SUSE, and Xandros, here's how to get the source code from the Internet for each application:

- **Debian:** Go through the list of mirror sites at www.debian.org/mirror/list and click the URL for the site nearest you. After the site loads, go to the pool directory and then look for source code files in one of the three directories — main, contrib, and non-free. The files are further organized into separate directories according to the first letter of the package's name. For example, the source code for the sendmail package is in the s directory. (See www.debian.org/doc/FAQ/ch-ftarchives.en.html#s-pools for more information about the pool directory.)
- **Knoppix:** Many packages for Knoppix are from the Debian project and their source code is available from the Debian Web site. (See the previous bullet for information on downloading Debian source code.) Download the Knoppix-specific source code from www.knopper.net/download/knoppix.
- **MEPIS:** Most packages in MEPIS are from the Debian project and their source code is available from the Debian Web site. (See the description of Debian for information on downloading Debian source code.) MEPIS-unique components such as MEPIS OS Center are proprietary and their source code is not available.
- **SUSE:** Download the source package for SUSE Linux from the server at http://ftp.opensuse.org/pub/opensuse/distribution/SL-OSS-stable/inst-source/suse/src/.
- **Ubuntu:** You can find the Ubuntu source code at http://archive.ubuntu.com/ubuntu/ and it's organized similar to the way Debian source code is organized (see the description of Debian). While running Ubuntu, you can download the source code for a package by typing the
