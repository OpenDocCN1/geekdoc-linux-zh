Replace tripwire_package.rpm with the RPM package appropriate for your system architecture. After you install Tripwire, run `rpm -ql tripwire_package.rpm` to determine where the files are installed. The default install location directory is /usr/local1/bin/ for Tripwire version 1.3.

The RPM package containing the binary distribution of Tripwire doesn't contain any man pages. However, the man pages are included in the source distribution, so install the source CD-ROM distribution of Tripwire, which is also included in the Application CD-ROM shipped with Red Hat.

After you install the source distribution using rpm, extract the source to the /usr/src/redhat/SOURCES directory to an appropriate location to access the man pages. If you want to install the man pages, follow these steps:

+   1.  Extract the source distribution tar file to a directory and change the directory to the man subdirectory.
+   2.  Edit the Makefile in the man directory and add `MANDIR = /usr/man` in a line after the comment lines at the top of the Makefile.
+   3.  Run make to install the man pages into appropriate man page locations in your system.

After you complete these steps, you have access to the sigen (8), tripwire (8), and tw.cfg (5) man pages, which you should read before continuing with Tripwire any further.

# Creating a Tripwire database

The very first task to get Tripwire working is to create a database of signatures for all the files and directories you want to compare against. To do that, you must specify the files and directory names in a configuration file called tw.cfg, which is also stored in the /usr/local1/bin/ directory. The RPM package version of the configuration file is custom-suited for Linux systems. Modify it after you have read the tw.cfg man pages and understand the syntax used. Listing 15-6 shows the tw.cfg file I use on a Red Hat Web server system.

# Listing 15-6 An example tw.cfg file

```
```
# Sld: tw.cfg.linux, v 1.1 1994/04/04 00:34:03 gkim Exp $

# last updated: 1998/04/17 gene
```
```