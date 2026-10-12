Building many software packages for Linux that are distributed in source form requires the use of GNU's autoconf utility. This program builds an executable shell script named configure that, when executed, automatically examines and tailors a client's build from source according to software resources, or dependencies (such as programming tools, libraries, and associated utilities), that are installed on the target host (your Linux system). The idea is to increase software project portability and ease the task of the programmer who is faced with a software project expected to run on many compatible, yet potentially disparate, software platforms.

Many Linux commands and graphical clients for X downloaded in source code form include configure scripts. To configure the source package, build the software, and then install the new program, the root user might use the script like this (after uncompressing the source and navigating into the resulting build directory):

```
# ./configure ; make ; make install
```

The autoconf program uses a file named configure.in that contains a basic ruleset, or set of macros. The configure.in file is created with the autoscan command. Building a properly executing configure script also requires a template for the makefile, named Makefile.in. Although creating the dependency-checking configure script can be done manually, you can easily overcome any complex dependencies by using a graphical project development tool such as KDE's KDevelop or GNOME's Glade. (See the section “Graphical Development Tools,” later in this chapter, for more information.)

# ## Managing Software Projects with RCS and CVS

Although make can be used to manage a software project, larger software projects require document management, source code controls, security, and revision tracking as the source code goes through a series of changes during its development. RCS and CVS provide source code version control utilities for this kind of large software project management. You can find both of these utilities in RPM packages on your Fedora Core Linux CD-ROMs.

The RCS and CVS systems are used to track changes to multiple versions of files, and they can be used to backtrack or branch off versions of documents inside the scope of a project. They can also be used to prevent or resolve conflicting entries or changes made to source code files by multiple developers.

Although RCS and CVS provide similar features, RCS uses a locking and unlocking scheme to control access for making revisions; CVS, on the other hand, provides a modification and merging approach to working on older, current, or new versions of software. RCS uses different programs to check in or out of a revision under a directory; CVS uses a number of administrative files in a software repository of source code modules to merge and resolve change conflicts.

![](bbox=[0.05, 0.915, 0.11, 0.93])

Numerous changes to a source tree (directory of source code files) can also be accomplished using the patch command. Although patch does not offer the source control features of RCS