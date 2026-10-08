# ## 6.24. Nurses-6.1

The Nurses package contains libraries for terminal-independent handling of character screens.

Approximate build time: 0.4 SBU
Required disk space: 42 MB

# ### 6.24.1. Installation of Nurses

Don't install a static library that is not handled by configure:

```
sed -i '/LIBTOOL_INSTALL/d' c++/Makefile.in
```

Prepare Nurses for compilation:

```
./configure --prefix=/usr \
    --mandir=/usr/share/man \
    --with-shared \
    --without-debug \
    --without-normal \
    --enable-pc-files \
    --enable-wide
```

The meaning of the new configure options:

+   --enable-wide
This switches wide-character libraries (e.g., libncursesw.so.6.1) to be built instead of normal ones (e.g., libncurses.so.6.1). These wide-character libraries are usable in multibyte and traditional 8-bit locales, while normal libraries work properly in 8-bit locales. Wide-character and normal libraries are source-compatible, but not binary-compatible.

+   --enable-pc-files
This switch generates and installs .pc files for pkg-config.

+   --without-normal
This switch disables building and installing most static libraries.

Compile the package:

```
make
```

This package has a test suite, but it can only be run after the package has been installed. The tests reside in the test/ directory. See the README file in that directory for further details.

Install the package:

```
make install
```

Move the shared libraries to the /lib directory, where they are expected to reside:

```
mv -v /usr/lib/libncursesw.so.* /lib
```

Because the libraries have been moved, one symlink points to a non-existent file. Recreate it:

```
ln -sfv ../../lib/$(readlink /usr/lib/libncursesw.so) /usr/lib/libncurses.so
```