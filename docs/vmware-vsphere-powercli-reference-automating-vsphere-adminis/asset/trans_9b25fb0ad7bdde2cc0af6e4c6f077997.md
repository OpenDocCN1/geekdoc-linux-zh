

# 第 12 章 整理你的灾难恢复

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

# 恢复虚拟机

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

第三部分

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

[第 472 页]

# 加固 vSphere 环境

在本章中，你将学习：

- 使用加固指南 442
- 参考指南 443 工作
  - ESXI 主机 ................................................ 444
  - 虚拟机 ........................................ 457
  - vNetwork ..................................................... 459
  - vCenter Server ............................................ 473
- 综合运用 474

# 第 13 章

加固系统涉及关闭潜在的安全漏洞。安全漏洞示例包括不必要的软件和账户、未使用的的服务以及未使用的端口。加固系统通过减少潜在的攻击向量来提高系统的安全性。除非你不在乎系统是否被破坏，否则不要运行不安全的系统。此外，不要忘记有许多法律要求你保护好系统。

如果你必须从零开始发现所有潜在风险并加固你的 vSphere 环境，你将面临一项巨大的任务。坦率地说，我们不需要独自完成这项巨大的任务。从 vSphere 4.0 开始，VMware 发布了安全加固指南（www.vmware.com/security/hardening-guides），列出了大部分（并非全部）的安全漏洞。加固指南不仅列出了这些漏洞，还展示了你可以采取的操作来关闭这些漏洞。

# 使用加固指南

你可以利用加固指南，从安全角度关注你虚拟基础设施中的设置和配置。虽然锁定每一个设置并关闭列出的每一个漏洞有助于使环境更加安全，但你需要在安全性与易用性功能之间取得平衡。虚拟基础设施必须提供所需的服务和资源，否则它将毫无价值。因此，你需要考虑加固指南中的内容，并决定遵循哪些、将哪些标记为“接受的安全风险”，这取决于你的具体环境。

