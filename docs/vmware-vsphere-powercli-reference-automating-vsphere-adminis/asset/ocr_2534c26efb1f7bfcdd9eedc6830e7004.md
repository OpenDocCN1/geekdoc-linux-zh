Automatic. With Disk Claim Mode set to Automatic, any disks added to hosts in the cluster will automatically be claimed by VSAN for consumption.

# LISTING 4.25 Enabling VSAN on a cluster

```
Get-Cluster 'VSAN01' | Set-Cluster -VsanEnabled:$true
-VsanDiskClaimMode Automatic -Confirm:$false
```

# Disk Groups and Disks

In VSAN, SSDs and HDDs are grouped together per ESXi host in disk groups. Depending on performance and capacity requirements, it may make sense to use multiple disk groups per ESXi host. There are PowerCLI cmdlets to assist with management of disk groups and disks in the VMware.VimAutomation.Storage module, as shown here:

```
PS C:\ Get-Command *VSAN*-Module VMware.VimAutomation.Storage

CommandType Name ModuleName
Cmdlet Get-VsanDisk VMware.VimAutomation.Storage
Cmdlet Get-VsanDiskGroup VMware.VimAutomation.Storage
Cmdlet New-VsanDisk VMware.VimAutomation.Storage
Cmdlet New-VsanDiskGroup VMware.VimAutomation.Storage
Cmdlet Remove-VsanDisk VMware.VimAutomation.Storage
Cmdlet Remove-VsanDiskGroup VMware.VimAutomation.Storage
```

Typically, the Get commands are used for reporting purposes. The New and Remove commands are most likely used for scenarios where VSAN disk operations are required outside of a cluster which has Disk Claim Mode set to Automatic. The New and Remove commands are also used for custom configurations when the Disk Claim Mode setting is Manual.

In Listing 4.26, we add a new HDD to an existing disk group. Note that the code is similar to the code we used to add local or SAN datastores earlier in the chapter. First, we must identify the canonical name of the disk to add to the VSAN disk group using the Get-SCSILUN cmdlet.

# LISTING 4.26 Adding a disk to an existing VSAN disk group

```
Get-VMHost vsanesxi01* | Get-ScsiLun -LunType disk |
Format-Table CanonicalName
$VSANDiskGroup = Get-VsanDiskGroup -VMHost vsanesxi01*
```