
## Library Principles

  The idea behind a library is to simplify programmers’ lives by providing commonly used program fragments. For instance, one of the most important libraries is the *C library* (libc), which provides many of the higher-level features associated with the C programming language. Another common type of library is associated with *GUIs*. These libraries are often called *widget sets* because they provide the on-screen *widgets* used by programs—buttons, scroll bars, menu bars, and so on. The GNOME Tool Kit (GTK+) and Qt are the most popular Linux widget sets, and both ship largely as libraries. Libraries are chosen by programmers, not by users; you usually can’t easily substitute one library for another. (The main exceptions are minor version upgrades.)

  Linux uses the **GNU C library (glibc)** version of the C library. Package-manager dependencies and other library references are to glibc specifically. As of glibc 2.3.4, for historical reasons the main glibc file is usually called /lib/libc.so.6, but this file is sometimes a symbolic link to a file of another name, such as /lib/libc-2.3.4.so.

  In principle, the routines in a library can be linked into a program’s main file, just like all the object code files created by the compiler. This approach, however, has certain problems:

- The resulting program file is huge. This means it takes up a lot of disk space, and it consumes a lot of RAM when loaded.
- If multiple programs use the library, as is common, the program-size issue is multiplied several times.
- The program can’t take advantage of improvements in the library without recompiling (or at least relinking) the program.

  For these reasons, most programs use their libraries as shared libraries (a.k.a. *dynamic libraries*). In this form, the main program executable omits most of the library routines. Instead, the executable includes references to shared library files, which can then be loaded along with the main program file. This approach helps keep program file size down, enables sharing of the memory consumed by libraries across programs, and enables programs to take advantage of improvements in libraries by upgrading the library.

  Linux shared libraries are similar to the dynamic link libraries (DLLs) of Windows. Windows DLLs are usually identified by .DLL filename extensions; but in Linux, shared libraries usually have .so or .so.version extension, where version is a version number. (.so stands for *shared object*.) Linux *static libraries* (used by linkers for inclusion in programs when dynamic libraries aren’t to be used) have .a filename extensions.

  On the downside, shared libraries can degrade program load time slightly if the library isn’t already in use by another program, and they can create software management complications:

- Shared library changes can be incompatible with some or all programs that use the library. Linux uses library numbering schemes to enable you to keep multiple versions of a library installed at once. Upgrades that *shouldn’t* cause problems can overwrite older versions, whereas major upgrades get installed side-by-side with their older counterparts. This approach minimizes the chance of problems, but sometimes changes that *shouldn’t* cause problems *do* cause them.
- Programs must be able to locate shared libraries. This task requires adjusting configuration files and environment variables. If it’s done wrong, or if a program overrides the defaults and looks in the wrong place, the result is usually that the program won’t run at all.
- The number of libraries for Linux has risen dramatically over time. When they’re used in shared form, the result can be a tangled mess of package dependencies, particularly if you use programs that rely on many or obscure libraries. In most cases, this issue boils down to a package problem that can be handled by your package management tools.
- If an important shared library becomes inaccessible because it was accidentally overwritten, due to a disk error or for any other reason, the result can be severe system problems. In a worst-case scenario, the system might not even boot.

  In most cases, these drawbacks are manageable and are much less important than the problems associated with using static libraries. Thus, dynamic libraries are very popular.

![](img/f339a9f48c4b443e61c74acb4c9c3da4_139_0.png)

  Static libraries are sometimes used by developers who create programs using particularly odd, outdated, or otherwise exotic libraries. This enables them to distribute their binary packages without requiring users to obtain and install their oddball libraries. Likewise, static libraries are sometimes used on small emergency systems, which don’t have enough programs installed to make the advantages of shared libraries worth pursuing.

### Locating Library Files

  The major administrative challenge of handling shared libraries involves enabling programs to locate those shared libraries. Binary program files can point to libraries either by name alone (as in `libc.so.6`) or by providing a complete path (as in `/lib/libc.so.6`). In the first case, you must configure a *library path*—a set of directories in which programs should search for libraries. This can be done both through a global configuration file and through an environment variable. If a static path to a library is wrong, you must find a way to correct the problem. In all of these cases, after making a change, you may need to use a special command to get the system to recognize the change, as described later in “Library Management Commands.”

### Setting the Path Systemwide

  The first way to set the library path is to edit the /etc/ld.so.conf file. This file consists of a series of lines, each of which lists one directory in which shared library files may be found. Typically, this file lists between half a dozen and a couple dozen directories. Some distributions have an additional type of line in this file. These lines begin with the `#include` directive; they list files that are to be included as if they were part of the main file. For instance, Ubuntu 8.04's `ld.so.conf` begins with this line:

```
include /etc/ld.so.conf.d/*.conf
```

  This line tells the system to load all the files in /etc/ld.so.conf.d whose names end in .conf as if they were part of the main /etc/ld.so.conf file. This mechanism enables package maintainers to add their unique library directories to the search list by placing a .conf file in the appropriate directory.

  Some distributions, such as Gentoo, use a mechanism with a similar goal but different details. With these distributions, the `env-update` utility reads files in /etc/env.d to create the final form of several /etc configuration files, including /etc/ld.so.conf. In particular, the LDPATH variables in these files are read, and their values make up the lines in `ld.so.conf.` Thus, to change `ld.so.conf` in Gentoo or other distributions that use this mechanism, you should add or edit files in /etc/env.d and then type `env-update` to do the job.

  Generally speaking, there's seldom a need to change the library path system-wide. Library package files usually install themselves in directories that are already on the path or add their paths automatically. The main reason to make such changes would be if you installed a library package, or a program that creates its own libraries, in an unusual location via a mechanism other than your distribution's main package utility. For instance, you might compile a library from source code and then need to update your library path in this way.

  After you change your library path, you must use `ldconfig` to have your programs use the new path, as described later in “Library Management Commands.”

![](img/f339a9f48c4b443e61c74acb4c9c3da4_140_0.png)

> In addition to the directories specified in `/etc/ld.so.conf`, Linux refers to the trusted library directories, /lib and /usr/lib. These directories are always on the library path, even if they aren't listed in `ld.so.conf`.

### Temporarily Changing the Path

  Sometimes, changing the path permanently and globally is unnecessary and even inappropriate. For instance, you might want to test the effect of a new library before using it for all your programs. To do so, you could install the shared libraries in an unusual location and then set the LD_LIBRARY_PATH environment variable. This environment variable specifies additional directories the system is to search for libraries.

![](img/f339a9f48c4b443e61c74acb4c9c3da4_140_1.png)

> Chapter 9, “Writing Scripts, Configuring E-Mail, and Using Databases,” describes environment variables in more detail.
