
## Using `ncftp` for Downloading

3. Type `binary` (to make sure the file is downloaded as a binary file).

4. To download a file from the current working directory, type `get file` where `file` is the application name. For example, to download the whichman application while `/pub/Linux/apps` doctools is the current directory, type:

   ```
   > `get whichman-2.0.tar.gz`
   ```

5. When the download is complete, type `exit`.

> **TIP**: Before you start the `ncftp` command, make sure that your current directory is the one in which you want to download the file. Alternatively, you could change to the directory you want by using the `lcd` command within `ncftp`. For example, to change to `/tmp/abcapp`, type `lcd /tmp/abcapp`.

## Using `rpmfind` for downloading

If you are looking for software packages you know are in RPM format, `rpmfind` is probably the best tool for finding and downloading them. Besides finding the packages you request, `rpmfind` checks your Linux system so it can find packages that best match your current configuration.

To use `rpmfind`, type `rpmfind` along with the software package you want. If you are connected to the Internet, `rpmfind` finds the package and asks if you want to download it. Here is an example of how you may use the `rpmfind` command to find the `xv` software packages:

```
# cd /tmp
# rpmfind xv
Installing xv will require 943 KBytes
Non-qualified hostname: maple (none)
ftp://ftp.redhat.com/pub/redhat/redhat-7.1/powertools/i386/RedHat/RPMS/
xv-3.10a-23.i386.rpm
Do you want to download these files to /tmp? [Y/n/a/i] ? : Y
```

After you type Y, the software package is downloaded to your current directory (in this case, `/tmp`). You can then use the `rpm -i /tmp/xv*` command to install the package. (Replace `/tmp/xv*` with the name of the package you want to download.)

> **NOTE**: I particularly recommend using the `rpmfind` command to get software packages that were part of the Red Hat Linux PowerTools CD that was discontinued for Red Hat Linux 7.2. Those packages are not included with this book, though several previous PowerTools packages (such as `xv`) are referenced in this book. For RPMs that are part of the Red Hat Linux distribution, you should use the `update` command, as described in Chapter 10.

## Understanding package names and formats

You just downloaded a massive file from the Internet that contains lots of names, numbers, dots, *gzs*, and *tars*. What does all that stuff mean? Well, when you break it down, it’s really not that complicated.

Most of the names of archive files containing Linux applications follow the GNU-style package-naming conventions. The following example illustrates the package-naming format:

```
mycoollapp-4.2.3.i386.rpm
mycoollapp-4.2.3.tar.gz
mycoollapp-4.2.3.src.tar.gz
mycoollapp-4.2.3.bin.SPARC.tar.gz
mycoollapp-4.2.3.bin.ELF.static.tar.gz
```

These examples represent several different packages of the same software application. The name of this package is *mycoollapp*. Following the package name is a set of numbers that represent the version of the package. In this case, it is version 4.2.3 (the major version number is 4, followed by minor version number and patch level 2.3). After the version number is a dot, followed by some optional parts, which are followed by indications of how the file is archived and compressed.

The first line shows a package that is in Red Hat Package Manager (.rpm) format. The .i386 before the .rpm indicates that the package contains binaries that are built to run Intel i386 architecture computers (in other words, PCs). See the sidebar “RPM Versus Building from Source” for the pros and cons of using prebuilt RPM binary packages as opposed to compiling the program yourself.

In the next two lines of the previous example, each file contains the source code for the package. The files that make up the package were archived using the *tar* command (.tar) and compressed using the *gzip* command (.gz). You use these two commands to expand and uncompress the packages when you are ready to install the applications.

Between the version number and the .tar.gz suffixes there can be optional tags, separated by dots, which provide specific information about the contents of the package. In particular, if the package is a binary version, this information provides details about where the binaries will run. In the third line, the optional .src tag is added because the developer wanted to differentiate between the source and binary versions of this package. In the fourth line, the .bin.SPARC indicates that it is a binary package, ready to run on a SPARC workstation. The final line indicates that it is a binary package, consisting of ELF format executables that are statically linked.

## RPM Versus Building from Source

Binaries created in RPM format are easily installed, managed, and uninstalled using Red Hat tools. This is the recommended installation method for Red Hat Linux novices. Sometimes, however, building an application from source code may be preferable. Here are some arguments on both sides:

- **RPM** — Installing applications from an RPM archive is easy. After the application is installed, there are both shell commands and GUIs for managing, verifying, updating, and removing the RPM application. You don't need to know anything about Makefiles or compilers. When you install an RPM package, RPM tools even check to make sure that other packages that the package depends on are installed. Because Red Hat has released RPM under the GNU, other Linux distributions have begun using it to distribute their software. Thus, most Linux applications are, or will be, available in RPM format.

- **Source code** — It sometimes takes a while for a source-code package to be made into RPM binaries. If you use RPM you may find yourself with software that is several versions old, when you could simply download the latest source code and run a few tar and make commands. Also, by modifying the source code, you may be able to tailor the application to better suit your needs. When you compile the source code on your computer, it is also more likely to be optimized to run efficiently on your computer.

Here is a breakdown of the parts of a package name:

- **name** — This is generally an all-lowercase string of characters that identifies the application.
- **dash (-)**
- **version** — This is shown as major to minor version number from left to right.
- **dot (.)**
- **src or bin** — This is optional, with src usually implied if no indication is given.
- **dot (.)**
- **type of binary** — This is optional and can include several different tags to describe the content of the binary archive. For example, i386 indicates binaries intended for Intel architectures (386, 486, Pentium, and so on) and SPARC indicates binaries for a Sparc CPU.
- **dot (.)**
- **archive type** — Often tar is used (.tar)
- **compression type** — Often gzip is used (gzip)

## Using different archive and document formats

Many of the software packages that are not associated with a specific distribution (such as Red Hat, Debian, or Open Linux) use the tar/gzip method for archiving and compressing files. However, you may notice files with different suffixes at Linux FTP sites. Sometimes these files represent documents that can be in various formats. Also, several of the distributions have their own software packaging format, which are indicated by a different suffix.

> **NOTE:** Because we are using Red Hat Linux, most of the software applications we install are in Red Hat Package Management format (.rpm). Unless you want to build the software yourself — in which case you’ll need the source code — RPM is the format to look for. When it is available, an RPM package from a Red Hat FTP site will provide your best chance for getting a software package that will run without modification on a Red Hat Linux system. RPM packages also let you use RPM tools to query packages, add packages, and remove the packages.

Table 5-1 describes the different file formats that you will encounter as you look for software at a Linux FTP site. Table 5-2 lists some of the common document formats that are used in distributing information in Linux.

### Table 5-1: Linux Archive File Formats

| Format | Suffix | Description |
| :--- | :--- | :--- |
| Gzip file | .gz or .z | File was compressed using the GNU gzip utility. It can be uncompressed using the gzip or gunzip utilities (they are both the same). |
| Tar file | .tar | File was archived using the tar command. tar is used to gather multiple files into a single archive file. You can expand the archive into separate files using tar with different options. |
| Bzip2 | .bz2 | File was compressed with the bzip2 program. |
| Tar/compressed | .taz or .tz | File was archived with tar and compressed with the UNIX compress command. (The compress command is not part of the GNU because it is patented.) |
| Linux Software Map | .lsm | File contains text that describes the content of an archive. |
| Debian Binary Package | .deb | File is a binary package used with the Debian Linux distribution. (See descriptions of how to convert Debian to Red Hat formats later in this chapter.) |
| Red Hat Package Management | .rpm | File is a binary package used with Red Hat Linux. Format also available to other Linux distributions. |
