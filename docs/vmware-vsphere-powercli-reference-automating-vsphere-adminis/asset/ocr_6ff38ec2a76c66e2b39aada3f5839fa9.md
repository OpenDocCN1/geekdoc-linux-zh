```
$Pool = $queryPool.ipamAddressPools.ChildNodes | where
{$_Name -eq "$IPPool"
$Pool
catch [Exception] {
throw "Error occurred while trying to create $IPPool"
}
}
```

# NSX Controllers

Now you've satisfied the requirements to create an NSX controller, you can add one to the environment. Check the most-up-date documentation from VMware to determine the recommended number of NSX controllers for your environment. Listing 3.29 details how to add an NSX controller.

# LISTING 3.29 Adding an NSX controller to your environment

```
function New-NSXController {
<#n.SYNOPSIS
    Add NSX Controller
.DESCRIPTION
    Add NSX Controller
.PARAMETER NSXIP
    NSX IP Address
.PARAMETER NSXPassword
    The Admin password given during deploy
.PARAMETER IPPoolName
    Name of IP Pool being used
.PARAMETER ControllerName
    New Name for the Controller
.PARAMETER DESCRIPTION
    Description of the controller
.PARAMETER Cluster
    Name of Cluster being deployed to
.PARAMETER Datastore
    Name of Datastore being deployed to
.PARAMETER Network
```