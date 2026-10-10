Between the version number and the .tar.gz extension there can be optional tags, separated by dots, which provide specific information about the contents of the package. In particular, if the package is a binary version, this information provides details about where the binaries will run. In the third line, the optional .src tag was added because the developer wanted to differentiate between the source and binary versions of this package. In the fourth line, the .bin.SPARC detail indicates that it is a binary package, ready to run on a SPARC workstation. The final line indicates that it is a binary package, consisting of statically linked ELF format executables.

Instead of using gzip, many software packagers today use the bzip2 utility to compress their software archives. In that case, files names shown in the examples above might instead end with .bz2 or .tar.bz2 extensions.

Here is a breakdown of the parts of a package name:

+   - **name** — This is generally an all-lowercase string of characters that identifies the application.
+   - **dash (-)**
+   - **version** — This is shown as major to minor version number from left to right.
+   - **dot (.)**
+   - **src or bin** — This is optional, with src usually implied if no indication is given.
+   - **dot (.)**
+   - **type of binary** — This is optional and can include several different tags to describe the content of the binary archive. For example, i386 indicates binaries intended for Intel architectures (Pentium CPU) and SPARC indicates binaries for a Sparc CPU.
+   - **dot (.)**
+   - **archive type** — Often tar is used (.tar).
+   - **compression type** — Often gzip is used (.gz).

# Using different archive and document formats

Many of the software packages that are not associated with a specific distribution (such as Fedora or Debian) use the tar/gzip method for archiving and compressing files. However, you may notice files with different suffixes at software project sites.

Table 5-1 describes the different file formats that you will encounter as you look for software at a Linux FTP site. Table 5-2 lists some of the common document formats that are used in distributing information in Linux.