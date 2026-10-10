the filesystem area when recompiling your kernel. Many distributions ship with this support pre- compiled, so recompiling your kernel may not be necessary, but you should be aware of this option if you do recompile your kernel.

# Caveats

The usual root cautions apply to this task. In addition, setting limits that are too restrictive can cause problems for users: They may be unable to create files or their processes may be unceremoniously terminated if they exceed the CPU time and memory limits.

# Procedure

Disk quotas are more difficult to set than CPU time and memory limits. To enable disk quotas, you must both configure various tools (including, perhaps, recompiling your kernel) and enable quota support for various users. CPU time and memory limits, by contrast, are set by PAM options.

# Enabling Quota Support

Quotas require support in both the kernel for the filesystem being used and various user-space utilities. If your kernel lacks quota support, consult Phase 2 for information on recompiling your kernel.

Two general quota support systems are available for Linux. The first was used through the 2.4.x kernels and is referred to as the quota v1 support. The second was added with the 2.6.x kernel series and is referred to as the quota v2 system. This description applies to the latter sys- tem, but the former works in a similar way.

Outside of the kernel, you need support tools to use quotas. For the quota v2 system, this package is usually called **quota**, and it installs a number of utilities, configuration files, SysV startup scripts, and so on.

![](bbox=[0.14, 0.69, 0.25, 0.73])

> You can install the support software from source code, if you like; however, this job is handled most easily using a package from your distribution. This description assumes that you install the software in this way. If you don't, you may need to create SysV or local startup scripts to initialize the quota support when you boot your computer. The *Quota Mini-HOWTO*, at `http:// en.tldp.org/HOWTO/Quota.html`, provides details of how to do this.

You must modify your /etc/fstab entries for any partitions on which you want to use the quota support. In particular, you must add the usrquota filesystem mount option to employ user quotas and the grpquota option to use group quotas. Entries that are so configured resemble the following:

```
/dev/hdc5 /home ext3 usrquota,grpquota 1 1
```