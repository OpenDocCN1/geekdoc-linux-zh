# # The Logical Volume Manager

When is a device not a device? When it is a pseudo-device!

In the logical volume manager (LVM) we see yet another type of abstraction layer. HPUX builds file systems, allocates swap space, and allows raw data storage on disk volumes. The LVM subsystem allows the administrator to create logical volumes from the pooled space of physical volumes. Once a logical volume has been configured, it may be used in the same manner as a physical volume. Logical volume management gives the administrator a great deal of control over the size of individual file systems, swap, and raw space. In this chapter, we examine the underlying disk- and kernel-resident metadata structures used by LVM.

# ## LVM Design Concept

Why have multiple file systems? Most UNIX file systems allow a file to grow within the boundary of the volume on which it was created. As such, a single runaway file may completely fill a file system. A file system that is 100 percent full presents challenges to the kernel when it needs to manage the space. If file systems holding operating system directories are filled, the kernel may have difficulties performing many of its tasks and in an extreme case even crash.

To avoid this scenario, most administrators prefer to create a number of individual file systems, sizing each to match its use. This allows the isolation of system directories (e.g., /usr, /lib) from user (e.g., /home) and application (e.g., /opt, /var/opt) directories. The kernel's virtual file system layer is then used to build what appears to applications and users as a single, seamless virtual file system. The kernel handles all transversal of mount points and directory structures during file open calls.