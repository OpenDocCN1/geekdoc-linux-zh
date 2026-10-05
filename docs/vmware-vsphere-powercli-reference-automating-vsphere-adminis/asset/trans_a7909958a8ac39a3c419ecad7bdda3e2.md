

## 整合一切

在本章中，我们查看了《加固指南》中的安全加固准则，重点关注了针对本指南的准则。该指南未提供评估和或修复的 PowerCLI 自动化功能。我们提供了命令、代码块或函数供您使用以关闭安全漏洞。现在，您的主机、虚拟机和 vNetwork 将为它们面临的安全威胁做好更充分的准备。

下一步的改进方向：与其为每个准则单独运行这些检测和修复脚本，我们希望看到一个利用评估和修复代码整体运行的模块或工具——例如，某种可以调度的、并在每个周期报告环境安全“硬度”的东西，类似于 Alan Renouf 的 vCheck-vSphere (https://github.com/alanrenouf/vCheck-vSphere)，但侧重于安全（我们可以将其命名为 vseCheck）。

虽然创建这样的工具更符合理想情况，但它已超出了本章的范围。如果您对此类框架感兴趣，请在书籍网页上（访问 www.wiley.com/vmpherepowercli）告诉我们，我们将尽力满足。或者，您可以启动这样的项目，将其开源（也许在 GitHub 上），并让大家知道，以便我们都能为您的项目做出贡献！

祝在使用 PowerCLI 让您的 vSphere 环境更加安全。

## 在您的 vSphere 环境中维护安全

在本章中，您将学习到：

- 安装 VCenter 更新管理器 PowerCLI 扩展程序 476
- 使用基线 (Baselines) 477
  - 创建基线 . . . . . . . . . . . . . . . . . . . 477
  - 更新基线 . . . . . . . . . . . . . . . . . . . 480
  - 挂载和取消挂载基线 . . . . . . . . . . . . . . . 481
- 处理升级和补丁 482
  - 扫描主机. . . . . . . . . . . . . . . . . . . . . . . 482
  - 将补丁暂存到主机. . . . . . . . . . . . . . . . . . . . . 483
  - 修复主机 . . . . . . . . . . . . . . . . . . . . . . . 483
  - 将补丁作为主机部署的一部分. . . . . 486
- 报告安全状态 486
  - 理解数据中心合规性 . . . . . . . . . . . . . . . . . . 487
  - 报告特定基线的合规性 . . . . . . . . . . . . . . . . . . 489
  - 报告所需的补丁 . . . . . . . . . . . . . . . . . . . . . 491
- 在不使用 vSphere 更新管理器的情况下应用补丁 492
  - ZIP 文件 . . . . . . . . . . . . . . . . . . . . . . . 493
  - VIB 文件. . . . . . . . . . . . . . . . . . . . . 494

无论管理员负责的是哪种操作系统或应用程序，通过应用供应商提供的软件更新来保持其最新始终非常重要。ESXi 在方面也是如此，VMware 提供了一个名为 vCenter Update Manager (VUM) 的管理工具来协助此过程。该工具可管理主机、客户机和虚拟设备。可以下载另一套独立的 PowerShell 命令行来实现 VUM 的自动化。此外，我们还将演示如何在无法使用 VUM 的情况下自动化 ESXi 主机补丁更新。

## 第 14 章

最后，VMware 在 vSphere 5.0 中移除了虚拟机操作系统的补丁。因此，在本章中，我们将关注 ESXi 补丁，尽管也会涵盖更新 VMware Tools 和升级虚拟机硬件的内容。

## 安装 vCenter Update Manager PowerCLI 扩展程序

在可以使用 VUM PowerCLI 扩展程序之前，您必须先下载并安装它。它是核心 PowerCLI 模块的独立下载项，通常必须使两者的发布版本匹配才能正常运行。

> 注意：随着 6.0 版本的发布，VUM 扩展程序包含了对 .NET 4.5 和 PowerShell 4.0 的支持。之前的扩展程序缺少这些支持，导致 VUM 命令行难以与核心 PowerCLI 扩展程序配合使用（核心 PowerCLI 扩展程序从 5.5 R2 版本起已支持 PowerShell 4.0）。通常，在安装了 PowerShell 4.0 的系统上让两者协同工作，需要使用 `powershell.exe -Version 2` 打开 PowerShell 会话，以便在 PowerShell 2.0 版本中使用 VUM 命令行。

此外，VUM 6.0 版本带来了对多个服务器版本 VUM 支持——这是一个欢迎的功能。在 6.0 之前，VUM 扩展程序的版本与服务器版本匹配至关重要。不匹配可能会在升级工作中带来特定挑战。请咨询 6.0 VUM 扩展程序的发布说明，以确认支持哪些 6.0 的版本。

一旦安装了 VUM PowerCLI 命令行，使用以下行使其在现有的 PowerShell 会话可用：

```
Add-PSSnapin VMware.VumAutomation
```

为了节省每次都要操作的精力，考虑将相同的行添加到您的 PowerShell 配置文件中。PowerShell 配置文件是一个每次启动 PowerShell 时都会执行的脚本文件。默认情况下，PowerShell 配置文件不存在；您可以使用以下命令创建一个：

```
New-Item -Path $PROFILE -Type File
```

要编辑配置文件，可以使用记事本打开它：

```
notepad $PROFILE
```

## 使用基线 (Baselines)

一旦安装了 vCenter 更新管理器并填充了补丁库，使用基线的第一步是创建一个基线。我们将考虑两种类型的基线：静态和动态。两者的本质在于，静态基线不会在下载新补丁时更新，而动态基线会。

## 创建基线

首先，为主机获取一组补丁。列表 14.1 显示了如何获取该补丁集：

```
$Patches = Get-Patch -TargetHost -Product 'embeddedESX 5.5' -After '01 Oct 2014'
```

## 在您的 vSphere 环境中维护安全

列表 14.1 获取补丁集

| 名称 | 发布日期 | 严重性 | ID |
| . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . | . | . | . |
| esx-base | 15/10/2014 | 重要 | ES550-20140 |
| esx-base | 02/12/2014 | 关键 | ES550-201441 |
| misc-drivers | 15/10/2014 | 重要 | ES550-201442 |
| sata-ahci | 15/10/2014 | 重要 | ES550-201443 |
| xhci-xhci | 15/10/2014 | 重要 | ES550-201444 |
| tools-light | 15/10/2014 | 重要 | ES550-201445 |
| net-vmxnet3 | 15/10/2014 | 重要 | ES550-201446 |

现在所需的补丁已存储在 `$Patches` 变量中，这些补丁可以作为 `New-PatchBaseline` 创建的新静态基线的一部分（列表 14.2）。

## 列表 14.2 创建静态补丁基线

```
$New-PatchBaseline -Static -TargetTypeHost -Name \
  'ESXi Current (Static)' -Description \
  'ESXI 5.5 patches since 01Oct2014 - 22Jan2015' \
  -IncludePatch $Patches
```

类似的，您也可以创建一个新的动态基线，它基本上会像静态的基样开始。该基线适用于自 2014 年 1 月 1 日以来 VMware 的 ESXi 主机（列表 14.3）。

## 列表 14.3 创建动态基线

```
$New-PatchBaseline -Dynamic -TargetTypeHost -Name \
  'ESXi Current (Dynamic)' -Description 'to the current date -SearchPatchVendor \
  'VMware*' -SearchPatchProduct 'embeddedESX 5.5.0' \
  -SearchPatchStartDate '01 Oct 2014'
```

