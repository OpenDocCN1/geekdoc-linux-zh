
## CHAPTER 14
## Installing Additional Software

### IN THIS CHAPTER
- Introduction to Packages
- Installing Packages
- Removing Packages
- Introduction to Ports
- Installing and Removing Ports
- Upgrading a Port
- Updating and Maintaining Your Ports
- Fresh Ports

Up until now, we have covered topics that are largely applicable to many different types of Unix systems. Pretty much any such system, whether commercial or open source, operates the same way regarding the filesystem structure, process automation, and general administration. What sets FreeBSD apart from its BSD brethren (Linux and commercial Unix software) is the model by which the administrator adds new software.

With Solaris, if you want to add a new piece of the software to the system, you have to find a precompiled binary for your particular platform and install it yourself (usually without the aid of installers that help you put it in the right place), because Solaris typically doesn't come with *gcc* (the standard GNU C/C++ compiler). Other systems, such as IRIX and HP-UX, do come with *gcc*, but you still have to find the source code for the program you want to install and then run its configuration script, compile it (a step that's often much easier said than done), and install it.

Different flavors of Linux take this a step further with the concept of *packages*, which are essentially all-in-one bundles that contain the proper binary for your system as well as any required libraries, plus the necessary information about where to install everything. The Red Hat Package Manager (RPM) system is a GNU-licensed packager that runs on many systems, including FreeBSD. Its popularity was a large part of what pushed Red Hat to the top of the Linux distributions, edging out the previous favorite, Slackware. RPM allows administrators to keep tabs on their installed software and to upgrade, deinstall, and add new packages with unprecedented ease.

But FreeBSD takes things to yet another level of convenience. It has its own package management system, the `pkg_*` tools, which this chapter covers in detail. FreeBSD also has a supplementary system called the ports. Ports allow you to compile software from its original sources with guaranteed, one-command simplicity.

### Introduction to Packages

Jordan Hubbard, formerly one of the core developers of FreeBSD (now working at Apple as an architect of Mac OS X), is responsible for most of the initial work on the package system. FreeBSD's system has been adopted by NetBSD and other platforms and refined over the years, with the best of the independent development efforts being rolled back into FreeBSD.

By its simplest definition, a package system is a way of bundling up software (including config files, shared libraries, and documentation) and extracting it again onto another machine, in which its configuration will be valid enough that the software can run properly on the new machine. Early package managers did little more than manage the bundling and extraction processes. RPM and FreeBSD's packagers both have numerous additional features:

- They maintain a database on each machine that shows which software and which version of each package are installed.
- They can grab a remote file from an FTP site (generally, the primary distribution site).
- They keep track of dependencies or any additional packages that must be installed for the one you're installing to run.
- They can do upgrades and deinstalls as well as installations.

The difference between the two packagers is related very closely to the different development philosophies of FreeBSD and Linux. Linux has a number of different distributions, with different versions of glibc (a set of core-shared libraries not relevant to FreeBSD) and a nearly infinite variety of hardware on which the operating system can run. RPM must necessarily be quite complex in order to handle all this diversity—and indeed it is. Its command-line interface is fairly arcane and requires a lot of documentation to be used properly. FreeBSD, however, benefits from a centralized development model and a single supported hardware platform, so the package model can be much simpler, both in architecture and usage.

As we discussed in Chapter 8, “The FreeBSD Filesystem,” the /usr/local hierarchy is reserved for items that you install yourself, which refers specifically to software you install from the ports and packages. Table 14.1 shows the /usr/local directory structure (although your installation may vary slightly).

**TABLE 14.1** Directory Structure Within /usr/local

| Subdirectory | Purpose |
| :--- | :--- |
| bin | Binaries (compiled programs) |
| etc | Configuration files |
| include | C include files, used for building new software |
| info | Various supporting types of data for building documentation |
| lib | Shared libraries |
| libexec | Supporting binaries used by other programs |
| man | Manual pages for installed software |
| sbin | System binaries (programs that alter system behavior) |
| share | Platform-independent materials (data files, documentation, and so on) |
| var | Variable files for installed software |

In other words, `/usr/local` has the same hierarchy found directly within `/usr` (with the exception that `man` pages are found at `/usr/local/man` rather than `/usr/local/share/man`, as you might expect). FreeBSD's package system keeps anything you install in the `/usr/local` tree and out of the `/usr` tree, thus maintaining the seamless but strict separation between base and user-installed software.

### Shared Libraries and Dependencies

A *shared library* is a centralized file that provides precompiled function calls. Using a shared library, a program can access certain functions without having to have those functions built in to itself. This technique, known as *dynamic linking*, reduces file size and redundancy in comparison to static linking, which compiles all necessary functions into every program. Shared libraries exist on nearly all platforms, although they have different names—for instance, Windows calls them Dynamic Link Libraries (DLLs).

FreeBSD already has a large number of shared libraries installed in the base system—enough to support all the software that's part of the base system—and provides hooks for software that you might install later. Nevertheless, you're almost certain to run across a program that needs a shared library that doesn't exist in the base FreeBSD.

In FreeBSD, basic shared libraries are stored in `/usr/lib`, and any shared libraries that you install go into `/usr/local/lib`. All programs know automatically to look first in `/usr/lib` for the shared libraries they need, and then look in `/usr/local/lib` (as well as a couple of other places). You can control this search path in `/etc/rc.conf`, as you saw in Chapter 10, “System Configuration and Startup Scripts.”

Every package has a listing of dependencies that includes both shared libraries and executables (programs). If a dependency isn't already installed, the package system automatically hunts it down and installs it before proceeding with the installation. If you later remove some program or library (via the package tools) that is a dependency for some other installed package, the tools tell you about this and refuse to proceed.

### Obtaining Information on Installed Packages

The first step toward getting to know the packages is to explore the information about the packages that you have already installed. Chances are you’ve installed some packages as you read earlier sections of this book, or you may have some from a custom installation. If not, don’t worry—the information here will be just as useful to you later.

The tools you use to manage packages are `pkg_add`, `pkg_delete`, `pkg_info`, `pkg_update`, `pkg_version`, and `pkg_create`. Each one does pretty much what you would expect it to do; one hallmark of FreeBSD’s style is to use differently named programs rather than obscure switches and parameters. Each of these tools interacts with a filesystem database at `/var/db/pkg`, which you can consult by simply using `ls` to take a quick glance at your system’s package status. This repository has a directory for each installed package that includes information about the packing list (the manifest of files in the package) and the dependencies. `pkg_info` uses this database to print out the short descriptions of every package you currently have installed, as you can see in Listing 14.1.

**LISTING 14.1** Sample Output from `pkg_info`

```text
# `pkg_info`
`ImageMagick-5.2.7_2` An X11 package for display and interactive manipulation of
`analog-4.16` An extremely fast program for analyzing WWW logfiles
`apache-1.3.19` The extremely popular Apache http server. Very fast, very
`arc-5.21e_8` Create & extract files from DOS `.ARC` files
`aub-2.0_5` Assemble uasent binaries
`autoconf-2.13` Automatically configure source code on many Un*x platforms
`dict-1.4_9` Dictionary Server Protocol (RFC2229) client
`elm-2.4ME+68` A once-popular mail user agent, unofficial clone
`emacs-19.34b` GNU editing macros
```

You can also get lots of information on any single package with the `-v` switch. As with RPM, packages in FreeBSD have names with multiple parts separated by dashes—the package name, followed by the version. However, RPM files tend to be geared toward multiple platforms, so the “platform” part of the package name is not used. Instead, a FreeBSD package file takes the form `name-version.tgz`. Here’s an example: `bzip-0.21.tgz`

Packages are generally `.tgz` files (called `tarbals`), which is shorthand for `.tar.gz`. Using tarbals is the traditional way of archiving a directory structure under Unix—you first pack the directory into one file using `tar` and then compress it using `gzip`. To use tools such as `pkg_info -v`, you need to specify the full package name, including the version, as shown in Listing 14.2.
