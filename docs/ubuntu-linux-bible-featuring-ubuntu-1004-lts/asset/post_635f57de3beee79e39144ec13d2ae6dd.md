
# Part II: Ubuntu for Desktop Users

Figure 19-11 displays a menu in aptitude using aptitude's default color scheme. Need I say more? This is the sort of thing that gives Linux applications a bad name to people who are used to Macintosh (or even Windows) graphics.

# FIGURE 19-11

A menu in the default aptitude interface

```
root@ubuntu:~$ apt remove vlc
aptitude [command] package search option views help
  aptitude [2.1.0]
  (2013)
  Installed Packages: ...
  Up to date since the last time you opened
  your window. Tip: Use the screen menu.

This group contains 355 packages

(1) Suggest removal
2) Apply next
3) Execute all and remove
```

For more detail (and less opinionated) information about using the aptitude user interface, see the online reference information for aptitude (man aptitude) or search the Web for rel-event information.

# Using aptitude to Install Recommended Software

If you are using apt-get to install new software and the apt-get utility informs you that other packages are recommended or suggested for installation, you may want to consider using aptitude's command-line interface rather than apt-get. The DEB packages by Ubuntu identify various dependencies, divided into five classes:

- Conflicts: Packages (or package versions) with which a package conflicts, and which cannot therefore be installed on a system when a specified package is being installed
- Depends: Packages that are mandatory for the correct operation of a package, and which therefore must also be installed when a given package is installed
- Enhances: Packages whose operation is improved or simplified as a result of installing a package, but between which there is no direct relationship
- Pre-Depends: Packages that must be completely installed on your system before you can install a given package

# Chapter 19: Adding, Removing, and Updating Software

- Recommends: Packages that you should probably have, but which are not absolutely required for the correct operation of a given package
- Suggestions: Packages that may be useful, and which are normally installed on systems where a given package is installed

Requirements marked as Pre-Deps (which are rarely used or necessary) must be satisfied before you install a given package. Requirements marked as Depends are automatically installed along with a given package. The aptitude utility enables you to automatically install packages that are recommended for installation by including the --recommends command-line option on your aptitude install command.

The aptitude utility is the only command-line package installation utility that enables you to automatically install recommended packages with required packages. Specifying the --recommends command-line option when installing from the command line can be quite convenient and save you time in the future if you discover that you want to use a recommended package. A similar option to aptitude's --recommends option for apt, --recommends, and a related one for installing suggested packages, --suggest, have been "suggested for apt for a long time, but are not available in any version of apt that I've ever seen. As I'll discuss in this section of the chapter on Synaptic the Synaptic tool provides configuration options for considering recommended packages to be dependencies and automatically installing them; similarly, its interface provides a runtime option to manually selecting suggested packages and including them as part of the package installation process.

# Advantages of using aptitude to Install and Remove Software

Although I am not such a fan of the aptitude user interface, aptitude itself does provide some significantly useful capabilities. Its search capabilities, discussed earlier in this chapter in the section, "Listing the Packages That Are Available for Your System," are easy to use and powerful—exactly what you want from a utility. Similarly, the current version of aptitude has some advantages when installing and specifically, when removing packages. The most significant of these is fact that aptitude remembers dependency information when installing packages. Every Ubuntu Package Management utility understands requirements when installing packages, aptitude remembers this information and can therefore use it if you decide to remove packages.

The following sample output shows an attempt to remove the PostgreSQL database system from one of my Ubuntu systems using apt-get:

```
$ sudo apt-get remove postgresql
Password:
Reading lists... Done
Building dependency tree... Done
The following packages will be REMOVED
postgresql
```

# Part II: Ubuntu for Desktop Users

0 upgraded, 0 newly installed, 1 to remove and 0 not upgraded.
Need to get MB of archives.
After unpacking 45.1kB disk space will be freed.
Do you want to continue [Y/n]? n
Abort.

With aptitude to remove the same package is much more useful because it also offers to remove packages that were installed along with the postgresql package that are no longer needed on that system if the postgresql package itself is removed, and in the following example:

```
$ sudo aptitude remove postgresql
Reading package lists... Done
Building dependency tree... Done
Reading extended state information
Initializing package states... Done
Building database... Done
The following packages are unused and will be REMOVED:
postgresql-libpq-7.4 postgresql-libpython-7.4 postgresql-pltlc-7.4
The following packages will be REMOVED:
postgresql
0 packages upgraded, 0 newly installed, 4 to remove \
0 and not upgraded.
Need to get MB of archives. After unpacking 651kB will be freed.
Do you want to continue? [Y/n]? Y
[much output deleted]
```

For me, this makes aptitude a much more attractive command-line package solution than apt-get. Note that aptitude uses dependency information for packages that it has installed, so I tend to use aptitude from the command line for both package installation and removal. Otherwise, if you actively install and remove large numbers of packages, your system tends to accumulate packages that you no longer need but you're not aware of. For information about ways of checking for unneeded packages and removing them, the last section of this chapter, "Keeping your System Lean, Mean, and Pristine."

# Using Synaptic to Add and Remove Software

The Synaptic Package Manager is a graphical, GNOME application for installing, removing, and generally managing Ubuntu software packages. In the unlikely event that this is the only sentence you read in this book, you may not know that I recommend using the Synaptic Package Management utility for almost all package management tasks on Ubuntu systems. It's true. Synaptic is the type of administrative application that users of other Linux distributions and other personal computer operating systems they had.

# Chapter 19: Adding, Removing, and Updating Software

Synaptic was originally developed by the folks at Connectiva Linux, a Latin Linux distribution was eventually acquired by Mandrake Linux, which then changed its name to Mandriva to highlight that it wasn't your father's Mandrake Linux distribution anymore. Synaptic was originally written using the WINGS toolkit by the Window Maker X manager (www.windowmaker.info), which attempted to provide a look and feel familiar to users of NeXT computer systems. Today, Synaptic is built with the standard GTK+ toolkit by GNOME. Interestingly, Connectiva was an RPM-based distribution, but Synaptic is now more commonly associated with the DEB packages provided by distributions such as Ubuntu and Debian.

The Synaptic Package Management utility is installed by default as part of any Ubuntu installation. Select the System Administration Synaptic Package Manager menu item to start the Synaptic tool. When trying to run any graphical administrative application on Ubuntu, you will be prompted for your administrative password before Synaptic actually starts. Figure 19-12

# FIGURE 19-12

The start dialog for Synaptic utility

![](img/1a233c34336fbf5a85d6eb785e401709_740_0.png)

The left pane of the Synaptic dialog in Figure 19-12 shows the conceptual categories into which software is organized based on the default repositories enabled when you first install Ubuntu.

- Left pane: Organizes available software into various conceptual categories based on the repositories listed in /etc/apt/sources.list.
