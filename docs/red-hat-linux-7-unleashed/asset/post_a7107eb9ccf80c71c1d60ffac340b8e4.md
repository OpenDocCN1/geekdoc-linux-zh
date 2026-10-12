
RPM packages can “depend” on other packages, which means that they require other packages to be installed in order to run properly. If you try to install a package for which there is such an unresolved dependency, you’ll see

```
[root@cartoons]# rpm -iVh boatt-1.0-1.1386.rpm
failed dependencies:
banana is needed by boatt-1.0-1
[root@cartoons]# 
```

To resolve failed dependencies, install the requested packages. If you want to force the installation anyway (a bad idea since the package probably will not run correctly), use the -nodeps option.

## Uninstalling

After you have been using your Red Hat Linux system for a period of time, you may decide to remove a package because you never use it or you need to free up some disk space. RPM makes it easy, doing all the hard work for you.

Uninstalling a package is just as simple as installing. You use the following command:

```
[root@cartoons]# rpm -e banana
```

Note that we used the package name “banana,” rather than the name of the original package file banana-1.0-1.1386.rpm.

You can encounter a dependency error when uninstalling a package if some other installed package depends on the one that you are trying to remove. For example:

```
[root@cartoons]# rpm -e banana
removing these packages would break dependencies:
banana is needed by boatt-1.0-1
[root@cartoons]# 
```

You can force RPM to ignore these dependencies by using the -nodeps option, but this option is not recommended because it can leave your system in an unstable state.

## Upgrading

Upgrading a package is similar to installing one. The upgrade command is

```
[root@cartoons]# rpm -Uvh banana-2.0-1.1386.rpm 
banana    ####################################################
[root@cartoons]# 
```

What you don’t see on the preceding command is that RPM automatically uninstalled old versions of the banana package. In fact, you may want to always use -U to install packages because it works fine even when there are no previous versions of the package installed. Because RPM performs intelligent upgrading of packages with configuration files, you may see a message such as saving /etc/banana.conf as /etc/banana.conf.rpmave. This means that during the upgrade, RPM considered your changes to the existing file to be potentially incompatible with the new configuration file in the new package. RPM saved your original configuration file and installed a new one. You should investigate and resolve the differences between the two files as soon as possible to ensure that your system continues to function properly.

Because upgrading is really a combination of uninstalling and installing, you can encounter regular errors from those modes, plus one additional error: If RPM thinks you are trying to upgrade to a package with an older version number, you will see

```
[root@cartoons]# rpm -Uvh banana-1.0-1.i386.rpm
banana    package banana-2.0-1 (which is newer) is already installed
error: banana-1.0-1.i386.rpm cannot be installed
[root@cartoons]#
```

To cause RPM to upgrade anyway, include --oldpackage in the upgrade command:

```
[root@cartoons]# rpm -Uvh --oldpackage banana-1.0-1.i386.rpm
banana    ####################################################
[root@cartoons]#
```

## Querying

You can query the database to find installed packages by using the rpm -q command. A simple use is rpm -q banana, which will print the package name, version, and release number of the installed package banana. For example:

```
[scooby@cartoons]$ rpm -q banana
banana-2.0-1
[scooby@cartoons]$
```

## Package Specification Options

Instead of specifying the package name, you can use the Package Specification Options with -q to specify the package(s) that you want to query. These options include the following:

- -a Queries all currently installed packages.
- -f <file> Queries the package owning the specified file.
- -p <packagefile> Queries the specified package filename.

## Information Options

You can specify what information to display about queried packages. The following options are used to select the type of information for which you are searching:

- -i displays package information such as name, description, release, size, build date, install date, vendor, and other miscellaneous information.
- -l displays the list of files that the package “owns.”
- -s displays the state of all the files in the package.
- -d displays a list of files marked as documentation (man pages, info pages, READMEs, and so on).
- -c displays a list of files marked as configuration files. These are the files that you change after installation to adapt the package to your system (sendmail.cf, passwd, inittab, and so on).

For those options that display file lists, you can add -v to the query command to view the list in the familiar ls -l format.

Here’s an example of doing a more sophisticated query:

```
[scooby@cartoons]$ rpm -qi kernel
Name       : kernel                Relocations: (not relocatable)
Version    : 2.2.16    Build Date: Wed 26 Jul 2000 09:19:08 PM EST
Release    : 5.0
Install date: Sat 05 Apr 2000 08:44:13 AM EDT   Build Host: porky.redhat.com
Group      : System Environment/Kernel Source RPM: kernel-2.2.16-17.src.rpm
Size       : 15122940         License: GPL
Packager   : Red Hat, Inc. <http://bugzilla.redhat.com/bugzilla>
Summary    : The Linux kernel (the core of the Linux operating system).
Description:
The kernel package contains the Linux kernel (vmlinuz), the core of your
Red Hat Linux operating system. The kernel handles the basic functions
of the operating system: memory allocation, process allocation, device
input and output, etc.
```

For more details about using RPM, check out man rpm.

# Using Gnome-RPM

Red Hat Linux includes a very nice tool named Gnome-RPM that is also referred to as gnome RPM. Gnome-RPM is a Gnome-compliant GUI for the Red Hat package manager. With Gnome-RPM, you can easily perform many of the same package management tasks that are available to the command line.

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_750_0.png)

The Gnome-RPM interface, shown in Figure 21.1, has several features:

- **Package Panel**—Located on the left of the UI; it allows you to browse groups of packages.
- **Display Window**—Located on the right of the package panel; it shows the contents of your folders in the panel.
- **Toolbar**—Located above the display and panel; it is a graphical display of package tools.
- **Menu**—Located above the toolbar; it contains text-based commands, as well as help info, preferences, and other settings.
- **Status Bar**—Located beneath the panel and display windows; it shows the total number of selected packages.

Figure 21.1
Gnome-RPM.

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_751_0.png)

## Managing Users and Groups with linuxconf

The `linuxconf` command is a highly welcome addition to Red Hat Linux. Having a GUI tool to manage users and groups takes a lot of hassle out of making small changes, but I’m sure that many system administrators still prefer the command-line method.

## Creating and Modifying Users

Adding a user is one of the more basic tasks you can perform with `linuxconf`. When you installed Red Hat Linux you should have at least set up one user account. Adding additional users is easy.

To add a new user account, follow these steps:

1. Start `linuxconf`.
2. Click the Config tab.
3. Expand the tree browser under Users Accounts, Normal, User Accounts.
4. Click on User Accounts. You should now see the Users Accounts panel.
5. Click Add.
6. Complete the required fields.
7. Click Accept.

That’s all there is to it.

**Tip**
The user account that you are creating is a login shell account. Although it is not a required field, it is probably a good idea to specify a home directory for your user.

Figure 21.2 shows the User Account Creation tab used for adding a user to `linuxconf`.

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_752_0.png)
