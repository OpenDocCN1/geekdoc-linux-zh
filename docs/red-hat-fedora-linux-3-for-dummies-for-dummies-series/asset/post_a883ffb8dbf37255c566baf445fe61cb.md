
# Introducing the Red Hat Package Manager

One of the primary reasons that the Red Hat Linux (and, subsequently, Fedora Core) distributions became so popular was that Red Hat, Inc. added value for its customers with technologies such as RPM.

All the software that was installed during the Fedora Core installation process is stored in RPM’s format, called packages. A package is a collection of individual software (applications, libraries, and documentation, for example) contained in one file.

The package-management concept has been around for quite a while. The major Unix vendors supply their own systems. The idea is to distribute, in a single file, some software that performs a particular function — and have a Package Manager do the work of installing, removing, and managing the individual files. The Linux world has benefited greatly from this system, which simplifies the distribution and use of software.

You can install software without RPM, but we’re not sure why you would want to — the RPM package contains everything you need to install and run an application. For example, if you didn’t have the RPM package, installing Mozilla would work a little something like this: You would have to install the individual pieces that make up the Mozilla system, which can require dozens of steps. You can also install, update, or uninstall RPM software (see the following section for details).

We remember, back in the day, when we used the Linux operating system for the first time. We had to install all the software using the dreaded tape archive system (TAR) ... from dozens of floppies! Trust us: Installing, maintaining, and upgrading Linux with tar was a difficult task. RPM has made life easier for those of us who used to walk uphill both ways in the snow to school and back.

The `/Fedora/RPMS` directory on the companion DVD contains all the Fedora Core RPM packages.

RPM performs three basic functions: It installs, upgrades, and removes packages. In addition to these functions, it can find out all sorts of information about installed and yet-to-be-installed packages. (All this, and it washes windows too.) Here’s a brief rundown of each function:

- **Installing packages:** RPM installs software. Software systems, such as Mozilla, have files of all types that must be put into certain locations in order to work properly. For example, under Red Hat, some (but not all) Mozilla files need to go into the `/usr/bin` directory. RPM performs this organizational stuff automatically, without any fuss or muss. RPM not only installs files in their proper directories, but also performs tasks such as creating the directories and running scripts to do the things that need to be done. (It’s such a tidy and organized little scamp.)

- **Upgrading packages:** Gone are the days when updating a system was worse than going to the dentist. RPM acts like the personal Linux assistant that we all wish we’d had, by updating existing software packages for you. RPM also keeps track (in its own database) of all the packages you have installed. When you upgrade a package, RPM does all the bookkeeping chores and replaces only the files that need to be replaced. It also saves the configuration files it replaces.

- **Removing packages:** The package database RPM keeps is also useful in removing packages. To put it simply, RPM takes out the trash. (Housekeeping was never so easy.) RPM goes to each file and uninstalls it. Directories belonging to the package are also removed when no files from other packages occupy them.

- **Querying packages and files:** RPM can also give you a great deal of information about a package and its files. You can use the query function to find out the function of a package and which files belong to it. RPM can also work on the RPM packages themselves, regardless of whether they have been installed.

- **Verifying packages:** RPM can validate an installed package against a `checksum` (a computer fingerprint) to see whether and how it has been changed. This feature is useful for security reasons. If you suspect that a file or system has been hacked, you can use RPM to find out how it has changed.

RPM packages often include configuration files as part of their installation. If you erase an RPM package, those configuration files are **not deleted** but rather are renamed by appending the suffix `.rpmsave` to the end of the original filename. For example, removing the Kerberos package, `krb5afs`, saves the configuration file by renaming it `/etc/krb.conf` to `/etc/krb.conf.rpmsave`.

When you remove a package, RPM removes the associated files and directories. RPM cleans up after itself — what Martha Stewart (when she’s not on laundry detail) would definitely call “a good thing.”

## Using the Red Hat Package Manager

Fedora Core provides a tool named Red Hat Package Manager for working with RPM packages. The Package Manager graphical tool provides all the functions for managing RPMs. It’s like putting an automatic transmission on a car: The Package Manager does the shifting for you — okay, but you still have to drive it.

The Package Manager provides easy access to RPM functions; you can install, upgrade, remove, query, and verify. This section describes how to use the Package Manager to rev up your RPM.

To start the Package Manager, click the GNOME Menu button and choose System Settings Add/Remove Applications. If you aren't logged in as the root user, type the root password in the Input window when you're prompted. A progress window appears briefly while the Package Manager determines which packages you have installed. After "thinking," the Package Management window appears.

The Package Manager displays all the Red Hat packages groups that are installed by default on your system. Individual packages are organized into groups, such as the X Window System and GNOME. When the check box to the left of a group is active — as designated by a check mark — one or more packages from that group is installed. The number to the right of the Package group shows how many packages of the total number in the group are installed.

Clicking the Details option opens the GNOME Desktop Package Details window, which shows all the base and optional packages in the group; short, one-line descriptions of each package are also displayed next to each package. Standard Packages are always installed with a package group. Extra packages are, well, optionally installed.

## Installing an RPM package from the DVD

When you install your Fedora Core system, all the software that is copied to your hard drive from the DVD comes from RPM packages. When you want to add software from the companion DVD or an RPM repository, such as www.freshmeat.net, or from Red Hat, at www.redhat.com, you can do so by using the Install button. To install an RPM package from a CD-ROM, follow these steps:

1. **Start the Package Manager: Choose System Tools Add/Remove Packages.**
   Enter the root password in the Information window, if you're prompted.

2. **When the Add and Remove Software window opens, select the package group you want to install.**
   For example, if you want to install the Mozilla e-mail client, you have to do some exploring first. Scroll down to the Graphical Internet package group. The short description next to the package group says "This group includes graphical e-mail, Web, and chat clients," which indicates that you're on the right path.

3. Click the Details button to find out the details of the package you're installing.
   For example, select the Graphical Internet group and the Graphical Internet Package Details window opens. You see that the Mozilla mail client is included.

4. Select the check box next to the menu option.

5. Click the Close button to return to the Package Management window.

6. Click the Update button and the Preparing Systems Update window opens.
   The Package Manager determines which additional packages are needed by the package you're installing. After the dependencies are determined, the Completed System Preparation window displays the number of packages to be installed and how much disk space they require.

7. Click the Continue button.
   The Information window opens and you're prompted to insert the DVD.

8. Insert the CD and click OK.
   The System Update Progress Installing window shows a progress meter.

9. Insert additional CDs, if you're prompted, and click the OK button in the Information window.
   After the installation process is finished, the System Update Process window shows the Update Complete message.

10. Click the OK button to return to the Add and Remove Software window.

Until the advent of the RPM (and the Debian Package Manager on Debian Linux systems), Linux software was distributed only by tar archives, which are sometimes referred to as tarballs (or more descriptively, hairballs). The tar file storage mechanism stores one or more files in a single file in a tar format. A tar file has the `.tar` file suffix; if the tar file is compressed, it has a suffix like `.tgz` or `.tar.gz`. Using the tar-based distribution system is sufficient if your software doesn't change often and you're young. But when you need to upgrade or change software or work with complex software systems, tar becomes quite difficult to work with. Rather than spend your life spitting up hairballs, use systems such as RPM to greatly simplify your life.

## Removing an RPM package

You can remove Red Hat packages as easily as you install them. Use the RPM erase (-e) function, which is the opposite of the install (-i) function. The
