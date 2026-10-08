# 6.48. Libelf from Elutfils-0.177

Libelf is a library for handling ELF (Executable and Linkable Format) files.

Approximate build time: 1.1 SBU
Required disk space: 95 MB

# 6.48.1. Installation of Libelf

Libelf is part of elutfils-0.177 package. Use the elutfils-0.177.tar.bz2 as the source tarball.

Prepare Libelf for compilation:

```
./configure --prefix=/usr
```

Compile the package:

```
make
```

To test the results, issue:

```
make check
```

Install only Libelf:

```
make -C libelf install
install -vm644 config/libelf.pc /usr/lib/pkgconfig
```

# 6.48.2. Contents of Libelf

Installed Library: libelf.so
Installed Directory: /usr/include/elutfils