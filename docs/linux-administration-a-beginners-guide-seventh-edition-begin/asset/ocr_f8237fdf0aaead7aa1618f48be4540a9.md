# cgroups

Control groups (cgroups) provide a mechanism for managing system resources on a Linux-based system. Resources such as memory allocation, process scheduling, disk I/O access to blocked devices, and network bandwidth can all be controlled and allocated via cgroups.

The resources are managed by so-called “resource controllers” (also known as subsystems or modules). Following are some common cgroup subsystems that can be used to control specific system tasks and processes:

+   - blkio (block input and output controller)
- cpuact (CPU accounting controller)
- cpuset (CPUs and memory nodes controller)
- freezer (suspending, resuming, and check-pointing tasks)
- memory (memory controller)
- net_cls (network traffic controller)
- devices (tracking, granting, or denying access to creation or use of device files)

To view a list of the subsystems supported on your system, type the following:

```
root@server ~# cat /proc/cgroups
#subsys_name hierarchy num_cgroups enabled
cpuuset 2 1 1
cpu 3 32 1
cpuacct 4 1 1
memory 5 1 1
devices 6 1 1
reezer 7 1 1
net_cls 8 1 1
blkio 9 1 1
```

> TIP provides various tools and libraries that can be used for manipulating, controlling, monitoring, and administering control groups. On RPM-based distros like Fedora, CentOS, and RHEL, you can install the libcgroup package using Yum or the newer DNF package manager. Here you can use DNF by:
# dnf -y install libcgroup-tools

cgroups make use of the cgroup pseudo-file system (cgroupfs), which in turn makes use of the Linux virtual file system (VFS) abstractions. cgroupfs provides a hierarchy of sorts for managing, grouping, and partitioning tasks and processes running on a system. Subsystems are attached to directories mounted under cgroups, and different constraints can be applied to these by placing processes and tasks in control