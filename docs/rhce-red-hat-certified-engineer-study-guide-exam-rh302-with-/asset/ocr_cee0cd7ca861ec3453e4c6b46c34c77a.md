# Summary

In this chapter, you learned about shared libraries. The most important topics covered are:

**Program Forms** Programmers write source code, which a compiler translates into object code. Object code can be stored in a library for reuse.

**Program Linking** A linker combines object code modules to create an executable program. A statically linked program does not refer to external libraries. A dynamically linked program refers to external libraries, which must be present when the program is run.

**Linux Executables** Most Linux executables are organized using the structure ELF (executable and linking format). Older executables use the obsolete a.out structure.

**Shared Libraries** The most important shared libraries are:

+   - /lib The main shared libraries

+   - /usr/lib Supplementary shared libraries

+   - /usr/i486-linux-libc5/lib Shared libraries for use with the old version of the C standard library, glibc5

+   - /usr/X11R6/lib6 Shared libraries related to FreeX86

+   - /usr/i486-linuxout/lib The a.out shared libraries

**The ldd Command** The ldd command lets you determine which shared libraries a program references.

**The Library Path** The environment variable LD_LIBRARY_PATH specifies the library search path.

**The Shared Library Configuration** The file /etc/ld.conf contains the shared library configuration, which consists of a list of installed libraries. You may need to revise the file if you install a non-RPM package or unpacked software.

**Querying RPM Package Files** You can query RPM packages files to determine which file, if any, contains a particular shared library.