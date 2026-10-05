# ZIP Files

New VMware patches are distributed in ZIP format, which is supported by the PowerCLI Core cmdlet Install-VMHostPatch. There are a few different ways to make the patch file accessible to the ESXi host to be updated. If the patch needs to be deployed to more than one host, then it makes good sense to copy that patch to a shared datastore that is available to all the hosts requiring it. Listing 14.21 demonstrates how to copy a folder patches for vSphere 5.5 U2 to a shared datastore.

# 14.21 Copying a patch to a shared datastore

```
$Datastore = Get-Datastore "NFS10"
New-PSDrive -Location $Datastore -Name ds -PSProvider \
VimDatastore -Root "\"
New-Item -ItemType Directory 'ds:\Patches-from-esxi5.5-5.5_update02'
Copy-DatastoreItem 'C:\Scripts\update-from-esxi5.5-5.5_update021*' -Recurse \
Destination=$ds:\Patches-from-esxi5.5-5.5_update02
```

Now that the patch files are available to ESXi hosts via a shared datastore, you can run the commands in Listing 14.22 to install the patch. Note that Install-VMHostPatch requires the full path to the metadata.zip file in the folder containing the patches.

# 14.22 Installing a patch with Install-VMHostPatch

```
$Datastore = Get-Datastore "NFS10"
$FilePath = 'Patches/update-from-esxi5.5-5.5_update02/metadata.zip'
$DatStoreURL = $Datastore.ExtensionData.Info.Url -Replace 'ds://'
$FullPath = $FilePath
$VMHost = Get-VMHost vesxi10.sunnydale.local
$VMHost = Set-VMHost -State Maintenance -Confirm:$false
$VMHost = Install-VMHostPatch -HostPath $FullPath
$VMHost = Restart-VMHost -Confirm:$false
```

![](bbox=[0.903, 0.343, 0.925, 0.437])

PART III