
# FINDING THE PACKAGE THAT HOLDS A FILE YOU NEED 521

Do you want to continue? [Y/n?] y
Writing extended state information... Done
(Reading database ... 123778 files and directories currently installed.)
Removing apache2.2-common ... ...
Purging configuration files for apache2.2-common ...

# Finding THE PACKAGE THAT HOLDS A FILE YOU NEED

Finding a package with a name that sounds like...

- tip The aptitude search command looks for packages with names that match a pattern. For example, the command aptitude search vnc displays a list of packages that have vnc in their names. See page 529 for more information.

You may know the name of a file or utility you need but not know the name of the package that holds the file. There are several ways you can locate a package that holds the file. The Ubuntu web page, packages.ubuntu.com, allows you to search for packages based on several criteria. Partway down the page is a section titled Search that gives you two ways to search for packages. Search the contents of packages, to search for a package that holds a specific file. Enter the name of the file in the text box labeled Keyword, click the radio button labeled packages that contain files named like this, select the distribution and architecture you are working with, and click Search. The browser displays a list of packages that hold the file you are looking for. For example, suppose you are compiling a program and get the following error message:

```
xv.h:174:22: error: X11/Xlib.h: No such file or directory
```

On an Intel x86-compatible system running Lucid and the file Xlib.h holds in the X11 directory. When you enter the X11/Xlib in the text box labeled Keyword (on packages.ubuntu.com), the browser displays the following list:

```
usr/include/X11/Xlib.h libx11-dev
usr/lib/terra/lib/include/x5/lib/api/X11.lib tender
```

Click the package name on the right to display more information about the package holding the file listed on the left. The most likely candidate is the first entry, which is supported by Ubuntu and is the most generic. You can install this package using the following command:

```
$ sudo apt install libx11-dev
```

apt-file You can also use the apt-file utility to search for a package containing a specified file. Before you can use this, you must install it and update the package list on the local system. Updating the package list takes a few minutes. Because apt-file displays multiple, sequential, identical lines, you can pipe its output through uniq (page 168) to make the job of finding the right package easier:

```
$ sudo aptitude install apt-file
```

```
$ sudo apt-file update
```

```
$ apt-file search X11/Xlib.h | uniq
ivtools-dev:usr/include/lib-X11/Xlib.h
libpng6-x11-dev:usr/lib/lib-X11-1.2.1/gcc-6.6.1/Graphics/X11/Xlib.h
libbugs-x11-bundled:usr/lib/hubs/packages/X11/Graphics/X11/Xbs.hs
libx11-dev:usr/include/X11/Xlib.h
tender: usr/lib/terra/include/x5/api/X11/Xlib.h
```

Again, the most recent package (the next-to-last one listed) is probably the one you want. While apt-cache (page 530) searches installed packages, the aptitude search command (page 529) and apt-file search all packages from the repositories listed in /etc/apt/sources.list, including packages that have not downloaded. Also see dpkg-search (page 538) and dpkg-list (page 538) for other ways of searching for files.

# APT KEEPS THE SYSTEM UP-DATE

APT (Advanced Package Tool) is a collection of utilities that download, install, remove, upgrade, and report on software packages. APT utilities download packages and call dpkg (page 532) to manipulate the packages once they are on the local system. For more information refer to www.debian.org/doc/manual/apt-how.

# REPOSITORIES

Repositories hold collections of software packages and related information, including headers that describe each package and provide information on what the package depends on. Ubuntu maintains repositories for each release. Software packages from Ubuntu repositories are divided into several categories including the following:

- Ubuntu-supported open-source software
- universe—Community-maintained open-source software
- multiverse—Software restricted by copyright or legal issues
- restricted—Proprietary device drivers
- partner—Packages not part of Ubuntu; offered by other vendors
- backports—Packages from later releases

APT selects packages from repositories based on the categories specified in the sources.list file. You do not need to reconfigure APT to install supported software. You may get the following error message when you try to install a package:

```
$ sudo aptitude install xxx
Couldn't find package "xxx". However the following packages contain "xxx" in their name:
No packages will be installed, upgraded, or removed.
```

This message means that the package requested does not exist in the repositories APT is searching. It may also mean that the package does not exist; check the spelling. If you are not running the latest version of Ubuntu, it may be available on a later version by enabling the backports repository in sources.list.

# sources.list: SPECIFIES REPOSITORIES FOR APT TO SEARCH

The /etc/apt/sources.list file specifies the repositories APT searches when you ask it to find or install a package. You may modify the sources.list file to download software from non-default repositories. You can use software-properties-gtk to display the windows to modify sources.list (as explained on page 131) or you can use an editor to modify it (as explained in this section). Each line in sources.list describes one repository and has the following format:

type (deb for packages of executable files and deb-src for packages of source files); URI (the name of the repository, usually cdrom or an Internet address that starts with http://); category-list (a space-separated list of categories, see “Software categories” in the preceding section). When a line specifies a non-Ubuntu repository, the repository and category may have other values. Comments begin with a hash (#) anywhere on a line or at the end of the line. The comment #Added by software-properties indicates that software-properties-gtk added the line to sources.list. Replacing deb with deb-src causes APT to search for source packages in the same manner. Use the apt-get command to download source packages (page 532).

```
deb http://archive.ubuntu.com/ubuntu lucid restricted
```

```
deb-src http://archive.ubuntu.com/ubuntu lucid main restricted
```

Default repositories The default sources.list file includes repositories such as lucid (as originally released), lucid-updates (major bug fixes after the release of Intrepid), lucid-security (critical security-related updates), and lucid-backports (newer, less-tested software that is not reviewed by the Ubuntu security team). Separating updates from other updates enables you to set up a system to automatically install security updates while allowing you to review other updates before installing them. As installed, the sources.list file allows you to search for retrieve packages from the main, multiverse, and restricted categories (page 522) of the lucid, lucid-updates, and lucid-security repositories. Some repositories in sources.list are commented out. Removing the leading hash (#) on the lines of the repositories you want to enable. If you modify sources.list, give the command aptitude update (page 528) to update the local package indexes.

The next line, which was added to sources.list, enables APT to search a third-party repository (but see the following):

```
deb http://download.skype.com/linux/repos/debian/ stable non-free
```

In this case, the repository is named stable and the category is non-free. Although the code is compiled for Debian, it runs on Ubuntu, as is frequently the case. There are many repositories of software packages. Search the Internet for ubuntu repositories to display a sampling of them. Be selective in repositories you add to sources.list, however: when you add a repository, you are trusting the person who runs the repository not to put malicious software in packages you may download. In addition, packages that are not supported by Ubuntu can conflict with other packages and cause upgrades to fail.

# APT LOCAL PACKAGE INDEXES AND THE APT CACHE

The /var/lib/apt/lists directory holds the local package index and associated files. For each repository listed in /etc/apt/sources.list (page 523), this directory holds a file that lists information about the most recent version of each package in that repository. APT uses these files to determine whether the packages on the system, and in its cache, are the most recent versions.

The /var/cache/apt/archives directory holds downloaded deb files (page 533). By default, the apt cron script (next) limits the size of this directory and the age of the files in it.

# The apt cron Script AND APT CONFIGURATION FILES

Traditionally, APT configuration instructions are kept in a single file: /etc/apt/apt.conf; Ubuntu breaks this into smaller files that it keeps in /etc/apt/apt.conf.d. The apt cron script, kept in /etc/cron.daily so it runs daily, reads the configuration files in apt.conf.d and maintains the APT local package indexes and the APT cache based on the instructions in those files. APT tools, such as aptitude, also read these as they start. This section explains few of the many directives you can use to control APT tools.
