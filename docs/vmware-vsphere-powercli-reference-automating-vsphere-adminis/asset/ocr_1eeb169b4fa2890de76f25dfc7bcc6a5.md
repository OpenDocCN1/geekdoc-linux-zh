[int]$Hours = 0,
[int]$Minutes = 0

```
process{
  $ts = New-TimeSpan -Hours $Hours -Minutes $Minutes -Days $Days
  Get-Task | Where-Object {_.StartTime -gt ((Get-Date) - $ts)}
}
```

# Get-ClIView

Just as PowerShell has the Get-View cmdlet for vSphere, which allows administrators to return vSphere objects and work with the underlying vSphere API, the Get-ClIView cmdlet fulfills the same function for vCloud Director as well as vCloud Air. Get-ClIView is a very powerful way to not only retrieve more detailed information about the target object, but also to perform tasks via the API.

# ExtensionData

ExtensionData is a property that exposes information for a given object via the API. It allows users to dig down deep into a given object. The information returned by the ExtensionData property can be used for reporting, for troubleshooting, or even for invoking API tasks. Let's see what is returned when looking at both a vApp and its virtual machines.

In this example, we have created a variable, $vApp, which is populated with the returned ClIView object:

```
$vApp = Get-ClIVApp Nested | Get-ClIView
$vApp
```

```
OvfDescriptorUploaded : True
Owner : VMware.VimAutomation.Cloud.Views.Owner
InMaintenanceMode : False
```