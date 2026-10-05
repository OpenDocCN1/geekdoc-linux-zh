# CHAPTER 12 * ORGANIZE YOUR DISASTER RECOVERY

```
$entityView = Get-View -ViewType $permission.Entity \
  -Property Name -Filter \
  @("Name" = ${(permission.Entity.Name | \
  Escape-MetaCharacters))
$newPermission = New-Object VMware.Vim.Permission
$newPermission.principal = $permission.Principal
$newPermission.group = $permission.IsGroup
$newPermission.propagate = $permission.Propagate
$newPermission.roleId = $(Get-VIROle $permission.Role).id

$authMgr.SetEntityPermissions($entityView.MoreRef, \
$newPermission)
```

# Networking

Once your permissions are set, your folders are in place, and the virtual structure is set up, you can restore the virtual distributed switch. If you are restoring the distributed switch back onto the original vCenter server from which it was exported, the ESXI hosts should reconnect to the switch automatically. If you are importing the distributed switch configuration onto a new vCenter server, you will need to reconnect the vmnics of the ESXI distributed switch to each host.

Start by importing the virtual distributed switch; if you have more than one virtual datacenter, you will need to specify the correct folder using the Get-Datacenter cmdlet at the beginning of the Get-Datacenter cmdlet

```
$Folder = Get-Datacenter Main-DC | Get-Folder -Name Network \
New-VDS -Name "VDS-Primary" -Location $Folder \
  -BackupPath "c:\Temp\VDS-Primary.zip"
```

If you are restoring a distributed switch that already exists in vSphere, restoring the switch overwrites the current settings of the distributed switch and its port groups. Note that it does not delete existing port groups that are not part of the configuration file.

Once you have imported your distributed switch and are ready to reconnect your host's vmnics to their respective port groups, you can leverage the Import-VMHostVmnicVDSConfiguration cmdlet in Listing 12.10 to restore the configuration that you had exported earlier in the chapter.