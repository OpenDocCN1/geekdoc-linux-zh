
# 第 7 章 • 使用模板和定制化规范

## 列表 7.11 将定制化克隆到非持久性规范

```powershell
# Clone our Spec
$Spec = Get-OSCustomizationSpec 'Win2012R2' |
New-OSCustomizationSpec -Name 'tmp01' -Type NonPersistent
# Update Spec with our desired IP information
Get-OSCustomizationNiMapping -Spec $Spec |
Set-OSCustomizationNiMapping -IPMode Static|
-IpAddress '192.168.2.42' |
-SubMask '255.255.255.0' |
-DefaultGateway '192.168.2.1' |
-Dns '192.168.2.8', '192.168.2.1'

# Get updated Spec Object
$Spec = Get-OSCustomizationSpec -Name 'tmp01'
# Get Template to deploy from
$Template = Get-Template -Name 'Win2012R2'
# GetVMHost to deploy new VM on
$VMHost = Get-VMHost -Name 'vSphere'
# Deploy VM
New-VM -Name 'WEB001' \
-VMHost $VMHost
-Template $Template 
-OSCustomizationSpec $Spec |
Start-VM
```

> 警告 当你使用非持久定制化规范时，它存储在该 PowerCLI 会话的内存中。其他 PowerCLI 会话对访问克隆的定制化规范无所知。然而，在创建定制的会话中，非持久规范的管理方式就像持久性规范一样——这意味着你不能拥有两个同名的规范。

![](img/62596f5acc979040608a4e5111beb7d6_284_0.png)

因此，我们所有的示例只有一个网络适配器。具有多个网络适配器的机器呢？事实证明，该过程几乎完全相同。唯一的区别是每个适配器必须通过位置进行特定目标。因此，必须知道每个 Nic 的当前 Nic 位置。可以通过对你已修改的规范 运行 `Get-OSCustomizationNicMapping` 常用词来获取此信息：

| SpecId | Position | IPMode | IPAddress | DefaultGateway |
| --- | --- | --- | --- | --- |
| `Win2012R2_IIS` | `1` | `UseStaticIP` | `192.168.2.165` | `192.168.2.1` |
| `Win2012R2_IIS` | `2` | `Static` | `192.168.2.42` | `192.168.2.1` |

```powershell
# Update Spec Customization with our desired IP information
Get-OSCustomizationSpec -Name 'Win2012R2' |
  Get-OSCustomizationNicMapping |
    Set-OSCustomizationNicMapping -IPMode UseStaticIP \
      IpAddress '192.168.2.165' \
      SubnetMask '255.255.255.0' \
      DefaultGateway '192.168.2.1' \
      Dns '192.168.2.8','192.168.2.1'
# Get updated Spec Object
$Spec = Get-OSCustomizationSpec -Name 'Win2012R2'
# Get Template to deploy from
$Template = Get-Template -Name 'WS2012R2'
# Get VMHost to deploy new VM on
$VMHost = Get-VMHost -Name 'vSphere1'
# Deploy VM
New-VM -Name 'WEB001' \
  -VMHost $VMHost \
  -Template $Template \
  -OSCustomizationSpec $Spec \
  Start-VM
```

## 维护模板

模板是一个极其强大的工具——对于虚拟机的生命周期至关重要。然而，保持模板的更新也非常重要。这取决于工作量的投入：维护一个模板比在部署后修补或更新许多虚拟机要容易得多。有些公司选择每季度更新一次模板，并依靠其管理工具来填补这一空白。我们认为这种做法是愚蠢的：无论企业级工具有多强大，既然维护源模板更简单，为什么要在部署新的客机时反复循环呢？无论做如何决定，请记住：PowerCLI 会为你提供帮助。考虑到这一点，有几个常见的问题，但模板有一个通用的痛点。

无论你在做什么，第一步总是将模板转换为虚拟机，最后一步是将其转换回模板。在过程中，你可能需要或不需要启动虚拟机。你会发现，在任何更新期间，你都会不断考虑虚拟机的状态。为了协助这项琐碎的工作，你可以使用 `Wait-VMQuest` 函数（参见列表 7.15）。

## 列表 7.15 `Wait-VMQuest` 函数

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
