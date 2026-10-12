
Download the compressed tar file by using anonymous FTP or through your Web browser. Typically, this involves no effort on your part beyond clicking a link and saving the file in an appropriate directory on your system.

To try your hand at downloading and building a software package, you can practice on the X Multimedia System (XMMS) — a graphical X application for playing MP3 and other multimedia files. XMMS is bundled with Red Hat Linux and should already be installed on your system. However, there is no harm in downloading and rebuilding the XMMS package again.

Download the source files for XMMS from www.xmms.org/download.php. The files are packed in the form of a compressed tar archive. Click the ftp link for the source files and then save them in the /usr/local/src directory in your Red Hat Linux system. (Be sure to log in as root; otherwise, you cannot save in the /usr/local/src directory.)

After downloading the compressed tar file, examine the contents with the following tar command:

```
tar ztf xmms*.gz | more
```

You should see a listing similar to the following:

```
xmms-1.2.7/
xmms-1.2.7/Makefile.in
xmms-1.2.7/README
xmms-1.2.7/stamp-h.in
xmms-1.2.7/ABOUT-NLS
xmms-1.2.7/AUTHORS
xmms-1.2.7/COPYING
xmms-1.2.7/ChangeLog
xmms-1.2.7/INSTALL
xmms-1.2.7/Makefile.am
xmms-1.2.7/NEWS
xmms-1.2.7/TODO
xmms-1.2.7/acconfig.h
xmms-1.2.7/acinclude.m4
xmms-1.2.7/aclocal.m4
xmms-1.2.7/config.guess
xmms-1.2.7/config.h.in
xmms-1.2.7/config.sub
xmms-1.2.7/configure
... rest of the output not shown ...
```

The output of this tar command shows you what's in the archive and gives you an idea of the directories that will be created after you unpack the archive. In this case, a directory named xmms-1.2.7 will be created in the current directory, which, in my case, is /usr/local/src. From the listing,

you'll also learn the programming language used to write the package. If you see `.c` and `.h` files, that means the source files are in the C programming language used to write many open-source software packages.

To extract the contents of the compressed `tar` archive, type the following `tar` command:

```
tar zxvf xmms*.gz
```

You'll again see the long list of files as they are extracted from the archive and copied to the appropriate directories on your hard drive.

Now you're ready to build the software.

## Building the software from source files

After you unpack the compressed `tar` archive, all source files will be in a directory whose name is usually that of the software package with a version-number suffix. For example, the XMMS version 1.2.7 source files are extracted to the `xmms-1.2.7` directory. To start building the software, change directories with the following command:

```
cd xmms*
```

You don't have to type the entire name — the shell can expand the directory name and change to the `xmms-1.2.7` directory.

Nearly all software packages come with some sort of `README` or `INSTALL` file — a text file that tells you how to build and install the package. XMMS is no exception; it comes with a `README` file you can peruse by typing `more README`. There is also an `INSTALL` file that contains instructions for building and installing XMMS.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_499_0.png)

Most open-source software packages, including XMMS, also come with a file named `COPYING`. This file contains the full text of the GNU General Public License (GPL), which spells out the conditions under which you can use and redistribute the software. If you're not familiar with the GNU GPL, read this file and show the license to your legal counsel for a full interpretation and an assessment of applicability to your business.

To build the software package, follow the instructions in the `README` or `INSTALL` file. For the XMMS package, the `README` file lists some of the prerequisites (such as libraries) and tells you what commands to type to build and install the package. In the case of XMMS, the instructions tell you to use the following steps:

- 1. **Type ./configure to run a shell script that checks your system configuration and creates a file named Makefile — a file the make command uses to build and install the package.** (You can type ./configure --help to see a list of options that configure accepts.)
- 
- 2. **Type make to build the software.**
  This step compiles the source files in all the subdirectories (compiling source code converts each source file into an object file — a file containing binary instructions that your PC's processor can understand).
- 
- 3. **Type make install to install the software.**
  This step copies libraries and executable binary files to appropriate directories on your system.

Although these steps are specific to XMMS, most other packages follow these steps — configure, make, and install. The configure shell script guesses system-dependent variables and creates a Makefile with commands needed to build and install the software.

Usually, you don't have to do anything but type the commands to build the software, but you must install the software-development tools on your system. This means you must install the Software Development package when you install Red Hat Linux. To build and run XMMS, you must also install the X Software Development package because it's an X application.

To begin building XMMS, type the following command to run the configure script (you must be in the xmms-1.2.7 directory when you type this command):

```
./configure
```

The configure script starts running and prints lots of messages as it checks various features of your system — from the existence of the C compiler to various libraries needed to build XMMS. Finally, the configure script creates a Makefile you can use to build the software.

If the configure script displays error messages and fails, review the INSTALL and README files to find any clues to solving the problem. You may be able to circumvent it by providing some information to the configure script through command-line arguments.

After the configure script finishes, build the software by typing make. This command runs the GNU make utility, which reads the Makefile and starts compiling the source files according to information specified in the Makefile. The make command goes through all the source directories, compiles the

![](img/a7eec43a54473e95dc5ea333fecf1bd7_500_0.png)

![](img/a7eec43a54473e95dc5ea333fecf1bd7_500_1.png)

Book VI
Chapter 4
Managing Applications

source files, and creates the executable files and libraries needed to run XMMS. You'll see a lot of messages scroll by as each file is compiled. These messages show the commands used to compile and link the files.

The `make` command can take 10 to 15 minutes to complete. After `make` is done, you can install the XMMS software with the following command:

```
make install
```

This command also runs GNU `make`, but the `install` argument instructs GNU `make` to perform a specific set of commands from the `Makefile`. These instructions essentially go through all the subdirectories and copy various files to their final locations. For example, the binary executable files `xmms`, `gnomexmms`, `wmxmms`, and `xmms-config` are copied to the `/usr/bin` directory.

Now that you have installed XMMS, try running it from the GNOME or KDE desktop by typing `xmms` in a terminal window or by choosing Main Menu→Sound & Video→Audio Player. XMMS already comes with Red Hat Linux, but now you should get the new version of XMMS (the difference is that the newly built version can play MP3 files without any add-ons). From the XMMS window, press L to get the Load File dialog and select an MP3 file to play. Your PC must have a sound card, and the sound card must be configured correctly for XMMS to work. Figure 4-1 shows a typical view of XMMS playing an MP3 music clip.

Figure 4-1:
You can play MP3 music with the version of XMMS you built from source files.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_501_0.png)

Here's an overview of the steps you follow to download, unpack, build, and install a typical software package:

- 1. Use a Web browser to download the source code, usually in the form of a `.tar.gz` file, from the anonymous FTP site or Web site.
- 2. Unpack the file with a `tar zxvf filename` command.
- 3. Change the directory to the new subdirectory where the software is unpacked, with a command such as `cd software_dir`.
