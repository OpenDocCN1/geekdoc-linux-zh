# 26.27. Libcap-2.27

The Libcap package implements the user-space interfaces to the POSIX 1003.1e capabilities available in Linux kernels. These capabilities are a partitioning of all the powerful root privilege into a set of distinct privileges.

**Approximate build time:** less than 0.1 SBU
**Required disk space:** 1.5 MB

# 26.27.1. Installation of Libcap

Prevent a static library from being installed:

```
sed -i '/install.*STALENAME/d' libcap/Makefile
```

Compile the package:

```
make
```

This package does not come with a test suite.

Install the package:

```
make RAISE_SETFCAP=no libcap prefix=/usr install
chmod -v 755 /usr/lib/libcap.so.2.27
```

The meaning of the make option:

> RAISE_SETFCAP=no
This parameter skips trying to use setcap on itself. This avoids an installation error if the kernel or file system does not support extended capabilities.

libcap
This parameter installs the library in $prefix/lib rather than $prefix/lib64 on x86_64. It has no effect on x86.

The shared libraries need move to /lib, and as a result the .so file in /usr/lib will need to be recreated:

```
mv -v /usr/lib/libcap.so.* /lib
ln -sf ../../lib=$(readlink /usr/lib/libcap.so) /usr/lib/libcap.so
```

# 26.27.2. Contents of Libcap

+   **Installed programs:** capsh, getcap, getpcaps, and setcap
**Installed library:** libcap.so

# Short Descriptions

+   - capsh A shell wrapper to explore and constrain capability support
- getcap examines file capabilities
- getpcaps Displays the capabilities on the queried process(es)
- setcap Sets file capabilities
- libcap Contains the library functions for manipulating POSIX 1003.1e capabilities