# 200 CONFIGURATION AND ADMINISTRATION

compilation is carried out fully automatically. Compiling also does not constitute a safety risk – and if you stick to the following instructions you will afterwards be able to start up your computer with both the old and the new kernel.

Preconditions for compiling the kernel are the installation of the kernel and the installation of an appropriate compiler (see below) together with the appropriate tools (such as make, various libraries). Caution, the kernel code is fairly large! With the resulting binary files, it takes up more than 40 Mbytes.

# Compiler questions

Today's Linux world knows two popular C compilers, gcc (the 'classic' GNU compiler) and egcs (experimental step in the development of GCC). egcs is required in particular because of the new libc6 (alias glibc2) (see also page 120).

+   Further information on egcs can be found in the egcs-FAQ:
http://egcs.cygnus.com/faq.html

For the translation of kernel 2.0 you absolutely need gcc, preferably in its version 2.7. For the new kernel 2.2 it is again recommended that gcc is used, however, egcs appears to work as well. As the majority of kernel developers use gcc, you would be well advised to do the same.

How do you determine which compiler is used on your system? The easiest way is to find out from which package gcc originates:

```
root# which gcc
/usr/bin/gcc
root rpm -q /usr/bin/gcc
egcs-981208-1
```

In this case we see that egcs is installed. In many distributions, simultaneous installation of kernel and egcs leads to problems – therefore, you should install egcs first, and then gcc (probably together with gccfront).

# Kernel version numbers

There are 'stable' kernel versions (1.0.n, 1.2.n, 2.0.n, 2.2.n) and so-called developer or hacker kernels (1.1.n, 1.3.n, 2.1.n, 2.3.n, and so on). For the vast majority of Linux users makes no sense to keep chasing after the latest version of the developer kernel. Developer kernels are only intended for Linux users who want to participate in the development, test the latest code and correct it. Here, problems might be expected. Once you have installed an optimized kernel for your computer and it runs without problems, there is no reason for an update.

This section is based on kernel 2.2.n. At the time of writing these lines, the most-to-date version available was 2.2.pre7c, nearly but not entirely ready. Big changes between the version described here and version 2.2.0 are, in any case, not to be expected. (pre7 means that we are dealing with the seventh pre-release of the anxiously awaited kernel 2.2.0. ac4 means that, in addition, the fourth patch version to 2.2.pre7 by Alan Cox was taken into account. Some patches