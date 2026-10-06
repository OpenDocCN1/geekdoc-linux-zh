
# Part II: Using Fedora and RHEL

the dvgrab RPM (which is part of Fedora) in my local directory and I wanted to check it. I could run the following command:

```
# rpm --checks dvgrab-3.2-1-fc10.rpm
dvrgrab:3.2-1-fc10.i386.rpm (sha) sha md5 gpg OK
```

The preceding output shows that the GPG/DSA key was found and used to check that the package's digital signatures (dsa, sha, and md5) were correct. However, if you got a package for which you didn't have the GPG/DSA key installed, you would need to get and import that key before you could verify the package.

If you trust the Internet where you are getting the RPM you want to install, look for an indication that the site has signed its packages. Download the GPG public key and import it. That will allow you to check the validity of the packages from that site. For example, I decided to use the KDE-red (http://apt.kde-redhat.org) project to replace all my packages from Fedora. I downloaded the digikam package and tried to verify it as:

```
# rpm --checks digikam-doc-0.9.4-2.fc10.rpm
digikam-doc-0.9.4-2.fc10.rpm:(SHA1) DSA sha md5 (GPG) NOT OK (MISSING KEYS: GPG#ff6382fa)
```

Because the GPG public key was not installed, the contents couldn't be verified as correct. I went to the KDE-red project site and downloaded the GPG public key to the current directory. I imported the key as follows:

```
# rpm --import gpg-pubkey-ff6382fa-3e1ab2ca
```

With the GPG public key imported, the second check of the RPM showed it was clean:

```
# rpm --checks digikam-doc-0.9.4-2.fc10.rpm
digikam-doc-0.9.4-2.fc10.rpm:(sha) dsa sha md5 gpg OK
```

Most of the public keys you need for the basic repositories used with Fedora in the fedora-release package. GPG public keys from other repositories are stored with those in the /etc/pki/rpm-gpg directory.

Remember, however, it is best to get packages automatically from known repositories with yum (or related tools). Besides checking the signatures of packages, yum will also make sure all dependencies are cleared up.

# Installing with rpm

To install an RPM file that is not yet installed on your system with the rpm command, most people generally use the same options if they were upgrading the (-U option). Here's an example of a line you could use to install a new RPM package:

```
# rpm -U [options] package
```

Package is the name of the RPM archive file. This package may be in the current directory, on a DVD or CD (for example, /media/disk/Packages/x.rpm), or on an accessible FTP site (for example, http://ftp.example.com/pub/whatever.1386.rpm).

> CAUTION: Interrupting rpm package during installation can leave stale lock files and possibly corrupt the database. As a result, subsequent rpm commands may hang. If this happens, you can probably correct the problem by removing old database files. If it doesn't work, you can also try checking whether the database is corrupt and, if so, rebuilding the RPM database. Rebuilding the database can take a long time, so only it if other options don't clear the problem. Here's how to remove lock files, check the database, and rebuild (as root user):

```
# rm -f /var/lib/rpm/*
# rpm --rebuilddb
```

Along with the -U option, you can use the following options to get feedback during a new installation:

- -v - Provides debugging information during installation. This is a good way to see everything that happens during the install process. (This output can be long, so you may want to pipe it to the less command.) You can get more information by adding multiple -v options (for example, -vv)
- -h - Prints 50 hash marks (#) as the package unpacks. The intent is to see the progress of the unpacking process (so you can tell if the program is still working or stalled)
- -percent - Prints the percentage of the total package that has been installed throughout the install.

Before installing a package, rpm checks to make sure that it is not overwriting newer files or installing a package that has dependencies on other packages that are not installed. The following options can be used to override conditions that might otherwise cause the installation to fail:

- -force - Forces the contents of the current package to be installed, even if the current package is older than the one already installed, contains files placed by other packages, or is already installed. (This is the same as the oldpackage, replacefiles, and replacepkgs options.) Although it is dangerous to do so, people often use this option to override any issue that might cause the package to install fail (such as an RPM fail).

- -oldpackage - Forces the package to be installed, even if the current package is older than the one already installed.
- -replacefiles - Forces files in this package to be installed, even if the files were placed by other packages.
- -replacepkgs - Forces packages in this archive to be installed, even if they are already installed on the system.

- - **nodops** Skips dependency checks and installs the package, even if packages it are not installed. This option should be used with extreme caution! By not resolving dependencies, you can end up with broken software.

- - **--ignore** Forces package to be installed, even if the binaries in the package don't match the architecture of your host computer.

- - **--excludedocs** Excludes any package members, infotext, or other files marked as documentation.

- - **--ignoreos** Forces package to be installed, even if the binaries in the package don't match the architecture of your operating system.

The following is a simple command used to install an RPM package:

```
# rpm -U AdobeReader_enu-7.0.9-1.i386.rpm
```

I like to see feedback when I install something (by default, rpm is surprisingly quiet when it succeeds). Here is what the command looks like when I add the -vy option to get verbose feedback, along with some of the output:

```
# rpm -Uv AdobeReader_enu-8.1.3-1.i486.rpm
=============================================
D: AdobeReader_enu-8.1.3-1.i486.rpm
D: Expected size: 494981060 Iad96vs+agt(180)+pad(4)+data(49472806)
D: Actual size: 494981060
D: loading keys from /var/lib/rpm/pubkeys/*
D: couldn't find any keys in /var/lib/rpm/pubkeys/*
D: loading keys from rpmsdb
D: opening db /var/lib/rpm/Packages dbcl:spool:join
D: opening db index /var/lib/rpm/Packages rdnly node mode=0x0
D: locked db index /var/lib/rpm/Packages
D: opening db index /var/lib/rpm/sams rdnly node mode=0x0
D: read head #963 Header sanity check: OK
D: added key gpg-pubkey-ff6382fa-3e1ab2ca
With the GPG public key imported, the second check of the RPM showed it was clean:

```
# rpm --checks digikam-doc-0.9.4-2.fc10.rpm
digikam-doc-0.9.4-2.fc10.rpm:(sha) dsa sha md5 gpg OK
```

Most of the public keys you need for the basic repositories used with Fedora in the fedora-release package. GPG public keys from other repositories are stored with those in the /etc/pki/rpm-gpg directory.

Remember, however, it is best to get packages automatically from known repositories with yum (or related tools). Besides checking the signatures of packages, yum will also make sure all dependencies are cleared up.

# Installing with rpm

To install an RPM file that is not yet installed on your system with the rpm command, most people generally use the same options if they were upgrading the (-U option). Here's an example of a line you could use to install a new RPM package:

```
# rpm -U [options] package
```

Package is the name of the RPM archive file. This package may be in the current directory, on a DVD or CD (for example, /media/disk/Packages/x.rpm), or on an accessible FTP site (for example, http://ftp.example.com/pub/whatever.1386.rpm).

> CAUTION: Interrupting rpm package during installation can leave stale lock files and possibly corrupt the database. As a result, subsequent rpm commands may hang. If this happens, you can probably correct the problem by removing old database files. If it doesn't work, you can also try checking whether the database is corrupt and, if so, rebuilding the RPM database. Rebuilding the database can take a long time, so only only it if other options don't clear the problem. Here's how to remove lock files, check the database, and rebuild (as root user):

```
# rm -f /var/lib/rpm/*
# rpm --rebuilddb
```

Along with the -U option, you can use the following options to get feedback during a new installation:

- -v - Provides debugging information during installation. This is a good way to see everything that happens during the install process. (This output can be long, so you may want to pipe it to the less command.) You can get more information by adding multiple -v options (for example, -vv)
- -h - Prints 50 hash marks (#) as the package unpacks. The intent is to see the progress of the unpacking process (so you can tell if the program is still working or stalled)
- -percent - Prints the percentage of the total package that has been installed throughout the install.

Before installing a package, rpm checks to make sure that it is not overwriting newer files or installing a package that has dependencies on other packages that are not installed. The following options can be used to override conditions that might otherwise cause the installation to fail:

- -force - Forces the contents of the current package to be installed, even if the current package is older than the one already installed, contains files placed by other packages, or is already installed. (This is the same as the oldpackage, replacefiles, and replacepkgs options.) Although it is dangerous to do so, people often use this option to override any issue that might cause the package to install fail (such as an RPM fail).

- -oldpackage - Forces the package to be installed, even if the current package is older than the one already installed.
- -replacefiles - Forces files in this package to be installed, even if the files were placed by other packages.
- -replacepkgs - Forces packages in this archive to be installed, even if they are already installed on the system.

- - **nodops** Skips dependency checks and installs the package, even if packages it are not installed. This option should be used with extreme caution! By not resolving dependencies, you can end up with broken software.

- - **--ignore** Forces package to be installed, even if the binaries in the package don't match the architecture of your host computer.

- - **--excludedocs** Excludes any package members, infotext, or other files marked as documentation.

- - **--ignoreos** Forces package to be installed, even if the binaries in the package don't match the architecture of your operating system.

The following is a simple command used to install an RPM package:

```
# rpm -U AdobeReader_enu-7.0.9-1.i386.rpm
```

I like to see feedback when I install something (by default, rpm is surprisingly quiet when it succeeds). Here is what the command looks like when I add the -vy option to get verbose feedback, along with some of the output:

```
# rpm -Uv AdobeReader_enu-8.1.3-1.i486.rpm
=============================================
D: AdobeReader_enu-8.1.3-1.i486.rpm
D: Expected size: 494981060 Iad96vs+agt(180)+pad(4)+data(49472806)
D: Actual size: 494981060
D: loading keys from /var/lib/rpm/pubkeys/*
D: couldn't find any keys in /var/lib/rpm/pubkeys/*
D: loading keys from rpmsdb
D: opening db /var/lib/rpm/Packages dbcl:spool:join
D: opening db index /var/lib/rpm/Packages rdnly node mode=0x0
D: locked db index /var/lib/rpm/Packages
D: opening db index /var/lib/rpm/sams rdnly node mode=0x0
D: read head #963 Header sanity check: OK
D: added key gpg-pubkey-ff6382fa-3e1ab2ca
With the GPG public key imported, the second check of the RPM showed it was clean:

```
# rpm --checks digikam-doc-0.9.4-2.fc10.rpm
digikam-doc-0.9.4-2.fc10.rpm:(sha) dsa sha md5 gpg OK
```

# Chapter 5: Accessing and Running Applications 203

Package is the name of the RPM archive file. This package may be in the current directory, on a DVD or CD (for example, /media/disk/Packages/x.rpm), or on an accessible FTP site (for example, http://ftp.example.com/pub/whatever.1386.rpm).

> CAUTION: Interrupting rpm package during installation can leave stale lock files and possibly corrupt the database. As a result, subsequent rpm commands may hang. If this happens, you can probably correct the problem by removing old database files. If it doesn't work, you can also try checking whether the database is corrupt and, if so, rebuilding the RPM database. Rebuilding the database can take a long time, so only only it if other options don't clear the problem. Here's how to remove lock files, check the database, and rebuild (as root user):

```
# rm -f /var/lib/rpm/*
# rpm --rebuilddb
```

Along with the -U option, you can use the following options to get feedback during a new installation:

- -v - Provides debugging information during installation. This is a good way to see everything that happens during the install process. (This output can be long, so you may want to pipe it to the less command.) You can get more information by adding multiple -v options (for example, -vv)
- -h - Prints 50 hash marks (#) as the package unpacks. The intent is to see the progress of the unpacking process (so you can tell if the program is still working or stalled)
- -percent - Prints the percentage of the total package that has been installed throughout the install.

Before installing a package, rpm checks to make sure that it is not overwriting newer files or installing a package that has dependencies on other packages that are not installed. The following options can be used to override conditions that might otherwise cause the installation to fail:

- -force - Forces the contents of the current package to be installed, even if the current package is older than the one already installed, contains files placed by other packages, or is already installed. (This is the same as the oldpackage, replacefiles, and replacepkgs options.) Although it is dangerous to do so, people often use this option to override any issue that might cause the package to install fail (such as an RPM fail).

- -oldpackage - Forces the package to be installed, even if the current package is older than the one already installed.
- -replacefiles - Forces files in this package to be installed, even if the files were placed by other packages.
- -replacepkgs - Forces packages in this archive to be installed, even if they are already installed on the system.

- - **nodops** Skips dependency checks and installs the package, even if packages it are not installed. This option should be used with extreme caution! By not resolving dependencies, you can end up with broken software.

- - **--ignore** Forces package to be installed, even if the binaries in the package don't match the architecture of your host computer.

- - **--excludedocs** Excludes any package members, infotext, or other files marked as documentation.

- - **--ignoreos** Forces package to be installed, even if the binaries in the package don't match the architecture of your operating system.

The following is a simple command used to install an RPM package:

```
# rpm -U AdobeReader_enu-7.0.9-1.i386.rpm
```

I like to see feedback when I install something (by default, rpm is surprisingly quiet when it succeeds). Here is what the command looks like when I add the -vy option to get verbose feedback, along with some of the output:

```
# rpm -Uv AdobeReader_enu-8.1.3-1.i486.rpm
=============================================
D: AdobeReader_enu-8.1.3-1.i486.rpm
D: Expected size: 494981060 Iad96vs+agt(180)+pad(4)+data(49472806)
D: Actual size: 494981060
D: loading keys from /var/lib/rpm/pubkeys/*
D: couldn't find any keys in /var/lib/rpm/pubkeys/*
D: loading keys from rpmsdb
D: opening db /var/lib/rpm/Packages dbcl:spool:join
D: opening db index /var/lib/rpm/Packages rdnly node mode=0x0
D: locked db index /var/lib/rpm/Packages
D: opening db index /var/lib/rpm/sams rdnly node mode=0x0
D: read head #963 Header sanity check: OK
D: added key gpg-pubkey-ff6382fa-3e1ab2ca

# Upgrading packages with rpm

The upgrade option (-U) with rpm can, as you might expect, also be used to upgrade existing packages. The format is as we have described above:

```
# rpm -U [options] package
```

> TIP: Although there is a separate install option (-i), I recommend using the -U option whether are doing a new install or an upgrade. With -U, the package installs in either case. So rpm -U always works (with one exception), while rpm -i fails if the package is already installed.
The exception is when installing kernel packages. Use -i when installing a new kernel or your old (presumably, working) kernel will be removed and you could be stuck with an unbootable system!

One issue when upgrading is installing an older version of a package. For example, if you install a new version of some software and it doesn't work, you will want to go back to the old version. To do this, use the --oldpackage option as follows:

```
# rpm -U --oldpackage AnotherLevel-0.7.4-1.noarch.rpm
```

If a later package of this name already exists, it is removed and the older version is installed.

# Freshening packages with rpm

An option that is similar to the upgrade (-U) is the freshen (-F) option. The main difference between the two is what happens if you are updating or freshening is not already installed on your Fedora system. The -U can either a fresh install or an upgrade. The -F will only do an upgrade (so if the package is not already installed, rpm will do nothing).

A great use for when you have a directory of updated rpm files that you want to install on your system. But you only want to update those packages that are already
