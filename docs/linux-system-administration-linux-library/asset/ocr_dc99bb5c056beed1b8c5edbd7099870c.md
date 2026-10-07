# Chapter 8 Software Administration

Removing unnecessary drivers The default kernel includes drivers for a wide variety of hardware components. In most cases, these drivers do no harm because they're compiled as *modules* (separate driver files), which aren't loaded unless necessary. A few are compiled into the kernel proper, however. These consume unnecessarily, thus degrading system performance slightly.

Adding drivers You may need to add a new or experimental driver to your system. This may be necessary if you're using an unusually new component, or if there's a bug fix that's not yet integrated into the main kernel tree. Such changes require you to *patch* the kernel—to replace one or more kernel source code files. For details on how to do this, check with the site that provides the new driver.

Changing options You may want to change options related to drivers, in order to optimize performance or improve reliability. As you examine the kernel configuration, you'll see many examples of such options.

Upgrading the kernel You may want to run the latest version of the kernel. Sometimes you can obtain an upgrade in precompiled form, but occasionally you'll have to compile a kernel from source code, particularly if it's a very recent or experimental release.

Of course, kernel compilation isn't without its drawbacks. It takes time to configure and compile a kernel. It's also possible that the kernel you won't work. Be sure to leave yourself a way to boot using the old kernel, or you'll have a hard time booting your system after an upgrade. (The discussion in this chapter describes how to boot the computer into either the old or the new kernel, so you shouldn't have a problem if you follow these instructions).

On the whole, compiling your own kernel is something that every Linux administrator should be able to do, even if it's not something you do on every system you maintain. Using a custom-compiled kernel helps you optimize your system and use cutting-edge drivers, which can give your system an advantage. In some cases, this is the only way you can get certain features to work (as drivers for particularly new hardware).

# Obtaining a Kernel

Before you compile a kernel, you must obtain one. For other software packages, you obtain a kernel either precompiled or in source code form; in RPM, Debian package, or tarball form. We favor installing a kernel from source tarball form, because it allows you to be sure you're working from an original standard base. Kernel RPMs, are often modified in various ways. Although these modifications sometimes be useful, they can also interfere with the smooth installation of patches they should be needed. (On the other hand, the kernels distributed as RPMs sometimes *include* the very patches you might want to install, thus simplifying matters).