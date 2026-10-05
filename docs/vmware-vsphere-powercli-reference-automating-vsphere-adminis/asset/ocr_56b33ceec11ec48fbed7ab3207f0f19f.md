To create the datastore on LUN, you need to provide what is known as the canonical name to the New-Datastore cmdlet. The $LocalLun variable includes the CanonicalName property, which you can retrieve. It will look something like this:

```
$LocalLun.CanonicalName
aa.60022180a9de3f00114e4d006df11de
```

You can now create the datastore using the New-Datastore cmdlet (4.7).

# Creating a datastore on local storage

```
$LocalLun = Get-VMHost vesxi05* | Get-ScsiLun -LunType disk |
Where { $_Model -match "PERC 6/i" }
New-Datastore -Vmfs -VMHost vesxi05* -Name LocalStorage \
-Path $LocalLun.CanonicalName
```

# NAME THAT LUN

The Network Address Authority (NAA) identifier just seen is an industry standard method of generating a unique number to identify a LUN. This value remains the same when accessed by any ESXI host. In terms of object returned by the Get-SCSLun cmdlet, it is referred to as the CanonicalName property—which was the more commonly used term when identifying LUNs in ESX 3.

# SAN Storage

For Fibre Channel or iSCSI storage, you can use the Get-ScsiLun cmdlet to identify LUNs made available from a particular vendor. For instance if you have the storage from the Vendor NetApp, the Vendor property is help tagged as NetApp:

```
$ISCLun = Get-VMHost vesxi05* | Get-ScsiLun -LunType disk |
Where { $_Model -match "NetApp" }
```

With SAN-based datastores, you will likely be dealing with multiple datastores. Let's say you need to add 10 new iSCSI datastores and a naming convention for datastores in the format iSCSI_01, iSCSI_02, and so on. For these datastores, we will start with iSCSI_10. Listing 4.8 provides the code to create them.