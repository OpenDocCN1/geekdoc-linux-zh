![](bbox=[0.13, 0.11, 0.35, 0.2])

A module (also called a kernel module) is a self-contained driver library file. The advantage of using modules, instead of compiling all their features into the kernel, is that they keep the Linux kernel lighter and more agile. We can add certain kernel functionality as needed or on demand because modules can be loaded and unloaded into the kernel dynamically. They extend the functionality of the kernel without the need to reboot the system.

We'll take a look at the various kernel module types, where their files are stored, and module configuration file locations. We'll also explore in this chapter how to dynamically link and unlink the modules, view module information, and remove modules.

# # Exploring Kernel Modules

Kernel modules come in different flavors. They are as follows:

+   - Device driver: Facilitates communication with a hardware device.
+   - Filesystem driver: Required for filesystem I/O.
+   - Network driver: Used to implement network protocols.
+   - System calls: Provides additional functions for adding/modifying system services.
+   - Executable loader: Allows additional executable formats to load.

There are a few different files and directories you should be familiar with when working with modules. Modules required to support a kernel are stored in the /lib/modules/ directory tree. Each Linux kernel version available on your system has its own subdirectory within the /lib/modules/ directory. An example of this directory and its kernel version subdirectories on an Ubuntu 20.04 distribution is shown in Listing 14.1.

**Listing 14.1:** Viewing a /lib/modules directory

```
```
$ ls -F /lib/modules
5.11.0-40-generic/ 5.4.0-31-generic/ 5.4.0-47-generic/
5.4.0-26-generic/ 5.4.0-42-generic/ 5.4.0-48-generic/

$
```
```