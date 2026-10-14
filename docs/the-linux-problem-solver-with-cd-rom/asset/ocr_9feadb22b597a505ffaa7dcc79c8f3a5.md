# What You Need to Build the Kernel

To build a Linux kernel, you'll need:

+   - A C compiler (gcc) and make (found in the development packages of most distributions).

+   - Two assembler and linker programs called as86 and ld86 (from bin86-0.4-7.rpm in Red Hat 6.0, dev86-version.rpm in later releases).

> NOTE See /usr/src/linux/README for the version of gcc you need (found under 'COMPILING the kernel' heading as recently as 2.2). (Use gcc -v to find your version number.) If your Linux distribution is at all recent, you won't have a hopelessly outdated version of gcc.

+   - Space—the source code is large. At version 2.2.12, a compiled kernel with a lot of modules took up 75MB. Unfortunately it's hard to say how much space future versions will take.

+   - A relatively fast computer with a decent amount of memory, if you plan to finish in any reasonable amount of time. It took me over an hour to compile a 2.2 kernel on a 486 with 20MB of memory, but my newer machines were much faster. (If you want the kernel on a slow machine but don't want the wait, you can compile it on a faster machine and then copy it to the slower one.)

# Setting Up Kernel Source Code

Before you can set up the kernel, you need to unpack the source. Unpacking the source is as easy as with the packages described in Chapter 6. You use either

```
# cd /usr/src
# umask 022
# bzip2cat linux-version.tar.bz2 | tar xvf -
```

or

```
# cd /usr/src
# umask 022
# zcat linux-version.tar.gz | tar xvf -
```

Your choice of unpacking command depends on the type of compression in your source file (see the underlined text above; an extension of .bz2 means you need the bzip2cat program, whereas .gz means you should use zcat).