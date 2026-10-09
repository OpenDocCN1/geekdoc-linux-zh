
Native POSIX Threads Library by Ulrich Drepper et al
`libpthread` 6.2.3-T58
Thread-local storage support included.
For bug reporting instructions, please see: <http://www.gnu.org/software/libc/bugs.html>.

## Major revision version symbolic links

Major revision versions do not follow the same numbering as the actual glibc version. The major revision version for the actual shared C library in glibc 2.3.6, `libc-2.3.6.so`, is 6, not 2 as the name suggests. In contrast, the major revision version for `libdl-2.3.6.so` truly is 2. The names of the symbolic links for the major revision version are formatted as `lib${LIBRARY_NAME}.so.${MAJOR_REVISION_VERSION}`, where `MAJOR_REVISION_VERSION` is the major revision version of the library. For the actual C library, for instance, the symbolic link is `libc.so.6`. For `libdl`, it is `libdl.so.2`. Once a program has been linked to a library, it will refer to this symbolic link. At startup, the loader will therefore look for this file before loading the program.

## Version-independent symbolic links to the major revision version symbolic links

The role of these links is to provide a universal entry for all the programs that need to link with a particular library, regardless of the actual major revision or the version of glibc involved. These symbolic links are typically formatted as `lib${LIBRARY_NAME}.so`. For example, `libm.so` points to `libm.so.6`, which itself points to the actual shared library, `libm-2.3.6.so`. The only exception to this is `libc.so`, which, as we said in Chapter 4, is a link script. The version-independent symbolic link is the one used when linking programs.

## Static library archives

These archives are used by applications that choose to link statically with a library. The names of these archives are formatted as `lib${LIBRARY_NAME}.a`. The static archive for `libdl`, for instance, is `libdl.a`.

You will also find some other types of files in `${TARGET_PREFIX}`/lib, such as `crt1.o` and `crti.o`, but you will not need to copy them to your target’s root filesystem. These files are used by the GNU linker ld when producing executable binaries that need to “bootstrap” themselves (load themselves into memory and initialize). Thus, their role is finished after linking, and they are not used at runtime.

Out of the four types of files just described, you need only two for each library: the actual shared libraries and the major revision version symbolic links. The other two file types are needed only when linking executables and are not required for the runtime operation of your applications.

In addition to the library files, you need to copy the dynamic linker and its symbolic link. The dynamic linker itself follows the naming convention of the various glibc libraries and is usually called `ld-GLIBC_VERSION.so`. In what is probably one of the most bizarre aspects of the GNU toolchain, however, the name of the symbolic link to the dynamic linker differs depending on the architecture for which the toolchain has been built. If the toolchain is built for the i386, the ARM, the SuperH, or the m68k, the symbolic link to the dynamic linker is usually called *ld-linux.so.MAJOR_REVISION_VERSION*. If the toolchain is built for the MIPS or the PowerPC, the symbolic link to the dynamic linker is usually called *ld.so.MAJOR_REVISION_VERSION*.

Before you actually copy any glibc component to the target’s root filesystem, however, you need to select the glibc components required for your applications. Table 6-2 provides the description of all the components in glibc and provides inclusion guidelines for each component. In addition to our guidelines, you will need to evaluate which components your programs need, depending on how they are linked.

## Table 6-2. Library components in glibc and root filesystem inclusion guidelines

| Library component | Content | Inclusion guidelines |
| :--- | :--- | :--- |
| *ld* | Dynamic linker. * | Compulsory. Needed to use any shared libraries. Theoretically not necessary if using only a statically built root filesystem—although this is quite rare, unless you are only using BusyBox, for example. |
| *libBrokenLocale* | Fixup routines to get applications that have broken locale features to run. Overrides application defaults through preloading. (Need to use LD_PRELOAD.) | Rarely used. |
| *libSegFault* | Routines for catching segmentation faults and doing backtraces. | Rarely used. |
| *libanl* | Asynchronous name lookup routines. | Rarely used. |
| *libbsd-compat* | Dummy library for certain BSD programs that are compiled with *-lbsd-compat*. | Rarely used. |
| *libc* | Main C library routines. | Compulsory. |
| *libcrypt* | Cryptography routines. | Required for most applications involved in authentication. |
| *libdl* | Routines for loading shared objects dynamically. | Required for applications that use functions such as dlopen(). |
| *libm* | Math routines. | Required for math functions. |
| *libmemusage* | Routines for heap and stack memory profiling. | Rarely used. |
| *libns1* | NIS network services library routines. | Rarely used. |
| *libnss_compat* | Name Switch Service (NSS) compatibility routines for NIS. | Loaded automatically by the glibc NSS. *b* |
| *libnss_dns* | NSS routines for DNS. | Loaded automatically by the glibc NSS. |
| *libnss_files* | NSS routines for file lookups. | Loaded automatically by the glibc NSS. |
| *libnss_hesiod* | NSS routines for Hesiod name service. | Loaded automatically by the glibc NSS. |
| *libnss_nis* | NSS routines for NIS. | Loaded automatically by the glibc NSS. |
| *libnss_nisplus* | NSS routines for NIS plus. | Loaded automatically by the glibc NSS. |
| *libprofile* | Program counter profiling routines. | Rarely used. |
| *libpthread* | POSIX 1003.1c threads routines for Linux. | Required for threads programming. |
| *libresolv* | Name resolver routines. | Required for name resolution. |
| *librt* | Asynchronous I/O routines. | Rarely used. |
| *libthread_db* | Thread debugging routines. | Loaded automatically by gdb when debugging threaded applications. Never actually linked to by any application. |
| *libutil* | Login routines, part of the user accounting database. *a* | Required for terminal connection management. |

*a* This library component is not itself a library. Instead, ld.so is an executable invoked by the ELF binary format loader to load the dynamically linked libraries into an application’s memory space.

*b* See Chapter 4 for details.

If you wish to find out which dynamic libraries a given application uses, the usual way is with the ldd command. In a cross-platform development environment, however, your host’s ldd command will fail when provided with target binaries. Instead, you can use the cross-platform readelf command you installed in Chapter 4 to identify the dynamic libraries that your application depends on. Here is an example using readelf to retrieve the BusyBox utility’s dependencies:

```bash
$ powerpc-linux-readelf -a ${PRJROOT}/rootfs/bin/busybox \
> grep "Shared library"
 0x00000001 (NEEDED)		Shared library: [libc.so.6]
```

Ideally, however, if you installed uClibc, you should use the ldd-like command installed by uClibc, which has cross-platform capabilities. For our control module target, which is based on a PowerPC board, the command’s name is powerpc-uclibc-ldd. This way, you can build the list of libraries your target binaries depend on. Here are the dependencies of the BusyBox utility, for example (one line has been wrapped to fit the page):

```bash
$ powerpc-uclibc-ldd ${PRJROOT}/rootfs/bin/busybox
  libc.so.0 => /home/karim/control-project/control-module/tools/uclibc/lib/
  libc.so.0
  /lib/ld-uClibc.so.0 => /lib/ld-uClibc.so.0
```

Having determined the library components you need, you can copy them and the relevant symbolic links to the /lib directory of the target’s root filesystem. Here is a set of commands that copy the essential glibc components:

```bash
$ cd ${TARGET_PREFIX}/lib
$ for file in lib libc crypt libdl libm \
> libpthread libresolv libutil
> do
> cp $file*.so ${PRJROOT}/rootfs/lib
> cp -d $file.so.['0'-9] ${PRJROOT}/rootfs/lib
```
