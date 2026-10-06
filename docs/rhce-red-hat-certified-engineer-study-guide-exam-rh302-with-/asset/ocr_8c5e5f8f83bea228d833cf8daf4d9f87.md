# Adding Packages 289

If a package requires a capability's provided neither by a package specified in the same command nor by an installed package, the rpm command prints an error message. For example:

```
# rpm -i gnorpm-0.9-10.i386.rpm
error: failed dependencies:
  usermode >=1.13 is needed by gnorpm-0.9-10
  librpm.so.0 is needed by gnorpm-0.9-10
```

To resolve a dependency, you must install the appropriate package, providing the required capability, or upgrade an existing package to a later version. For instance, the error message states that a newer version of the usermode package is required and that the library named librpm.so.0 is required. In this chapter, you will learn how to discover what capabilities a package provides so that you can determine, for example, what package will provide the librpm.so.0 library.

If you try to install a package that conflicts with an existing package or file, you will see an error message that resembles this one:

```
# rpm -i gnorpm-0.9-10.i386
file /usr/bin/gnrpm from install of gnorpm-0.9-10
--conflicts with file from package goway-0.8-5
file /usr/share/gnome/apps/System/gnrpm.desktop
--install of gnorpm-0.9-10 conflicts with file from
--package goway-0.8-5
file /usr/share/gnome/help/gnrpm/gnrpm.html
--install of gnorpm-0.9-10 conflicts with file from
--package goway-0.8-5
```

You'll see another error message if you attempt to install a package for which there is insufficient disk space.

Suppose you install a software program distributed by a TAR file. Later, a newer version of the software is published, one that uses RPM for distribution. When you install the new package, RPM determines whether it will overwrite existing files. Rather than overwrite files RPM recognizes as configuration files, it saves each existing configuration by appending .rpms to its name.

To overcome errors and other exceptions, you may have occasional need for the following special rpm arguments:

+   - --force, which overwrites new packages or existing files
- --nodeps, which skips dependency checking
- --replacefiles, which replaces files owned by another package

Copyright ©2000 SYBEX, Inc., Alameda, CA www.sybex.com