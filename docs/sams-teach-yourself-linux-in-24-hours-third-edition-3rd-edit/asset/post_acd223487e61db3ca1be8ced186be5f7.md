
missing program files, and how to build an RPM file (that is, if you're the programming type and want to write programs for Linux).

Another source of information is the RPM Web site at www.rpm.org.

Q Is all the software available for the Linux operating system in the RPM format?

A No, you'll find other formats that can be installed on your system. Sometimes you will see binary distributions, which use the gzip or compressed tar file format. Binary distributions are ready to use. All you need to do is unpack the archive and the files will be placed in the proper location in your system.

Another format that you'll see is a source distribution. With a source distribution, you'll need to issue commands to compile the software and then install it on the system. To use a source distribution, unpack the source code files (with the tar command) and place them in a subdirectory of the /usr/src directory. Next, browse through the files and look for a README file or any other installation notes. The README file will give you further instructions on how to compile the specific source code and how to install the program after it is compiled.

The other format that you'll run across is the DEB distribution. These files are intended for the Debian Linux operating system. Quite a number of good applications are available as DEB packages. If you use KPackage to install software, you'll find that KPackage can handle DEB files.

## Workshop

Test your knowledge of the material covered in this hour by answering the following questions and working through the exercises.

### Quiz

### 1. What is a package manager and which ones will you find on your system?

A package manager enables you to view the applications installed on your system, display a description of an application, remove applications from the system, and add new applications to the system. The base of the package manager system is the rpm command. There are several different front ends to the rpm command that enable you to manage applications from a graphical user interface. Linux-Mandrake uses RPMDrake to add and delete packages from the system. The KDE desktop contains a utility called KPackage that makes it easy to install software. Other Linux distributions might have developed their own front ends to the rpm command.

### 2. How do you use the rpm command to list the commands, applications, utilities, and libraries installed on your system?

You use the rpm command with the query all option (as in rpm -qa). This lists all the installed packages on your system. Depending on your system, this might be a long list and hard to read in a terminal window. To make it easier to read the list, pipe the output to a pager (using rpm -qa | less) or redirect the output to a file (using rpm -qa > filename).

### 3. What is the quick and easy way to find information about how an installed program works, the version number, and the program's creator?

The easiest way is to query an individual package using the rpm command with the -qi command option followed by the name of the application. For example, to display a description of the Gimp graphics program, type rpm -qi gimp and press Enter.

### 4. Why are dependencies important in Linux?

One of the advantages of the Linux operating system is that the package size is quite small. Linux uses shared libraries that contain all the common functions needed to run many programs. These common functions are stored in libraries and any installed program can read the libraries and use the needed functions. If you remove a library upon which other applications depend, those applications will no longer work.

### Exercises

- 1. Take inventory of the applications installed on your Linux system. Use the rpm command to query the database and send the output to a file (for example, use the command sequence rpm -qa > filename). After you have a list of files, display the information about the programs that you haven't used and don't know anything about. Use this information to create more space on your hard drive and uninstall unneeded programs. Then, to find out whether you can safely remove programs that you don't want, test the uninstall process for each program (type rpm --test -evv package-name). If no dependencies show up, you can safely uninstall the package.
- 2. If your Internet connection is up and running, take some time to find new and interesting applications for your Linux system on the Web. With some searching, you'll find many applications that aren't on the distribution CD-ROM. If you use the X Window System, go to ftp.x.org and explore the software available through X.org and XFree86.

## Hour 16

### Updating the Linux Kernel

The ability to upgrade your Linux kernel for free is a really nice thing. Now that you have installed Linux, you certainly should want the latest release, right? Actually, the answer to this question is probably no. If this were Microsoft Windows or a Macintosh operating system, you might be left behind if you didn’t upgrade, particularly at cocktail parties. But when you installed Linux, you got a better deal. To put it succinctly, if you don’t need new drivers and you don’t have any bugs, you don’t need to upgrade. Of course, you might still want to know something about upgrading your Linux kernel in case you need to do so in the future.

In this hour, you will

- Get everything ready before you start the kernel upgrade
- Download the kernel source code
- Learn how to compile the kernel and install it on your system

![](img/782ecfdc0b083a767896cc983e10427f_262_0.png)

### Preparing to Upgrade the Kernel

Before we get further into this business of upgrading the kernel, we need to make some serious preparations. First, let's take a look at what is required to do the job:

- 1. Read the kernel HOWTO very carefully. It has been written and maintained by Brian Ward since 1994. Thanks to his efforts and those of other contributors (listed in the HOWTO), this has long been a source of the best information about kernel updates. It is found at www.kernel.org.
- 2. For those who might be upgrading to Kernel version 2.2 from an earlier distribution, you can find information about changes in the kernel for the 2.2 kernel distribution at www.crynwr.com/kchanges. Unfortunately, as is the case with all technical things that change rapidly, this site has yet to be updated to the current exact version of 2.2.x, but it does have changes for the 2.3.x development kernel, so you can see where things might be headed.
- 3. In addition to these sources, here is a short list of others you should investigate before you begin:
  - The Linux newbie guide at linux.umbc.edu/mirrors/newbie-admin-faq
  - Another beginner's guide is Josh's GNU/Linux Guide at jgo.local.net/LinuxGuide
  - Of course, you'll want to look at The Linux System Administrator's Guide at www.linuxdoc.org/LDP/sag/index.html
  - Linux Administration Made Easy at www.linuxdoc.org/LDP/lame/LAME/linux-admin-made-easy/book1.html
- 4. Look at this group of HOWTOs gleaned from the kernel HOWTO:
  - The Sound-HOWTO if you need to know about sound cards and utilities
  - The SCSI-HOWTO for the scoop about SCSI controllers and devices
  - The NET-2-HOWTO is the networking HOWTO
  - The PPP-HOWTO for dial-up PPP networking in particular
  - The PCMCIA-HOWTO to find driver information if you have a notebook computer
  - The ELF-HOWTO explains what ELF is because the 2.2.x kernel is compiled in ELF
  - The Hardware-HOWTO gives an overview of Linux-supported hardware
  - The Module mini-HOWTO contains still more info about kernel modules
  - The Kerneld mini-HOWTO talks about kerneld (the kernel daemon)

This list doesn't even scratch the surface of all of the information that is out there. But it gives you a basic grounding and some understanding of what goes on in a kernel upgrade.

5. Make sure that you have the current minimal requirements. The kernel upgrade will actually be done by Linux, using the resources available on your present Linux installation in the form of commands, libraries, and utilities. These resources are used to interactively tailor the installation of the new kernel and attach modules for the things that you might want. These utilities must be updated to the ones required for the new kernel, or you won't be able to tell which of the things you encounter are actually bugs, should you encounter any. Linus Torvalds puts the information regarding which versions of these libraries and utilities will be required in the readme file included in the kernel distribution. But you'll have to download the kernel distribution to get the readme file, so to get an idea of the things you need to consider, Table 16.1 is a summary of the present minimal requirements for software to run the 2.3 kernel. If you want to see what you're currently running, the suggested command should tell you.

### TABLE 16.1 The Minimal Required Versions of the Libraries and Utilities Necessary to Upgrade to the 2.3 Kernel

| Requirement | Version | Command to Determine Version |
|---|---|---|
| Kernel modules | 2.3.10 | insmod -V |
| GNU C | 2.7.2.3 | gcc --version |
| Binutils | 2.9.1.0.7 | ld -v |
| Linux libc5 C Library | 5.4.46 | ls -l /lib/libc* |
| Linux libc6 C Library | 2.0.7pre6 | ls -l /lib/libc* |
| Dynamic Linker (ld.so) | 1.9.9 | ldd --version or ldd -v |
| Linux C++ Library | 2.7.2.8 | ls -l /usr/lib/libg++.so.* or ls -l /usr/i486-linux-libc5/lib/libg++.so.* |
| Procps | 1.2. | ps -version |
| Procinfo | 16 | procinfo -v |
| psmisc | 17 | pstree -V |
