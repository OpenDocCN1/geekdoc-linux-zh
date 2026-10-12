Linux 2.0 kernel dynamic loader and allows the automatic loading and unloading of kernel modules, there is no real need to include IPC in the main kernel; removing kernel support from the IPC module has also reduced its size by 40%.

# sysctl Support

Adding sysctl provides means for controlling the running kernel either through system calls, or, if the /proc filesystem is enabled, through pseudo-files in the /proc/sys directory. In the /proc interface, the directory is partitioned into several areas that govern different aspects of the kernel:

+   * dev/device—Specific information (for example, dev/crom/info)
+   * fs/contro1—Control of specific filesystems, such as setting the number of filehandles and inodes, dentry and quota tuning, and configuring the support for arbitrary binaries (see “Support for Misc Binaries” later in this chapter)
+   * kernel/1—Kernel status and tuning
+   * net/1—Networking parameters
+   * sunrpc/—SUN Remote Procedure Call (RPC)
+   * vm/1—Virtual memory, and buffer and cache management

> **Tip**
> The First Rule of Optimization: Don't.
> The Second Rule of Optimization (for experts only): Don't (yet).

These services are both powerful and dangerous. Be sure you know what you are getting into before you fiddle with these files! Kernel parameters include the interpretation of Ctrl+Alt+Delete, the time delay for a reboot after a kernel panic, your system host and domain name, and a number of architecture-dependent features for the Sparc and Mac platforms. The sunrpc directory also includes debug flags for kernel hacking of remote procedure calls.

Detailed information on using and interpreting all these features can be found in linux/Documentation/sysctl.

# Virtual Memory Tuning Through sysctl

Virtual memory tuning allows for hand-optimizing the machine for disk activity. For example, by setting the system's tolerance for dirty memory pages to a higher value, the kernel will have less disk activity (which saves power and improves speed) although it