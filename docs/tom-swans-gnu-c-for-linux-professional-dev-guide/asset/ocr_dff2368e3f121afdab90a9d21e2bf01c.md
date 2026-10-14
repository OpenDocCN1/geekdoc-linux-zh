+   1. Back up all files. Even though upgrading your installation doesn’t affect user directories, making a complete backup before upgrading is a good idea in case something goes wrong.
+   2. Insert the CD-ROM and reboot. If Linux is running, to reboot, log on as root and enter the command `shutdown -r now`.
+   3. When you see the opening installation screen, press Enter for a normal installation—do not select expert mode. Select various options such as your keyboard type and language.
+   4. Eventually, you are shown a titled Installation Path. Choose the Upgrade button (press Tab and Enter). This bypasses the drive-partitioning parts of the installation and proceeds straight to building a database of installed packages. This takes a few minutes.
+   5. Eventually, you see another window titled Upgrade Packages. Answer Yes to customize the set of packages already installed. Unfortunately, this part of the installation is not the same as the original that presents components for installation—instead, you must specify each package. Select a listed entry to display the individual packages. At the least, select Development/Debuggers (gdb, xxgdb), Development/Languages (gcc, libstdc++-devel, pgcc, pgcc-c++), Development/Libraries (glib-devel, glibc-devel, gtk+-devel, readline-devel, Xaw3d-devel, XFree86-devel), and Development/Tools (autoconf, automake, make, patch, and others). You may also select other packages at this time. Select the Done command when you are finished, but review all your selections before selecting Done—the only way to return to this step is to start over.

> **Tip**
> 
> A log of the upgraded packages is saved in `/tmp/upgrade.log`. Read and save this file after the upgrade installation finishes.

The rest of the upgrade-installation is automatic, although you might have to enter responses in a few more display screens. When installation finishes, Linux reboots. Be sure to remove the CD-ROM when this happens.

After logging on, enter the test command `g++ -v` to check that GNU C++ is properly installed. If so, you can skip to “How to Install This Book’s Sample Programs.”

# INSTALLING PACKAGES WITH RPM

Another way to install packages is to run the Red Hat Package Manager (RPM). This utility has become a standard on many different types of Linux, so even if you aren’t using Red Hat’s version, you probably have RPM on your system. (The included CD-ROM comes with RPM for console and X display modes.) RPM maintains a database of installed packages, so you can use it also to check whether a particular file is installed.

A package is an archive that contains the files for a single program, or for a group of programs. A package might also contain updates in the form of patches, and it includes directory and installation information. You can find packages on various Linux Web sites and also on most Linux CD-ROMs. They are typically located in directories named RPMS (binary