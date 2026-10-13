packages — one contains the binary distribution and the other contains the source distribution. Unless you are interested in compiling your own copy, use the binary distribution. Normally, I compile security software if I can, but because Red Hat packages this software in its product, I have a certain degree of trust in its professionalism; therefore, the binary installation is presented here.

As usual, the binary installation is quite simple; run the rpm command as follows:

```
rpm -ivh tripwire_package.rpm
```

Replace tripwire_package.rpm with the RPM package appropriate for your system architecture. After you install Tripwire, run rpm -ql tripwire_package.rpm to find out where the files are installed. The default installation directory is /usr/local/bin/tw for Tripwire version 1.3.

The RPM package containing the binary distribution of Tripwire doesn't contain any man pages. However, the man pages are included in the source distribution, so install the source RPM distribution of Tripwire, which is also included in the Application CD-ROM shipped with Red Hat.

After you install the source distribution using rpm, extract the source in the /usr/src/redhat/SOURCES directory to an appropriate location to access the man pages. If you want to install the man pages, follow these steps:

+   1. Extract the source distribution tar file in a directory and change the directory to the man subdirectory.
+   2. Edit the Makefile in the man directory and add MANDIR = /usr/man in a line after the comment lines at the top of the Makefile
+   3. Run make to install the man pages into appropriate man page locations in your system.

After you complete these steps, you have access to the siggen (8), tripwire (8), and tw.config (5) man pages, which you should read before continuing with Tripwire any further.

# Creating a Tripwire database

The very first task to get Tripwire working is to create a database of signatures for all the files and directories