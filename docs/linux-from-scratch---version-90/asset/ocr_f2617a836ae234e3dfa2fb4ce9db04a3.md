# 5.4. Binutils-2.32 - Pass 1

The Binutils package contains a linker, an assembler, and other tools for handling object files.

Approximate build time: 1 SBU
Required disk space: 580 MB

# 5.4.1. Installation of Cross Binutils

> Note
Go back and re-read the notes in the previous section. Understanding the notes labeled important will save you a lot of problems later.

It is important that Binutils be the first package compiled because both Glibc and GCC perform various tests on the available linker and assembler to determine which of their own features to enable.

The Binutils documentation recommends building Binutils in a dedicated build directory:

```
mkdir -v build
cd build
```

> Note
In order the SBU values listed in the rest of the book to be of any use, measure the time it takes to build this package from the configuration, up to and including the first install. To achieve this easily, wrap the commands in a time command like this: time ( .configure ... && make install; );

> Note
The approximate build SBU values and required disk space in Chapter 5 does not include test suite data.

Now prepare Binutils for compilation:

```
../configure --prefix=/tools         \
      --with-sysroot=$LFS             \
      --with-lib-path=/tools/lib     \\
      --target=$LFS_TGT               \
      --disable-nls                   \
      --disable-error
```

The meaning of the configure options:

--prefix=/tools
This tells the configure script to prepare to install the Binutils programs in the /tools directory.

--with-sysroot=$LFS
For cross compilation, this tells the build system to look in LFS for the target system libraries as needed.

--with-lib-path=/tools/lib
This specifies which library path the linker should be configured to use.