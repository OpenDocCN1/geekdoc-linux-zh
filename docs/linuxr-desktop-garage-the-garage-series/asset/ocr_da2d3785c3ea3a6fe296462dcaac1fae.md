more is more. Because we are human. Because we are greedy. Because we want it all. Because, "All your base are belong to us." The real reasons are, of course, that with computers, there are always new programs, new options, and new versions to download and install. Staying up-to-date and trying new programs make up the vibrant, plugged-in heart of most computer users.

# Installing New Software in Order of Sanity

With so many sources and methods for installing new software on your Linux system, you might not know where to turn. You don't want to get stuck installing incorrect versions or configuring a version of some program that creates a lot more work than a more appropriate version might. To avoid frustration, check out these avenues for installing new software, in the order of sanity:

+   1. Apt, Yum, or Mandrake Update
+   2. Your installation disks
+   3. RPM packages downloaded from the developers' or company's Web site
+   4. Sourceforge.net
+   5. Rpmfind.net or rpm.pbone.net
+   6. Downloaded compressed files of the source code to install from

If you look for your new software in this order, you will usually save the time and trouble of unnecessary dependency issues, errors, or configuration tweaks.

Yeah, yeah, yeah, in Linux, there are always choices. If you're tired of hearing me say that, just get used to it. The abundance of choices is an intrinsic characteristic of all things Linux. In the case of installing new software, you have some common choices and some different choices, based on which distribution you are using.

# RPM Files

Using packages is the most efficient way to install new software in Linux. Both Fedora and Mandrake use RPM packages for installing programs. RPM (Red Hat Package Manager) files are the closest Linux has to a standard program installer. An RPM package contains installation files and instructions for where to install the package files. Locations for system directories differ among distributions, and not all distributions can use RPM files. For distros that are RPM based (including Fedora, Mandrake, SUSE, and Yellow Dog), programs usually have different RPMs for different Linux distributions. RPM packages can also be specific to your computer's CPU architecture. You might see an architecture specified in a package's filename. You can use that part of the filename