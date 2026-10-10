Listing 8-4 shows the build output after a typical editing session on the module (all other modules have already been built in this kernel source tree.)

# Listing 8-4
Module Build Output

```
$ make ARCH=arm CROSS_COMPILE=scale_be- modules
CHK		include/linux/version.h
make[1]: 'arch/arm/kernel/asm-offsets.s' is up to date.
make[1]: 'include/asm-arm/mach-types.h' is up to date.
CC [M]  drivers/char/examples/hello1.o
Building modules, stage 2.
MODPOST
LD [M]  drivers/char/examples/hello1.ko
```

# 8.1.5 Installing Your Device Driver

Now that this driver is built, we can load and unload it on a running kernel to observe its behavior. Before we can load the module, we need to copy it to an appropriate location on our target system. Although we could put it anywhere we want, a convention is in place for kernel modules and where they are populated on a running Linux system. As with module compilation, it is easiest to let the kernel build system do that for us. The Makefile target modules_install automatically places modules in the system in a logical layout. You simply need to supply the desired location as a prefix to the default path.

In a standard Linux workstation installation, you might already know that the device driver modules live in /lib/modules/`<kernel-version>`/.... ordered in a manner similar to the device driver directory hierarchy in the Linux kernel tree.2 The `<kernel-version>` string is produced by executing the command uname -r on your target Linux system, by default. If you do not provide an installation prefix to the kernel build system, your modules are installed in your own workstation's /lib/modules/.... directory. This is probably not what you had intended. You can point to a temporary location in your home directory and manually copy the modules to your target's file system. Alternatively, if your target embedded system uses NFS root mount to a directory on your local development

> 2 This path is used by Red Hat and Fedora distributions, and is also required by the File System Hierarchy Standard referenced at the end of this chapter. Other distributions might use different locations in the file system for kernel modules.