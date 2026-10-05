To do this on multiple virtual machines, the obvious answer is to script it.
Fortunately, PowerVCLI provides a simple method for doing so:

```
Get-VM VM001 | New-AdvancedSetting -Name "snapshot.maxSnapshots"
-Value 1
```

![](bbox=[0.218, 0.206, 0.273, 0.246])

> **NOTE** Setting Snapshot.maxSnapshots to 0 will disable snapshots on that VM. This setting explicitly configures the maximum number of snapshots vSphere can take on a per-VM basis.