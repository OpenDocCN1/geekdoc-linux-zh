# Manage Users

vCloud Director cmdlets do not allow for adding or modifying users, they are available for reporting and auditing. These cmdlets allow administrators to quickly and easily create these reports to validate the settings, roles, and properties of users in each org. The Get-CIUser and Get-CIRole cmdlets can be used together for more in-depth views of the users configuration.

```
Get-Org | Foreach {
  Write-Host | Org:($_.Name) " -ForegroundColor Green;
  Get-CIUser -Org $_ | Foreach {
    Write-Host $_.Name -ForegroundColor yellow;
    Get-CIControl -user $_.Name}
  }
```

# Access Control Rules

It is critical to create rules and rights for objects within your private cloud environment. As in vCenter, you can define rules and rights for different users and groups within vCloud Director. It is wise to review each access control periodically. In addition to the rules and rights given to users and groups, you can set control levels on objects within your vCloud environment.

# Creating Access Control Rules

To create new access rules, use the New-CIAccessControlRule cmdlet. It requires several parameters to succeed: -AccessLevel,-User -EveryoneInOrg,-Entity. The access level allows you to specify Read, ReadWrite, or FullControl permissions for the selected object. You can choose specific users for a given access level, or set it for everyone in the organization of the selected object. Entity refers to the object that will receive the access control rules; this may be either a catalog or a vApp.

Let's say that you do not want others to be able to change the configuration of a specific vApp. You could create a new access control rule that gives everyone read-only access to that vApp:

```
New-CIAccessControlRule -Entity 'SecuredVApp' -EveryoneInOrg -AccessLevel "Read" -Confirm:$false
```