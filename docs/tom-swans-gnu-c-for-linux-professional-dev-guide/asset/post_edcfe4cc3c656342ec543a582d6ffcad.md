
## CHAPTER 3: Installing GNU C++

Because GNU C++ comes with Linux, installing the operating system may already have installed the compiler and other necessary files. In that case, you can skip to “How to Install This Book’s Sample Programs” in this chapter. However, depending on the options you selected during installation, you might have to install additional files using one of the methods explained here.

> **Note**
> 
> For C programmers in the audience who want to learn C++, a section, “Comparing C and C++,” near the end of this chapter compares features in the C and C++ languages. This information might also be useful to readers who are upgrading C programs to C++, or who simply need help deciphering C source code files.

### WHERE TO GET GNU C++

The best source for GNU C++ is right here, on this book’s CD-ROM. However, if you want to upgrade to a newer release, or if you already have Linux or UNIX running and you want to add GNU C++ to your system, begin your search for the necessary files at the following Web site:

`http://www.gnu.org/`

You’ll have to hunt for the page that offers the release files, and because this is a very busy server, you might need to download the files using a mirror FTP (file transfer protocol) site. At this writing, the FTP location of the files is `ftp://ftp.gnu.org/gnu/gcc`. At the minimum, you need the GCC compiler, all associated library files, and preferably, any documentation files you come across. These files are provided in “tarred and zipped” format. For example, a recent release of GNU C++ comes in a file cryptically named something like `gcc-g++-2.95.1.tar.gz`. Files for upgrading an installed compiler also are available. These are generally smaller than the full system and take less time to download.

The “gz” filename extension indicates the file is compressed using GNU’s gzip file compression utility. You can unzip the file by using gunzip. The “tar” in the filename indicates that the files are packed using the age-old UNIX tar (tape archive) utility, which despite its name, works just fine with disks and other media, not only tape. For more information on these utilities, read their online documentation by entering the commands `info tar`, `info gzip`, and `info gunzip`. Also read the following sections for more installation suggestions.

> **Note**
> 
> Until just before this book was scheduled to be published, the GNU C++ compiler went by the name EGCS (Experimental GNU Compiler System). It is now again known, as it had been originally, as GCC, but this acronym has been changed to stand for “GNU Compiler Collection.” In any case, despite its many different names, they all refer to the same GNU compiler system that you can use to write programs using ANSI C++ and ANSI C as explained in this book.

### How to Install the GNU C++ Compiler

Before you go to the trouble of installing GNU C++, check whether the compiler is already installed. To do that, get to a console prompt and enter the following command (notice that the correct command is not c++ but g++, the g referring to GNU C++):

```
$ g++ -v
Reading specs from /usr/lib/gcc-lib/i686-pc-linux-gnu/
#pgcc-2.91.66/specs
gcc version pgcc-2.91.66 19990314 (egcs-1.1.2 release)
```

If you see a similar response—don't worry about the version number or exact filename spellings—you are ready to go. However, if the compiler's version number is earlier than 2.3, you might need to install an upgrade to make full use of this book's advanced chapters. If all seems well, turn to "How to Install This Book's Sample Programs."

If you receive an error message such as "bash: g++: command not found," you need to install GNU C++ before continuing. Basically, you have four choices:

- Reinstall Mandrake-Linux 6.0 from scratch using this book's CD-ROM.
- Upgrade your installation to add GNU C++ and associated library files, using the upgrade option on this book's CD-ROM automatic installer.
- Install individual packages from this book's CD-ROM using the Red Hat Package Manager (RPM), either from a console window or using an X window manager.
- Download the GNU C++ compiler release files from the Internet and install the files manually (not recommended unless you know your way around Linux and UNIX).

The following sections discuss each of these installation methods. The first three methods are relatively simple. Of these, the first two methods can be used by anyone. The third requires you to know your system's root password. The last method might require additional research into how your system is organized and also requires you to know the root password.

### REINSTALLING EVERYTHING

This is the easiest method. Reboot to the attached CD-ROM, and follow instructions in Chapter 2, "Installing Linux," to install the operating system and GNU C++. Be sure to select the proper components during installation, as suggested in the chapter. GNU C++ is not installed by default unless you select that component. If you have the room, install Everything.

### UPGRADING AN EXISTING INSTALLATION

If you have already installed Mandrake-Linux 6.0, but neglected to install the GNU C++ compiler, you can add the necessary files without affecting existing user directories and files. Follow these steps:
