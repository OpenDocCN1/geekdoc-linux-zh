# Permissions

After defining roles, the next step in setting up your security is assigning permissions to users and groups. In case of disaster, it's always nice to be able to restore permissions to a recent state. You can quickly restore access to the vCenter Server without making everyone an administrator (temporarily) until you sort out the permissions. To retrieve permissions, you can use the Get-VIPermission cmdlet:

```
Get-VIPermission
```

| EntityId | Role | Principal | IsGroup Propagate |
| --- | --- | --- | --- |
| Folder-group-di | ReadOnly | VIReport | False True |
| Folder-group-di | Admin | Administrators | True |

You can put permissions on a lot of different object types, you'll want to know what object type the permission is granted. Therefore, you'll need to retrieve the object using the EntityId property and use the GetType() method to retrieve the object type:

```
(Get-View $permission.EntityID).GetType().Name
```

You can simply add the object type to the permission object using the Add-Member cmdlet:

```
$permissions=@ ()
ForEach ($permission in Get-VIPermission) {
$permission | Add-Member -Member Notopperty \
-Name EntityType\
-Value (Get-View $permission.EntityID).GetType().Name
$permissions += $permission
}
$permissions | Export-Clixml "C:\Export\Permissions.xml"
```

# VM Locations

Just like datacenters and clusters, your virtual machines have a specific location. This is represented in your infrastructure by the blue folders. The blue folders are perfect candidates for assigning permissions, so be sure to export every VM's locations. If you don't, users might not be able to access the VMs if they're not restored to the correct location. To export each VM's location, use the Get-ViPath function from Listing 12.3. In addition to the location, you must know which datacenter the