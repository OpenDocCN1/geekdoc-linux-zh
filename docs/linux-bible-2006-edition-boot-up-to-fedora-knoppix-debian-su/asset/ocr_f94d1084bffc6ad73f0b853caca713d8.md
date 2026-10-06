# 796 Part VI ♦ Programming in Linux

names to the members in which the symbols are defined. The speed up compilation and linking. Static libraries are typically named with the extension .a, which stands for archive.

+   * Shared libraries—Like static libraries, shared libraries are files that contain other object files or pointers to other object files. They are called shared libraries because the code they contain is not linked into programs when they are compiled. Rather, the dynamic linker/loader loads shared library code into runtime.

Shared libraries have several advantages over static libraries. First, they require fewer resources. They use less disk space because shared library code is not compiled into each binary but loaded from a single location dynamically. They use less system memory because the kernel shares the memory among all the programs that use the library.

Second, shared libraries are slightly faster because they need to be loaded into memory only. Finally, shared libraries simplify code and system maintenance. As bugs fix or features added, users need only the updated library and install it. With static libraries, each program that the library must be recompiled.

The dynamic linker/loader, ld.so, links symbols name to the appropriate shared library in which they are defined at runtime. Shared libraries have a special name, the soname, that consists of the library name and the major version number. The full name of the C library on one of my systems, for example, is libc-2.3.4.so. The library name is libc:so; the major version is 2; the minor version is 3; and the release patch level is 4. For historical reasons, the C library's soname is libc.so6. Minor version numbers and patch levels change as bugs are fixed, the soname remains the same and newer versions are compatible with older versions.

I emphasize the soname because applications link against it. How does linking work? The ldconfig utility creates a symbolic link from the actual library, say libc-2.3.2.so, to the soname, libc.so.6, and stores this information in /etc/ld.so.cache. At runtime, ld.so scans the cache file, finds the required soname and, because of the symbolic link, loads the actual library into memory and maps function calls to the appropriate symbols in the loaded library.

# The nm Command

The nm command lists all of the symbols encoded in an object or binary file. It is used to see what function calls a program makes or to see if a library or object file provides a needed function. nm has the following syntax:

```
nm [options] file
```