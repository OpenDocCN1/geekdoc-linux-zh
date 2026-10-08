
## 6.22. Bzip2-1.0.8

The Bzip2 package contains programs for compressing and decompressing files. Compressing files with bzip2 yields a much better compression percentage than the traditional gzip.

**Approximate build time:** less than 0.1 SBU

**Required disk space:** 7.7 MB

### 6.22.1. Installation of Bzip2

Apply a patch that will install into the documentation for this package:

```
patch -Np1 -i ../bzip2-1.0.8-install_docs-1.patch
```

The following command ensures installation of symbolic links are relative:

```
sed -i 's@(ln -s -f \$(PREFIX)/bin/@@g' Makefile
```

Ensure the manual pages are installed into the correct location:

```
sed -i "s@ (PREFIX)/man@(PREFIX)/share/man@g" Makefile
```

Prepare Bzip2 for compilation with:

```
make -f Makefile-libbz2_so
make clean
```

The meaning of the make parameter:

> -f Makefile-libbz2_so

This will cause Bzip2 to be built using a different Makefile file, in this case the Makefile-libbz2_so file, which creates a dynamic libbz2.so library and links the Bzip2 utilities against it.

Compile and test the package:

```
make
```

Install the programs:

```
make PREFIX=/usr install
```

Install the shared bzip2 binary into the /bin directory, make some necessary symbolic links, and clean up:

```
cp -av bzip2-shared /bin/bzip2
cp -sv ../lib/libbz2.so.1.0 /lib/libbz2.so
rm -v /usr/bin/(bzip2,bzcat,bzip22)
ln -sv bzip2 /bin/bzip2
ln -sv bzip2 /bin/bzcat
```

### 6.22.2. Contents of Bzip2

- **Installed programs:** bzip2 (link to bzip2), bzcat (link to bzip2), bzcmp (link to bdiff), bdiff, bzegrep (link to bzegrep), bzfgrep (link to bzegrep), bzgrep, bzip2, bzip2recover, bless (link to bzmore), and bzmore
- **Installed libraries:** libbz2.[a,so]
- **Installed directory:** /usr/share/doc/bzip2-1.0.8

# Short Descriptions

| Program | Description |
| :--- | :--- |
| bunzip2 | Decompresses bzipped files |
| bzcat | Decompresses to standard output |
| bzcmp | Runs **cmp** on bzipped files |
| bzldiff | Runs **diff** on bzipped files |
| bzegrep | Runs **egrep** on bzipped files |
| bzfgrep | Runs **fgrep** on bzipped files |
| bzgrep | Runs **grep** on bzipped files |
| bzip2 | Compresses files using the Burrows-Wheeler block text compression algorithm with Huffman coding; the compression rate is better than that achieved by more compressors using “Lempel-Ziv” algorithms, like **gzip** |
| bzip2recover | Tries to recover data from damaged bzipped files |
| bzless | Runs **less** on bzipped files |
| bzmore | Runs **more** on bzipped files |
| libbz2 | The library implementing lossless, block-sorting data compression, using the Burrows-Wheeler algorithm |

## 6.23. Pkg-config-0.29.2

The Pkg-config package contains a tool for passing the include path and/or library paths to build tools during the configure and make file execution.

**Approximate build time:** 0.4 SBU
**Required disk space:** 30 MB

### 6.23.1. Installation of Pkg-config

Prepare Pkg-config for compilation:

```
./configure --prefix=/usr \
    --with-internal-glib \
    --disable-host-tool \
    --docdir=/usr/share/doc/pkg-config-0.29.2
```

The meaning of the new configure options:

- --with-internal-glib
This will allow pkg-config to use its internal version of Glib because an external version is not available in LFS.
- --disable-host-tool
This option disables the creation of an undesired hard link to the pkg-config program.

Compile the package:

```
make
```

To test the results, issue:

```
make check
```

Install the package:

```
make install
```

### 6.23.2. Contents of Pkg-config

- **Installed program:** pkg-config
- **Installed directory:** /usr/share/doc/pkg-config-0.29.2

# Short Descriptions

**pkg-config** Returns meta information for the specified library or package

## 6.24. Nurses-6.1

The Nurses package contains libraries for terminal-independent handling of character screens.

Approximate build time: 0.4 SBU
Required disk space: 42 MB

### 6.24.1. Installation of Nurses

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

- --enable-wide
This switches wide-character libraries (e.g., libncursesw.so.6.1) to be built instead of normal ones (e.g., libncurses.so.6.1). These wide-character libraries are usable in multibyte and traditional 8-bit locales, while normal libraries work properly in 8-bit locales. Wide-character and normal libraries are source-compatible, but not binary-compatible.
- --enable-pc-files
This switch generates and installs .pc files for pkg-config.
- --without-normal
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

Linux From Scratch - Version 9.0

Many applications will expect the linker to be able to find non-wide-character Ncurses libraries. Trick such applications into linking with wide-character libraries by means of symlinks and linker scripts:

```
for lib in ncurses menu ; do
  rm -vf /usr/lib/lib${lib}.so
  echo "INPUT-${lib}w" > /usr/lib/lib${lib}.so
  ln -sfn ${lib}w.pc /usr/lib/pkgconfig/${lib}.pc
done
```

Finally, make sure old applications that use -lcurses at build time are buildable:

```
rm -vf /usr/lib/libcurses.sw
echo "INPUT-(ncursesw)" > /usr/lib/libcurses.so
ln -sfn libncurses.so
```

If desired, install the Ncurses documentation:

```
mkdir -v /usr/share/doc/ncurses-6.1
cp -v -R doc/* /usr/share/doc/ncurses-6.1
```

![](img/78f4ce02ad2a3526b7a07a130d5ef5bd_144_0.png)

> Note
The instructions above don't create non-wide-character Ncurses libraries since package installed by compiling from sources would link against them at runtime. However, the only known binary-only applications that link against non-wide-character Ncurses libraries require version. If you must have such libraries, recompile the with the following commands:

```
make distclean
./configure --prefix=/usr \
  --with-shared \
  --without-normal \
  --without-debug \
  --without-cxx-binding \
  --with-abi=5
make sources libs
cp -av libn*.so /usr/lib
```

## 6.2.4. Contents of Nurses

- **Installed programs:** captoinfo (link to tic), clear, infocmp, intofac (link to tic), ncursesw6-reset (link to tset), tabs, tic, toep, and tost
- **Installed libraries:** libcurses.so (symlink and linker script to libncurses.so), libform.so, libmenew.so, libncurses.so, libncurses++, libpanel.so, and their non-character counterparts without "w"
- **Installed directories:** /usr/share/tabset, /usr/share/terminfo, and /usr/share/doc/ncurses-6.1

# Short Descriptions

| Program | Description |
| :--- | :--- |
| captoinfo | Converts a termcap description into a terminfo description |
| clear | Clears the screen, if possible |
| infocmp | Compares or prints terminfo descriptions |
| infotcap | Converts a terminfo description into a termcap description |
| ncursesw6-config | Provides configuration information for ncurses |
| reset | Initializes a terminal to its default values |
| tabs | Clears and sets stops on a terminal |
| tic | The terminfo entry-description compiler that translates a terminfo file from source format into the binary format needed for the ncurses library routines |
| toe | Lists all available terminal types, giving the primary name and description for each |
| tput | Makes the values of terminal-dependent capabilities available to the shell; it can also be used to reset or initialize a terminal or report its long name |
| tset | Can be used to initialize terminals |
| libcursesw | A link to libncurses |
| libncurses | Contains functions to display text in many complex ways on a terminal screen; a good example of the use of these functions is the menu displayed during the kernel's make menuconfig |
| libformw | Contains functions to implement forms |
| libmenuw | Contains functions to implement menus |
| libpanelw | Contains functions to implement panels |
