
# Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

Previous Table of Contents Next

## Non-RPM Packages

Although RPM is great, there are times that the software you are to install won’t be in the form of an RPM package. FTP sites like http://sunsite.unc.edu/pub/Linux/distributions/redhat/contrib/i386/ have tons of programs already packaged in RPM, so you should check there to see if what you need is already available in package format.

If it is not, more than likely it will be supplied in a tar or compressed tar file. Working with the tar program for backups is discussed in great detail in Chapter 19, “Backups: Safeguarding Your Work.” If you need to install a program that doesn’t come packaged in RPM format, it is a good idea to install this program into its own directory in the /opt directory. The /opt directory contains mostly third-party software, such as KDE, Netscape, and so on. To make the program visible to the shell, you can create a link for its executable file in the /opt/bin directory. If this directory doesn’t exist, you should create it and add it to your PATH environment variable.

## Tar

To extract files from a tar file, follow these steps:

- 1. Create a directory where you are going to put the files from the archive. It is possible that the tar file will scatter a number of files to the current directory, so it is always a good idea to create a new directory to receive the files.
- 2. Move the tar archive to the destination directory.
- 3. Put the cd into the directory.
- 4. Extract the file using tar: tar xvf afile.tar.

If the maker of the tar file was conscientious enough to place all the files into a directory, you are set. Sometimes the tar file will contain a file called install.sh or some other installation script. Follow instructions as per any readme files (view them with a page such as less).

## UNIX Compressed Archives: Gzip and Compress

Many times tar files will be distributed in compressed format; the typical extensions for compressed files are .gz (gnu zip, or gzip), .Z for the compress program, and .zip for Windows zip compressed archives. If the file has a name like file.tar.gz, that file is a gnu zip compressed tar file. To extract it, you’ll have to specify the z option to tar:

```
[alberto@digital /tmp]$ tar -xzvf file.tar.gz
nsmail/
nsmail/Drafts
nsmail/.Drafts.summary
nsmail/Trash
nsmail/.Trash.summary
nsmail/Sent
nsmail/.Sent.summary
nsmail/Unsent Messages
nsmail/.Unsent Messages.summary
nsmail/Inbox
nsmail/.Inbox.summary
```

Another way of accomplishing the same task is to use pipes using the gzcat program (similar to cat). This program reads information in the compressed archive, decompresses it, and copies it out to the STDOUT. Here’s an example of how to use gzcat and tar together:

```
gzcat file.tar.gz | tar -xf -
```

In this example, gzcat pipes the resulting output, a tar file, to the tar program. The tar program looks for data in its STDIN stream because the dash (–) is provided to the f option as an argument.

Another way is to decompress the gzip file and then use tar normally. This is more inefficient, and if you are short on disk space, it could cause you to run out of space:

```
gunzip file.tar.gz; tar -xf file.tar
```

The gunzip, gzcat, and the z option to tar can handle files with the .gz or Z extension. If you find a really old archive, you might find it with a .z extension; this is also a gzip compressed file.

If the file is not compressed with tar, it just sports a .gz extension. You can

use gunzip to decompress it, like this:

```
gunzip file.gz
```

## Windows Compressed Archives: Zip

The zip archive format (.zip) originally developed for DOS by Phil Katz is in use by virtually every Windows computer. Linux users can also extract and create this file format using the unzip and zip tools.

To unzip a file, just use the unzip command:

```
[alberto@digital /tmp]$ unzip file.zip
Archive:  file.zip
  creating: nsmail/
 extracting: nsmail/Drafts
  inflating: nsmail/.Drafts.summary
  inflating: nsmail/Trash
  inflating: nsmail/.Trash.summary
  inflating: nsmail/Sent
  inflating: nsmail/.Sent.summary
 extracting: nsmail/Unsent Messages
  inflating: nsmail/.Unsent Messages.summary
  inflating: nsmail/Inbox
  inflating: nsmail/.Inbox.summary
```

## Chapter 21
LISA: Linux Installation and System Administration Utility

### In This Chapter

- Basic Functions of LISA
- Verbose System Analysis
- Software Package Administration
- System Configuration
- Network Configuration Area

Caldera OpenLinux includes an administration and configuration tool called LISA. LISA provides an interface to user management, package installation, and system configuration. Some of these tasks are described in other sections because it is faster and more powerful to use the host programs directly rather than use them through LISA. LISA is not freely distributed software, so it is not a common part of other Linux distributions. For simple networks, it provides access to all the common aspects of system and software configuration.

To use LISA, you must be logged in as root. LISA provides a UI through a console; therefore, system configuration can be done even if you are not using the X Window system. Navigation and operation are done using the arrow keys to select command options. The Enter key is used to choose selected

commands, and the Esc key is used to go up a level or to exit the program. On screens that display controls, you can use the Spacebar to mark a highlighted option.

## Basic Functions of LISA

LISA groups its functionality into three categories:

- System Analysis
- Software Package Administration
- System Configuration

The utility also provides a help system that discusses several topics of interest for system administrators. You should browse this section for additional information and help resources.

Here’s the main screen it presents when you start it up.

![](img/edf072a03d4de1f8f4a13465ac79e7fb_253_0.png)

The main LISA screen. Use your arrow keys to highlight a category and press Enter to go there. Press Esc to exit the program. For viewing online help about using LISA, press F1. Detailed information about the current selection can be obtained by pressing F2.

## Verbose System Analysis

The system analysis area can give you information about your hardware and configuration settings. This information is useful to assess your current hardware and configuration settings.

The system analysis area is subdivided into several other areas:

- **Automatic System Analysis**: This area displays basic system information, such as when the system was last started, the current load, the host name, and the IP address of your computer.
- **Automatic Kernel Analysis**: The kernel analysis displays information on the kernel currently in use on your system. It includes information such as kernel version, who built it, the compiler used for building it, the file systems that it supports, and current devices.
- **Automatic Hardware Analysis**: The hardware area displays the more detailed information about your hardware, such as the type of processor installed, the amount of RAM, the size of the swap disk, information about your graphics card, disk drives, PCMCIA, and other hardware devices.
- **Automatic Partition Analysis**: This area displays information on the disk partitions in your computer. It lists the partitions by their device names and provides the size and type for each of the partitions.
- **Automatic Network Analysis**: The network area provides
