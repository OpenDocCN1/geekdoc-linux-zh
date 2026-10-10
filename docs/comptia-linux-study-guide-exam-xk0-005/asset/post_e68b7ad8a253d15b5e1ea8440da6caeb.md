
To help solve that problem, Linux distributions have created a system for bundling already compiled applications for distribution. This bundle is called a **package**, and it consists of all the files required to run a single application. You can then install, remove, and manage the entire application as a single package rather than as a group of disjointed files.

Tracking software packages on a Linux system is called **package management**. Linux implements package management by using a database to track the installed packages on the system. The package management database keeps track of not only what packages are installed but also the exact files and file locations required for each application. Determining what applications are installed on your system is as easy as querying the package management database.

As you would expect, different Linux distributions have created different package management systems for working with their package management databases. However, over the years, two main package management systems have risen to the top and have become standards:

-   Debian package management
-   Red Hat package management

Because of their popularity, these are the two package management methods covered by the Linux+ exam, so these are the two package management methods we’ll cover in detail in this chapter.

Each package management system uses a different method of tracking application packages and files, but they both track similar information:

-   **Application files:** The package database tracks each individual file as well as the folder where it’s located.
-   **Library dependencies:** The package database tracks what library files are required for each application and can warn you if a dependent library file is not present when you install a package.
-   **Application version:** The package database tracks version numbers of applications so that you know when an updated version of the application is available.

The following sections discuss the tools for using each of these package management systems.

## Installing and Managing Packages

Both the Debian and Red Hat package management systems have similar sets of tools for working with software packages in the package management system. We’ll now take a look at both systems and the tools to use with them.

## Debian Package Tools

As you can probably guess, the Debian package management system is mostly used on Debian-based Linux systems, such as Ubuntu. Debian bundles application files into a single DEB package file for distribution. The core tool to use for handling DEB files is the dpkg program.

The dpkg program is a command-line utility that has options to install, update, and remove DEB package files on your Linux system. The basic format for the dpkg command is as follows:

```
dpkg [options] action package-file
```

The action parameter defines the action to be taken on the file. Table 13.2 lists common actions you'll need to use.

### TABLE 13.2 The dpkg command actions

| Action | Description |
|---|---|
| -C | Searches for broken installed packages and suggests how to fix them |
| --configure | Reconfigures an installed package |
| --get-selections | Displays currently installed packages |
| -i | Installs the package |
| -I | Displays information about an uninstalled package file |
| -l | Lists all installed packages matching a specified pattern |
| -L | Lists the installed files associated with a package |
| -p | Displays information about an installed package |
| -P | Removes an installed package, including configuration files |
| -r | Removes an installed package but leaves the configuration files |
| -S | Locates the package that owns the specified files |

Each action has a set of options that you can use to modify the basic behavior of the action, such as to force overwriting an already installed package or ignore any dependency errors.

To use the dpkg program, you must have the DEB software package available, either from an installation DVD or by downloading the package from the Internet. Often you can find DEB versions of application packages ready for distribution on the application website, or most distributions maintain a central location for packages to download.

![](img/c0a399aca0d18f8822d714ad0a173123_468_0.png)

The Debian distribution also provides a central clearinghouse for Debian packages at www.debian.org/distrib/packages.

When you download a DEB package for a precompiled application, be careful that you get the correct package for your workstation processor chip. Source code files are compiled for specific processors, and trying to run the wrong one on your system will not work. Usually the processor type is added as part of the package name.

Once you download the DEB package, use dpkg with the `-i` option to install it:

```
$ sudo dpkg -i zsh_5.3.1-4+b2_amd64.deb
Selecting previously unselected package zsh.
(Reading database ... 20432 files and directories currently installed.)
Preparing to unpack zsh_5.3.1-4+b2_amd64.deb ...
Unpacking zsh (5.3.1-4+b2) ...
dpkg: dependency problems prevent configuration of zsh:
 zsh depends on zsh-common (>= 5.3.1-4); however:
 Package zsh-common is not installed.

dpkg: error processing package zsh (--install):
 dependency problems - leaving unconfigured
Processing triggers for man-db (2.8.3-2ubuntu0.1) ...
Errors were encountered while processing:
 zsh
$
```

You can see in this example that the package management software checks to ensure that any packages that are required for the application are installed and produces an error message if any of them are missing. This gives you a clue as to what other packages you need to install.

If you'd like to see all of the packages installed on your system, use the `-l` option:

```
$ dpkg -l
Desired=Unknown/Install/Remove/Purge/Hold
| Status=Not/Inst/Conf-files/Unpacked/half-conf/Half-inst/trig-aWait/Trig
|| Err?=(none)/Reinst-required (Status, Err: uppercase=bad)
||/ Name Version Architecture Description
+++================+++++++++++++++++++================+=
ii accountsservic 0.6.45-1ubun amd64 query and manipulate accounts
ii acl 2.2.52-3buil amd64 Access control list utilities
ii acpi-support 0.142 amd64 scripts for handling ACPI
ii acpid 1:2.0.28-1ub amd64 Advanced Config and Power
ii adduser 3.116ubunt1 all add and remove users
ii adjm-theme-ub 0.3.4-0ubunt all Ajdium message style for Ubuntu
ii adwaita-icon-t 3.28.0-1ubuntu all default icon theme of GNOME
ii aisleriot 1:3.22.5-1 amd64 GNOME solitaire card game
```

You can also provide a search term on the command line to limit the packages returned in the output:

```
$ dpkg -l openssh*
Desired=Unknown/Install/Remove/Purge/Hold
| Status=Not/Inst/Conf-files/Unpacked/half-conf/Half-inst/trig-aWait/Trig
|| Err?=(none)/Reinst-required (Status,Err: uppercase=bad)
||/ Name Version Architecture Description
++=-----------------------------------------------------------------=
ii openssh-client 1:7.6p1-4ubuntu amd64 secure shell (SSH) client
un openssh-server <none> <none> (no description available)
```

If you need to remove a package, you have two options. The `-r` action removes the package but keeps any configuration and data files associated with the package installed. This is useful if you're just trying to reinstall an existing package and don't want to have to reconfigure things. If you really do want to remove the entire package, use the `-P` action, which purges the entire package, including configuration files and data files from the system.

![](img/c0a399aca0d18f8822d714ad0a173123_469_0.png)

The dpkg tool gives you direct access to the package management system, making it easier to install applications on your Debian-based system.

## Red Hat Package Tools

The Red Hat Linux distribution, along with other Red Hat-based distributions such as Fedora, Rocky, and CentOS, use the RPM package file format. The main tool for working with RPM files is the rpm program.

Similar to the dpkg tool, the rpm program is also a command-line program to install, modify, and remove RPM software packages. The basic format for the rpm program is as follows:

```
rpm action [options] package-file
```

The actions for the rpm command are shown in Table 13.3.

To use the rpm command, you must have the RPM package file downloaded onto your system. While you can use the `-i` action to install packages, it's more common to use the `-U` action, which installs the new package or upgrades the package if it's already installed. Adding the `-vh` option is a popular combination that shows the progress of the update and what it's doing:
