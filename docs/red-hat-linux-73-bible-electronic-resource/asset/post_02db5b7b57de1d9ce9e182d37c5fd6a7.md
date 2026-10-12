
## Table 5-2: Linux Document Formats

| Format | Suffix | Description |
| :--- | :--- | :--- |
| Hypertext Markup Language | .html or .htm | File is in hypertext format for reading by a Web browser program (such as Netscape Communicator). |
| PostScript | .ps | File is in PostScript format for outputting on a PostScript printer. |
| SGML | .sgml | File is in SGML, a standard document format. SGML is often used to produce documents that can later be output to a variety of formats. |
| DVI | .dvi | File is in DVI, the output format of the TeX text-processing tools. Convert these files to PostScript or Hewlett-Packard's PCL using the dvips and dvilj commands. |
| Plain text | | Files without a suffix are usually plain-text files (in ASCII format). |

If you are not sure what format a file is in, use the `file` command as follows:

```
$ file archive-file
```

This command tells you if it is a GNU tar file, RPM, gzip, or other file format. (This is a good technique if a file was renamed and lost its suffix.)

## Converting software packages with the alien command

If there is a package available in a non-RPM format that you want to use on your Red Hat Linux system, you may be able to use the alien command to convert the package to RPM format. The alien command lets you convert packages from Debian (.deb), Stampede (.slp), Slackware (.slp), or Red Hat package management (.rpm) to any of those other formats.

The advantage of converting a package from another format to RPM is that you can then manage that package using various RPM tools. As an example, I downloaded the bsdgames package from the Debian FTP site (`ftp://ftp.us.debian.org`). I then converted the package, which was in .deb format, to RPM format as follows:

```
# alien --to-rpm bsdgames_2.9-3.deb
```

In this case, an RPM file was created from the Debian package. The new file was called bsdgames-2.9-4.i386.rpm. After it was created, I could install it as I would any RPM file:

```
# rpm -i bsdgames-2.9-4.i386.rpm
```

After that, I could query the bsdgames package as I would any RPM package. For example, I could type `rpm -ql bsdgames` to list the contents of the package. Later, to delete the package, I can use the `rpm -e bsdgames` command.

With the alien command, you can also make Debian packages (--to-deb option), Slackware packages (--to-tgz), or Stampede packages (--to-slp). To create Debian packages, you need extra software packages that include gcc, make, debmake, dp-dev, and dpkg packages.

> **CAUTION:** Though alien provides a quick way to convert software packages to different formats, it should not be used to convert critical operating system packages. For example, you shouldn't expect system initialization packages to be reliably converted so they can be used in Red Hat Linux.

## Installing Red Hat Linux Applications

Most of the Linux applications that you want to install are available in RPM format. There is probably a binary version of the application that specifically suits your platform. If no RPMs are available for the applications, you can probably find a source code version (often stored as a tar/gzip archive) that you can use to build the software yourself.

This section describes how to install and manage applications using tools created for RPM archive files. Later in this section, you will learn how to build and install applications that come as source code packages.

### Installing and managing RPM files

When you get an application that is packaged in RPM format, you typically get a single file. The command used to work with RPM package files is `rpm`. To manage RPM packages, the `rpm` command has options that let you list all the packages that are installed, upgrade existing packages to newer versions, and query packages for information (such as the files or documentation included with the package). There is also a verify option that lets you check that all files that make up the package are present and unchanged.

The `rpm` command has these modes of operation:

- install (-i)
- upgrade (-u)
- query (-q)
- verify (-V)
- signature check (--checksig)
- uninstall (-e)
- build (-b)
- rebuild database (--rebuilddb)
- fix permissions (`--setperms`)
- set owners/groups (`--setugids`)
- show RC (`--showrc`)

With these options, you can install RPM packages and verify that their contents are properly installed, correcting any problems that occur.

The following sections describe how to use `rpm` to install and work with your RPM applications.

> **CAUTION:** You must be logged in as the root user to add or remove packages. You may, however, list installed packages, query packages for information, or verify a package’s contents without being logged in as the root user.

### Installing with rpm

To install an RPM archive file with the `rpm` command, use the following syntax:

```
rpm -i [options] package
```

`package` is the name of the RPM archive file. This package may be in the current directory, on a mounted CD (for example, /mnt/cdrom/RedHat/RPMS/whatever.rpm), or on an accessible FTP site (for example, ftp://sunsite.unc.edu/pub/Linux/apps/sound/cdrom/X/xcd-2.0-1.i386.rpm).

> **NOTE:** When you indicate a package from an FTP site, the file is downloaded before it is installed.

Along with the -i option, you can use these options to get feedback during the installation:

- -vv — Prints debugging information during installation. This is a good way to see everything that happens during the install process. (This output can be long, so you may want to pipe it to more.)
- -h — Prints 50 hash marks (#) as the package is unpacked. The intent is just to see the progress of the unpacking process (so you can tell if the program is still working or stalled).
- -percent — Prints the percentage of the total package that has been installed throughout the install process.

Before installing a package, `rpm` checks to make sure that it is not overwriting newer files or installing a package that has dependencies on other packages that are not installed. The following install options can be used to override conditions that may otherwise cause the installation to fail:

- --force — Forces the contents of the current package to be installed, even if the current package is older than the one already installed, contains files placed there by other packages, or is already installed. (This is the same as using the oldpackage, replacefiles, and replacepkgs options.)
- --oldpackage — Forces the package to be installed, even if the current package is older than the one already installed.
- --replacefiles — Forces files in this package to be installed, even if the files were placed there by other packages.
- --replacepkgs — Forces packages in this archive to be installed, even if they are already installed on the system.
- --nodeps — Skips package dependency checks and installs the package, even if packages it depends on are not installed.
- --ignorearch — Forces package to be installed, even if the binaries in the package don’t match the architecture of your host computer.
- --ignoreos — Forces package to be installed, even if the binaries in the package don’t match the architecture of your operating system.

The following is a simple `rpm` command line used to install an RPM archive.

```
# rpm -i audiofile-devel-0.1.6-1.i386.rpm
```

I personally like to see some feedback when I install something (by default, `rpm` is suspiciously quiet when it succeeds). Here is what the command looked like when I added the -vv option to get more verbose feedback, along with some of the output:

```
# rpm -ivv audiofile-devel-0.2.1-2.i386.rpm
D: counting packages to install
D: found 1 packages
D: looking for packages to download
D: retrieved 0 packages
D: finding source and binary packages
D: New Header signature
.
D: opening database in /var/lib/rpm/
D: installing binary packages
Installing audiofile-devel-0.2.1-2.i386.rpm
.
D: package: audiofile-devel-0.2.1-2 files test = 0
D: running preinstall script (if any)
D: running postinstall script (if any)
```

From this output, you can see that `rpm` finds one package in this archive, verifies the signature, opens the RPM database, installs the packages, and runs any pre- or postinstall scripts.
