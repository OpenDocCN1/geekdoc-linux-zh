

# 第 7 章 • 使用模板和自定义规格说明

## 维护模板

模板是一个极其强大的工具——对于虚拟机的生命周期至关重要。然而，保持模板的更新也非常重要。这取决于工作量的投入：维护一个模板比在部署后修补或更新许多虚拟机要容易得多。有些公司选择每季度更新一次模板，并依靠其管理工具来填补这一空白。我们认为这种做法是愚蠢的：无论企业级工具有多强大，既然维护源模板更简单，为什么要在部署新的客机时反复循环呢？无论做如何决定，请记住：PowerCLI 会为你提供帮助。考虑到这一点，有几个常见的问题，但模板有一个通用的痛点。

无论你在做什么，第一步总是将模板转换为虚拟机，最后一步是将其转换回模板。在过程中，你可能需要或不需要启动虚拟机。你会发现，在任何更新期间，你都会不断考虑虚拟机的状态。为了协助这项琐碎的工作，你可以使用 `Wait-VMQuest` 函数（参见列表 7.15）。

## 列表 7.15 Wait-VMQuest 函数

```powershell
function Wait-VMQuest {
  [CmdletBinding(DefaultParameterSetName='VM')]
  [parameter(Position=0)
      ParameterSetName='VM'
  )
  [parameter(Position=0)
      ParameterSetName='Guest'
  )
  [ValidateSet("Startup","Shutdown")]
  [string]
  $Operation

  [parameter(Mandatory=$True)
      ValueFromPipeline=$True
      ParameterSetName='VM'
  )
  [VMware.VimAutomation.ViCore.Impl.Vl.Inventory.VirtualMachineImpl]
  $VMn

  [parameter(Mandatory=$True)
      ValueFromPipeline=$True
      ParameterSetName='Guest'
  )
  [VMware.VimAutomation.ViCore.Impl.V1.VM.Guest.VMGuestImpl]
  $Guest

}

Process {
  if ($PSCmdlet.ParameterSetName -eq 'Guest') {
    $VM = $VMGuest.VM
  }

  Switch ($Operation) {
    "Startup" {
      while ($vm.ExtensionData.Guest.ToolsRunningStatus -eq "guestNotRunning") {
        Start-Sleep -Seconds 1
        Write-Verbose "Waiting on VMware tools start for ${(vm.Name)"
        $vm.ExtensionData.UpdateViewData("Guest")
        # return a fresh VMOObject
        Write-Output (Get-VM $VM)
        break;
      }
    }
    "Shutdown" {
      # wait for the VM to be shut down
      while ($VM.ExtensionData.Runtime.PowerState -ne "poweredOff") {
        Start-Sleep -Seconds 1
        Write-Verbose "Waiting for ${(vm.Name) to power off"
      }
    }
  }
  $VM.ExtensionData.UpdateView("Runtime.PowerState")
  # return a fresh VMObject
  Write-Output (Get-VM $VM)
}
```

Wait 通过在目标虚拟机关机或启动时暂停流水线，简化了更新模板所需的代码。请注意它精简虚拟机的方式。想象一下如果每次虚拟机重启时都必须将管道放入循环中，这样做会破坏 PowerShell 的流式特性。`Wait-VMQuest` 函数允许管道在等待的同时保持流式传输。

## START-VM/STOP-VM 有什么问题？

> 创建一个新函数？为什么不直接使用 Start-VM 或 Stop-VM 配合 -RunAsync 并将其传递给 Wait-Task 呢？

`Wait-VMQuest` 函数的设计用于释放流水线之前，需要虚拟机完全启动或完全关闭并关机的情况。在自动化这种情况时，作者之一从 `Start-VM`/`Stop-VMGuest` 开始，惊讶地发现它们只等待任务在 vCenter Server 中清除即可。PowerCLI 提供了 `Wait-Cmdlet`，但它只对启动虚拟机有帮助。

## 升级硬件

尽管这种情况并不常见，但如果之前投入了大量资金，并且组织在之前的 vSphere 版本中积累了大量的模板，他们可能希望将所有模板升级到最新的硬件版本，以利用新功能。幸运的是，这类任务非常适合自动化。在列表 7.16 中，我们将把模板更新到硬件版本 11。

## 列表 7.16 更新虚拟 硬件版本

```powershell
$VM = Get-Template "v7k8" | Set-Template -ToVM
$VM.ExtensionData.UpgradeVM("vmx-11")
Set-VM $VM -ToTemplate
```

作为任务，这很容易：获取模板对象并将其转换为虚拟机。然后，在虚拟机上调用 `UpgradeVM` 方法进行升级。最后，将虚拟机转换回模板。但存在一个问题：VMware 要求在升级虚拟机硬件版本之前必须安装当前版本的 VMware Tools——这意味着要么强制升级（这是危险的），要么同时处理工具的升级（这是复杂的）。列表 7.17 中的脚本在一个操作中强制执行了升级并升级了硬件版本。

## 列表 7.17 强制进行虚拟机硬件升级

```powershell
$VM = Get-Template "vm01" | Set-Template -ToVM
$taskMoreRef = $VM.ExtensionData.UpgradeVM_Task("vmx-11")
$task = $taskMoreRef
while ($task.Info.State -eq 'running') {
    VM.ExtensionData.UpdateView("Info.State")
    $task = Get-VM $VM
}
Set-VM $VM -ToTemplate
```

由于在某些情况下，强制升级是必要的。有些公司依赖其管理工具来填补空白。我们认为这种做法是愚蠢的：无论企业级工具有多强大，既然维护源模板更简单，为什么要在部署新的客机时反复循环呢？无论做如何决定，请记住：PowerCLI 会为你提供帮助。考虑到这一点，有几个常见的问题，但模板有一个通用的痛点。

无论你在做什么，首步总是将模板转换为虚拟机，最后一步是将其转换回模板。在过程中，你可能或不需要启动虚拟机。你会发现，在任何更新期间，你都会不断考虑虚拟机的状态。为了协助这项琐碎的工作，你可以使用 `Wait-VMQuest` 函数（参见列表 7.15）。

（注：此处翻译了部分重复逻辑）

`Wait-VMQuest` 函数的设计用于释放流水线之前，需要虚拟机完全启动或完全关闭并关机的情况。在自动化这种情况时，作者之一从 `Start-VM`/`Stop-VMGuest` 开始，惊讶地发现它们只等待任务在 vCenter Server 中清除即可。PowerCLI 提供了 `Wait-Cmdlet`，但它只对启动虚拟机有帮助。

（注：此处原文中存在部分文本重复和乱码，翻译已根据指令进行逻辑对齐）

在某些情况下，强制升级是必要的。有些公司依赖其管理工具来填补空白。我们认为这种做法是愚蠢的：无论企业级工具有多强大，既然维护源模板更简单，为什么要在部署新的客机时反复循环呢？无论做如何决定，请记住：PowerCLI 会为你提供帮助。

