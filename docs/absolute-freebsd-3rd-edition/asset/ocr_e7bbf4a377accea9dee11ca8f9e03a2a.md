The `kldstat(8)` command shows modules loaded into the kernel.

```
```
# kldstat
 Id Refs  Address      Size  Name
 1    1 0xffffffff80200000  204c3e0 kernel
 2    1 0xffffffff8224e000  3c14f0  zfs.ko
 3    2 0xffffffff82610000  d5f8    opensolaris.ko
 4    1 0xffffffff82821000  ac15    linprocfs.ko
 - snip -
```
```

This desktop has three kernel modules loaded. The first is the kernel proper **1**; then, modules to support ZFS **2** and the OpenSolaris kernel functions needed by ZFS **3** follow. I experiment with Linux software on this host (see Chapter 17), so finding the `linprocfs(5)` module **4** loaded is not a surprise.

Each module contains one or more submodules, which you can view using `kldstat -v`, but the kernel itself has a few hundred submodules—so be ready for a lot of output.

# ## Loading and Unloading Modules

Loading and unloading kernel modules is done with `kldload(8)` and `kldunload(8)`. For example, suppose I’m experimenting with IPMI on a test host. This requires the `ipmi(4)` kernel module. While I’d normally load this automatically at boot using `loader.conf`, I’m in the lab. I use the `kldload` command and the name of the kernel module or the file containing the kernel module for that feature:

```
```
# kldload /boot/kernel/ipmi.ko
```
```

If I happen to remember the name of the module, I can just use that. The module name doesn’t need the `.ko` at the end of the file. I happen to recall the name of the IPMI module.

```
```
# kldload ipmi
```
```

Most often, my feeble brain relies on tab completion in my shell to remind me of the module’s full and proper name.