+   - GNOME (desktop environment): version 2.28.0
+   - KDE (desktop environment): version 4.3.3
+   - X Window System (X.org graphical windowing system): version 11, Release 1.7.1
+   - OpenOffice.org (office suite): version 3.1.1
+   - GIMP (image manipulation application): version 2.6.7
+   - GCC (GNU C language compilation system): version 4.4.2
+   - Apache (Web server): version 2.2.13
+   - Samba (Windows SMB file/print sharing): version 3.4.2
+   - CUPS (print services): version 1.4.2
+   - Sendmail (Mail Transport Agent): version 8.14.3
+   - vsFTpd (secure FTP server): version 2.2.0
+   - INN (Usenet news server): version 2.5.0
+   - MySQL (database server): version 5.1.39
+   - BIND (Domain Name System server): version 9.6.1

> TIP: These features are constantly being updated. Fedora ships with tools to help keep your system up-to-date with the latest versions of software.

The following sections describe major new features of Fedora 12 (besides the latest versions of those basic components just named).

# PackageKit Software Management improvements

Starting in Fedora 9, PackageKit became the default GUI package for managing software updates and adding software packages. It is a community-developed software management system that has replaced the Red Hat-developed Package Updater and Package Manager applications.

With PackageKit, an icon in the top panel alerts you when software updates are available. Or you can use the PackageKit Package Manager for GNOME to search for and install additional packages.

> NOTE: One of the more controversial new features of PackageKit in the latest release of Fedora involves allowing a regular user to install signed packages with PackageKit without entering the root password. After Fedora 12 was released, that feature was reversed. So, once you get the first round of updates for Fedora, you will again be required to provide the root password to install packages. PackageKit is described in Chapter 5.