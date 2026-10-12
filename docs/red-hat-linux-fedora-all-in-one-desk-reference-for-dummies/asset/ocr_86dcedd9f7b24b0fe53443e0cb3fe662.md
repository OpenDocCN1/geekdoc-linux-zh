the kernel with the new driver code. Rebuilding the kernel means you have to reboot the PC with the new kernel before you can use the new device driver. Luckily, the Linux kernel uses a modular design that does away with rebooting hassles. Linux device drivers can be created in the form of modules that the kernel can load and unload without having to restart the PC.

Driver modules are one type of a broader category of software modules called Loadable Kernel Modules. Other types of kernel modules include code that can support new types of file systems, modules for network protocols, and modules that interpret different formats of executable files.

![](bbox=[0.12, 0.27, 0.2, 0.42])

# Loading and unloading modules

You can manage the loadable device driver modules by using a set of commands. You have to log in as root to use some of these commands. In Table 5-1, I summarize a few of the commonly used module commands.

Table 5-1 Commands to Manage Kernel Modules

| This Command | Does the Following |
|---|---|
| insmod | Inserts a module into the kernel |
| rmmod | Removes a module from the kernel |
| depmod | Determines interdependencies between modules |
| ksyms | Displays a list of symbols along with the name of the module that defined the symbol |
| lsmod | Lists all currently loaded modules |
| modinfo | Displays information about a kernel module |
| modprobe | Inserts or removes a module or a set of modules intelligently (for example, if module A requires B, then modprobe automatically loads B when asked to load A) |

If you have to use any of these commands, log in as root or type su - in a terminal window to become root.

To see what modules are currently loaded, type

```
lsmod
```

You should see a list of modules. For example, here is a list on one of my PCs:

```
Module Size Used by Not tainted
nls_iso8859-1 3516 1 (autoclean)
nls_cp437 5148 1 (autoclean)
sd_mod 13516 2 (autoclean)
vfat 13036 1 (autoclean)
fat 38808 0 (autoclean) [vfat]
```