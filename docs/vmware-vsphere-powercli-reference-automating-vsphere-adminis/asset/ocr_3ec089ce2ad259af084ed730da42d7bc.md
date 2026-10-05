Beginning with vSphere4, it became possible to add vDirectPath I/O pass-through devices, also referred to as PCI pass-through devices. The other type of pass-through availability is the SCSI pass-through device. You can connect to it pass-through devices to a virtual machine using the Add-PassthroughDevice cmdlet. Remember that before PowerCLI can connect a PCI pass-through device to your virtual machine, the device must be enabled for pass-through on the ESX host:

```
$DeviceList = Get-VMHost ESX0 | Get-PassthroughDevice \
Get-VM VM001 | Add-PassthroughDevice \
-PassthroughDevice $DeviceList[0]
```

# Optimize Storage Usage with Thin Provisioning

When a new virtual disk is created and disk type is not specified, the disk type is thick by default for any VMFS datastore. A thick virtual disk preallocates all space during the creation of the disk. You can create a thin virtual disk. A thin virtual disk does not preallocate the space. The blocks of a thin disk are allocated on demand when first written to. You create a thin-provisioned disk by specifying the -Format parameter on the New-HardDisk cmdlet:

```
Get-VM VM001 | New-HardDisk -CapacityGB 10 -StorageFormat Thin
```

In a VMware environment, every VM needs to have its own boot and data volumes. The initial size of the boot volume is dictated by the size of the operating system and applications. The size of the data volume is dictated by the size of the existing application data. Typically, there is also an amount of free space available to each partition to accommodate future patches, service packs, upgrades, and application growth. Traditionally volumes are designed to take into account data for the upcoming year or even years, disks used to be fixed in an era when servers were installed on direct attached disks. Nowadays, servers store their files on storage arrays, which are more flexible in size, and presented disks (logical units) can easily be extended.

But still, are many minds designed the old-school way. This leads to lots of free unused space on your expensive storage arrays. With this provisioning, you can reclaim this wasted space and increase your storage capacity utilization. This boost in capacity utilization (typically 20–30 percent) saves an equal percentage of your annual storage costs, because the same servers and applications are stored on less space.