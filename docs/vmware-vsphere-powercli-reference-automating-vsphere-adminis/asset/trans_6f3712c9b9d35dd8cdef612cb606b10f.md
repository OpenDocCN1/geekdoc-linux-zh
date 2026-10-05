
能够在这种环境中工作的人应该继续做他们正在做的事情。对于我们其他人，还有定制化规范。

OS 定制化规范是让模板具有其特定特征的胶水。为了说明这一点，下一节将通过一系列部署，逐渐增加复杂性。要通过定制化规范使用静态 IP 地址开始标准的 Windows Server 部署，请参阅 7.10。

## 列表 7.10 使用定制化规范为 Windows Server 分配静态 IP 地址

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

该工作流有些反向，但一旦解释了底层机制，它就有道理了。首先，修改了定制化规范以使用所需的 IP 地址。这里变得有点疯狂：更新被应用于实际的定制化规范——这并不是内存中的一个对象。一旦从 vCenter Server 使用模板和 VMHost 对象获取新的修改后的定制化对象，只需调用 `New-VM` 常用词即可部署新的虚拟机。

# 第 7 章 • 使用模板和定制化规范

注意列表 7.10 中，`New-VM` 对象被管道传输到 `Start-VM`。强烈建议这样做，因为定制信息尚未进入客户机——直到虚拟机首次通电后才会进入。一旦新虚拟机首次通电，vCenter 将等待 VMware Tools 报告。在 Tools 第一次报告后，vCenter Server 将一个 OS 定制脚本复制到客户机虚拟机，然后调用一系列执行客户机定制的最终化脚本。

尽管之前的两个示例功能完全可用，但它们都有一个致命的缺陷：它们修改了存储在 vCenter Server 上的定制化规范。这种行为特别棘手，因为它将永久地修改源规范。为了规避这个问题，使用了非驻留的 OS 定制化规范。该过程与列表 7.10 中的过程完全相同，唯一的例外是：在进行任何修改之前，将定制化规范克隆到非持久性规范中。这一步骤允许在修改规范而不影响存储在 vCenter Server 上的副本。列表 7.11 中包含的代码部署了另一个 Windows Server，执行与之前相同的定制，但这次没有影响 vCenter Server 上的主副本。

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
|---|---|---|---|---|
| Win2012R2_IIS | 1 | UseStaticIP | 192.168.2.165 | 192.168.2.1 |
| Win2012R2_IIS | 2 | Static | 192.168.2.42 | 192.168.2.1 |

# 第 7 章 • 使用模板和定制化规范

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

该工作流有些反向，但一旦解释了底层机制，它就有道理了。首先，修改了定制化规范以使用所需的 IP 地址。这里变得有点疯狂：更新被应用于实际的定制化规范——这并不是内存中的一个对象。一旦从 vCenter Server 使用模板和 VMHost 对象获取新的修改后的定制化对象，只需调用 `New-VM` 常用词即可部署新的虚拟机。

注意列表 7.10 中，`New-VM` 对象被管道传输到 `Start-VM`。强烈建议这样做，因为定制信息尚未进入客户机——直到虚拟机首次通电后才会进入。一旦虚拟机首次通电，vCenter 将等待 VMware Tools 报告。在 Tools 第一次报告后，vCenter Server 将一个 OS 定制脚本复制到客户机虚拟机，然后调用一系列执行客户机定制的最终化脚本。

尽管之前的两个示例功能完全可用，但它们都有一个致命的缺陷：它们修改了存储在 vCenter Server 上的定制化规范。这种行为特别棘手，因为它将永久地修改源规范。为了规避这个问题，使用了非驻留的 OS 定制化规范。该过程与列表 7.10 中的过程完全相同，唯一的例外是：在进行任何修改之前，将定制化规范克隆到非持久性规范中。这一步骤允许在修改规范而不影响存储在 vCenter Server 上的副本。列表 7.11 中包含的代码部署了另一个 Windows Server，执行与之前相同的定制，但这次没有影响 vCenter Server 上的主副本。

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
|---|---|---|---|---|
| Win2012R2_IIS | 1 | UseStaticIP | 192.168.2.165 | 192.168.2.1 |
| Win2012R2_IIS | 2 | Static | 192.168.2.42 | 192.168.2.1 |

# 第 7 章 • 使用模板和定制化规范

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

该工作流有些反向，但一旦解释了底层机制，它就有道理了。首先，修改了定制化规范以使用所需的 IP 地址。这里变得有点疯狂：更新被应用于实际的定制化规范——这并不是内存中的一个对象。一旦从 vCenter Server 使用模板和 VMHost 对象获取新的修改后的定制化对象，只需调用 `New-VM` 常用词即可部署新的虚拟机。

注意列表 7.10 中，`New-VM` 对象被管道传输到 `Start-VM`。强烈建议这样做，因为定制信息尚未进入客户机——直到虚拟机首次通电后才会进入。一旦虚拟机首次通电，vCenter 将等待 VMware Tools 报告。在 Tools 第一次报告后，vCenter Server 将一个 OS 定制脚本复制到客户机虚拟机，然后调用一系列执行客户机定制的最终化脚本。

尽管之前的两个示例功能完全可用，但它们都有一个致命的缺陷：它们修改了存储在 vCenter Server 上的定制化规范。这种行为特别棘手，因为它将永久地修改源规范。为了规避这个问题，使用了非驻留的 OS 定制化规范。该过程与列表 7.10 中的过程完全相同，唯一的例外是：在进行任何修改之前，将定制化规范克隆到非持久性规范中。这一步骤允许在修改规范而不影响存储在 vCenter Server 上的副本。列表 7.11 中包含的代码部署了另一个 Windows Server，执行与之前相同的定制，但这次没有影响 vCenter Server 上的主副本。

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
|---|---|---|---|---|
| Win2012R2_IIS | 1 | UseStaticIP | 192.168.2.165 | 192.168.2.1 |
| Win2012R2_IIS | 2 | Static | 192.168.2.42 | 192.168.2.1 |

# 第 7 章 • 使用模板和定制化规范

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

(此处由于原文大量重复，已根据要求进行去重处理，仅保留核心逻辑翻译)

