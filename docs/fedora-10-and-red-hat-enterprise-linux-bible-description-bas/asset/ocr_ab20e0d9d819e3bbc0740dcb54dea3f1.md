# Chapter 5: Accessing and Running Applications 203

Package is the name of the RPM archive file. This package may be in the current directory, on a DVD or CD (for example, /media/disk/Packages/x.rpm), or on an accessible FTP site (for example, http://ftp.example.com/pub/whatever.1386.rpm).

> CAUTION: Interrupting rpm package during installation can leave stale lock files and possibly corrupt the database. As a result, subsequent rpm commands may hang. If this happens, you can probably correct the problem by removing old database files. If it doesn't work, you can also try checking whether the database is corrupt and, if so, rebuilding the RPM database. Rebuilding the database can take a long time, so only only it if other options don't clear the problem. Here's how to remove lock files, check the database, and rebuild (as root user):

```
# rm -f /var/lib/rpm/*
# rpm --rebuilddb
```

Along with the -U option, you can use the following options to get feedback during a new installation:

+   -v - Provides debugging information during installation. This is a good way to see everything that happens during the install process. (This output can be long, so you may want to pipe it to the less command.) You can get more information by adding multiple -v options (for example, -vv)
-h - Prints 50 hash marks (#) as the package unpacks. The intent is to see the progress of the unpacking process (so you can tell if the program is still working or stalled)
-percent - Prints the percentage of the total package that has been installed throughout the install.

Before installing a package, rpm checks to make sure that it is not overwriting newer files or installing a package that has dependencies on other packages that are not installed. The following options can be used to override conditions that might otherwise cause the installation to fail:

+   -force - Forces the contents of the current package to be installed, even if the current package is older than the one already installed, contains files placed by other packages, or is already installed. (This is the same as the oldpackage, replacefiles, and replacepkgs options.) Although it is dangerous to do so, people often use this option to override any issue that might cause the package to install fail (such as an RPM fail).

+   -oldpackage - Forces the package to be installed, even if the current package is older than the one already installed.
-replacefiles - Forces files in this package to be installed, even if the files were placed by other packages.
-replacepkgs - Forces packages in this archive to be installed, even if they are already installed on the system.