
Or, you can edit the /etc/profile or ~/.bash_profile file and export it from there.

> **CAUTION**
> Although this must be known for the exam, the **LD_LIBRARY_PATH** is considered to be a security risk because it might allow unauthorized programs access to system libraries accidentally or otherwise expose system library paths to unauthorized users.

Some library files might not have enough header or internal information to be correctly identified by the `ldconfig` program when it builds the links in the library directories.

The `ldconfig` program reads the headers of all the libraries in the /lib and /usr/lib directories and any directories noted in the /etc/ld.so.conf file. From those headers and the filenames of the libraries, `ldconfig` makes the proper links to the libraries, particularly for the legacy programs that expect older libraries to exist.

The `ldconfig` program also builds the /etc/ld.so.cache file, a binary file that is an ordered list of the libraries on the system. This file is not readable as text but is used as a quick reference by the system linker `ld.so`.

## Installing Software with Packages

A typical Linux installation has more than 2,000 packages, with many multiple files per package. A *package* is a container file that holds applications, configuration files, and anything else that a particular program or set of programs needs to function.

Two types of packages are tested on the LPI exams:

- Red Hat Package Manager (RPM)
- Debian Package Manager (DPKG)

> **NOTE**
> This chapter focuses on the majority player, RPM, with the Debian package management information covered in Appendix A, "Debian Package Management."

## Red Hat Package Management

RPM refers not only to the package format, but the `rpm` command and the RPM Database. The components of the RPM package management style are:

- **The RPM Database**—A collection of files that manages the RPMs on a system
- **Package files**—The packages in RPM format that are distributed with the `.rpm` extension
- **The `rpm` command**—Used for all package installation, removal, and query tasks

> **NOTE**
> A quick word is needed about graphical package management tools such as gnomap or the RPM-handling routines built in to the various file managers (Nautilus and Konqueror). These are typically just a front end to the text-mode `rpm` command and provide a friendly interface for installing packages.

> **ALERT**
> Although the 101-RPM exam usually has only about 14 questions that cover both installation and package management, it'll seem like most of the exam is about RPM, particularly if you're not adequately prepared. Study the RPM sections in this text thoroughly, read the man pages for man (8) and the extra documentation in `/usr/share/doc/rpm-4.0.4`, and (most importantly!) try the commands and options shown previously.

### The RPM Database

The RPM Database is a collection of Berkeley database files that together make up a database of the packages and the files that were installed by those packages on the system.

The RPM Database is located in the `/var/lib/rpm` directory, with each file in that directory being part of the database as a whole. Thankfully, you don't need to know all the files and their purposes, just that they are there and exist in an uncorrupted state.

> **ALERT**
> The RPM Database is mostly restricted to the root user, except for querying and verification, which can be run by any user.

Like any database, the RPM Database can become outdated or corrupted with heavy usage and need to be rebuilt. To rebuild the database from the installed package's headers, you use the following command:

```bash
rpm --rebuilddb
```

This command does not produce any output unless errors are found, and even then the errors are purely informational and not of much use for fixing the problem.

The RPM Database is locked during most operations, such as an installation or removal. Thus, any attempt to run additional commands results in this message:

```text
error: cannot get exclusive lock on /var/lib/rpm/Packages
error: cannot open Packages index using db3 - Operation not permitted (1)
error: cannot open /var/lib/rpm/packages.rpm
```

This message simply conveys that the database is in use and cannot be locked for additional tasks at this time. This keeps multiple sysadmins from causing corruption by performing incompatible tasks simultaneously.

### RPM Package Files

RPM packages come in two types: source and binary. A *source* RPM file is a collection of the source files needed for installing the package, plus some instructions for building the binary RPM from the source. A *binary* RPM file is a discrete package that, when installed, copies the compiled binary files, other associated files such as documentation, and any other files needed to run that package to the specified locations.

![](img/49f4f38f3aec011238fa50f89e643db3_275_0.png)

> An important distinction must be made between *installed* packages and *uninstalled* package files. Information about an installed package comes from the RPM database, whereas information about an uninstalled package comes from the RPM file itself.
> After an RPM file has been installed, the original RPM is no longer required.

RPM packages contain a set of files and configuration scripts that comprise a software program or application in most instances. Notable exceptions are packages that are strictly for placing text configuration files, such as files that are in the /etc directory. RPM packages should contain at least the following:

- Compressed binary application files
- The name and version of the package’s software
- The build date and host on which it was built
- A description of the package and its purpose
- The checksums and dependencies required

### Package Name Conventions

Installed packages are known by a short name, although some operations require the long names be used. Typically, long package names are needed for deletions when multiple packages whose short names match exist.

Here's an example of a short package name:
`ethereal`

Here's an example of a long package name:
`ethereal-0.8.9-1.1386`

An example of two packages installed with different versions of the same software is as follows:
`rpm -q tree`

This returns the output:
```text
tree-1.2-17
tree-1.2-7
```

This makes viewing a particular package's information difficult if you use the `-l` and `-i` options for file listings and info pages. This is fine if you want to compare the differences, but it's maddening when you really need to see just the latest version's information. You need to use the long name (`tree-1.2-17`) to get just that package's information.

![](img/49f4f38f3aec011238fa50f89e643db3_276_0.png)

> The instances of multiple packages with the same short names appear in the package removal questions, with the `--allmatches` option being necessary to remove multiple packages with the same short names. You can find more on this in the next section.

### The rpm Command

The text-mode `rpm` package tool is used to perform all operations on packages on the system, either installed and in the RPM Database, or uninstalled and on disk.

Common operations that use the `rpm` command include:

- Installing packages
- Upgrading packages
- Removing and uninstalling packages
- Querying the RPM database for information
- Verifying the package file
- Checking installed files
- Building a binary package from the source

The `rpm` command keywords and options come in several formats. The common options are short and use a single letter—for example, `-i` is the installation option. There are almost always long options that match, and some options occur only in the long format.

> On the exam you might see long options in several locations, either right after a short option or on the end of the entire command. The important thing is to have tried the long options and to know that you can tuck them on the end, as long as something else doesn’t depend on that option’s placement.

### Validation of Packages

It’s important that you validate or check the signatures of packages that are downloaded from any source other than the distribution vendor’s site.

Validating packages typically takes place when the package is accessed or installed, although it can be triggered explicitly. To check the md5 checksum and gpg signatures for the gentoo file manager, you would use the following command:

```bash
rpm -K gentoo-0.11.39-1.fr.1386.rpm
```

This returns the following output:

```text
gentoo-0.11.39-1.fr.1386.rpm: (SHA1) DSA sha1 md5 (GPG) NOT OK
MISSING KEYS: GPG#42d547b
```

If the package has a gpg signature, that file might need to be downloaded and imported into the RPM Database with the `--import` option.

> Knowing that signatures come in md5 and gpg varieties, plus the `--checksig` and `-K` options, is plenty for the exam. The key is to be sure that the package you have is the original from the maintainer, not one full of Trojan horses and rootkits.

### Installation of Packages

Installing software via packages requires root access, the `rpm` command, and a package(s). Installation causes the `rpm` command to check the following:
