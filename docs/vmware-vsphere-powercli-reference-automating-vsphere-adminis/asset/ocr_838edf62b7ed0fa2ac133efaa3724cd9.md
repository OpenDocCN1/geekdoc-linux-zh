Using the Get-NetworkAssociation function, get the networks that need to be con-figured for the IP pool (Listing 10.19).

# LISTING 10.19 Getting networks that need to be configured

```
Get-Vapp App01 |
Get-VM |
Get-NetworkAdapter |
Select-Object -ExpandProperty NetworkName -Unique |
Get-NetworkAssociation
Network
-----
distributedVirtualPortgroup-dvportgroup-109 vDS01-10.10.10.0
```

In this case, only one network needs to be configured. For that task the Set-IPPool function shown in Listing 10.20.

# LISTING 10.20 The Set-IPPool function

```
#
.SYNOPSIS
Modify an existing IP Pool within vCenter
.DESCRIPTION
Modify an existing IP Pool within vCenter
.PARAMETER Datacenter
Datacenter to create the new IP Pool in.
.PARAMETER Name
Pool name.
.PARAMETER Name
New pool name. Must be unique.
.PARAMETER DnsDomain
Dns Domain. For example, vmware.com. This can be an empty string if no domain is configured.
.PARAMETER DNSSearchPath
DNS Search Path. For example, eng.vmware.com;vmware.com
.PARAMETER HostPrefix
Prefix for hostnames.
.PARAMETER HttpProxy
The HTTP proxy to use on this network
```