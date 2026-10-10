# # swapon / swapoff

Purpose: Activate/deactivate swap space.

Usage syntax: swapon [OPTIONS] [DEVICE]

```
# swapon /dev/sdb1
```

Activating swap storage

The swapon command activates swap storage. The above example demonstrates activating a newly created swap space using swapon.

> Note 
> Newly created swap space does not become usable by the system until it is activated using the swapon command. Most systems have at least one swap space that is activated at boot by default. Additional swap devices created after installation must be added to the /etc/fstab file to be automatically activated at boot.

The swapoff command deactivates swap storage. The next example demonstrates using swapoff to deactivate the /dev/sdb1 swap device.

Usage syntax: swapoff [OPTIONS] [DEVICE]

```
# swapoff /dev/sdb1
```

Deactivating swap storage

Swap storage must be deactivated with the swapoff command before it can be changed or removed.

> Note 
> Solaris systems use the swap command in place of swapon and swapoff.

Common usage examples:

+   * swapon -a
+   * swapon [DEVICE]
+   * swapon -s
+   * swapoff -a
+   * swapoff [DEVICE]

+   * Enable all swap spaces
+   * Enable the specified swap space
+   * Display swap usage by device
+   * Disable all active swap spaces
+   * Disable the specified swap space