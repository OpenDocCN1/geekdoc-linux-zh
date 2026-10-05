```
Else{
  Write-Warning "Failed to associate IP Pool, check vCenter tasks"
}
```

At this point the vApp is ready to associate the new IP pool with the virtual network that the vAM(s) are using, as shown in Listing 10.21.

# **LISTING 10.21** Associating the IP pool to a virtual network

```
Get-VApp App01 | Get-VM | Get-NetworkAdapter |
  Select-Object -ExpandProperty NetworkName -Unique |
  Get-NetworkAssociation |
    Set-IPPool -Name '10.10.10.0' \
-Datacenter (Get-Datacenter DC1)
```

# # Using IP Assignment

With the IP pool configured, vApps can now be configured to use pools for IP assignment. By default, a new vApp does not have any IP protocols or allocation methods enabled, and its IP allocation policy is set to fixedPolicy. This means, out of the box, vApp IP allocation is disabled. Enabling IP assignment is a two-step process.

+   1. Enable the IP allocation/protocol.
2. Set the IP allocation/protocol.

Retrieve the current IP assignment configuration of a vApp, use the Get-vAppAssignment function in Listing 10.22.

# **LISTING 10.22** The Get-vAppAssignment function

```
#
.SYNOPSIS
  Get the IP assignment for the specified vApp.
.DESCRIPTION
  Get the IP assignment for the specified vApp.
.PARAMETER vApp
```