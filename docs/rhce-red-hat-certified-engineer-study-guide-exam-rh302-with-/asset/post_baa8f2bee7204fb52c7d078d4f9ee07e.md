
To compile a Linux kernel, you should install several packages, including kernel-source, kernel-headers, gcc, cpp, dev86, make, glibc-devel, ncurses, ncurses-devel.

## Kernel Modules
The kernel module configuration file is /etc/conf.modules. Important commands for working with kernel modules include depmod, insmod, modprobe, rmmod, and uname.

## Key Terms

Before going on to the next chapter, be sure you're familiar with the following terms:

- developmental release
- extraversion code
- major versions
- minor versions
- modular
- monolithic
- patch level
- stable release

## Additional Sources of Information

If you'd like further information about the topics presented in this chapter, you should consult the following sources:

- The Linux kernel documentation in /usr/src/linux/Documentation
- The man pages for the commands that manipulate modules: insmod, rmmod, modprobe, depmod

## Review Questions

1. Which of the following is generally true of monolithic Linux kernels in comparison to modular Linux kernels?
A. They boot faster.
B. They execute faster.
C. They occupy less RAM.
D. They’re more flexible.

2. What is the minor version number of Linux 2.4.5-6?
A. 2
B. 4
C. 5
D. 6

3. Which of the following kernels is part of the stable release development tree?
A. 2.4.5-test
B. 2.4.6-stable
C. 2.5.5-test
D. 2.5.6-stable

4. What command displays the version number of the running Linux kernel?
A. dmesg
B. motd
C. uname
D. w

5. Which of the following commands loads the module known as heavy?
A. depmod heavy
B. insmod heavy
C. load heavy
D. modprobe heavy

6. Which of the following correctly specifies the common name of the Linux kernel?
A. /boot/bzImage
B. /boot/kernel
C. /boot/vmlinuz
D. /boot/vmlinux

7. Which of the following /etc/conf.modules lines specifies a command to be used when loading a module?
A. path=
B. pre-install
C. install
D. post-install

## Answers to Review Questions

1. B. Monolithic kernels do not use loadable modules to communicate devices, so they execute faster than modular kernels. But they're larger and therefore slower to boot.
2. B. The major version number is 2. The minor version number is 4. The patch level is 5. The extraversion code is 6.
3. A, B. The minor version of stable kernel is even.
4. C. The uname -r command displays the kernel version.
5. B, D. Either the insmod or modprobe command can be used to load a module. The insmod command, however, does not automatically load other modules needed by the module.
6. C. The common name of the Linux kernel is /boot/vmlinuz; however, the filename is arbitrary.
7. C. The install line specifies the command to load a module.

## Chapter 18: Configuring, Building, and Installing a Custom Kernel

PREPARATION TOPICS COVERED IN THIS CHAPTER:
- Be able to configure, build, and install the Linux kernel and modules from source.
- Be familiar with kernel configuration issues associated with using Red Linux.

## Configuring the Kernel

This section and the following sections explain the procedure for configuring, building, and installing the Linux kernel. To help you keep your place, procedurally important subsections are titled with a step number that indicates their place in the overall process:

1. Change to the kernel source directory.
2. Recover the default configuration (optional).
3. Define the extraversion code.
4. Specify the configuration options.
5. Build the kernel and modules.
6. Install the kernel and modules.
7. Create the boot ramdisk.
8. Revise the LILO configuration.
9. Create a new boot disk.

### Step 1: Changing to the Kernel Source Directory

Configuring the kernel, like building and installing the kernel, is done from the root directory of the kernel source tree; /usr/src/linux. To begin configuring the kernel, you should change to:

```bash
cd /usr/src/linux
```

### Step 2: Recovering the Default Configuration

If you have already built a kernel on the local host, you may want to simply tweak the kernel configuration. However, if you've previously built a kernel, you should recover the default Red Linux configuration. To do so, issue the commands:

```bash
cp configs/kernel arch/i86/defconfig
make clean
make oldconfig
```

where kernel is the name of the file in the configs directory that corresponds to the standard kernel on which you want to base your kernel. The make clean command removes old configuration files and the results of previous builds. The make oldconfig command selects the config.in file, referring to the defconfig file to determine default values for parameters.

### Step 3: Defining the Extraversion Code

As explained in the previous chapter, Red Hat Inc. recommends that you define an extraversion code that distinguishes differently configured kernels of the same version. To do so, edit the file /usr/src/linux/Makefile. The first few lines of the file should resemble:

```makefile
VERSION = 2
PATCHLEVEL = 2
SUBLEVEL = 1
EXTRAVERSION = -2
```

Add some descriptive text following the -2 in the fourth line, which specifies the Red Hat build protocol. For example, if the new kernel supports Wireless Access Protocol (WAP), you might revise the line to read:

```makefile
EXTRAVERSION = -2WAP
```

The extraversion code is reported by uname and determines the subdirectory of /lib/modules into which kernel modules are installed, preventing conflicts between modules of similar kernels.

### Step 4: Specifying the Kernel Configuration Options

The kernel configuration options reside in the file /usr/src/linux/.config. In principle, you could modify this file by using a text editor. However, Linux provides three utilities that make kernel configuration much simpler:

- config
- menuconfig
- xconfig

To use one of these utilities, issue a command of the form:

`make [utility]`

where utility is the name of one of the three utilities. It is a text-based, question-and-response utility. The config utility is the oldest of the three utilities. It is available as part of many Linux distributions. However, most users find it clumsy to use. A significant drawback is that config provides no way to modify a response once entered. So, if you discover you must exit the procedure (by typing Ctrl+C) and start once over. The dialog provided by config resembles the following:

```text
# make config
rm -f include/asm
( cd include ; ln -sf asm-i386 asm)
/bin/sh scripts/configure arch/i386/config.in
#
# Using defaults found in .config
#
*
Code maturity level options
*
Prompt for development and/or incomplete code/drivers (CONFIG_EXPERIMENTAL) [Y/n/?]
*
* Processor type and features
* Processor family (386, 486, 586)
```
