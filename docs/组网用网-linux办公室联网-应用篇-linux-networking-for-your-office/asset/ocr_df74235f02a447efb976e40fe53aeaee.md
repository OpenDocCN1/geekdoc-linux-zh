Most mainstream Linux distributions use the RPM format for their files. Debian, of course, uses the Debian format. Slackware uses tarballs. A few others, like Stampede, use assorted other formats. You can install the package managers for a foreign distribution on any system. For instance, you can install the RPM utilities on a Slackware system, or the Debian utilities on a Red Hat system. It’s best to stick with one package format per computer, though, to avoid conflicts.

> NOTE
> 
> Because RPM is used so widely, my comments on it apply to non-Red Hat distributions that use RPM, such as Mandrake and SuSE, as well as to Red Hat itself.

# Understanding the RPM Database

The RPM utilities maintain a database of packages you’ve installed in the directory /var/lib/rpm. The files in this directory have .rpm extensions, but they aren’t RPM package files; rather, they’re databases that maintain information on installed packages, such as

+   - Names—The names of the packages that you have installed, such as glibc and samba.
+   - Versions—The version number associated with each installed package, such as 2.1.1-6 for glibc. The version number includes both the software version (2.1.1) and a build number (6). The build number refers to minor changes to the package implemented at compile time. A revised build might add or delete support files, change the location in which a file is installed, or apply a patch that’s not part of the official software release.
+   - Installed package dependencies—Most packages depend on one or more others for proper functioning. For instance, most programs link against the standard C libraries, which are contained in the glibc package. Therefore, most packages depend upon glibc. Sometimes a package depends upon a specific version of another package; for instance, a package might depend upon glibc 2.1 or later. The RPM system allows searching for dependencies in reverse, too. For instance, if you were to try to remove glibc, the system would refuse on the grounds that so many additional packages depend upon glibc.
+   - Descriptions—Each package has assorted descriptive information associated with it, including the system on which the RPM file was created, copyright and distribution terms, and an English description of what the package does.
+   - Included files—RPM maintains a list of files that are associated with each package. RPM can use this information to delete old files when you update or remove a package. You can also search the database to find out what package owns a specific file.