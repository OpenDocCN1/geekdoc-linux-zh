
## Exercise 8-6: Working with Shared Libraries

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_361_0.png)

For more information watch Exercise 8-6.

In this exercise, you will practice managing shared libraries. Complete the following:

- 1. With your system running, open a terminal session.
- 2. If necessary, change to your root user account by entering `su -` followed by your root user's password.
- 3. View the shared libraries used by the ping executable on your system by entering `ldd -v /bin/ping` at the shell prompt. You should see that ping requires the `libc.so.6` shared library.
- 4. Find the location of the `lib64/libc.so.6` library file on your system by entering `find / -name libc.so.6` at the shell prompt. On a 32-bit system, you should see that the file resides in `/lib`. On a 64-bit system, it probably resides in `/lib64`.
- 5. View your system's library cache by entering `ldconfig -p` at the shell prompt.
- 6. Rebuild your library cache by entering `ldconfig -v` at the shell prompt.

That's it for this chapter! Terms like *apt*, *tarball*, and *rpm* should no longer frighten you because you know how to effectively manage software on a Linux system!

## Chapter Review

In this chapter, I discussed how you go about managing software on a Linux system. I first pointed out that you can use either graphical or command-line tools to manage software on a Linux system. I emphasized that a good Linux admin shouldn't be dependent on the graphical tools to manage software. He or she should also know how to use command-line software management tools. I also pointed out that not all software can be managed using graphical tools. In fact, the LPIC-1/CompTIA Linux+ exam focuses strictly on command-line utilities.

We first looked at managing RPM packages. I pointed out that RPM stores information about installed packages in the RPM database file (*var/lib/rpm*). I spent time reviewing the various resources available to you for obtaining Linux software. These include the following:

- Your installation CD or DVD
- Open source project web sites
- http://www.rpmfind.net
- http://www.sourceforge.net
- http://linux.tucows.com
- http://www.freshmeat.net
- http://www.linux.org

I pointed out that you should verify your downloads using checksums whenever possible. You can generate a checksum using the sum command on the file you downloaded and compare it to the checksum provided on the web site where you obtained it.

We then reviewed the process for installing software using RPM packages. I pointed out that you have to use a package manager to manage prepackaged software, such as the Red Hat Package Manager (RPM). RPM packages are precompiled software packages that the package manager can install on your system. Because they are precompiled, you need to verify that a given package is compatible with your system before installing it. To do this, you need to review the package filename. The package filename includes the following information:

- Package name
- Version number
- Release number
- Compatible distribution (optional)
- Architecture type

You can enter rpm --checksig to verify the digital signature of an RPM package before you install it. You can then enter rpm -i to actually install the package file on your system. I pointed out that many RPM packages are dependent on other packages being installed on the system for them to work properly. If these packages aren't present, the software won't run. The rpm utility automatically checks to see if dependent software is installed before it installs a new package. You can also run rpm -test to check for dependencies before installing.

I then discussed the process you need to follow to uninstall software from your Linux system. To uninstall an RPM package, you enter rpm -e.

I also pointed out that you can use the rpm command to update an existing package to a newer version. This is done using the rpm -U command. The rpm command can also be used to query and verify RPM packages. To query a package, you use the -q option with rpm. To verify a package, you use the -V option. If you determine that a package has been damaged, you can re-install an existing package by entering rpm -U --replacepkgs.

Next, we looked at using the yum command as an alternative to rpm. I pointed out that yum allows you to download and then install a package and all of its dependencies with a single command. We looked at commonly used yum commands, such as yum install packagename and yum remove packagename. If you only want to download the file but not install it, you can use the yumdownloader command instead of yum. We looked at the yum.conf file, which is the configuration file for yum. It defines such things as the software repository URLs and their names where yum will search for packages, the directory (cachedir) where downloaded packages will be saved, and where the yum log file (logfile) will be saved. I also pointed out that repository information can be stored in this file or in separate files named filename.repo in the /etc/yum.repos.d directory.

I then discussed the process you need to follow to install software from source code. I pointed out that most software installed in this manner is distributed in tarball format. After downloading the file, you need to use the tar -xzvf command to extract the files from the tarball file. Once extracted, you switch to the new directory created when the tarball was extracted and run . / configure. This script checks your system and creates the Makefile file. You then run the make command to create the binary executable file from the source code text files using the instructions provided in the Makefile file. Once done, you use the make install command to install the executable on the system. Software installed from source code will use either an uninstall script in the original installation files or an uninstall target in the Makefile file that is called using the make uninstall command.

We then shifted gears and looked at managing Debian software packages. Distributions based on the Debian distribution use the Debian Package Manager (dpkg). Debian packages use a naming convention that is similar to that used by RPM packages: *package_name_version_architecture.deb*. Like RPM packages, Debian packages include dependency information.

We then looked at using the dpkg command to install, uninstall, query, and verify Debian packages. We also looked at the apt-cache command, which is used to query package information from the Debian package database (called the package cache). I also reviewed how to use apt-get, which is the Debian equivalent of yum on an RPM-based system. It automatically downloads and installs packages (along with all dependent packages) for you. The /etc/apt/sources.list file defines the repositories where apt-get can install packages from. I ended the Debian section of this chapter by looking at the aptitude utility, which uses a text-based, menu-driven interface to manage Debian packages.

I ended this chapter by discussing how to manage shared libraries. I pointed out that applications running on the system can share code elements called shared libraries. Shared libraries make it such that software developers don’t have to re-invent the wheel each time they write a new program. Linux applications can use either dynamic or static shared libraries. The dynamic shared library configuration file is /etc/ld.so.conf. It contains a list of paths in the file system where shared library files are stored. To view a list of all shared libraries available on your Linux system, enter **ldconfig -p** at the shell prompt.

You can also view the shared libraries required by a specific application using the ldd command. The syntax is: **ldd -v executable_filename**. The library cache is /etc/ld.so.cache. This file contains a list of all the system libraries and is refreshed when the system is initially booted. If you add library files to a directory not listed in the ld.so.conf file, you must add them and then use the ldconfig command to rebuild the library cache manually. You can also add the path to the LD_LIBRARY_PATH environment variable.

## Accelerated Review

- You can use either graphical or command-line tools to manage Linux software.
- A good Linux administrator can use either type of utility.
- A great deal of software is freely available for Linux systems.
- Your distribution CDs or DVD is a great resource for Linux software.
- A variety of web sites are available for downloading Linux software.
- If possible, you should verify your downloads by comparing a checksum value you create with the sum command against the checksum value specified on the web site where you obtained the file.
