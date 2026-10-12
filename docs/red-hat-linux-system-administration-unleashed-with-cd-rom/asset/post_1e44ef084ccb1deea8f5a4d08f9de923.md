
## Enabling Module Support

Now that you have heard some of the advantages of using a modular kernel, let's take a look at what you need to take advantage of them. The first thing, of course, is to have a kernel configured. This involves selecting one or more of the following three kernel configuration options:

- CONFIG_MODULES
- CONFIG_MODVERSIONS
- CONFIG_KMOD

The first of these options is mandatory. If you do not set the CONFIG_MODULES variable to Y for yes, you will not be able to utilize modules.

The next option, CONFIG_MODVERSIONS, if defined, means that you may be able to use the same modules with different kernel versions. Depending on whether you want this flexibility, you may answer Y or N to this question. The safe bet for this configuration option is to say N, meaning that the modules you build will only work with the kernel with which they were compiled. One reason you might want to answer Y to this option is if you are using modules built by someone else, such as a hardware vendor who supplies a modular driver in binary form.

The final configuration option in this set is CONFIG_KMOD, which if set to Y means that the kernel will be able to load and unload modules automatically as needed. Whether or not you select this, modules will work. But if you do not say Y to this option, you lose one of the advantages of using modules, namely having the kernel load and unload modules as needed. You will almost always want to say Y here. Figure 35.1 shows these options set to support loadable kernel modules from the make xconfig dialog.

FIGURE 35.1
Enabling kernel module support.

![](img/4886c42c7629f445c7f7f3011ffbf3c3_1129_0.png)

## The Module Utilities

Having enabled module support and having selected drivers and features to be built as modules, the next requirement is to configure the module utilities. These utilities are contained in the RPM package called modutils-2.1.121-14.1386.rpm and are a standard part of every installation. The module utilities and their functions are detailed later in this chapter. The Red Hat 6.0 distribution comes with the correct module utilities for the default kernel, but if you change kernels, you should always check the Changes file in the kernel Documentation directory to find out which version of module utilities is required to support the kernel you are building. Listing 35.3 is an excerpt from this file that shows this information.

## LISTING 35.3 Changes File Excerpt

```
Excerpt from /usr/src/linux/Documentation/Changes

Current Minimal Requirements
Upgrade to at least these software revisions before thinking you've encountered a bug!
If you're unsure what version you're currently running, the suggested command should tell you.
- Kernel modutils      2.1.121          ; insmod -V
- Gnu C                2.7.2.3          ; gcc --version
- Binutils             2.8.1.0.23       ; ld -v
- Linux libc5 C Library 5.4.46          ; ls -l /lib/libc*
- Linux libc6 C Library 2.0.7pre6       ; ls -l /lib/libc*
- Dynamic Linker (ld.so) 1.9.9          ; ldd --version or ldd -v
- Linux C++ Library    2.7.2.8          ; ls -l /usr/lib/libg++.so.*
- Procps               1.2.9            ; ps --version
- Procinfo             16               ; procinfo -v
- Psmisc               17               ; pstree -V
- Net-tools            1.50             ; hostname -V
- Loadlin              1.6a
- Sh-utils             1.16             ; basename --v
- AutoFs               3.1.1            ; automount --version
- NFS                  2.2beta40        ; showmount --version
- Bash                 1.14.7           ; bash --version
- Ncpfs                2.2.0            ; ncpnmount -v
- Pcmcia-cs            3.0.7            ; cardmgr -V
```

## LISTING 35.3 continued

- PPP 2.3.5 ; pppd --version
- Util-linux 2.91 ; chsh -v

If you need to obtain a new version of the module utilities, they are distributed in the kernel source directories of the kernel FTP sites. For example, the module utilities noted in the Changes file, version 2.1.121, are found at the following URL:

```
ftp://ftp.us.kernel.org/pub/linux/kernel/v2.1/modutils-2.1.121.tar.gz
```

The version number of the module utilities matches the version number of the kernel that was current at the time of their release. This does not mean that you must upgrade immediately to this version. Always check the Changes file to determine the version required to support the kernel you are building.

The module utilities consist of several programs. Table 35.1 lists those utilities and describes their function. For usage information about these utilities, refer to the manual pages.

## TABLE 35.1 Module Utilities and Descriptions

| Utility | Description |
|---|---|
| lsmod | Lists the modules currently loaded by the kernel and whether they are in use. |
| insmod | Loads a module into the running kernel. |
| rmmod | Removes a module from the running kernel. |
| modprobe | Loads module(s) and can be used to handle dependencies through its configuration file. |
| depmod | Generates the dependency information required by the modprobe utility. |
| kerneld | The kernel daemon, used to automatically load and unload modules as required. |
| gensyms | Generates version information for module symbols. It is run during the kernel make process if the config variable CONFIG_MODVERSIONS is set. |
| ksyms | Shows module symbols. |
| modinfo | Displays information about a module. |

## When Not to Use Modules

There are parts of your kernel that should usually not be built as modules. These parts include the filesystem driver used by your root partition, normal hard drive support, network support, and TCP/IP support. In addition, if you do not want to rely on the initial RAM disk feature of the kernel, you should not compile the driver for your boot disk SCSI controller if you boot from a SCSI drive. All of these items are required to boot the kernel.

You can opt to build some of these items as modules provided that you include support for an initial RAM disk in your kernel. The initial RAM disk is loaded by the boot loader and loads modules required to continue booting the system. The Red Hat distributed kernel includes this support and uses the initial RAM disk to load SCSI drivers required to boot the system. The initial RAM disk alters the manner in which the kernel is booted, causing system startup to occur in two phases. The initial phase brings up the kernel with a minimal set of compiled in drivers, loads the initial RAM disk as the root filesystem, and then executes commands to load additional modules required to complete the boot process.

## Booting the System Utilizing Initial RAM Disk Support

These are the steps in booting the system when utilizing the initial RAM disk support:

1. The boot loader loads the kernel and creates the initial RAM disk.
2. The initial RAM disk is converted to a normal RAM disk and the memory used by the initial RAM disk is freed.
3. This new RAM disk is mounted read/write as the root filesystem.
4. An executable program or script called /linuxrc is executed. This script normally is used to load modules required to complete booting the system.
5. Upon termination of the /linuxrc script or program, the root filesystem is mounted. The root filesystem in this case is the one built in to the kernel.
6. If a directory called /initrd exists on the root filesystem, the initial RAM disk is moved to it, otherwise it is unmounted.
7. The normal boot sequence then commences with the invocation of the init process, using the new root filesystem.

With this basic knowledge of what modules are, when to use them, and why they are useful, we are ready now to proceed with configuring the Linux kernel.
