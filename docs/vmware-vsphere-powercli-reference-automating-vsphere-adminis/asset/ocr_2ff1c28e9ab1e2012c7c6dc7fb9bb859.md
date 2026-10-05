New-VIRole -Name $role.Name -Privilege ($privileges | 
? {$role.PrivilegeList -contains $._id})

# Permissions

Now that the roles are in place, you can start to restore the permissions throughout your inventory. New permissions can be assigned using the New-VIPermission cmdlet. Because you can assign permissions to all of objects in your inventory, you'll first need to determine what object type you want to restore permissions in order to use the right cmdlet to retrieve that. If the object is a folder, you'll need to use the Get-Folder cmdlet. If the object is a datacenter, you'll need to use the Get-Datacenter cmdlet, and so forth.

However, this can be more easily achieved using the Get-View cmdlet and making of the full SDK objects, this cmdlet allows you to specify the object type and hence can be used to retrieve all of objects. Because the Get-View cmdlet, you must specify a filter to indicate the objects you want to return. For example, to retrieve a VM called VM001, you would use the following:

```
Get-View "VirtualMachine" -Filter @{"Name" = "VM001"}
```

One important thing to know is that Get-View filters are regular expressions. Regular expressions can contain metacharacters special characters. These characters can also be part of the object's name, you'll have to escape them using the \ character. We've created a small helper function for this in List 12.9.

# LISTING 12.9 Escaping regular expression metacharacters

```
filter Escape-MetaChar {
  ForEach ($MetaChar in '^', '$', '(', ')', '[', ']', '{', '}', '.', '*', '\', 
  '*', '+', '?', '|', '!', ' '^', '<', '>', '-', '&') {
    $_.replace($MetaChar, "\\$MetaChar")
  }
}
```

To assign permissions using the SDK, use AuthorizationManager and its SetEntityPermissions() method. This method accepts a ManagedObjectReference to an inventory object and a VMware.Vim.Permission object:

```
ForEach ($permission in Import-Clixml 
  "C:\Export\Permissions.xml") {
```