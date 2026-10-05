
# Creating Storage Policy Rules and Rule Sets

Before creating the storage policy, you must create at least one policy rule and rule set using an existing tag. (The tag will be used to identify which storage will be present in the policy.) First create the storage policy rule and create the rule set for consumption by the storage policy. As part of the rule set creation, you will add the rule just created to the new set. In Listing 4.21, we create a rule and rule sets using a tag named Silver Storage.

- LISTING 4.21 Creating a storage policy and rule set

```bash
$SilverTag = Get-Tag 'Silver Storage'
$SilverTagRule = New-SpbmRule -AnyOfTags $SilverTag
$SilverTagRuleSet = New-SpbmRuleSet -AllOfRules $SilverTagRules
```

# Creating and Assigning Storage Policies

The prerequisites are now in place, and you can create a storage policy. In Listing 4.22, we create a policy named Silver Storage with a description of Policy for Silver Storage that uses the rule set from Listing 4.21.

- LISTING 4.22 Creating a storage policy

```bash
$SilverTagStoragePolicy = New-SpbmStoragePolicy -Name \
'Silver Storage' -Description \
'Policy for Silver Storage' \
-AnyOfRuleSets $SilverTagRuleSet
```

To use a policy, the cluster needs to be enabled for policies; then VMs must be assigned to a policy. In Listing 4.23, we enable policies for Cluster01 and assign the Silver Storage policy to any VMs starting with Server*.

- LISTING 4.23 Enabling a cluster for storage policies and assigning a policy to VMs in the cluster

```bash
Get-SpbmEntityConfiguration -Cluster01 | \
Set-SpbmEntityConfiguration -SpbmEnabled:$true
Get-VM Server* | Set-SpbmEntityConfiguration \
-StoragePolicy $SilverTagStoragePolicy
```

Typical output for the VMs will be similar to the following:

| Entity | Storage Policy | Status | Time Of Check |
| --- | --- | --- | --- |
| Server01 | Silver Storage | nonCompliant | 04/02/2015 14:35:33 |
| Server02 | Silver Storage | nonCompliant | 04/02/2015 14:35:38 |
| Server03 | Silver Storage | compliant | 04/02/2015 14:35:53 |

# vSphere APIs for I/O Filtering

vSphere APIs for I/O (VAIO) Filtering framework allows filters to process a VM's I/O to its Virtual Machine Disk (VMDK) files. Filters are inside ESXi (outside the VM) and are provided via a VIB file from a third party. VAIO can be used for access to a hot cache or provide replication filters. There are three PowerCLI cmdlets that assist with VAIO management in the VMware.VAutomation module, as shown here:

```bash
PS C:\ Get-Command *vaio* -Module VMware.VAutomation.Storage
```

| CommandType | Name | ModuleName |
| --- | --- | --- |
| Cmdlet | Get-VAIOFilter | VMware.VAutomation.Storage |
| Cmdlet | New-VAIOFilter | VMware.VAutomation.Storage |
| Cmdlet | Remove-VAIOFilter | VMware.VAutomation.Storage |

> NOTE As of this writing, no third-party VIBs are available to demonstrate the use of the VAIO cmdlets.

![](img/62596f5acc979040608a4e5111beb7d6_178_0.png)

# VSAN

Virtual SAN (VSAN), VMware's software-defined storage for vSphere, combines local server disks in ESXi hosts in a vSphere cluster to create shared storage, which can be accessed by any host in the cluster. VSAN offers high performance via read/write caching using server-side flash and both capacity and performance scalability. You can scale out by adding more hosts to the cluster or scale up by adding more disks to the hosts. PowerCLI contains a number of VSAN cmdlets for the VMware.VAutomation.Storage module. We will look at some examples of how to make use of these cmdlets, as well as how you to use vSphere APIs to cover areas the cmdlets do not currently reach.

# Configuration

VSAN has a number of networking requirements that must be met in order to be able to serve the shared datastore. Some of relate to physical networking and a couple must be considered for automation. vSphere Standard or Distributed Switches are supported with VSAN, so either type can be used as ESXI hosts configured for VSAN. For each network that you use for VSAN, you must configure a VMkernel port group with the VSAN port property activated.

> NOTE For detailed information, be sure to read the VSAN Networking Requirements and Best Practices documentation: http://vmw.re/1DH2MR0.

Chapter 3 contains examples for creating VMkernel port groups. Listing 4.24 demonstrates how to create a VMkernel port group for VSAN.

# LISTING 4.24 Creating a VMkernel port group for VSAN

```bash
$vSwitch0 = Get-VirtualSwitch -VMhost vsanesxi01* \
-Name "vSwitch0"
New-VMhostNetworkAdapter -VMhost vsanesxi01* -PortGroup "VSAN" \
-VirtualSwitch $vSwitch0 -IP 172.20.0.60 \
-SubnetMask 255.255.255.0 -VSANEnabled:$true
```

A minimum of three hosts for VSAN in the cluster must be properly configured to meet the networking requirements, and they need contributing local disks; at least one solid-state drive (SSD) and one hard disk (HDD) are required.

> NOTE For detailed information, be sure to read the Requirements for VSAN: http://vmw.re/bdpq72.

Once all the requirements have been met, VSAN is enabled at the cluster level. In Listing 4.25, we enable VSAN for the cluster and set Disk Mode to Automatic. With Disk Claim Mode set to Automatic, any disks added to hosts will automatically be claimed by VSAN.

# LISTING 4.25 Enabling VSAN on a cluster

```bash
Get-Cluster 'VSAN1' | Set-Cluster -VsanEnabled:$true -VsanClaimMode:Automatic
```

# Disk Groups and Disks

In VSAN, SSDs and HDDs are grouped together per ESXi host in disk groups. Depending on performance and capacity requirements, it may make sense to use multiple disk groups per ESXi host. There are PowerCLI cmdlets to assist with management of disk groups and disks in the VMware.VimAutomation.Storage module, as shown here:

```bash
PS C:\ Get-Command *VSAN*-Module VMware.VimAutomation.Storage

| CommandType | Name | ModuleName |
| --- | --- | --- |
| Cmdlet | Get-VsanDisk | VMware.VimAutomation.Storage |
| Cmdlet | Get-VsanDiskGroup | VMware.VimAutomation.Storage |
| Cmdlet | New-VsanDisk | VMware.VimAutomation.Storage |
| Cmdlet | New-VsanDiskGroup | VMware.VimAutomation.Storage |
| Cmdlet | Remove-VsanDisk | VMware.VimAutomation.Storage |
| Cmdlet | Remove-VsanDiskGroup | VMware.VimAutomation.Storage |
```

Typically, Get commands are used for reporting purposes. New and Remove commands are most likely used for scenarios where VSAN operations are required outside a cluster which has Disk Mode set to Automatic. The New and Remove commands are also used for custom configurations when the Disk Mode setting is Manual. In Listing 4.26, we add a new HDD to an existing disk group. Note that the code is similar to the code used to add local datastores earlier. First, we must identify the canonical name of the disk to add to the VSAN disk group using the Get-StorageLun cmdlet.

# LISTING 4.26 Adding a disk to an existing VSAN disk group

```bash
Get-VMHost vsanesxi01* | Get-ScsiLun -LunType disk | Format-Table CanonicalName
$VSANDiskGroup = Get-VsanDiskGroup -VMHost vsanesxi01* \
Where {$_.Name -eq 'Disk group' \
(0200000006000c29ca92f335c2481dc6ca8357a56692724756)} \
New-VsanDisk -DiskGroup $VSANDiskGroup -CanonicalName naa.6000293bb4ca806b04e8169e1420
```

Conversely, in Listing 4.27 we remove a disk from an existing disk group. Note that this time we can recover the canonical name using the Get-VsanDisk cmdlet. Also note that we need to identify the correct disk group to remove the disk from its (not particularly named).

# LISTING 4.27 Removing a disk from an existing VSAN disk group

```bash
$VSANDiskGroup = Get-VsanDiskGroup -VMHost vsanesxi01* | \
Where {$_.Name -eq 'Disk group' \
(0200000006000c29ca92f335c2481dc6ca8357a56692724756)} \
$VSANDiskGroup | Get-VsanDiskGroup | Format-Table CanonicalName
$VSANDiskGroup | Get-VsanDisk -CanonicalName naa.60002937b02be32b670035b8a435d74e66 \
Remove-VsanDisk -DiskGroup $VSANDiskGroup -Confirm:$false
```

In 4.28 we create a new VSAN disk group containing one SSD and one HDD. As usual, we will need the canonical name of both.

# LISTING 4.28 Creating a VSAN disk group

```bash
Get-VMHost vsanesxi01* | Get-ScsiLun -LunType | Format-Table CanonicalName
$VSANDiskGroup = New-VsanDiskGroup -VMHost vsanesxi01* \
-SsdCanonicalName naa.6000296622408072f5516467bfdfd1630 \
-DataDiskCanonicalName naa.600029c21f3e7a3428ef55c4bfe4081
```

![](img/62596f5acc979040608a4e5111beb7d6_181_0.png)

> NOTE The minimum requirement for a VSAN disk group is one SSD and one HDD.

In 4.29, we remove a VSAN disk group, which will also remove disks within the group.

# LISTING 4.29 Removing a VSAN disk group

```bash
Get-VsanDiskGroup -VMHost vsanesxi01* | \
Where {$_.Name -eq 'Disk group' \
(0200000006000c296622408072f516467bfdfd1630566927247561)} \
Remove-VsanDiskGroup -Confirm:$false
```
