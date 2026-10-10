# modinfo

Purpose: Display information about Linux kernel modules.

Usage syntax: modinfo [OPTIONS] [MODULE]

![](bbox=[0.08, 0.2, 0.9, 0.33])

modinfo displays information about Linux kernel modules. It includes helpful information such as the file location, license, version, and dependencies for the module. The above example demonstrates using modinfo to display information about the NFS kernel module.

> **Note** *Linux kernel modules typically are stored in the /var/lib/modules directory.*

+   Common usage examples:
+   modinfo [MODULE] | Display information about the specified module