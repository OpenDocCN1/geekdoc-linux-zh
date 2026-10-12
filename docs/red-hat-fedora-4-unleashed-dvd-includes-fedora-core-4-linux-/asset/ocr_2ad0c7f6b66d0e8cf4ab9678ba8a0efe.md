> **NOTE**
> For other software package formats, you can use the File Roller application (found in the Accessories menu) to easily display, browse, read, and extract contents of compressed files, including legacy archives such as tarballs or compressed tar archives (recognized by their .gz or .tgz extensions). Other compressed files, such as those created with the compress command (ending in .Z) or bzip2 files (ending in .bz2), are also supported by File Roller. The File Roller client will also convert compressed archives between gzip and bzip2 formats.

# ## Building RPMs from src.rpm Files

A rule of thumb is that you never build rpms as the root user even though the directories are already set up at /usr/src/redhat as follows:

```
```
# tree /usr/src/redhat
/usr/src/redhat
|-- BUILD
`-- RPMs
    |-- athlon
    |-- i386
    |-- i486
    |-- i586
    |-- i686
    `-- noarch
`-- SOURCES
`-- SPECS
`-- SRPMS
```
```

Using the mkdir command, re-create this directory tree structure in your home directory; you can name the new directory redhat (or anything you like). You might even want to create a new user just to build rpms and source code. (You can compile without being root; you just can't install the software systemwide as a regular user.)

The configuration information for building rpms is kept in three places:

+   * /usr/lib/rpm/*/macros—The systemwide defaults.
+   * /etc/rpm/macros.*—Where systemwide changes are kept.
+   * ~/.rpmmacros—Where user-specific changes are kept.

Because we need to tell rpm that we will not be using the systemwide default build location for our user, we can

```
```
$ echo "%_topdir $HOME/redhat" > $HOME/.rpmmacros
```
```