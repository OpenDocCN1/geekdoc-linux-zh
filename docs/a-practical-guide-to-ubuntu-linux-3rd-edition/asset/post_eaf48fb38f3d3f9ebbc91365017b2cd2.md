
# JUMPSTART: INSTALLING AND REMOVING PACKAGES USING aptitude

This section explains how to install packages on and remove packages from a system using **aptitude**, a versatile tool that is part of APT. The **aptitude** utility has two interfaces: pseudographical and textual. This chapter covers the textual interface. Give the command **aptitude** without arguments to display the pseudographical interface. Information on this interface is available in the *aptitude user's manual* (algebraichunk.net/~dburrows/projects/aptitude/doc/en/).

If you do not know the name of the package you want to install, see page 521. If you want **aptitude** to download packages that are not supported by Ubuntu, you must add the repositories that hold those packages to the *sources.list* file; see page 523.

Before using **aptitude** to install a package, give the command `sudo aptitude update` to update the local list of packages (more about this process on page 528). By default, the *apt cron* script (page 524) updates this list daily. Even so, it is a good idea to give this command periodically until you are sure the script is updating the list.

### aptitude install

The following example calls **aptitude** to install the *tclsh* shell, which is part of the *tclsh* package:

```bash
$ sudo aptitude install tclsh
Reading package lists... Done
Building dependency tree
Reading state information... Done
Reading extended state information
Initializing package states... Done
The following NEW packages will be installed:
  tclsh
0 packages upgraded, 1 newly installed, 0 to remove and 0 not upgraded.
Need to get 359kB of archives. After unpacking 733kB will be used.
Get:1 http://us.archive.ubuntu.com/ubuntu/ lucid/universe tclsh 8.5.9-0ubuntu2 [359kB]
Fetched 359kB in 4s (80.9kB/s)
Selecting previously deselected package tclsh.
(Reading database ... 123213 files and directories currently installed.)
Unpacking tclsh (from .../tclsh-8.5.9-0ubuntu2_i386.deb) ...
Processing triggers for man-db ...
Setting up tclsh (8.5.9-0ubuntu2) ...
update-alternatives: using /usr/bin/tclsh8.5 to provide /usr/bin/tclsh (tclsh) in auto mode.
...
```

The next command installs the *apache2.2-common* package. Because this package depends on other packages, and because those packages are not installed, **aptitude** lists the packages it will automatically install in addition to the one you asked it to install. When **aptitude** is going to install more packages than you requested, it asks if you want to continue. Reply **y** if you want to continue or **n** if you want to quit.

```bash
$ sudo aptitude install apache2.2-common
...
The following NEW packages will be installed:
apache2-utils[ar] apache2.2-bin[ar] apache2.2-common libapr1[ar]
libaprutil1[ar] libaprutil1-dbd-sqlite3[u] libaprutil1-ldap[ar]
0 packages upgraded, 7 newly installed, 0 to remove and 7 not upgraded.
Need to get 3,318kB of archives. After unpacking 9,994kB will be used.
Do you want to continue? [Y/n/?] y
...
```

When you install some packages, aptitude lists suggested packages. Suggested packages may be useful but are not required with the package you are installing.

The aptitude remove command removes a package but leaves its configuration files in place, allowing you to reinstall the package without having to reconfigure it. Use purge (discussed next) in place of remove to remove a package and its configuration files.

```bash
$ sudo aptitude remove tclsh
...
The following packages will be REMOVED:
tclsh
0 packages upgraded, 0 newly installed, 1 to remove and 0 not upgraded.
Need to get 0B of archives. After unpacking 733kB will be freed.
Writing extended state information... Done
(Reading database ... 123237 files and directories currently installed.)
Removing tclsh ...
...
```

When aptitude removes a package, it also removes the dependent packages it automatically installed when it installed the original package. The following example removes apache2.2-common and its dependencies:

```bash
$ sudo aptitude remove apache2.2-common
...
The following packages will be REMOVED:
apache2-utils[u] apache2.2-bin[u] apache2.2-common libapr1[u]
libaprutil1[u] libaprutil1-dbd-sqlite3[u] libaprutil1-ldap[u]
0 packages upgraded, 0 newly installed, 7 to remove and 0 not upgraded.
Need to get 0B of archives. After unpacking 9,994kB will be freed.
Do you want to continue? [Y/n/?] y
...
```

The next example uses an alternative approach—the aptitude purge command—to remove apache2.2-common, its dependencies, and all configuration files. The (p) following apache2.2-common indicates that aptitude is removing (purging) apache2.2-common’s configuration files, as does the last line of the example.

```bash
$ sudo aptitude purge apache2.2-common
...
The following packages will be REMOVED:
apache2-utils[p] apache2.2-bin[u] apache2.2-common[p] libapr1[p]
libaprutil1[p] libaprutil1-dbd-sqlite3[p] libaprutil1-ldap[p]
0 packages upgraded, 0 newly installed, 7 to remove and 0 not upgraded.
Need to get 0B of archives. After unpacking 9,994kB will be freed.
Do you want to continue? [Y/n/?] y
Writing extended state information... Done
(Reading database ... 123778 files and directories currently installed.)
Removing apache2.2-common ...
Removing apache2.2-common ...
Removing apache2.2-common ...
Purging configuration files for apache2.2-common ...
...
```

## Finding the Package That Holds a File You Need

### Finding a package with a name that sounds like...

> The aptitude search command looks for packages with names that match a pattern. For example, the command aptitude search vnc displays a list packages that have vnc in their names. See page 529 for more information.

You may know the name of a file or utility you need but not know the name of the package that holds the file. There are several ways that you can locate a package that holds a file. The Ubuntu Web page, packages.ubuntu.com, allows you to search for packages based on several criteria. Partway down the page is a section titled Search that gives you two ways to search for packages. You can use the second, Search the contents of packages, to search for a package that holds a specific file. Enter the name of the file in the text box labeled Keyword, click the radio button labeled packages that contain files named like this, select the distribution and architecture you are working with, and click Search. The browser displays a list of packages that hold the file you are looking for. For example, suppose you are compiling a program and get the following error message:

```text
xv.h:174:22: error: X11/Xlib.h: No such file or directory
```

You are working on an Intel x86-compatible system running Lucid and need the file Xlib.h located in the X11 directory. When you enter X11/Xlib.h in the text box labeled Keyword (on packages.ubuntu.com), the browser displays the following list:

```text
usr/include/X11/Xlib.h libx11-dev
usr/lib/TenDRA/lib/include/X5/lib_api/X11/Xlib.h tendra
...
```

Click the package name on the right to display more information about the package holding the file listed on the left. The most likely candidate is the first entry, which is supported by Ubuntu and is the most generic. You can install this package using the following command:

```bash
$ sudo aptitude install libx11-dev
```

You can also use the apt-file utility to search for a package containing a specified file. Before you can use this utility, you must install it and update the package list on the local system. Updating the package list takes a few minutes. Because apt-file displays multiple, sequential, identical lines, you can pipe its output through **uniq** (page 168) to make the job of finding the right package easier:

```bash
$ sudo aptitude install apt-file
...
$ sudo apt-file update
...
$ apt-file search X11/Xlib.h | uniq
ivtools-dev: usr/include/IV-X11/Xlib.h
libghc6-c-11-dev: usr/lib/X11-1.2.1/ghc-6.6.1/Graphics/X11/Xlib.hi
libhugs-x11-bundled: usr/lib/hugs/packages/X11/Graphics/X11/Xlib.hs
libx11-dev: usr/include/X11/Xlib.h
tendra: usr/lib/TenDRA/lib/Xlib/api/X11/Xlib.h
```

Again, the most generic package (the next-to-last one listed) is probably the one you want. While **cache** (page 530) searches installed packages only, the **aptitude search command** (page 529) and **apt-file search** all packages from the repositories listed in /etc/apt/sources.list, including packages that have not been downloaded. See also **dpkg — search** (page 538) and **dpkg — listfiles** (page 538) for other ways of searching for files.

# APT: KEEPS THE SYSTEM UP-TO-DATE

APT (Advanced Package Tool) is a collection of utilities that download, install, remove, upgrade, and report on software packages. APT utilities download packages and call **dpkg** (page 532) utilities to manipulate the packages once they are on the local system. For more information refer to www.debian.org/doc/manuals/apt-howto.

# REPOSITORIES

*Repositories* hold collections of software packages and related information, including headers that describe each package and provide information on other packages the package depends on. Ubuntu maintains repositories for each of its releases.

### Software package categories

Software packages from Ubuntu repositories are divided into several categories, including the following:

- **main**—Ubuntu-supported open-source software
- **universe**—Community-maintained open-source software
- **multiverse**—Software restricted by copyright or legal issues
- **restricted**—Proprietary device drivers
- **partner**—Packages that are not part of Ubuntu; offered by other vendors
- **backports**—Packages from later releases of Ubuntu that are not available for an earlier release

APT selects packages from repositories it searches based on the categories specified in the **sources.list** file (next). You do not need to reconfigure APT to install supported software. You may get the following error message when you try to install a package:
