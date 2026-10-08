# # 6.16. Binutils-2.32

The Binutils package contains a linker, an assembler, and other tools for handling object files.
Approximate build time: 7.4 SBU
Required disk space: 5.1 GB

#  6.16.1. Installation of Binutils

Verify that the PTYs are working properly inside the chroot environment by performing a simple test:

```
expect -c "spawn ls"
```

This command should output the following:

```
spawn ls
```

If, the output includes the message below, then the environment is not set up for proper \ operation. This issue needs to be resolved before running the test suites for Binutils and GCC:

```
The system has no more ptys.
Ask your system administrator to create more.
```

Now remove one test that prevents the tests from running to completion:

```
sed -i '/@/tincimental_copy/d gold/testsuite/Makefile.in
```

The Binutils documentation recommends building Binutils in a dedicated build directory:

```
mkdir -v build
cd build
```

Prepare Binutils for compilation:

```
./configure --prefix=/usr /\n--enable-gold /\n--enable-ld=default /\n--enable-plugins /\n--enable-shared /\n--disable-werror /\n--enable-64-bit-bfd /\n--with-system-zlib
```

The meaning of the configure parameters:

+   --enable-gold
Build the gold linker and install it as ld.gold (along side the default linker).
--enable-ld=default
Build the original bdf linker and install it as ld (the default linker) and ld.bfd.
--enable-plugins
Enables plugin support for the linker.