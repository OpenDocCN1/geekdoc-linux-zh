Based on that output, you can deduce that on this ESXi node three disk Luns and one CD-ROM drive are connected.

# vSphere View objects

The vSphere View objects are the objects that are used by vSphere internally. These objects are documented in the VMware vSphere API Reference, and will be discussed greater in Chapter 18, "The SDK." vSphere View objects are pre-sented to PowerCLI in two ways:

+   - Under the ExtensionData property in several places in PowerCLI objects

+   - As objects returned by the Get-View cmdlet

In both cases, this representation of the vSphere View objects is a read-only copy of the actual vSphere object. This means that the content of the properties is not updated automatically. You will have to get the object again or use the UpdateView method.

```
$vm.ExtensionData.Config.Hardware.NumCPU
1
Set-VM -VM $vm -NumCpu 2 -Confirm:$false
```

| Name | PowerState Num CPUs MemoryGB |
| --- | --- | --- | --- |
| VM1 | PoweredOff 2 | 4.000 |

```
$vm.ExtensionData.Config.Hardware.NumCPU
1
$vm.ExtensionData.UpdateView()
$vm.ExtensionData.Config.Hardware.NumCPU
2
```

The ConvertTo-Text function from Listing 15.1 can also be used on vSphere View objects. The following short sample searches under the Config property of an ESXi node for the location where IPv6Enabled can be found.

```
ConvertTo-Text -InputObject $esx.ExtensionData.Config -Depth 2 |
```