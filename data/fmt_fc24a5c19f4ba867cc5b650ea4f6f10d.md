
如果在离线期间没有缓存文件被修改，且客户端没有打开该共享的文件，CSC 将在网络或服务器故障后尝试动态重新连接。

# 基于服务器的 Interix

对于从 UNIX NFS 文件服务器执行的应用程序（通常在客户端使用 automount 和 NIS 映射），迁移到 Windows 平台和 Interix 会带来一些困难：

- Interix 不支持动态映射表（dynamic maps）或 NIS 映射。
- 与之前讨论的基于 Win32 的应用程序一样，CIFS 文件访问协议在网络或服务器失败场景下的行为与 UNIX 系统中常用的 NFS 协议不同。

通常，不建议从文件服务器提供 Interix 应用程序二进制文件，但确实需要时，建议的方法是使用静态（非自动挂载的）NFS 文件共享。如果静态文件共享不可接受，应考虑使用微软分布式文件系统 (DFS)。

# 使用微软分布式文件系统替换 Automount

如果需要将移植的 Interix 应用程序从与原始 UNIX 应用程序相同的组 NFS 文件服务器提供服务，您可以通过使用微软分布式文件系统 (DFS) 来满足 Interix 对自动挂载的需求。

> 注意：Microsoft DFS 不等同于开放系统基金会的分布式文件系统 (DFS)。

DFS 允许系统管理员让用户和应用程序更容易访问和管理物理分布在网络上的文件。通过 DFS，分布在多个服务器上的目录和文件看起来就像位于网络上的某处一样。DFS 充当具有单一根目录的网络文件系统。终端用户无需知道或指定文件的实际位置即可访问。

DFS 包含了基于服务器和基于客户端的 DFS 组件。有关 DFS 组件的更多信息，请参见 Windows 2000 Server 在机帮助中的“理解分布式文件系统 (DFS)”和“使用分布式文件系统 (DFS)”。

要设置 Interix 用户环境使其类似于 UNIX 自动挂载环境：

- 1. 为 UNIX NIS 域 automount 映射中定义的 NFS 共享创建 DFS 链接。（参见以下步骤。）
- 2. 使用 Interix 创建指向顶层 DFS 链接的符号链接（例如 apps、data、home、scratch 等）。
- 3. 修改本地 shell 启动脚本（C 和 Korn Shell）以使用这些链接。

该解决方案的优势是对于 NIS 自动挂载映射和 DFS 导入脚本都实现了单点管理。此过程中唯一需要在

## 第 13 章：创建活动环境

Windows 2000 DFS 服务器上执行的操作，是使用 DFSUTIL 命令行应用程序导入 DFS 配置信息以生成 DFS 链接。

要从 NIS automount 映射创建 DFS 链接：

- 1. 在每个 NIS automount 映射上运行 `ypcat` 以生成 NIS 映射的文本输出。
- 2. 运行 UNIX 文本处理工具创建符合 DFSUTIL 工具导入函数格式要求的文本文件。
- 3. 将导入文本文件复制到 Windows 2000 服务器。
- 4. 运行 DFSUTIL 创建 DFS 链接。

此过程如图 13.2 所示。

![](img/a92ad9df7b0b951660ea67fa842644c1_640_0.png)

图 13.2 如何将 automounts 转换为 Windows DFS

Windows 工作站使用 DFS 链接中的信息，为每个使用 UNIX 上 NFS 共享的用户挂载相应的应用程序镜像环境。此过程可以通过每个用户登录时运行的脚本来实现。您将在本章稍后的“使用 DFS 在 Interix 中自动挂载”中找到一个模拟自动挂载的脚本。

# 支持与维护系统

您的系统和应用程序管理员通常希望使用工具和脚本来管理迁移后的应用程序。在迁移到 Interix 和 Win32 时，您有权迁移以前在 UNIX 环境中使用的任何管理工具。在 Win32 迁移中，您还可以使用某些基于 Windows 的工具，例如微软系统管理服务器 (SMS)。

本节讨论了管理和支持迁移后应用程序的可用选项。对您拥有的基于 UNIX 的管理工具进行清单，并为每个工具决定 Windows 平台上最合适的解决方案。

您可能会考虑将 UNIX 管理工具移植到 Interix。如果您的应用程序继续使用与在 UNIX 上相同的配置文件和脚本工具，请考虑移植这些工具。在这种情况下，Services for UNIX (SFU) 3.0 提供了将 Perl 和 UNIX 脚本移植到 Win32 所需的工具，包括使用了 `awk`、`sed` 和 `grep` 等标准 UNIX 工具的。

# 远程管理与控制

UNIX、Interix 和 Windows 都包含基本的远程管理和控制。这些包括 UNIX 管理员熟悉的 `telnet`、`ftp` 和 Berkeley 命令。在部署了 Interix 的混合 Windows 环境中，可以使用基于 Windows 的管理。有一系列可用工具，将在第 6 章“UNIX 与 Windows 的互操作性”中进行讨论。然而，Win32 环境具有额外的远程工具，可以显著增强管理和控制。微软 SMS 就是其中一种工具。它标准包含图形化远程控制。除了 SMS 之外，许多第三方工具提供了远程控制：

- Norton PC Anywhere
- Compaq Carbon Copy

## 第 13 章：创建活动环境

在 Windows XP 专业版中，远程协助程序作为基础操作系统的一部分引入。这允许管理员控制远程桌面并解决问题。

# 在 Win32 中使用脚本远程管理

Windows Scripting Host 是 ActiveX 脚本引擎及其相关编程语言的驻留运行时。微软随 Windows 2000 提供了 Visual Basic Scripting Edition（ECMAScript Edition.3 的实现）和 Jscript。还有 Perl、REXX、Python 和其他语言引擎的第三方实现。ActiveX 脚本代码也可以由 ActiveX Pages、Microsoft Internet Explorer 和 Active Directory 脚本托管。

由 Windows Scripting Host 服务运行的脚本可以访问本地文件系统和映射的网络驱动器；桌面快捷方式；Windows 注册表；特殊文件夹（如我的文档）；Active Directory 对象；用户配置文件；环境变量；事件日志；性能计数器以及 Windows Installer 服务。脚本可以使用提供 ActiveX 接口的已安装应用程序（如 Microsoft Office 家族中的），并可以被远程调用。

结合 Windows 管理规范 (WMI) 和 Active Directory 脚本接口 (ADSI) 组件，Windows 环境中的几乎任何都可以编写脚本。

系统管理员用于自动化作业的其他工具包括网络登录脚本、任务计划程序以及计划服务的 AT 命令行界面。许多第三方工具提供了额外或不同的完成任务的方法。Windows 管理员还应该熟悉 Windows 2000 专业版和服务器版 CD 以及 Windows 2000 工具包提供的工具，其中包含许多实用程序，其中许多是为远程自动化设计的。

# 在 Win32 中启用脚本主机

可以按照以下步骤在基于 Win32 的应用程序中启用远程脚本

- 要启用远程脚本
- 1. 在两个系统上从 http://www.microsoft.com/scripting 安装 Windows Script Host 5.6。
- 2. 在执行脚本的远程服务器上更改以下注册表项：

```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Script Host\Settings remote = 1
```

- 3. 确保您拥有目标计算机的管理员权限。

# 在 Win32 中使用 Windows Script Host

在启用远程脚本后，提供的指向 WshController 对象的 `CreateScript` 方法的脚本不使用任何用户界面元素，例如 `WScript.Echo`、STDIO、`WshShell::Popup`、MsgBox、InputBox 以及其他生成用户界面的的方法和对象。

以下是你可以用于创建远程管理脚本的模板：

- Admin.vbs 是标准管理员工具的模板，用于复制和远程执行客户端脚本。
- Client.vbs 执行工作并报告远程计算机上触发的事件。在这种情况下，控制脚本使用 ADSI 从 Active Directory 中检索计算机名称。

以下是 `Admin.vbs` 脚本的代码：

```vbscript
************
'Admin.vbs
************
domainName = "YOUR_DOMAIN"
scriptName = "c:\client.vbs"

Dim ADContainer, ADComputer
Dim WSHCtrl

Set ADContainer = GetObject("WinNT://" & domainName)
ADContainer.Filter = Array("Computer")

For Each ADComputer In ADContainer
    Set wshctrl = CreateObject("WshController")
    Set wshRemote = 
    wshctrl.CreateScript(scriptName, ADComputer)

    Wscript.ConnectObject wshRemote, "WSH_"
    wshRemote.Execute

    Do While wshRemote.Status <> 2
        Wscript.Sleep 1000
    Loop
Next

'事件处理函数...
Function WSH_End()
    Wscript.Echo ADComputer.name & " End Event fired"
End Function

Function WSH_Error()
    Wscript.Echo "Error Number: " &
    CStr(Hex(WSHClient.Error.Number))
```

## 第13章：创建活动环境

```vbscript
Wscript.Echo Description: " " & WSHClient.Error.Description
Wscript.Echo Line Number: " " & WSHClient.Error.Line
WSH.Client.Terminate()
End Function

Function WSH.Start()
  MsgBox ADComputer.name & " Start Event fired"
End Function

Set ADComputer = Nothing
Set ADContainer = Nothing
Set WSHCtrl = Nothing
```

以下是 `Client.vbs` 脚本的代码：

```vbscript
************************
'Client.vbs
************************
Set fso = CreateObject("Scripting.FileSystemObject")
Set f = fso.CreateTextFile("C:\scripttest.txt", True)
Wscript.Sleep 5000
f.WriteLine "Script executed at " & Now
Wscript.Sleep 5000
f.Close
```

Windows Script Host (WSH) 包含三种操作 Windows 注册表的方法。虽然许多注册设置是通过组策略设置的，但通常有很多细微的变化需要注意。将这些语句嵌入到符合 WSH 标准的 .vbs 或 .js 文件中，然后从组策略中调用它们，可以减少登录脚本中等效命令行的使用。

```vbscript
************************
'DeleteAuto.vbs
************************
Dim WSHShell, regAuto
Set WSHShell = Wscript.CreateObject("Wscript.Shell")

regAuto = WSHShell.RegRead("HKLM\Software\Microsoft\NT\CurrentVersion\Winlog\AutoAdminLogon")

if regAuto="1" then
  WSHShell.Popup("Turning off auto logon...")

  WSHShell.RegWrite "HKLM\Software\Microsoft\NT\CurrentVersion\Winlog\AutoAdminLogon", 0
end if
```

# 远程管理与 Windows 管理接口

Windows Management Instrumentation (WMI) 是微软对基于网络的企业管理 (WBEM) 的实现，这是一套用于在企业网络上访问、收集和操作管理信息的行业标准。

WMI 包含一个符合通用信息模型 (CIM) 标准的对象存储库。CIM 对象管理器 (CIMOM) 负责处理存储库中的对象，并从 WMI 提供程序中收集动态和语义数据点。WMI 提供程序是操作系统组件、应用程序和驱动程序之间的中间代理。注册表提供程序从注册表中调取信息；简单网络管理协议 (SNMP) 则提供来自 SNMP 设备及其他源的数据和事件。

WMI 拥有其独立于 Windows Script Host 的运行运行能力。以下是一个 VBScript 示例，用于连接到远程计算机上的 WMI 服务并实例化一个新进程。你可以从远程进程中提取返回值。

在以下代码中，*remote_desktop* 将替换为应运行应用程序的服务器实际名称。

```vbscript
server = "remote_desktop"
Set MyProc = GetObject("wimmts:\" & server & "\root\cim2:win32_process")
Set InParams = MyProc.Methods("Create").InParams.SpawnInstance_()
InParams.CommandLine = "calc.exe"
Set OutParams = MyProc.ExecMethod("Create", InParams)
wscript.echo OutParams.ReturnValue, OutParams.ProcessID
```

在允许用户连接到本地或远程计算机上的 WMI 之前，WMI 会对每个用户进行验证。这种安全性是在操作系统现有安全性之上的额外叠加。WMI 不覆盖或绕过操作系统提供的任何现有安全机制。

默认情况下，Administrators 组的所有成员都对受管理计算机上的 WMI 服务具有完全控制权限。其他人仅在本地计算机上具有读取、写入和执行权限。

使用 Perl/Tcl

在 Windows 上，ActiveState 提供了脚本支持——兼容 Windows Script Host、Internet Explorer 和 Active Server Pages。这是一个允许使用 WMI 的示例：

```vbscript
#perl -w
# Copyright (c) 1997-2002 Microsoft
# WMI Sample Script - List services
# To retrieve instances of Win32_Service.
```

## 第13章：创建活动环境

# 使用 Windows Installer

本节介绍了如何使用本章介绍的工具创建 Windows Installer 包。在使用该工具之前，应执行某些准备工作：

1. 设置一台与目标计算机配置相同的计算机。
2. 在运行快照之前，关闭任何病毒检测和入侵检测。
3. 每次重新封装应用程序时，将模型计算机恢复到此状态。
4. 如果将使用 GPO 部署包，应以管理员账户登录，因为托管应用程序（分配型）使用提升权限安装。
5. 如果 MSI 通过其他可能不具有这些权限的方法发布，你在创建时必须考虑这一点。

此示例使用了 Wise Solutions 的 Wise for Installer 4.20 评估版，你应该现在安装并使用。

1. 将 Wise for Installer 安装到默认目录 `C:\Program Files\Wise Installer Evaluation`。它是一个可执行文件并将启动 Windows Installer 服务进行安装。
2. 在开始菜单中，点击所有程序，点击 Wise Solutions Evaluations，点击 Wise for Installer — Professional Edition。
3. 在新建安装文件对话框中，选择 SetupCapture 作为项目类型，点击创建标准 .MSI 或 .MSM 文件，然后点击确定。
4. 在 SetupCapture 欢迎对话框中，点击设置。
5. 在 SetupCapture 配置对话框中，执行以下操作：

- 在常规设置选项卡上，接受默认值。
- 在要观察目录选项卡上，双击 `C:\` 并取消勾选对话框中的包含子目录。点击添加 `C:\Windows`（或你当前的 Windows 系统目录）和 Program Files 并包含这些目录，然后点击确定。
- 在文件和文件夹排除选项卡上，列出了当前用户的临时目录。你可以添加其他安装过程中可能会修改但不会影响实际安装过程的目录。
- 在注册表排除选项卡上，列出安装过程中可能会变化但你不希望捕获的注册表项。（此选项卡通常不使用。）

## 第13 章：创建活动环境 625

![](img/a92ad9df7b0b951660ea67fa842644c1_648_0.png)

图 13.4

SetupCapture 配置对话框

- 6. 点击 **OK** 返回 **Welcome** 对话框，然后点击 **Next**。
