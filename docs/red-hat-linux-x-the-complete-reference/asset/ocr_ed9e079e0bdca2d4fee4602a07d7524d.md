# Selecting an Install Directory

Before you unpack the archive, move it to the directory where you want it. Source code packages should be placed in the /usr/local/src directory, and binary packages go in designated directories. Source code files are unpacked in the /usr/local/src directory, generating their own subdirectories from which you can compile and install the software. Once it is installed, you can delete this directory, keeping the original source code package file (.tar.gz).

Packages that hold binary programs ready to run, like Java, are meant to be extracted in certain directories. Usually this is the /usr/local directory. Most archives, when they unpack, create a subdirectory named with the application name and its release, placing all those files or directories making up the software package into that subdirectory. For example, the file cdrarchive-1.2.2.tar unpacks to a subdirectory called cdrarchive-1.2.2. In certain cases, the software package that contains precompiled binaries is designed to unpack directly into the system subdirectory where it will be used. For example, it is recommended that j2sdk-1.3.0-FCS-linux-i386.tar be unpacked in the /usr/local directory, where it will create a subdirectory called j2sdk-1.3.0. The /usr/local/j2sdk-1.3.0/bin directory holds the Java binary programs.

# Extracting Software

First, use tar with the t option to check the contents of the archive. If the first entry is a directory, then when you extract the archive, that directory is created and the extracted files are placed in it. If the first entry is not a directory, you should first create one and then copy the archive file to it. Then extract the archive within that directory. If no directory exists as the first entry, files are extracted to the current directory. You must create a directory yourself to hold these files.

```
# tar tvf htdig-3.1.6.tar
```

Now you are ready to extract the files from the tar archive. You use tar with the x option to extract files, the v option to display the pathnames of files as they are extracted, and the f option, followed by the name of the archive file:

```
# tar xvf htdig-3.1.6.tar
```

The extraction process creates a subdirectory consisting of the name and release of the software. In the preceding example, the extraction created a subdirectory called htdig-3.1.6. You can change to this subdirectory and examine its files, such as the README and INSTALL files.

```
# cd htdig-3.1.6
```

Installation of your software may differ for each package. Instructions are usually provided along with an installation program. Be sure to consult the README and INSTALL files, if included. See the following section on compiling software for information on how to create and install the application on your system.

# Compiling Software

Some software may be in the form of source code that you need to compile before you can install it. This is particularly true of programs designed for cross-platform implementations. Programs designed to run on various Unix systems, such as Sun, as well as on Linux, may be distributed as source code that is downloaded and compiled in those different systems. Compiling such software has been greatly simplified in recent years by the use of configuration scripts that automatically detect a given system's hardware and software configuration and then allow you to compile the program accordingly. For example, the name of the C compiler on a system could be gcc or cc. Configuration scripts detect which is present and select it for use in the program compilation.

A configure script works by generating a customized Makefile, designed for that particular system. A Makefile contains detailed commands to compile a program, including any preprocessing, links to required libraries, and the compilation of program components in their proper order. Many Makefiles for complex applications may have to access several software subdirectories, each with separate components to