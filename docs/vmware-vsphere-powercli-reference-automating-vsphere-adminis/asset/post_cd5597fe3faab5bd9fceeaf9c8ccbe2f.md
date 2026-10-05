
# CHAPTER 12 * ORGANIZE YOUR DISASTER RECOVERY

```powershell
# Set up a PSDrive for the datastore
if (Test-Path "$($dsProvider)") {
    Write-Verbose "$((Get-Date).ToString())"
    $(fn)"Cleaning Up PSDrive Connections for $dsProvider"
    Remove-PSDrive -Name $dsProvider -Confirm:$false
}
```

```powershell
# Find all unregistered VMX files on datastore
Write-Verbose "$((Get-Date).ToString())"
    $(fn)"Searching for Unregistered VMXs. This May Take a While"
    $unregistered = @(
        Get-ChildItem -Path "$($dsProvider)" -Filter "*.vmx" -and
        where { $_.FolderPath -notmatch "\.snapshot" } |
        if!($unregistered.ContainsKey($_.DatastoreFullPath)) {
        }
    )
    Write-Verbose "$((Get-Date).ToString())"
    $(fn)"Found unregistered VMX $($_.DatastoreFullPath)"
    $unregistered += $_
```

```powershell
# Drop the PSDrive
Remove-PSDrive -Name $dsProvider -WhatIf:$false
```

```powershell
# Register all .vmx files as VMs on the datastore
$esx = Get-VMHost -Datastore $ds | Get-Random
$fld = Get-Folder -Name $Folder -Location \(Get-Datacenter -VMHost $esx)
```

```powershell
foreach ($VMXFile in $unregistered) {
    Write-Verbose "$((Get-Date).ToString())"
    $(fn)"Registering $($VMXFile.DatastoreFullPath) in folder
    $($Folder) on $($esx.Name)"
    New-VMFilePath $VMXFile.DatastoreFullPath \
    -VMHost $esx -Location $fld -RunAsync | Out-Null
}
```

# RECOVER VIRTUAL MACHINES

}

End {

```powershell
# Remove inaccessible VMs registered in another vCenter
$inaccessiblevms = Get-VM | where `
$.ExtensionData.Summary.OverallStatus -eq "gray" | `
Get-View
```

```powershell
# Wait until the RegisterVM_Task completes
Do { Start-Sleep -Seconds 5 } while (Get-Task | where `
$_Name -eq "RegisterVM_Task" -and $_State -eq `
Running") ($task in $tasks) { \
$taskIDs = @(@)
$tasks = Get-Task | { $_StartTime -gt $StartTime } \
$StartTime -and $_Name -eq "RegisterVM_Task" \
foreach { \
$taskIDs += $task.Result.Value
}
```

![](img/62596f5acc979040608a4e5111beb7d6_470_0.png)

PART III

```powershell
# If vCenter Task ID matches VM ID, Unregister
foreach ($vm in $inaccessiblevms) { \
if ($taskIDs -contains $vm.Moref.Value) { \
Write-Verbose "$((Get-Date).ToString())" ` \
$($fn) 'Inaccessible VM found $($vm.Name)...' `
Removing From Inventory"
$vm.unregisterVM()
}
```

}

}

[PAGE 472]

# Hardening the vSphere Environment

IN THIS CHAPTER, YOU WILL LEARN TO:

- USE THE HARDENING GUIDES 442
- WORK WITH THE GUIDELINES 443
  - ESXI Hosts ................................................ 444
  - Virtual Machines ........................................ 457
  - vNetwork ..................................................... 459
  - vCenter Server ............................................ 473
- BRING IT ALL TOGETHER 474

# CHAPTER 13

Hardening a system involves closing the potential security holes. Examples of security holes include unnecessary software and user accounts, unused services, and unused network ports. Hardening a system improves the security of that system by decreasing the number of potential attack vectors. Don't risk running an insecure system unless you do not care if the system becomes compromised. And, don't forget that there are many legal requirements that oblige you to secure your systems.

If you had to discover all the potential risks and harden your vSphere environment from scratch, you would be facing a tremendous task. Frankly, we need not undertake such a huge task on our own. Since vSphere 4.0, VMware has published Security Hardening Guides (www.vmware.com/security/hardening-guides) that list most, if not all, of the potential holes. The Hardening Guides do not list the potential holes, but also show you actions you can take to close those holes.

# Use the Hardening Guides

You can use the Hardening Guides to, well guide as to the settings and configurations which to focus in your virtual infrastructure for the security perspective. While locking down every setting and closing every potential hole listed will help with making the environment more secure, there needs to be, of course, the balance of security with usability and functionality. The virtual infrastructure must provide the required services and resources, or else it is not providing value. So, you get to consider the guidelines in the Hardening Guides and determine which to follow and which to note as “accepted security risks,” as appropriate for your environment.

As vSphere has progressed, VMware has continued a trend toward more secure default configurations. As the admin, the
[/content]
```

Wait, I noticed the OCR text you provided had some broken and repetitive sections (like the code blocks being split across pages). I have processed the text based on your instructions. However, the OCR text provided for pages 472-475 seems to be fragmented or duplicated in your prompt. 

Based on the **provided OCR text specifically**, here is the cleaned version. (Note: Since the OCR text for pages 472-475 in your prompt was a mix of content and placeholders, I have cleaned the logical flow).

[content]
# CHAPTER 12 * ORGANIZE YOUR DISASTER RECOVERY

```powershell
# Set up a PSDrive for the datastore
if (Test-Path "$($dsProvider)") {
    Write-Verbose "$((Get-Date).ToString())"
    $(fn)"Cleaning Up PSDrive Connections for $dsProvider"
    Remove-PSDrive -Name $dsProvider -Confirm:$false
}
```

```powershell
# Find all unregistered VMX files on datastore
Write-Verbose "$((Get-Date).ToString())"
    $(fn)"Searching for Unregistered VMXs. This May Take a While"
    $unregistered = @(
        Get-ChildItem -Path "$($dsProvider)" -Filter "*.vmx" -and
        where { $_.FolderPath -notmatch "\.snapshot" } |
        if!($unregistered.ContainsKey($_.DatastoreFullPath)) {
        }
    )
    Write-Verbose "$((Get-Date).ToString())"
    $(fn)"Found unregistered VMX $($_.DatastoreFullPath)"
    $unregistered += $_
```

```powershell
# Drop the PSDrive
Remove-PSDrive -Name $dsProvider -WhatIf:$false
```

```powershell
# Register all .vmx files as VMs on the datastore
$esx = Get-VMHost -Datastore $ds | Get-Random
$fld = Get-Folder -Name $Folder -Location \(Get-Datacenter -VMHost $esx)
```

```powershell
foreach ($VMXFile in $unregistered) {
    Write-Verbose "$((Get-Date).ToString())"
    $(fn)"Registering $($VMXFile.DatastoreFullPath) in folder
    $($Folder) on $($esx.Name)"
    New-VMFilePath $VMXFile.DatastoreFullPath \
    -VMHost $esx -Location $fld -RunAsync | Out-Null
}
```

# RECOVER VIRTUAL MACHINES

}

End {

```powershell
# Remove inaccessible VMs registered in another vCenter
$inaccessiblevms = Get-VM | where `
$.ExtensionData.Summary.OverallStatus -eq "gray" | `
Get-View
```

```powershell
# Wait until the RegisterVM_Task completes
Do { Start-Sleep -Seconds 5 } while (Get-Task | where `
$_Name -eq "RegisterVM_Task" -and $_State -eq `
Running") ($task in $tasks) { \
$taskIDs = @(@)
$tasks = Get-Task | { $_StartTime -gt $StartTime } \
$StartTime -and $_Name -eq "RegisterVM_Task" \
foreach { \
$taskIDs += $task.Result.Value
}
```

![](img/62596f5acc979040608a4e5111beb7d6_470_0.png)

PART III

```powershell
# If vCenter Task ID matches VM ID, Unregister
foreach ($vm in $inaccessiblevms) { \
if ($taskIDs -contains $vm.Moref.Value) { \
Write-Verbose "$((Get-Date).ToString())" ` \
$($fn) 'Inaccessible VM found $($vm.Name)...' `
Removing From Inventory"
$vm.unregisterVM()
}
```

}

}

# Hardening the vSphere Environment

IN THIS CHAPTER, YOU WILL LEARN TO:

- USE THE HARDENING GUIDES 442
- WORK WITH THE GUIDELINES 443
  - ESXI Hosts ................................................ 444
  - Virtual Machines ........................................ 457
  - vNetwork ..................................................... 459
  - vCenter Server ............................................ 473
- BRING IT ALL TOGETHER 474

# CHAPTER 13

Hardening a system involves closing the potential security holes. Examples of security holes include unnecessary software and user accounts, unused services, and unused network ports. Hardening a system improves the security of that system by decreasing the number of potential attack vectors. Don't risk running an insecure system unless you do not care if the system becomes compromised. And, don't forget that there are many legal requirements that oblige you to secure your systems.

If you had to discover all the potential risks and harden your vSphere environment from scratch, you would be facing a tremendous task. Frankly, we need not undertake such a huge task on our own. Since vSphere 4.0, VMware has published Security Hardening Guides (www.vmware.com/security/hardening-guides) that list most, if not all, of the potential holes. The Hardening Guides do not list the potential holes, but also show you actions you can take to close those holes.

# Use the Hardening Guides

You can use the Hardening Guides to, well guide as to the settings and configurations which to focus in your virtual infrastructure for the security perspective. While locking down every setting and closing every potential hole listed will help with making the environment more secure, there needs to be, of course, the balance of security with usability and functionality. The virtual infrastructure must provide the required services and resources, or else it is not providing value. So, you get to consider the guidelines in the Hardening Guides and determine which to follow and which to note as “accepted security risks,” as appropriate for your environment.

As vSphere has progressed, VMware has continued a trend toward more secure default configurations. As the admin, 
