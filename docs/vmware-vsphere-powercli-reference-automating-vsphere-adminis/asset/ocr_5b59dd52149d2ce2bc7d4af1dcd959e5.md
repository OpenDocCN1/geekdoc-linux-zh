The name or IP of the ESXi host to configure.

.PARAMETER User
The username to connect to the ESXi host with.

.PARAMETER Password
ESXi password.

.PARAMETER IPAddress
The IP address to be assigned to the iSCSI vmnic.

.Parameter Location
The location in the vCenter inventory to add the nESXi host.

```
#>
Param(
[String]$VMHostName
[String]$User
[String]$password
[String]$IPAddress
[Object]$Location = (Get-Datacenter | Select-Object -First
```

# Add our host to vCenter, and immediately enable
# lockdown mode!
$VMhost = Add-VMHost -Name $VMHostName \
-User user \
-Password $Password \
-Location $Location \
-Force

Set-VMHostlockdown -VMhost $VMhost -Enable

```
# Add iSCSI kernel vNIC
$vSwitch = Get-VirtualSwitch -VMHost $VMhost \
-Name 'vSwitch0'
```

# we have to first create a portgroup to bind our vNIC.
$vPG = New-VirtualPortGroup -Name iSCSI \