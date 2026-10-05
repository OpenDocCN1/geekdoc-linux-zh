# CHAPTER 12 * ORANIZE YOUR DISASTER RECOVERY

To assist in the registration process, you can use the Register-VMX function, which is shown in Listing 12.13. This function provides much more flexibility you can search for one or more datastores, a host, a cluster, or a datacenter. Also, it speeds up by using SDK objects instead of the datastore provider, which is more than welcome in a larger environment.

# LISTING 12.13 Searching datastores for VMX files

```
function Register-VMX {
<#n.SYNOPSIS
Find and registers VMX's that are not currently in vCenter.
.DESCRIPTION
Find and register VM's that are on a datastore but not
registered in vCenter
.NOTES
Source: Automating vSphere Administration
Authors: Luc Dekens, Arnim van Lieshout, Jonathan Medd,
Alan Recnof, Glenn Sizembian, Brian Graf,
Andrew Sullivan
.PARAMETER Cluster
Name of Cluster to be searched (searches all datastores
associated to that cluster)
.PARAMETER Datastore
Name of Datastore to search for VMX files
.PARAMETER Folder
Name of Target VM folder in vCenter
.EXAMPLE
Register-VMX -Cluster Main-CL -Verbose -Confirm:$false
.EXAMPLE
Register-VMX -Datastore ISCSi-900a -Verbose
.EXAMPLE
Get-Datastore MyDS | Register-VMX -WhatIf -Verbose
#>
[CmdletBinding(SupportsShouldProcess = $True)]
[OutputType([string[]])]
param (
[parameter(ParameterName = 'Cluster')]
[PSObject]$Cluster,
```