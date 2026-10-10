
## Verifying installed packages with rpm

If something in a software package isn't working properly, or if you suspect that your system has been tampered with, the verify (-v) option of `rpm` can help you verify installed software against its original software package. Information about each installed package is stored on your computer in the RPM database. By using the verify option, you can check whether any changes were made to the components in the package.

> **NOTE:** The verify option uses the uppercase letter (-V), while the verbose option uses the lowercase (-v).

Various file size and permissions tests are done during a verify operation. If everything is fine, there is no output. Any components that have changed from when they were installed will be printed along with information indicating how they were changed. Here's an example:

```bash
# rpm -v ppp
S5...T. c /etc/ppp/chap-secrets
S5...T. c /etc/ppp/options
S5...T. c /etc/ppp/pap-secrets
```

This output shows that the ppp package (used to dial up a TCP/IP network such as the Internet) has had three files changed since it was installed. The notation at the beginning shows that the file size (S), the MD5 sum (5), and the modification time (T) have all changed. The letter *c* shows that these are all configuration files. By reviewing these files to see that the changes were only those that I made to get PPP working, I can verify that the software is okay.

The indicators that you may see when you verify the contents of a configuration file are:

- **5 (MD5 Sum)**— An MD5 checksum indicates a change to the file contents.
- **S (File size)**— The number of characters in the file has changed.
- **L (Symlink)**— The file has become a symbolic link to another file.
- **T (Mtime)**— The modification time of the file has changed.
- **D (Device)**— The file has become a device special file.
- **U (User)**— The user name that owns the file has changed.
- **G (Group)**— The group assigned to the file has changed.
- **M (Mode)**— If the ownership or permission of the file changed.

> **TIP:** A utility is available to browse the contents of RPM files from Microsoft Windows. With the `rpmbrowser.exe` utility, you can list and extract files from an RPM distribution. This utility is available from winsite.com (search for `rpmbrowser` from www.winsite.com/search).

## Using Software in Different Formats

There may not be RPMs available for every piece of software you want to install on your Fedora or RHEL system. Likewise, you may find that an RPM isn't configured exactly the way you would want it, so that you would be better served by building your own RPM from an RPM source code package. The following sections describe various forms in which you may encounter open source software and different ways of building and installing that software for you to use.

### Understanding software package names and formats

Whenever possible, you want to install the applications you use with Fedora from software packages in RPM format (files with a .rpm extension). However, if an RPM isn't available, the software that you want may come in other package formats.

Say you just downloaded a file from the Internet that contains lots of names, numbers, dots, gz, and tars. What does all that stuff mean? Well, when you break it down, it's really not that complicated.

Most of the names of archive files containing Linux applications follow the GNU-style package-naming conventions. The following example illustrates the package-naming format:

```
mycoolapp-4.2.3-1.i386.rpm
mycoolapp-4.2.3.tar.gz
mycoolapp-4.2.3.src.tar.gz
mycoolapp-4.2.3.bin.SPARC.tar.gz
mycoolapp-4.2.3.bin.BEP.static.tar.gz
```

These examples represent several different packages of the same software application. The name of this package is mycoolapp. Following the package name is a set of numbers that represent the version of the package. In this case, it is version 4.2.3 (the major version number is 4, followed by minor version number and patch level 2.3). After the version number is a dot, followed by some optional parts, which are followed by indications of how the file is archived and compressed.

The first line shows a package that is in the **RPM Package Manager** (.rpm) format. The .1.386 before the .rpm indicates that the package contains binaries that are built to run Intel i386 architecture computers (in other words, PCs). The -1 indicates the build level (the same package may have been rebuilt multiple times to make minor changes). See the sidebar “Using Binary RPMs versus Building from Source” for the pros and cons of using prebuilt RPM binary packages as opposed to compiling the program yourself.

### Using Binary RPMs versus Building from Source

Binaries created in RPM format are easily installed, managed, and uninstalled using tools such as **rpm** and **yum**. This is the recommended installation method for Fedora and RHEL novices. Sometimes, however, building an application from source code may be preferable. Here are some arguments on both sides:

- **RPM** — Installing applications from a binary RPM archive is easy. After the application is installed, there are both shell commands and GUIs for managing, verifying, updating, and removing the **RPM** package. You don't need to know anything about Makefiles or compilers. When you install a binary RPM package, **RPM** tools even check to make sure that other packages that the package depends on are installed. Because Red Hat has released **RPM** under the **GPL**, other Linux distributions also use it to distribute their software. Thus, most Linux applications are, or will be, available in **RPM** format.
- **Source code** — Not all source-code packages are made into **RPM** binaries. If you use **RPM**, you may find yourself with software that is several versions old, when you could simply download the latest source code and run a few tar and make commands. Also, by modifying source code, you can tailor the package to better suit your needs.

Refer to Appendix A for information on getting source code for Fedora **RPM** binary packages that are included on the DVD that comes with this book. You can modify that source code yourself and rebuild the **RPM** binaries. The rebuilt binaries can be tuned to your hardware and include the features you want with the package. For more information on **RPMs**, refer to the *Red Hat RPM Guide* by Eric Foster-Johnson (Red Hat Press/Wiley, 2003).

In the next two lines of the previous example, each file contains the source code for the package. The files that make up the package were archived using the **tar** command (.tar) and compressed using the **gzip** command (.gz). You use these two commands (or just the **tar** command with the *-tz option*) to expand and uncompress the packages when you are ready to install the applications.

Between the version number and the .tar.gz extension there can be optional tags, separated by dots, which provide specific information about the contents of the package. In particular, if the package is a binary version, this information provides details about where the binaries will run. In the third line, the optional .src tag was added because the developer wanted to differentiate between the source and binary versions of this package. In the fourth line, the .bin.SPARC detail indicates that it is a binary package, ready to run on a SPARC workstation. The final line indicates that it is a binary package, consisting of statically linked ELF format executables.

Instead of using gzip, many software packagers today use the bzip2 utility to compress their software archives. In that case, files names shown in the examples above might instead end with .bz2 or .tar.bz2 extensions.

Here is a breakdown of the parts of a package name:

- **name** — This is generally an all-lowercase string of characters that identifies the application.
- **dash (-)**
- **version** — This is shown as major to minor version number from left to right.
- **dot (.)**
- **src or bin** — This is optional, with src usually implied if no indication is given.
- **dot (.)**
- **type of binary** — This is optional and can include several different tags to describe the content of the binary archive. For example, i386 indicates binaries intended for Intel architectures (Pentium CPU) and SPARC indicates binaries for a Sparc CPU.
- **dot (.)**
- **archive type** — Often tar is used (.tar).
- **compression type** — Often gzip is used (.gz).

## Using different archive and document formats

Many of the software packages that are not associated with a specific distribution (such as Fedora or Debian) use the tar/gzip method for archiving and compressing files. However, you may notice files with different suffixes at software project sites.

Table 5-1 describes the different file formats that you will encounter as you look for software at a Linux FTP site. Table 5-2 lists some of the common document formats that are used in distributing information in Linux.
