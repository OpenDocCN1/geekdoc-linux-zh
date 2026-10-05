# CHAPTER 5 • USING ADVANCED VSPHERE FEATURES

Note that for the particular ESXi host in Listing 5.24 no Active Directory authentication has been defined; hence no domain membership is listed. To join the host to a domain, pipe the output of the Get-VMHostAuthentication cmdlet into the Set-VMHostAuthentication command.

# LISTING 5.25 Joining an ESXi host to a domain

```
$domainname = "powercli.lan"
$credential = Get-Credential
$hostname = "esxi-01.powercli.lan"

$splat = @{
  'Domain' = $domainname;
  'Credential' = $credential;
}

Get-VMHost $hostname | 
  Set-VMHostAuthentication @splat -JoinDomain
```

Now when you execute the Get-VMHostAuthentication against the host, you can see that it is joined to the domain.

By the default administrators group for the ESXi host is for ESX Admins, but since this is a well-known group, it may be undesirable to leave it from a security perspective. You can change the administrators group for the host by adjusting the value of a particular option: Config.HostAgent.plugins.hostsvc.exadmins-Group. You can use the web or desktop clients to modify the settings or use a simple PowerShell function, as shown in Listing 5.26.

# LISTING 5.26 Set-VMHostADAdminGroup function

```
function Set-VMHostADAdminGroup {
  <#SYNOPSIS
  Sets the Active Directory group to be used for ESXi host administrators.

  .EXAMPLE
  Get-VMHost host1 | Set-VMHostADAdminGroup -Group "VM Admins"

  .PARAMETER VMHost
  [VMware.Automation.ViCore.Impl.V1.Inventory.VMHost]
  The host to modify.
```