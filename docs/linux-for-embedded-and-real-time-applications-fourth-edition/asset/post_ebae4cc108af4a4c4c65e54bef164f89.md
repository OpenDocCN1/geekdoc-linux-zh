
The options that are not selected remain in the file but are “commented out.” The selected options get the appropriate value, “y” for features to be built into the kernel image, “m” for modules, a number or an element from a list. `.config` is included in the Makefile, where it controls what gets built and how. Early in the build process, `.config` is converted into a C header file, `include/linux/autoconf.h`, so that the configuration variables can be used to control conditional compilation.

```
#
# Automatically generated file; DO NOT EDIT.
# Linux/arm 3.8.13 Kernel Configuration
#
CONFIG_ARM=y
CONFIG_SYS_SUPPORTS_APM_EMULATION=y
CONFIG_GENERIC_GPIO=y
CONFIG_HAVE_PROC_CPU=y
CONFIG_STACKTRACE_SUPPORT=y
CONFIG_LOCKDEP_SUPPORT=y
CONFIG_TRACE_IRQFLAGS_SUPPORT=y
CONFIG_RWSEM_GENERIC_SPINLOCK=y
CONFIG_ARCH_HAS_CPUFREQ=y
CONFIG_GENERIC_HWEIGHT=y
CONFIG_GENERIC_CALIBRATE_DELAY=y
CONFIG_NEED_DMA_MAP_STATE=y
CONFIG_VECTORS_BASE=0xffff0000
CONFIG_ARM_PATCH_PHYS_VIRT=y
CONFIG_GENERIC_BUG=y
CONFIG_DEFCONFIG_LIST="lib/..modules/SUNAME_RELEASE/.config"
CONFIG_HAVE_IRQ_WORK=y
CONFIG_IRQ_WORK=y
CONFIG_BUILDTIME_EXTABLE_SORT=y
```

Listing 12.1
Excerpt of `.config`.

### A Problem

It turns out that the kernel we just patched and configured will not build. The file `arch/arm/kernel/return_address.c` does not compile, because a function it contains is also defined as an inline in `arch/arm/include/asm/ftrace.h`. Internet research revealed that the problem was that the kernel would not build under gcc version 6, and the solution was to drop back to gcc version 4.9.

So I built a gcc 4.9 tool chain, and had exactly the same problem. If you look at `ftrace.h` you can see the problem. There is a conditional based on a couple of configuration variables that ends up declaring the function `return_address()` as inline rather than a simple prototype. The real problem is that these configuration variables are controlled by `depends` and `selects`, and that makes it very difficult to change them using `make xconfig`.

My solution then was to edit *ftrace.h* to eliminate the conditional entirely by commenting it out, and just leave the function prototype. *Listing 12.2* highlights my edits. The lines that are changed are emboldened.

```
// #if defined(CONFIG_FRAME_POINTER) && !defined(CONFIG_ARM_UNWIND)

/*
 * return_address uses walk_stackframe to do it's work. If both
 * CONFIG_FRAME_POINTER= y and CONFIG_ARM_UNWIND= y walk_stackframe uses unwind
 * information. For this to work in the function tracer many functions would
 * have to be marked with ____notrace. So for now just depend on
 * !CONFIG_ARM_UNWIND.
 */

void *return_address(unsigned int);

// #else

// static inline void *return_address(unsigned int level)
// {
//      return NULL;
// }

// #endif
```

![](img/f03d6fa2c5faefc793771df52bbb2ef9_209_0.png)

I believe this is the first time I've had to edit a kernel source file in order to get the kernel to build. I do not take this lightly, and neither should you. Changing kernel code is not something you do on a whim, because there is a very real possibility your changes will create some other problem down the road. In this case it seems to work.

## Building the Kernel

The actual process of building the kernel varies a little depending on what you are building it for. Our primary objective is to build a kernel for the target board, so I'll describe that first. Then I'll describe the alternate process of building a new kernel for your workstation if you are so inclined.

The first two steps below can be executed as a normal user.

- `make clean`. Deletes all intermediate files created by a previous build. This ensures that *everything* gets built with the current configuration options. You will find that virtually all Linux makefiles have a *clean* target. Strictly speaking, if you are building for the first time, there are no intermediate files to clean up, so you do not have to run *make clean*.

- `make`. This is the heart of the matter. This builds the executable kernel image and all kernel modules. Not surprisingly, this takes a while. The resulting compressed kernel image is `arch/$(ARCH)/boot/zimage`.

The following step requires root user privileges.

- `make modules_install INSTALL_MOD_PATH=/export/rootfs`. Copies the modules to `$(INSTALL_MOD_PATH)/lib/modules/<kernel_version>` where `<kernel_version>` is the string identifying the specific kernel you are building. Note that when building for the target board, you must explicitly specify the root file system. Otherwise, the modules will go into `/lib/modules` of your workstation's file system. Strictly speaking, this step is not necessary in this case, because none of the modules are required to boot the kernel.

That is it. Note, incidentally, that the build process is recursive. Every subdirectory in the kernel source tree has its own Makefile dealing with the source files in that directory. The top level Makefile recursively invokes all of the sub Makefiles.

The process for building a kernel for your workstation differs in a couple of details. Do `make modules_install` without the INSTALL_MOD_PATH argument, and then execute this step, also as root:

- `make install`. This does several things. It copies the kernel executable, called `vmlinuz` for x86 builds, to `/boot` along with `System.map`, the linker map file. It adds a new entry to `/boot/grub/grub.conf`, so the GRand Unified Bootloader can offer the new kernel as a boot option. Finally, it creates an initial ramdisk, `initrd`, in `/boot`.

## Workstation Digression

Before we move on to loading and testing our new kernel, the last two items mentioned above deserve a passing explanation. Most workstation installations these days incorporate a boot loader called GRUB (GRand Unified Bootloader) to select the specific kernel or alternate operating system to boot. There is a very good reason for having the ability to boot multiple kernel images. Suppose you build a new kernel and it fails to boot properly. You can always go back and boot a known working image, and then try to figure out what went wrong in your new one. If you are curious, have a look at the file `/boot/grub2/grub.cfg` on your workstation. You will need to be root user to get into the `grub2` directory.

Most Linux kernels are set up to use `initrd`, which is short for initial ramdisk. An initial ramdisk is a very small Linux file system loaded into RAM by the boot loader and mounted as the kernel boots, before the main root file system is mounted. The usual reason for using `initrd` is that some kernel modules need to be loaded before mounting the root partition. Usually, these modules are required to support the file system used by the root partition, `ext3` for example, or perhaps the controller that the hard drive is attached to, such as SCSI or RAID.

## Booting the New Kernel

Now that we have a new kernel, how do we test it? We could, of course, load the new image into flash, either in addition to, or in place of, the kernel image presently there.

The other alternative is to boot the new image over the network using TFTP. This is particularly advantageous in a development environment, because we can quickly test a new kernel image without the time-consuming process of burning flash.

Move `arch/arm/boot/zImage` to `/var/lib/tftpboot`, or wherever else you chose as the TFTP directory. Probably the simplest way to accomplish this is with a minor change to `uEnv.txt`. Copy `uEnv.txt` to `uEnvnet.txt`, and open with an editor. Note the line near the bottom that starts out `netboot=`. This command loads the kernel image into memory over TFTP. This is the equivalent of `loadkernel` that is presently used to load the kernel image from eMMC flash. So, in the `uenvcmd`, just replace `loadkernel` with `netboot`.

As we did back in Chapter 6, The hardware when bringing up the BBB, save `uEnvnet.txt` to the boot partition of the eMMC. Boot the board into the u-boot prompt, change `bootenv` to `uEnvnet.txt`, and execute `boot`. After the kernel boots, execute the command `uname -a` and note that the kernel image has a timestamp corresponding to when you built it.

Congratulations! You can pat yourself on the back. You are now a Linux hacker.

## Behind the Scenes: What's Really Happening

The information in this section is not essential to the process of building a kernel, and you are free to ignore it for now. But when you reach the point of developing device drivers or other kernel enhancements (or perhaps hacking the kernel itself), you will need to modify the files that control the configuration process.

All the information in the configuration menus is provided by a set of text files named `Kconfig` that are scattered throughout the source tree. These are script files written in *Config Language*, which looks suspiciously like a shell scripting language but isn't exactly. The main `Kconfig` file is located in `linux/arch/${ARCH}`, where `ARCH` is the variable in `Makefile` identifying the base architecture.

Go to `kernel/arch/arm` and open `Kconfig`. Find the line that reads `menu "System Type"` down around line 249. Compare the structure of the file with the configuration menu starting at System Type, and the pattern should become fairly clear. Each configuration option is identified by the keyword `config` followed by the option's symbolic name, for example `config_FHMLI`. Each of these gets turned into a `Makefile` variable, or macro, such as `CONFIG_FHMLI`. The `Makefiles` then use these variables to determine which components to include in the kernel and to pass `#define` symbols to the source code.
