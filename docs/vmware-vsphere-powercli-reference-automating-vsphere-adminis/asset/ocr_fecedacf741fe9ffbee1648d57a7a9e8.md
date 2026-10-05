# RESTORE YOUR VCENTER SERVER

.PARAMETER Reconnect

An optional switch parameter to force a disconnect first

.EXAMPLE

```
Connect-VMHost -VMHost MyESX -User root -Password password
```

.EXAMPLE

```
Get-VMHost myESX | Connect-VMHost -User root -Password password
```

```
-Reconnect
```

.EXAMPLE

```
Get-VMHost myESX | Connect-VMHost -Credential (Get-Credential)
#>
```

```
Param (
    [Parameter (ValueFromPipeline = $true, Position = 0,
Mandatory = $true,
HelpMessage = "Enter an ESX(i) host
entity)]
    [VMware.Automation.ViCore.Impl.V1.VMHostImpl]$vmhost,
[Parameter (Mandatory = $true, ParameterName = "$cred",
HelpMessage = "Enter a PSCredential
object)]
    [System.Management.Automation.PSCredential]
    [Parameter (ParameterName = "$user")
ValidateNotNullOrEmpty()]
[string]$User = "root",
[Parameter (Mandatory = $true, ParameterName = "$user",
HelpMessage = "Enter the root account
password)]
    [string]$Password,
[switch]$Reconnect) {
```

```
Process {
    $vmHostView = $vmHost | Get-View -Property
    # Create a new HostConnectSpec
    $objHostConnectSpec = New-Object VMware.Vim.
HostConnectSpec
    if ($credential) {
        $objHostConnectSpec.username =
        $credential.GetNetworkCredential().UserName
```

![](bbox=[0.903, 0.335, 0.915, 0.435])

PART III