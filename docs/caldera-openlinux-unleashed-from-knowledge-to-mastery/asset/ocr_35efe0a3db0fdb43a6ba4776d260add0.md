All software that comes with Caldera OpenLinux is stored in RPM packages (often referred to as RPMs). RPM packages are file archives that include extra information about the archives including the package name, a description, the version number of the software, dependencies on other packages and files, as well as other information. The Red Hat Package Manager (rpm) is used to install, upgrade, remove, verify, and get information about packages.

Information about each installed package is stored in a database. This information includes a list of files in the package and all information about the package stored with it. rpm uses the information in the database to allow you to uninstall a package cleanly or to verify that all the files in a package have not changed or have not turned up missing since it was installed. Of course, you can always install software that you compile or that comes in “tarballs.” But you can keep your system cleaner and more organized and make it easier to uninstall something or make other changes if you can find and will use the RPM package you want. Learn to use rpm; it is your friend.

rpm has 10 modes of operation, each with its own set of command-line arguments. The different modes are install, uninstall, query, verify, signature check, build, rebuild database, fix permissions, set owners and groups, and show RC. In this chapter, we will discuss only the first three modes, which you are most likely to use.

# # Installing New Packages

At some point, you will come across a program that you absolutely must have and that either wasn’t installed when you installed OpenLinux 2.2 or didn’t come with the distribution. Well, you’re in luck. Installing new software that comes in RPMs is very easy. You use it with the -i option to put rpm in install mode. Here’s the general command-line format for installing a package:

```
rpm -i [install-options] <package-file>+
```

<package-file>+ represents one or more filenames of the package(s) to install.

There are three parts to the filename of a package. First is the name of the package. Second is the architecture that the package was put together for. Third is the .rpm extension indicating that the file is an RPM package.

```
<package-name>.<architecture>.rpm
```

For example, the package foo-1.2.i386.rpm is the RPM package foo-1.2 put together for Intel processor–based machines.