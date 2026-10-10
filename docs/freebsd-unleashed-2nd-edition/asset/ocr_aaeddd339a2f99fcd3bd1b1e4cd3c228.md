But FreeBSD takes things to yet another level of convenience. It has its own package management system, the pkg_* tools, which this chapter covers in detail. FreeBSD also has a supplementary system called the ports. Ports allow you to compile software from its original sources with guaranteed, one-command simplicity.

# # Introduction to Packages

Jordan Hubbard, formerly one of the core developers of FreeBSD (now working at Apple as an architect of Mac OS X), is responsible for most of the initial work on the package system. FreeBSD's system has been adopted by NetBSD and other platforms and refined over the years, with the best of the independent development efforts being rolled back into FreeBSD.

By its simplest definition, a package system is a way of bundling up software (including config files, shared libraries, and documentation) and extracting it again onto another machine, in which its configuration will be valid enough that the software can run properly on the new machine. Early package managers did little more than manage the bundling and extraction processes. RPM and FreeBSD's packagers both have numerous additional features:

+   - They maintain a database on each machine that shows which software and which version of each package are installed.
+   - They can grab a remote file from an FTP site (generally, the primary distribution site).
+   - They keep track of dependencies or any additional packages that must be installed for the one you're installing to run.
+   - They can do upgrades and deinstalls as well as installations.

The difference between the two packagers is related very closely to the different development philosophies of FreeBSD and Linux. Linux has a number of different distributions, with different versions of glibc (a set of core-shared libraries not relevant to FreeBSD) and a nearly infinite variety of hardware on which the operating system can run. RPM must necessarily be quite complex in order to handle all this diversity—and indeed it is. Its command-line interface is fairly arcane and requires a lot of documentation to be used properly. FreeBSD, however, benefits from a centralized development model and a single supported hardware platform, so the package model can be much simpler, both in architecture and usage.

As we discussed in Chapter 8, “The FreeBSD Filesystem,” the /usr/local hierarchy is reserved for items that you install yourself, which referers specifically to software you install from the ports and packages. Table 14.1 shows the /usr/local directory structure (although your installation may vary slightly).