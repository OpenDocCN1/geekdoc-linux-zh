Library version numbers provide at least two, and sometimes three, levels of versioning. For example, one instance of the libc shared library has version number 5.4.38. The major version of the software is the one that counts the most with regard to software compatibility. If you look in the `/lib/gnulibc1` and `/lib` directories, you should see that `libc.so.5` is a symbolic link (a reference) to `libc.so.5.4.46`, and that `libc.so.6` is a symbolic link to `libc-2.1.1.so`, which is the primary C shared library on your system. This is the single most important and widely used library in the system.

The shared library system is maintained with `ldconfig`. Whenever a new shared library is installed on the system, `ldconfig` is run and a new entry is made in the file `/etc/ld.so.cache`. Then a symbolic link is created with the name of the library and its major version number, which references the actual shared library file with the full version in its name. This all happens automatically when packages are installed using RPM because packages that install shared libraries generally have a post-install script that runs `ldconfig` for you. If you have installed shared libraries from TAR files, you might need to run this command yourself so that the libraries are registered with the system.

# Using ldd to Discover Required Shared Libraries

When a program is created, the linker records the versions of the shared libraries that it requires in the program file. You can examine which shared libraries an executable program needs by using `ldd`. For example, you can find out what shared library is used by `man` by typing `ldd /usr/bin/man`, which should result in something similar to the following output:

```
libc.so.6 => /lib/libc.so.6 (0x2aac6000)
/lib/ld-linux.so.2 => /lib/ld-linux.so.2 (0x2aaab000)
```

`man` is a fairly simple program. For a more interesting listing, try `ldd /usr/bin/emacs`.

If you determine that you have a shared library incompatibility problem, there are several ways to handle it.

If the library that is missing has a different major version number than the one your program needs, just find the package that provides the version of the library that you need and install it. If the major version numbers are different, the other software on your system will be unaffected by the addition of another library, even one of the same name.

Another solution is to create a symlink for the shared library name you need. Link it to an existing shared library on your system and hope that the library is compatible. This might work in some circumstances, depending on how extensively the library is used and what subroutines are referenced by the program. This is, however, a stopgap measure and should be used only when you know (that is, have it on good authority) that the library versions in question are compatible for the purposes of the target program.

The recommended solution is to actually install the correct version of the shared library that you need and use the environment variable `LD_LIBRARY_PATH` to alter the shared libraries that are used by your program.