
Packages are usually distributed as single files that are similar to tarballs (archives created with the tar utility and usually compressed with gzip or bzip2) or zip files. Once installed, most packages consist of dozens or hundreds of files, and the package system tracks them all. Packages include additional information that aids in the subsequent duties of package management systems.

## Installed file database

Package systems maintain a database of installed files. The database includes information about every file installed via the package system, the name of the package to which it belongs, and associated additional information.

## Dependencies

One of the most important types of information maintained by the package system is dependency information—that is, the requirements of packages for one another. For instance, if SuperProg relies on UltraLib to do its work, the package database records this information. If you attempt to install SuperProg when UltraLib isn't installed, the package system won't let you do so. Similarly, if you try to uninstall UltraLib when SuperProg is installed, the package system won't let you. (You can override these prohibitions, as described later in “Forcing the Installation.” Doing so is usually inadvisable, though.)

## Checksums

The package system maintains checksums and assorted ancillary information about files. This information can be used to verify the validity of the installed software. This feature has its limits, though; it's intended to help you spot disk errors, accidental overwriting of files, or other non-malicious problems. It's of limited use in detecting intrusions, because an intruder could use the package system to install altered system software.

## Upgrades and uninstallation

By tracking files and dependencies, package systems permit easy upgrades and uninstallation: Tell the package system to upgrade or remove a package, and it will replace or remove every file in the package. Of course, this assumes that the upgrade or uninstallation doesn't cause dependency problems; if it does, the package system will block the operation unless you override it.

## Binary package creation

Both the RPM and Debian package systems provide tools to help create binary packages (those that are installed directly) from source code. This feature is particularly helpful if you're running Linux on a peculiar CPU; you can download source code and create a binary package even if the developers didn't provide explicit support for your CPU. Creating a binary package from source has advantages over compiling software from source in more conventional ways, because you can then use the package management system to track dependencies, attend to individual files, and so on.

Both the RPM and Debian package systems provide all of these basic features, although the details of their operation differ. These two package systems are incompatible with one another in the sense that their package files and their installed file databases are different; you can't directly install an RPM package on a Debian-based system or vice versa. (Tools to convert between formats do exist, and developers are working on ways to better integrate the two package formats.)

![](img/f339a9f48c4b443e61c74acb4c9c3da4_107_0.png)

Most distributions install just one package system. It’s possible to install more than one, though, and some programs (such as ‘alien’) require both for full functionality. Actually *using* both systems to install software is inadvisable because their databases are separate. If you install a library using a Debian package and then try to install an RPM that relies on that library, RPM won’t realize that the library is already installed and will return an error.

# Using RPM

The most popular package manager in the Linux world is the RPM Package Manager (RPM). RPM is also available on non-Linux platforms, although it sees less use outside the Linux world. The RPM system provides all the basic tools described in the preceding section, “Package Concepts,” such as a package database that allows for checking conflicts and ownership of particular files.

# Red Hat Distributions and Conventions

Red Hat developed RPM for its own distribution. Red Hat released the software under the General Public License (GPL), however, so others have been free to use it in their own distributions—and this is precisely what has happened. Some distributions, such as Mandriva (formerly Mandrake) and Yellow Dog, are based on Red Hat, so they use RPMs as well as many other parts of the Red Hat distribution. Others, such as SUSE, borrow less from the Red Hat template, but they do use RPMs. Of course, all Linux distributions share many common components, so even those that weren’t originally based on Red Hat are very similar to it in many ways other than their use of RPM packages. On the other hand, distributions that were originally based on Red Hat have diverged from it over time. As a result, the group of RPM-using distributions shows substantial variability, but all of them are still Linux distributions that provide the same basic tools, such as the Linux kernel, common shells, an X server, and so on.

![](img/f339a9f48c4b443e61c74acb4c9c3da4_107_1.png)

Red Hat has splintered into three distributions: Fedora is the download-able version favored by home users, students, and businesses on a tight budget. The *Red Hat* name is now reserved for the for-pay version of the distribution, known more formally as Red Hat Enterprise Linux (RHEL). CentOS is a freely redistributable version intended for enterprise users.

RPM is a cross-platform tool. As noted earlier, some non-Linux Unix systems can use RPM, although most don’t use it as their primary package-distribution system. RPM supports any CPU architecture. Red Hat Linux is or has been available for at least five CPUs: x86, x86-64 (a.k.a. AMD64 and EM64T), IA-64, Alpha, and SPARC. Among the distributions mentioned earlier, Yellow Dog is a PowerPC distribution (it runs on Apple PowerPC-based Macs and some non-Apple systems), and SUSE is available on x86, x86-64, and PowerPC systems. For the most part, source RPMs are transportable across architectures—you can use the same source RPM to build packages for x86, AMD64, PowerPC, Alpha, SPARC, or any other platform you like. Some programs are composed of architecture-independent scripts and so need no recompilation. There are also documentation and configuration packages that work on any CPU.

The convention for naming RPM packages is as follows:

```
package name-a. b. c-x. arch . rpm
```

Each of the filename components has a specific meaning:

- **Package name**: The first component (packagename) is the name of the package, such as samba or samba-server for the Samba file and print server. Note that the same program may be given different package names by different distribution maintainers.
- **Version number**: The second component (a. b. c) is the package version number, such as 3.0. 25b. The version number doesn't have to be three period-separated numbers, but that's the most common form. The program author assigns the version number.
- **Build number**: The number following the version number (x) is the build number (also known as the release number). This number follows minor changes made by the package maintainer, not by the program author. These changes may represent altered startup scripts or configuration files, changed file locations, added documentation, or patches appended to the original program to fix bugs or to make the program more compatible with the target Linux distribution. Many distribution maintainers add a letter code to the build number to distinguish their packages from those of others. Note that these numbers are not comparable across package maintainers—George's build number 5 of a package is not necessarily an improvement on Susan's build number 4 of the same package.
- **Architecture**: The final component preceding the . rpm extension (arch) is a code for the package's architecture. The i386 architecture code is common; it represents a file compiled for any x86 CPU from the 80386 onward. Some packages include optimizations for Pentiums or above (i586 or i686), and non-x86 binary packages use codes for their CPUs, such as ppc for PowerPC CPUs or x86_64 for the x86-64 platform. Scripts, documentation, and other CPU-independent packages generally use the noarch architecture code. The main exception to this rule is source RPMs, which use the src architecture code.

As an example of RPM version numbering, the Mandriva 2008.0 distribution for x86-64 ships with a Samba package called samba-server-3.0.25b-4.5mdv2008.0.x86_64.rpm, indicating that this is build 4.5mdv2008.0 of Samba 3.0.25b, compiled with x86-64 optimizations. These naming conventions are just that, though—conventions. It's possible to rename a package however you like, and it will still install and work. The information in the filename is retained within the package. This fact can be useful if you're ever forced to transfer RPMs using a medium that doesn't allow for long filenames. In fact, early versions of SUSE eschewed long filenames, preferring short filenames such as samba.rpm.
