# 5.6. Linux-5.2.8 API Headers

The Linux API Headers (in linux-5.2.8.tar.xz) expose the kernel's API for use by Glibc.

Approximate build time: 0.1 SBU
Required disk space: 960 MB

# 5.6.1. Installation of Linux API Headers

The Linux kernel needs to expose an Application Programming Interface (API) for the system's C library (Glibc in LFS) to use. This is done by way of sanitizing various C header files that are shipped in the Linux kernel source tarball.

Make sure there are no stale files embedded in the package:

```
make mrproper
```

Now extract the user-visible kernel headers from the source. They are placed in an intermediate local directory and copied to the needed location HDRPATH=dest the extraction process removes any existing files in the target directory.

```
make INSTALL_HDR_PATH=dest headers_install
cp -rv dest/include/* /tools/include
```

Details on this package are located in Section 6.7.2, “Contents of Linux API Headers."