
Once the escli command has been converted, you might want to consider wrapping it into a PowerShell function, similar to the Get-VMHostCSIBinding and Set-VMHostCSIBinding functions, in order to make it feel more like a native PowerShell CLI cmdlet.

## Setting a Multipath Policy

If you are using Fibre Channel SAN, it's a good practice to use multiple HBA connections to the SAN whenever possible. With multiple HBA connections in place, should an active path to your SAN fail, a passive path is then made active so that storage traffic continues and the ESXI hosts remain connected to the storage for your VMs. Multipathing in vSphere makes it simple to use/Active Multipathing instead of Active/Passive if the array supports it. This means that not only you have resiliency in case of a failed path, you are also able to boost your storage performance by using multiple paths to the storage. The Native Multipathing Plug-in (NMP) module communicates with the Storage Array Type Plug-in (SATP) and the Path Selection Plug-in (PSP) to make these multipathing work.

> Contact your storage vendor before continuing further to support your storage array and to learn which to use SATP and PSP on the ESXi host.

Assuming your storage array is supported for multipathing and you have chosen the correct SATP to use, you need to configure the PSP on each LUN where you wish to multipathing. The PSP is per LUN and can take three values: Fixed, MostRecentlyUsed, or Robin—check your vendor documentation for which one to use. You can use a mixture of selections, it's a good idea to find what is currently used. To do that, you can use the Get-ScsLun cmdlet and select MultipathPolicy property.

```
Get-VMHost vsxi05* | Get-ScsLun | Select CanonicalName, MultipathPolicy
```

| CanonicalName | MultipathPolicy |
| --- | --- |
| mpx.vmhba32:C0:T0:L0 | Fixed |
| naa.600616019a93408059cb521a9bca22 | MostRecentlyUsed |
| naa.600016019a34003a8ef82239bca22 | MostRecentlyUsed |
| aa.600016019a3400185f0486a9bca22 | MostRecentlyUsed |

Typically with Fibre Channel SANs, you will be working with LUNs, not just three as in the previous example. Even making the change for the PSP to Round Robin via the GUI for three LUNs would soon become tedious, so by using this via PowerCLI can save you a lot of time. By-MultipathPolicy parameter of the Set-ScsLun cmdlet, you can make the change across your Fibre Channel LUNs in one line of code. You can also use Where-Object to filter out non-Fibre Channel LUNs, as we did in Listing 4.13.

### Listing 4.13 Setting multipath policy for multiple LUNs

```
GetVMHost vesxi05* | Get-ScsLun | Where {$_.CanonicalName -like 'naa.6000*'} | Set-ScsLun -MultipathPolicy "RoundRobin"
```

## Setting the Default PSP for an SATP

Once LUNs have been updated with the correct PSP, you may wish to update the Default PSP for the SATP in use so that any additional LUNs added in the future will be correct at the time of creation.

![](img/62596f5acc979040608a4e5111beb7d6_173_0.png)

> NOTE An alternative method to explicitly setting the Multipath policy via Set-ScsLun in Listing 4.13 is to set the default PSP (as we are about to demonstrate), place host in Maintenance mode, and reboot. This has the advantage that LUNs would not be tied to a specific PSP should future changes to the Default PSP be necessary and only reboot necessary again to change LUNs to a new PSP.

We can achieve this via the Get-ExCli method described earlier in the chapter. Listing 4.14 demonstrates how, for example, to set the default PSP for the SATP VMW_SAT_ALUA to Round Robin (VMW_PSP_RR).

### Listing 4.14 Setting the default PSP for an SATP

```
$DefaultPSP = 'VMW_PSP_RR'
$SATP = 'VMW_SAT_ALUA'
$EsxCli = Get-ExCli -VMHost vesxi05*
$EsxCli.storage.nmp.satp.set($null,$DefaultPSP,$SATP)
```

## Configuring Storage I/O Control

Storage I/O Control (SIOC) uses the average latency of all virtual disks across a datastore to calculate latency. This average is then weighted by the number of input/output operations per second (IOPS). When this weighted latency goes above the configured threshold, SIOC limits throughput to the array by resizing the device queue. Therefore, SIOC only runs during times of congestion.

SIOC has seen significant changes since the first edition of this book. First, NFS datastores have been supported since vSphere 5.0; all of storage protocol-based datastores can be enabled for SIOC. Next, PowerCLI version 5.0 added the StorageIOControlEnabled parameter to the Set-Datastore cmdlet. Consequently, the SIOC functions described in the first edition of this book are no longer required. SIOC can be enabled on a datastore without pre-checks for NFS and can be turned on a simple one-line command (Listing 4.15).

- Listing 4.15 Enabling SIOC on a datastore

```
Set-Datastore -Datastore ISCI01 -StorageIOControlEnabled=$true
Select-Object Name, StorageIOControlEnabled
```

## Datastore Clusters

Datastore clusters were introduced in vSphere 5 and enable the grouping of individual datastores into logical clusters to permit easier management. Coupled with the Distributed Resource Scheduler (SDRS), datastores can now be managed by vCenter in a similar fashion to VMs with DRS. With available space and storage performance statistics, vCenter is able to migrate VMs around the datastore cluster to improve resource utilization.

PowerCLI introduced support for datastore clusters in version 5.1. Listing 4.16 demonstrates how to create a datastore cluster.

- Listing 4.16 Creating a datastore cluster

```
New-DatastoreCluster -Name DatastoreCluster -Location Prod
```

Only the name and location can be specified at creation. To configure some interesting settings, such as SDRS and I/O metrics, you must use the Set-Datastore cmdlet. Listing 4.17 demonstrates how to enable SDRS with Full Automation, a 10ms latency threshold, and 90% space utilization.

- Listing 4.17 Enabling SDRS and I/O metrics on a datastore

```
Set-Datastore -DatastoreCluster Datastore1 -AutomationLevel FullyAutomated -SIOC=$true -OLatencyThreshold 10 -SpaceUtilizationThreshold 90
```

> NOTE When the Storage DRS automation level is set to Fully Automated, you do not need to specify the EvacuateAutomatically parameter of Set-Datastore because Storage DRS will migrate all machines automatically.

Now that the datastore cluster is configured as desired, you need to populate it with datastores. In Listing 4.18, we add three.

- Listing 4.18 Adding datastores into a cluster

```
$DatastoreCluster = Get-DatastoreCluster Datastore1
Get-Datastore | Move-Datastore -Destination $DatastoreCluster
```

> TIP For more information on how to use wildcards in PowerShell, type help about_wildcards.

Datastores in a cluster cluster have a Maintenance mode feature, evacuating VMs from that datastore with no downtime. This is similar to putting an ESXi host into Maintenance mode (Listing 4.19).

- Listing 4.19 Placing a datastore in Maintenance mode

```
Set-Datastore -1 -MaintenanceMode=$true
```

## Storage Policies

Storage Policy-Based Management (SPBM) enables vSphere administrators to better handle the demands of storage provisioning, capacity planning, and differing service levels. By allocating a VM to a storage policy rather than a specific datastore or datastore cluster, the micro-management nature of VM placement is taken away and dealt with in a policy-based fashion. For example, allocate a VM to a Tier 1 storage policy and let the technology place the VM on This is smarter than waiting for the administrator to find out which datastores are on Tier 1 and manually allocating the VM to that datastore. Automation tools such as PowerCLI can take advantage of the SPBM API to make this a further step. The SPBM cmdlets are part of the VMware.VmAutomation.PowerCLI module.

- TIP Storage policies can be based on capabilities advertised by the storage array, vSphere common capabilities, and vCenter tags. It is well worth checking out policies based on the capabilities of your array; check with your vendor for details. For the purposes of this chapter, we will be using vCenter tags until we cover Virtual SAN.

### Adding Tags to Datastores

To be able to allocate datastore to a policy, you first need to distinguish storage by one of the available methods—we will be using tags.

- NOTE For the purposes of this chapter, we are using pre-created tags to assign to the datastores, vCenter tags are covered in more depth in Chapter 5, "Using Advanced vSphere Features," which contains the necessary details for creating and managing your own tags.

Listing 4.20 demonstrates how to retrieve an existing tag, Silver Storage, and assign it to each of the datastores in datastore cluster `DatastoreCluster0`.

### Listing 4.20 Assigning a tag to all datastores in a datastore cluster

```
$SilverTag = Get-Tag 'Silver Storage'
Get-DatastoreCluster DatastoreCluster0 | Get-Datastore |
New-TagAssignment -Tag $SilverTag
```
