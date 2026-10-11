
correct kernel version directory /usr/src/<kernel-version>. Next, change to this directory and execute one of many make commands.

If the source code has been compiled previously, you can optionally use the `make mproper` command to remove any files created by previous kernel compilations; this speeds up compiling the new kernel. In addition, if you are compiling the same kernel version that is used, you can use the `make oldconfig` command to record the current kernel features and settings that can then be used as a starting point for further configuration.

Next, you must choose the certain features required for the kernel; this can be done using one of four commands:

- `make config` — Provides a text-based interface that prompts the user for information regarding kernel configuration in a question-by-question format, as shown in the following output:

```
root@server1 linux]# make config
HOSTCC  scripts/basic/fixdep
HOSTCC  scripts/basic/split-include
HOSTCC  scripts/basic/docproc
SHIPPED scripts/kconfig/zconf.tab.h
SHIPPED scripts/kconfig/zconf.tab.c
SHIPPED scripts/kconfig/lex.zconf.c
HOSTCC  -fPIC scripts/kconfig/zconf.tab.o
HOSTLDD -shared scripts/kconfig/libkconfig.so
HOSTCC  scripts/kconfig/conf.o
HOSTCC  scripts/kconfig/mconf.o
HOSTLD  scripts/kconfig/conf
scripts/kconfig/conf arch/i386/Kconfig
#
# using defaults found in /boot/config-2.6.5-1.358
#
*
* Linux Kernel Configuration
*
*
* Code maturity level options
*
*
Prompt for development and/or incomplete code/drivers
(EXPERIMENTAL) [Y/n/?]
```

- `make menuconfig` — Provides a text-based menu that allows easy navigation of kernel features for configuration, as shown in Figure 13-8.

- `make xconfig` or `make gconfig` — Allows the easiest navigation of kernel features via a graphical interface, as shown with `make gconfig` in Figure 13-9. `make xconfig` must be run in a KDE (Qt-based) GUI environment, and `make gconfig` must be run in a GNOME (GTK-based) GUI environment.

## Customizing the Kernel

![](img/09bf13b782f71165e17bb3839040c96a_534_0.png)

**FIGURE 13-8** The *make menuconfig* interface

![](img/09bf13b782f71165e17bb3839040c96a_534_1.png)

**FIGURE 13-9** The *make gconfig* interface

If you expand Power management options (ACPI, APM) in Figure 13-9, you can configure your kernel with ACPI support, as shown in Figure 13-10.

Note from Figure 13-10 that the Software Suspend feature is Experimental; if you are building a production server, it is good practice to avoid setting any experimental options. In addition, a Y in the Y column beside the option indicates that the support will be compiled into the kernel, whereas an M in the M column indicates that the support will be compiled into a module that can be inserted into the Linux kernel. An N in the N column disables support for a certain kernel feature.

### Chapter 13: TROUBLESHOOTING AND PERFORMANCE

![](img/09bf13b782f71165e17bb3839040c96a_535_0.png)

**FIGURE 13-10** Configuring power options in the Linux kernel

> **NOTE**
>
> All three choices (Y, M, N) might not be available for some features.
>
> You should disable support for unused kernel features to reduce the size of the Linux kernel and increase its speed. For the same reason, you should compile rarely used features as modules.

After you have configured the options you desire for your kernel, you can choose the Save button shown in Figure 13-10, exit the program, and return to the command prompt.

After the kernel features have been selected, you should run the `make clean` command to remove any files that are not required for compiling the kernel; this speeds up the time it takes to compile the kernel.

Next, you can compile the kernel by typing `make bzipImage` (or just `make`). After this has completed, you have a bzip2-compressed kernel called `/usr/src/linux/arch/i386/boot/bzImage`, which can then be copied to the /boot directory and renamed `vmlinuz-<kernel version>`. Following this, you should also copy the `/usr/src/linux/System.map` file to the /boot directory.

Afterward, to compile the necessary modules and copy them to the appropriate location under /lib/modules, you can type `make modules_install` at a command prompt.

![](img/09bf13b782f71165e17bb3839040c96a_536_0.png)

Because many kernel features and device support are required by the Linux kernel while it is being loaded at boot time, you should create a kernel ramdisk image. To do this, simply use the command `mkinitrd -v /boot/initrd-<Kernel version>.img <kernel version>`.

Finally, you can configure the boot loader to boot the new kernel by adding the appropriate lines for the kernel and ramdisk image to `/etc/lilo.conf` (if LILO is your boot loader) or `/boot/grub/grub.conf` (if GRUB is your boot loader), as described in Chapter 9.

### Patching the Linux Kernel

To install a more current Linux kernel version, you normally download the source code for that kernel and place it in a directory that will be referenced by `/usr/src/linux`. If the `/usr/src/linux` directory already contains the source code for the current kernel, you can instead choose to download and apply patches to this source code to change it into the desired version. Patches are not cumulative; to patch the Linux kernel version 2.6.7 to 2.6.9, you must apply the Linux kernel patches 2.6.8 and 2.6.9.

Patches are typically distributed in compressed form; to apply a patch, simply download and uncompress the patch file into the `/usr/src/linux` directory and execute the `patch` command. To execute a kernel patch, you can type `patch < patchfile`. When all patches have been applied, you can compile the kernel, as described in the previous section.

### Chapter Summary

- After installation, Linux administrators monitor the system, perform proactive and reactive maintenance, and document important system information.
- Common troubleshooting procedures involve collecting data to isolate and determine the cause of system problems, as well as implementing and testing solutions that can be documented for future use.
- System problems can be categorized as hardware- or software-related.
- IRQ conflicts, invalid hardware settings, absence of kernel support, and hard disk failure are common hardware-related problems on Linux systems.
- Software-related problems can be further categorized as application-related or operating system-related.
- Absence of program dependencies or shared libraries, program limits, and resource conflicts are common application-related problems, whereas boot failure, filesystem corruption, and the misconfiguration of serial devices are common operating system-related problems.
- System performance is affected by a variety of hardware and software factors, including the amount of RAM, CPU speed, kernel size, and process load.
- Using performance monitoring utilities to create a baseline is helpful when diagnosing performance problems in the future. The sysstat package contains many useful performance monitoring commands.
- System features and hardware support can be compiled into the Linux kernel or provided by a kernel module.
- You can compile a Linux kernel with only the necessary features and support to increase system performance.

### Key Terms

- **/etc/ld.so.cache file** — The file that contains the location of shared library files.
- **/etc/ld.so.conf file** — The file that contains a list of directories that contain shared libraries.
- **/etc/modprobe.conf file** — The file used to load and alias modules at system initialization.
- **/usr/src/linux directory** — The directory that typically contains source code for the Linux kernel during compilation.
- **/var/log directory** — The directory that contains most system log files.
- **baseline** — A measure of normal system activity.
- **BBC Linux** — A CD-based Linux distribution.
- **bus mastering** — The process by which peripheral components perform tasks normally executed by the CPU.
- **compressor/decompressor (codec)** — A file that contains the rules to compress or decompress multimedia information.
- **documentation** — The system information that is stored in a log book for future reference.
- **filehandles** — The connections that a program makes to files on a filesystem.
- **free command** — A command used to display memory and swap statistics.
- **Input/Output Statistics (iostat) command** — A command that displays Input/Output statistics for block devices.
