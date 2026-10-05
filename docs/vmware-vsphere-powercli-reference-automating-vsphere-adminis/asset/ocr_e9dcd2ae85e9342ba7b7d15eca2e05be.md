# DEFINE USERS AND THEIR PRIVILEGES

# Granting Privileges

Privileges are found in the vSphere Web Client. When using the Roles wizard, you are able to add new privileges. The privileges are listed in Figure 1.3.

# FIGURE 1.3 vCenter Privileges

![](bbox=[0.239, 0.233, 0.859, 0.489])

How many privileges are there? Think of any action you have ever performed in the vCenter Client. Think about the actions you have not yet come across or used in your everyday job. Add them up, and you will have some idea of how many privileges there are in vCenter Server. Luckily, we are able to use PowerCLI to come up with a scientific answer for this question. You can easily list all privileges available to assign to a user through vCenter Server using the Get-VIPrivilege cmdlet:

```
[vSphere PowerCLI] C:\> Get-VIPrivilege | Select Name,
```

Name Description
---------------- ----------------
Anonymous The only privilege held by sessions ...nView Visibility without read access to an...
Read Grants read access to an entity
Manage custom attributes Add, remove, and rename custom attri...
Set custom attribute Set the value of a custom attribute...
Log event Log a user-defined event on an object