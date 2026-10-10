# modinfo

Purpose: Display information about Linux kernel modules.

```
Usage syntax: modinfo [OPTIONS] [MODULE]

```
$ modinfo nfs
filename: /lib/modules/2.6.28-l1-generic/kernel/fs/nfs/nfs.ko
license: GPL
author: Olaf Kirch <okir@monad.swb.de>
srcversion: A400A4357849F5E18225B6F
depends: sunrpc,lockd,nfs_acl
vermagic: 2.6.28-l1-generic SMP mod_unload modversions
parm: enable_ino64:bool
Using the modinfo command to display information about the NFS module
```
```

modinfo displays information about Linux kernel modules. It includes helpful information such as the file location, license, version, and dependencies for the module. The above example demonstrates using modinfo to display information about the NFS kernel module.

> Note
> 
> *Linux kernel modules typically are stored in the /var/lib/modules directory.*

+   Common usage examples:
+   
+   ```
+   modinfo [MODULE]    Display information about the specified module
+   ```