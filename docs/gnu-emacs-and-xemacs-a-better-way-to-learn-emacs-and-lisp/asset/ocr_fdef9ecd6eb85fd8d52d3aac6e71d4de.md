```
```txt
---show-targets---
    --build-targets=G
    --builddir=D
    --prefix=PREFIX:1
    --infodir=DIR:1
    --mandir=DIR
    --localedir=DIR
    --libexecdir=DIR
    --program-prefix=PREFIX:0
    --program-suffix=SUFFIX
    --program-transform-names=RULE:PREFIX/SUFFIX:RULE
Help:
    --build:config
    --host=TRIPLET:1
    --target=TRIPLET:1
Features and makeflags:
    --enable-FEATURE
    --enable-FEATURE=ARG:2
    --with-PACKAGE:2
    --with-PACKAGE=ARG:3
    --with-emacs
    --without-emacs
    --with-x
    --without-x
    --with-libsystem
    --with-tls
    --with-pkgconfig
    --without-pkgconfig
    --with-modules
    --without-modules
    --with-native-compilation
    --without-native-compilation

Configure Emacs:
    make install:install
    make check:check
    make doc:doc
    make installcheck:installcheck
    make distclean:distclean
    make maintainer-clean:maintainer-clean
Switches can be displayed on your screen that allow you to change the installation directory or enable or disable certain features, among other things.
```
```
/opt/share/emacs/../
/opt/share/emacs/../
/opt/share/emacs/../
/opt/share/emacs/../
/opt/share/emacs/../
/opt/share/emacs/../
/opt/share/emacs/../
/opt/share/emacs/../
/opt/share/emacs/../
/opt/share/emacs/..
```
```

# *Figure 2.2* *Configure Script Help*

Switches will be displayed on your screen that allow you to change the installation directory or enable or disable certain features, among other things (see Figure 2.2).

An example of a switch is `prefix={directory}`. Let’s say you wanted Emacs installed in the directory `/opt` instead of the default, which is `/usr/local`. The command to type would look like this:

```
```sh
./configure --prefix=/opt
```
```

This switch would cause the Emacs executable to end up in `/opt/bin` (after the build and install process was completed), and the other Emacs files would be installed in `/opt/share/emacs`.

Unless you are really short on disk space in `/usr/local`, you probably can just run the configure script without any switches. Change to the directory that was created when you unpacked the source archive, and then type

```
```sh
./configure
```
```

The `.` typed before `configure` is a Linux convention. It tells your shell to run a script or executable named `configure` in the current directory, rather than searching your path and running the first file named `configure` that it finds. See Figure 2.3.