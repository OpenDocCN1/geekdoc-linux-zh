duration. Processes are assigned priorities that can slow or speed the completion of those processes' requests.

**Understand file systems and permissions** — Because the kernel is responsible for letting processes read, write, and execute files that are stored in different types of file systems, the kernel must know about how those file systems are structured. It must also know the permissions each user has to access those files.

There are many other things that a kernel does. However, these three are some of the most obvious functions of the kernel to someone using a Linux system.

One of the best ways to learn about the kernel is to read files that are included with the kernel source code. The location of the kernel source code has changed between Fedora Core 2 and Fedora Core 3, and you have to unzip it and build it yourself. As root user from a terminal window, do the following:

+   1. Install the kernel source package from the DVD that comes with this book (its name should be something like kernel-2.6.8-1.541.src.rpm from the SRPMS directory).

```
# rpm -Uhv kernel-2.6.8-1.541.src.rpm
```

+   2. Type the following:

```
# rpmbuild -bp --target noarch /usr/src/redhat/SPECS/kernel-2.6.spec
```

Now, the kernel source code that you used to be able to find in `/usr/src/linux` is now available in the `/usr/src/redhat/BUILD/kernel-*` directory. Look in that directory for `Documentation` directory. It contains descriptions of many of the drivers and other components in the 2.6 kernel. You can use the code from this package to rebuild the Linux kernel as well.

# Checking your current kernel

If you want to know what kernel your Linux system is currently running, you can type the `uname -a` command as follows:

```
# uname -a
Linux jukedbox.linuxtoybox.net 2.6.8-1.541 #1 Thu Nov 25 12:32:44 EDT 2004
i686 i686 i386 GNU/Linux
```

This example shows the current kernel as 2.6.8-1.541. Because you can have multiple kernels available on your hard disk, each of which may require drivers and modules that are specific to that kernel, the kernel version number is used to store the compatible components. For example, you can look for directories named for your kernel version in:

+   • `/lib/modules` — Modules that can be loaded as needed to support hardware connected to your computer are stored under the `/lib/modules` directory. One way that modules for the 2.6 kernel are different from the 2.4 kernel counterparts is that they end with a `.ko` extension (as opposed to a `.o` for 2.4 kernel modules). You can use the basename of the