
9. You have configured a job to run with the **batch** command, but apparently system utilization never drops as low as the default value. Which of the following commands can be used to set a custom value for the **batch** command?

- A. **batchavg**
- B. **atconfig**
- C. **atrun**
- D. **crontab**

Answer C is correct because the **atrun** command can be used to set the load average that **batch** uses as its threshold. Answer A is incorrect because there is no such command as batchavg. Answer B is incorrect because there is no such command as atconfig. Answer D is incorrect because the **crontab** command has no such capability.

10. You need to run a command that will let you take the hardware clock time and make it the system clock time before running the **ntpd** daemon. Fill in the blank below with the correct command, options, and arguments to accomplish this:

The correct answer is **hwclock --hctosys**. There are no alternative answers.

![](img/49f4f38f3aec011238fa50f89e643db3_382_0.png)

## Kernel Configuration and Custom Compilation

- **Terms you’ll need to understand:**
  - Archive
  - Compile
  - Compression
  - Driver
  - Kernel
  - Module
  - Patch
  - Tarball

- **Techniques you’ll need to master:**
  - Understanding kernel options
  - Configuring modules
  - Patching a kernel source tree
  - Compiling a kernel
  - Troubleshooting kernel boot issues
  - Repairing library issues
  - Identifying stable kernel versions

## Overview of the Kernel

The Linux kernel doesn't constitute much of what we refer commonly to as Linux. The majority of the Linux operating system is made up of software packages, daemons, and applications that are not needed to actually run the OS.

The kernel handles a multitude of things, including but not limited to, the following:

- Memory management
- Dividing up processor time amongst tasks
- Providing an interface for applications to talk to hardware

It's important to note that, although the Linux kernel is the lynchpin of the Linux OS, it can be compiled and recompiled for nearly any task.

The user can swap in and out of experimental kernels with just a simple reboot and a menu choice. This is difficult, if not impossible, on many other operating systems.

> Unlike when you apply service packs on Windows; when you are recompiling the kernel the system is fully functional. Until the newly compiled kernel is installed and the system rebooted, the new kernel is just another software package.

## The Kernel Versions

When you start working with the kernel, it can be confusing to figure out just what the version numbers signify on the Linux kernel.

The kernel version numbers work like this:

```
major . minor . patch
```

Where the numbers might be 2.6.2.

The most important version number is the middle, or minor, version. In all cases, if this is an even number, that version is considered a stable or production version. If the minor is an odd number, it's considered a development or testing version and should never be used in a production environment.

As a point of understanding, it’s key to note that the kernel is in constant development, with the stable version being in production and bugfix mode, while the development version is being worked on and bug-tested.

Other examples of the versions include:

- **2.4.12** — A stable 2.4 kernel at patch level 12
- **2.5.6** — A development 2.5 kernel at patch level 6
- **3.1.2** — A development version, not for production

If you don’t know the version of your kernel, you can easily check with the *uname* command:

```
uname -r
```

This produces output similar to:

```
2.4.18-3
```

Additionally, you can run the all-inclusive option for the *uname* command to get all the information about the machine *uname* can provide:

```
uname -a
```

This produces output similar to:

```
Linux localhost.localdomain 2.4.18-3 #1 Thu Apr 18 07:37:53 EDT 2004 i686 unknown
```

## Monolithic Versus Modular Kernels

There are advantages to having both a *monolithic* (everything compiled in) and a *modular* (essentials only, it depends on modules for additions) kernel, and indeed most distributions ship a mostly modular version of the kernel that is designed to work on most machines.

This is exactly why it’s nice to be able to compile your own kernel; the ones Red Hat or Debian puts into the distributions aren’t tuned for your system or, in some cases, to your level of processor. You might be running a kernel that has been tuned for and works best on a 386-class processor. Most sysadmins begin to compile their own custom kernels after they’ve gained a certain amount of experience and have a little extra time to experiment.

A monolithic kernel has the following advantages:

- It has all the necessary drivers compiled in.
- No load time is required for modules.
- It's good when you can't update or recompile.

A modular kernel has the following advantages:

- The necessary modules can be loaded/unloaded.
- It's smaller than a monolithic kernel.
- It's best for flexible systems.

Most Linux systems use a modular kernel or a kernel that includes less compiled-in code and relies more on external modules of code that are loaded on demand.

### Modules

Essentially, a *module* is a software driver that enables interaction with hardware from the kernel or processes. If you don't want to wait for modules to load, or want the driver instantly available, compile it into the kernel.

Because the kernel is the arbiter of what has access to the hardware, modules must be made available for the kernel to load if that hardware is to be used. A module is referenced by name and assumed to be in the correct hierarchy of directories under the `/lib/modules` tree.

For example, you can see the current hierarchy of module directories with the following command:

```
tree -d /lib/modules
```

This returns output that's much lengthier than the following, which has been truncated for brevity:

```
/lib/modules
|-- 2.4.10-3
    |-- build -> ../../usr/src/linux-2.4.10-3
    |-- kernel
        |-- abi
        |   |-- cxenix
        |   |-- ibcs
        |   |-- isc
        |   |-- scc
        |   |-- svr4
        |   `-- util
        |       `-- uw7
        `-- arch
            `-- i386
```

![](img/49f4f38f3aec011238fa50f89e643db3_386_0.png)

> If your distribution doesn't have the `tree` command, get the RPM for it from www.rpmfind.net. Red Hat removed the `tree` command from Red Hat Linux 8 and 9.

### Module Dependencies

When you use a modular kernel, you have to depend on the modules you have created and compiled. When the kernel needs a module for something, it requests that the module and its dependencies be loaded.

This is perhaps best illustrated by Figure 14.1, which is something I constructed as an attempt to explain this multidependency process to attendees.

![](img/49f4f38f3aec011238fa50f89e643db3_386_1.png)

As you can see, the kernel uses the `kmod` process to request that the `modprobe` command load the necessary modules, such as in the case of a newly attached piece of hardware.

The `modprobe` command uses the existing `/lib/modules/`uname -r`/modules.dep` file to determine exactly what must be loaded and in what order to satisfy the dependencies modules might have on other modules.

The `modules.dep` file is built by the `depmod` command using the `/etc/modules.conf` file as its input. The `modules.conf` file (often known as conf.modules in the past) contains a list of variables, paths, and aliases that, when read by the `depmod` command, cause the `modules.dep` map to be built.

![](img/49f4f38f3aec011238fa50f89e643db3_386_2.png)

> Watch out for questions that test your ability to remember how this complex set of commands and configuration files is read and processed. Remember that the `modules.conf` file is read by `depmod` and produces the `modules.dep` file, which is read by `modprobe` to find the right modules to load in the correct order so the `kmod` process can report a success to the kernel.
