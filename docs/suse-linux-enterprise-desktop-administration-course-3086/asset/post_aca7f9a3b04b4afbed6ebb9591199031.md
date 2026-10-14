
## Query the RPM Database and RPM Archives

With the -q option, you can query the RPM database of installed packages and, by adding the option -p, inspect RPM archives that are not yet installed.
Table 6-1 shows the most commonly used RPM query options.

| Option | Results |
|---|---|
| `-a` | List all installed packages. |
| `-i` | List package information. |
| `-l` | Display a file list. |
| `-f file` | Find out to which package file belongs (the full path must be specified with file). |
| `-d` | List only documentation files (implies `-l`). |
| `-c` | List only configuration files (implies `-l`). |
| `--dump` | Display a file list with complete details (to be used with `-l`, `-c` or `-d`). |
| `--provides` | List features of the package that another package can request with `--requires`. |
| `--requires, -R` | List the capabilities the package requires. |
| `--scripts` | List installation scripts (preinstall, postinstall, uninstall). |
| `--changelog` | Displays a detailed list of information (updates, configuration, modifications, etc.) on a specific package. |

Table 6-1

For example, the `rpm --qi wget` command displays the following information:

```
da10:~ # rpm --qi wget
Name        : wget                         Relocations: (not relocatable)
Version     : 1.10.2                       Vendor: SUSE LINUX Products GmbH,
Nuernberg, Germany
Release     : 15                           Build Date: Mon May 8
21:16:26 2006                              Build Host: nicolai.suse.de
Install Date: Wed May 15 10:28:23 2006
Group       : Productivity/Networking/Web/Utilities Source RPM: wget-
1.10.2-15.src.rpm
Size        : 1532429                      License: GPL
Signature   : DSA/SHA1, Mon May 8 21:20:08 2006, Key ID a84edae89c800aca
Packager    : http://bugs.open\-suse.org
URL         : http://wget.sunsite.dk/
Summary     : A Tool for Mirroring FTP and HTTP Servers
Description :
Wget enables you to retrieve WWW documents or FTP files from a server.
This can be done in script files or via the command line.
Authors:
---------
    Hrvoje Niksic <hn niksic@srce.hr>
Distribution: SUSE Linux Enterprise 10 (i586)
```

The option -f only works if you specify the complete filename with a full path. You can enter several filenames, as in the following:

```
da10:~ # rpm -qf /bin/rpm /usr/bin/wget
rpm-4.4.2-43
wget-1.10.2-15
```

This returns information for both /bin/rpm and /usr/bin/wget. With the help of the RPM database, you can perform verification checks with the option -V, or --verify. If any files in a package have been changed since installation, they will be displayed.

RPM uses the character symbols shown in Table 6-2 to provide hints about the changes.

| Character | Description |
|---|---|
| 5 | MD5 check sum |
| S | File size |
| L | Symbolic link |
| T | Modification time |
| D | Major and minor device numbers |
| U | Owner |
| G | Group |
| M | Mode (permissions and file type) |

Table 6-2

In the case of configuration files, the letter c is displayed. The following is an example for changes to /etc/wgetrc (wget):

```
rpm -V wget
S.5.....T c /etc/wgetrc
```

## Install, Update, and Uninstall Packages

For most RPM packages, you use the following command to install the software:

```
rpm --i *package_name*.rpm
```

When you install an RPM package, the executable programs, documentation files, configuration files, and start scripts are copied to the appropriate directories in the file system.

You can use the options -U (or --upgrade) and -F (or --freshen) to update a package by using the following syntax:

```
rpm --F *package_name*.rpm
```

This command removes the files of the old version and immediately installs the new files. If no previous version is installed, the package is not installed.

If an old version is installed, the option -U does the same as -F. However, if no previous version is installed, -U installs the new version.

To uninstall (remove) an RPM package, enter the following:

```
rpm --e package_name
```

When you uninstall a package, all files except modified configuration files are removed from the system with the help of the RPM database. This ensures a clean uninstall.

RPM will delete the package only if this does not break dependencies. If other packages depend on the package you want to delete, these are listed in the error message.

![](img/9129877170834ca9d5fdac5319bf5f12_197_0.png)

See the manual page or RPM for a complete reference on available options.

![](img/9129877170834ca9d5fdac5319bf5f12_197_1.png)

## Exercise 6-3: Manage Software with RPM

In this exercise, you gather information on installed software, and uninstall and install software packages. First, get information on RPMs by looking for information on the /usr/bin/wget file:

- Find out what package contains the /usr/bin/wget file.
- Get information on that package.
- List the files contained in that package.
- Verify the integrity of the files.
- List the files in that package which contain documentation.

Then, install the gcal package from the DVD, run the program gcal, and uninstall gcal.

### Detailed Steps to Complete This Exercise

- Part I: Get Information on a Software Package
- Part II: Remove and Install Software with RPM

### Part I: Get Information on a Software Package

To get information on a software package, do the following:

- 1. Use RPM to find out information on the wget package:

  - a. From a terminal window, determine which package installed the /usr/bin/wget file by entering:

```
rpm -qf /usr/bin/wget
```

Notice that the wget package installed the wget file.

  - b. Find out information on the wget package by entering:

```
rpm -qi wget
```

Notice that the information includes the install date and a description.

- c. Show all the files installed by the wget package by entering:

```
rpm -ql wget
```

Where can you find information on the wget package? (Notice the location of the README files.)

- 2. Log in as root and, using an editor of your choice, modify some comment in the `/etc/wgetrc` file. See what has changed in the files on your hard drive since the wget RPM was originally installed by entering:

```
rpm -V wget
```

- 3. View the documentation files for the wget command by entering:

```
rpm -qd wget
```

Notice that some of the files are still compressed (`*.gz`).

### Part II: Remove and Install Software with RPM

To remove and install software with RPM, do the following:

- 1. From a terminal window, switch to user root (`su -`, password `nov311`).
- 2. Remove the gcalctool package by entering:

```
rpm -e gcalctool
```

- 3. Verify that the package is no longer installed by entering:

```
rpm -ql gcalctool
```

- 4. Insert *SUSE Linux Enterprise Desktop 10 SP1 Product DVD* into your CD-ROM drive.
- 5. Enter the command `ls /media`. There will be a directory named according to the label of the DVD. Note the name of the directory.
- 6. List all files included in the not installed gcalctool package by entering:

```
rpm -qpl /media/cdlabel/suse/i586/gcalctool*.i586.rpm
```

- 7. Install the gcalctool package by entering:

```
rpm -ihv /media/cdlabel/suse/i586/gcalc*.i586.rpm
```

- 8. Remove the DVD from your drive.
- 9. (Conditional) If the CD drive does not open, enter the following:

```
eject
```

Then try again.

- 10. Test the installation of the software package by entering:

```
gcalctool
```

- 11. List all files included in the installed gcal package by entering

```
rpm -ql gcalctool
```

- 12. Log out as root by entering

```
exit
```

- 13. Close the terminal window.

## Summary

- The easiest way to install, update, manage, and uninstall software packages after a SUSE Linux installation is to use the Software Management module of YaST. Although YaST obtains software packages from your installation media by default, you can specify other installation sources such as a network server or software repository on the Internet.
- You can use the Online Update module of YaST to obtain the latest software updates for your SUSE Linux system provided that you have a valid SUSE Customer Center subscription.
- Most Linux software is in Red Hat Package Manager (RPM) format. RPM package file names include the software version, release number, architecture, and the rpm extension.
- SUSE Linux maintains a database of all RPM installed software in the `/var/lib/rpm` directory and backs up this database to the `/var/adm/backup/rpmdb` directory on a daily basis.
- You can install, remove, verify, and find information about RPM software packages using the `rpm` command in a terminal or using YaST in a desktop environment.
- To configure the default options for the `rpm` command, you can edit the `/etc/rpmrc` and `~/.rpmrc` files.
- Periodically, you should verify the contents of packages using the `-V` (or `--verify`) option to the `rpm` command.

## Key Terms

| Term | Definition |
|---|---|
| `/etc/rpmrc` | A file that contains configuration information that is written to the `/usr/lib/rpm/rpmrc` file. |
| `/etc/sysconfig/backup` | The configuration file that controls automatic system backups. |
| `/usr/lib/rpm/rpmrc` | The main RPM configuration file. |
| `/var/adm/backup/rpmdb` | The directory that stores backup copies of the RPM database. |
| `/var/lib/rpm` | The directory that stores the RPM database. |
| `~/.rpmrc` | A file that contains configuration information that is written to the `/usr/lib/rpm/rpmrc` file. |
| **Installation Source** | A YaST module that allows you to specify the source of software packages available for installation. |
