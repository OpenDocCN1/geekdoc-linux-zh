
# SuSE System Administration
PART III

If any of these files reported a state of missing, there would probably be problems with the package.

In addition to the state of the files in a package, the documentation files and the configuration files can be listed. To list the documentation that comes with the g package, use the following:

```
# rpm -qd gv
```

This produces the following list:

```
/usr/X11R6/man/man1/gv.1.gz
/usr/doc/packages/gv/Copyright
/usr/doc/packages/gv/comments.doc.gz
/usr/doc/packages/gv/gs.interface.gz
/usr/doc/packages/gv/gv-1.html
/usr/doc/packages/gv/gv-10.html
```

To get the configuration files for the same package, you use the following query:

```
# rpm -qc gv
```

This results in the following list:

```
/usr/X11R6/lib/X11/app-defaults/Gv
/usr/X11R6/lib/X11/gv/gv_class.ad
/usr/X11R6/lib/X11/gv/gv_system.ad
/usr/X11R6/lib/X11/gv/gv_user.ad
```

In addition to these queries, complete information about a package can be determined by using the info option. For example, the following input:

```
# rpm -qi gv
```

gives the following information about the installed kernel package:

| Name : gv | Relocations: (not relocatable) |
| :--- | :--- |
| Version : 3.5.8 | Vendor: SuSE GmbH, Nuernberg, Germany |
| Release : 74 | Build Date: Thu Jul 22 21:01:09 1999 |
| Install date: Fri Sep 10 04:40:17 1999 | Build Host: wiles.011.suse.de |
| Group : unsorted | Source RPM: gv-3.5.8-74.src.rpm |
| Size : 431277 | License: 1992 Timothy O. Theisen; 1995-97 Johannes Plass |
| Packager : feedback@suse.de | |

# Software Management
CHAPTER 19 587

Summary : GV -- a ghostview derive
Description : GV offers an X11 GUI for viewing PostScript files. This is an X11 interface to ghostscript.

Authors:
----
Tim Theisen <tim@cs.wisc.edu>
Johannes Plass <class@dipmza.physik.uni-mainz.de>

The following is a summary of the query options:

- -l Lists all files in a package
- -s Lists the state of files in a package
- -d Lists all files in a package that are marked as documentation
- -c Lists all files in a package that are marked as configuration
- - i Lists the complete information for a package

If any of these options (except -i) are given along with a -v option, the files are listed in list format. For example.

```
# rpm -qlv gv
```

outputs the following:

```
-rwx-xr-x root root 243420 Jul 22 21:01 /usr/X11R6/bin/gv
-rw-r--r-- root root 3524 Jul 22 21:01 /usr/X11R6/lib/X11/app-defaults/GV
drwxr-xr-r-- root root 1024 Jul 22 21:01 /usr/X11R6/lib/X11/gv
-rw-r--r-- root root 39445 Jul 22 21:01 /usr/X11R6/lib/X11/gv_class.ad
-rw-r--r-- root root 3524 Jul 22 21:01 /usr/X11R6/lib/X11/gv_system.ad
-rw-r--r-- root root 3524 Jul 22 21:01 /usr/X11R6/lib/X11/gv_user.ad
-r--r--r-- root root 9654 Jul 22 21:01 /usr/X11R6/man/man1/gv.ix.gz
drwxr-xr-r-- root root 1024 Jul 22 21:01 /usr/doc/packages/gv
```

In addition to the preceding, RPM understands the following query options:

- - a Lists all installed packages
- -f file Lists the package that owns the specified file
- -p package Queries a local or remote uninstalled package

# Verifying Packages

Verifying packages is an easy way to determine any problems with an installation. In verification mode, RPM compares information about an installed package against information about the original package, which is stored in the package database at install time.

The basic syntax for verifying a package is as follows:

```
rpm -V [package]
```

If a package is verified correctly, rpm does not output anything. If rpm detects a difference between the installed package and the database record, it outputs an 8-character string, where tests that fail are represented by a single character and tests that pass are represented by a period (.). The characters for failed tests are as follows:

| Character | Failed Test |
| :--- | :--- |
| 5 | MD5 Sum |
| S | Filesize |
| L | Symlink |
| T | Mtime |
| D | Device |
| U | User |
| G | Group |
| M | Mode (permissions and file type) |

For example, verifying the bash package on a system by using the following code:

```
# rpm -V bash
```

fails as follows:

```
.M..L.... /bin/bash
....L.... /bin/sh
```

This indicates that the size of the installed bash is different from the information stored in the database. This could be the result if you recompiled bash.

In addition, you can use the query option -f to verify a package containing a particular file, which is helpful when diagnosing problems with programs. For example, if ksh is behaving peculiarly, the following

```
# rpm -Vf /bin/ksh
```

# Managing Software with YaST

The YaST is a powerful graphical and command-line tool for managing software on SUSE Linux. It allows you to install, update, remove, and query software packages. Using yast is often the recommended way to manage software on SUSE because it provides a user-friendly interface and handles complex dependencies automatically.

The following command is used to start the yast interface:

```
# yast
```

When you run yast, you will be presented with a menu of options. One of the most common options is Software Management, which allows you to manage the packages installed on your system.
