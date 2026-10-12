| File System | Description |
| :--- | :--- |
| UFS | File system used by the BSD (Berkeley Software Distribution) variants of UNIX (such as SunOS, FreeBSD, NetBSD, and NeXTstep). |
| VFAT | Windows 95/98/NT/2000 file systems with long filenames. |

# ## Kernel hacking

This set of options enables you to debug the kernel and use the SysRq key (usually the PrintScreen key on your keyboard) to get important status information right after a system crash. This information is useful if you’re a Linux developer who expects to debug the kernel. Most users disable these options (because most users run a stable version of the kernel and don’t expect to fix kernel errors).

# ## Security options

Through these options, you can include support for the Security Enhanced Linux (SELinux), which was developed by the National Security Agency (NSA) — a U.S. government agency. SELinux comes with Fedora Core, but you can turn it off during booting by providing `selinux=0` as a boot option. For more information on SELinux, visit www.nsa.gov/selinux/.

# # Building the Kernel and the Modules

After configuring the kernel options, click the Save and Exit button in the main configuration window (refer to Figure 6-7). Now you have to build the kernel. This part can take a while. Depending on your system, making a new kernel can take anywhere from a few minutes to over an hour.

Type the following on a single line to initiate the process:

```
```
make
```
```

The `make` command creates the new kernel as well as any modules that you have specified through the configuration step.

As the kernel is built, you see a lot of messages on-screen. When it’s all over, a new kernel in the form of a compressed file named bzImage is in the `/usr/src/linux*/arch/i386/boot` directory.

To use the new kernel, you have to copy the kernel file to the /boot directory under a specific name and edit the /etc/grub.conf file to set up GRUB — the boot loader. Before you proceed with the kernel installation, however, you have to install the modules and build a new initial RAM disk.