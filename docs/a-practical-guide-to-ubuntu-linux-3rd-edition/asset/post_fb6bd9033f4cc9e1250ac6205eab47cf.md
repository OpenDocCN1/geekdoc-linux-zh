
If you are not working in /usr/src, you must copy the linux-source* file to the directory you are working in; otherwise, cd to /usr/src. Use tar to unpack the Linux source file:

```
$ tar -xjf linux-source-2.6.32.tar.bz2
```

## git: Obtaining the latest kernel source code

The git utility (GNU interactive tools, git-scm.com) can download the latest versions of the source code for several different kernels and can keep that source code up-to-date. If it is not already installed, give the following command to install git:

```
$ sudo aptitude install git-core
```

### Install the git-core package, not the git package

> Make sure to install the **git-core** package and not the **git** package. The **git** package is not useful for downloading kernel source code.

The following command uses git to download a copy of the development (not the released) kernel into the **ubuntu-2.6** subdirectory of the working directory. As a member of the src group, you can work in the /usr/src directory. Otherwise, you can work in any directory you have write access to. You can and should work as a nonprivileged user.

```
$ git clone git://kernel.ubuntu.com/ubuntu/Ubuntu-lucid.git ubuntu-2.6
Initialized empty Git repository in /home/sam/ubuntu-2.6/.git/
remote: Counting objects: 1624172, done.
remote: Compressing objects: 100% (292458/292458), done.
remote: Total 1624172 (delta 1346815), reused 1590040 (delta 1315854)
Receiving objects: 100% (1624172/1624172), 468.69 MiB | 392 KiB/s, done.
Resolving deltas: 100% (1346015/1346015), done.
Checking out files: 100% (31201/31201), done.
```

See kernel.ubuntu.com/git and git.kernel.org for a list of Ubuntu kernels you can download. Substitute the URL of the kernel you want to download for the URL in the preceding command and specify the name of an appropriate directory to hold the files you download. For example, the following command downloads the latest Jaunty kernel into the jaunty directory in the working directory:

```
$ git clone git://kernel.ubuntu.com/ubuntu/Ubuntu-jaunty.git jaunty
```

Once you have downloaded the kernel, cd to the directory that holds the code and give the following command to update the source code to match that available at the URL you specified in the git-clone command:

```
$ git pull
Already up-to-date.
```

The files you just downloaded should be up-to-date, as shown in the example. Give this command any time you want to synchronize the code in the working directory with the latest source code at the URL.

## /usr/src/linux: The Working Directory

Traditionally the source for the kernel that the system is running is kept in /usr/src/linux. The following command creates the appropriate symbolic link. This example shows the name of the kernel directory as linux-source-2.6.32; the name on the system you are working on will be slightly different.

```
$ ln -s /usr/src/linux-source-2.6.32 /usr/src/linux
```

After you give these commands, the kernel source is located in /usr/src/linux. The rest of this chapter assumes that the kernel source is in this location.

### Now the working directory is /usr/src/linux

> **tip** All commands in this section on building a kernel are given relative to the top-level directory that holds the kernel source. Traditionally this directory is /usr/src/linux. Make sure that this directory is your working directory before proceeding. If necessary, link the directory holding the kernel source in /usr/src to /usr/src/linux as explained above.

## READ THE DOCUMENTATION

The kernel package includes the latest documentation, some of which may not be available in other documents. You may wish to review the README file in the top level of the kernel source directory and the relevant files in the Documentation subdirectory. In addition, a lot of information is available in the /usr/share/doc/kernel-package directory. Read the Linux Kernel-HOWTO for a detailed, somewhat dated, generic guide to installing and configuring the Linux kernel.

## CONFIGURING AND COMPILING THE LINUX KERNEL

This section describes how to configure the kernel, how to compile it, and how to download and compile kernel modules.

### .config: CONFIGURES THE KERNEL

Before you can compile the code and create a Linux kernel, you must decide and specify which features you want the kernel to support. You can configure the kernel to support most features in one of two ways: by building the feature into the kernel or by specifying the feature as a loadable kernel module (page 580), which is loaded into the kernel only as needed. In deciding which method to use, you must weigh the size of the kernel against the time it takes to load a module. Make the kernel as small as possible while minimizing how often modules have to be loaded. Do not make the SCSI driver modular unless you have a reason to do so.

The .config file in the directory you downloaded the source code in controls which features the new kernel will support and how it will support them. "Customizing a Kernel" (page 577) explains how to create a default version of this file if it does not exist and how to edit the file if it does exist.

### REPLACING A CUSTOM KERNEL

If you have already configured a custom kernel, you may want to replace it with a similarly configured, newer kernel. Each kernel potentially has new configuration options, however—which explains why it is poor practice to use an old **.config** file for compiling a new kernel. This section explains how to upgrade an existing **.config** file so it includes options that are new to the new kernel and maintains the existing configuration for the old options.

Work in the directory you downloaded or extracted the source code to. The system keeps a copy of the configuration file for the kernel the local system is running in /boot. The following command copies this file to **.config** in the working directory:

```
$ cp /boot/config-$(uname -r) .config
```

In this command, the shell executes **uname -r** and replaces **$(uname -r)** with the output of the command, which is the name of the release of the kernel running on the local system. For more information refer to “Command Substitution” on page 362.

Next give the command **make oldconfig** to patch the **.config** file with options from the new kernel that are not present in the old kernel. This command displays each kernel option that is the same in the new and old kernels and automatically sets the state of the option in the new kernel the same way it was set in the old kernel. It stops when it finds an option that appears in the new kernel but not in the old kernel. It then displays a prompt, which is similar to [N/y/?] (NEW), showing possible responses and indicating this option is new. The prompt shows the default response as an uppercase letter; you can type this letter (uppercase or lowercase) and press RETURN, or just press RETURN to select this response. In the example, the Tickless System option is new and the default response is Y for yes. include the option in the new kernel. To select a nondefault response (n means no, do not include the option and m means include the option as a module), you must type the letter and press RETURN. Enter ? followed by RETURN to display more information about the option.

```
$ make oldconfig
scripts/kconfig/conf -o arch/i386/Kconfig

* Linux Kernel Configuration
*
*
* Code maturity level options
*
* Prompt for development and/or incomplete code/drivers (EXPERIMENTAL) [Y/n/?] y
*
* General setup
*

Local version - append to kernel release (LOCALVERSION) []
Automatically append version information to version string (LOCALVERSION_AUTO) [N/y/?] n
---
 * Processor type and features

TICKLESS_SYSTEM (NO_HZ) [Y/n/?] (NEW) ? ?
This option enables a tickless system: timer interrupts will
only trigger on an as-needed basis both when the system is
idle and when the system is busy.

TICKLESS_SYSTEM (NO_HZ) [Y/n/?] (NEW) ? RETURN
HIGH_RES_TIMERS [Y/n/?] y
Symmetric multi-processing support (SMP) [Y/n/?] y
Subarchitecture Type
> 1. PC-compatible (X86_PC)
> 2. AMD Elan (X86_ELAN)
---
# configuration written to .config
#
```

## Customizing a Kernel

You can use one of three standard commands to build the **.config** file that configures a Linux kernel:

```
$ make config
$ make menuconfig
$ make gconfig
```

See “Prerequisites” on page 572 for a list of packages required to run all but the first of these commands.

If a **.config** file does not exist in the working directory, each of these commands except the first sets up a **.config** file that matches the kernel the local system is running and then allows you to modify that configuration. The commands can set up **.config** file only if the configuration file for the locally running kernel is in **/boot/config-$(uname -r)**. See the preceding section if you want to build a new kernel with a configuration similar to that of an existing kernel.

The **make config** command is the simplest of the three commands, uses a textual interface, and does not require additional software. It is, however, the most un- giving and hardest to use of the configuration interfaces. The **make menuconfig** command uses a pseudographical interface and also displays a textual interface. The **make gconfig** command uses GTK+ (www.gtk.org) and displays a graphical interface.

Each command asks the same questions and produces the same result, given the same responses. The first and second commands work in character-based environments; the third command works in graphical environments. For many administrators working with a GUI, the third method is the easiest to use.
