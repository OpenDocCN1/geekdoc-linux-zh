

# 列表 21.11 用于 New-DRRule Set Alignments 任务的 vRO JavaScript 代码

```
var arguments = "-Name " + drsRuleName + "-Cluster " + cluster +
+ "-VM " + vms + "-vCenter " + vCenter + "-Username " + username +
  + "-Password " + password;

if (keepTogether) {
  arguments += " --KeepTogether"
}
```

在工作流架构中，使用之前创建的 Invoke-ExternalPSScriptReturnCode 工作流（图 26）。

# 图 21.26 添加 Invoke-ExternalPSScriptReturnCode 工作流

![](img/62596f5acc979040608a4e5111beb7d6_777_0.png)

在 Invoke-ExternalPSScriptReturnCode 工作流的“输入”（In）选项卡中，创建以下内容（图 21.27）：

- **powershellHost** 类型：PowerShell:PowerShellHost，作为工作流属性。将值设置为作为 PowerShell 插件设置的一部分创建的 PowerShellHost。
- **scriptPath** 类型：String，作为工作流属性。将值设置为 c:\Scripts\New-ClusterDRSRule.ps1。
- 并选择以下现有属性（图 21.27）：
    - **arguments** 类型：String

# 图 21.27 Invoke-ExternalPSScriptReturnCode（输入 选项卡）

![](img/62596f5acc979040608a4e5111beb7d6_778_0.png)

在工作流的选项卡上，创建以下内容（图 21.28）：
- **returnCode** 类型：string，作为工作流属性

# 图 21.28 Invoke-ExternalPSScriptReturnCode（输出 选项卡）

![](img/62596f5acc979040608a4e5111beb7d6_778_1.png)

关闭 Invoke-ExternalPSScriptReturn 工作流并保存并关闭工作流。

我们现在已准备好使用 New-DRSRule 工作流。运行它并按照如下设置设置参数（图 21.29）：

- - drsRuleName: TestRule01（规则名称）
- cluster: cluster01（vSphere 集群名称）
- 用逗号分隔多个虚拟机：Server01, Server02（要添加到规则的虚拟机）
- keepTogether: 否 
- vCenter: vcenter05.sunnyydale.local（vCenter DNS 名称）
- username: Sunnyydale\vcosvc（具有创建 DRS 规则 vCenter 权限 AD 账户）
- password: *****（该用户的密码）

# 图 21.29 启动 New-DRSRule 工作流

![](img/62596f5acc979040608a4e5111beb7d6_779_0.png)

在工作流日志中，你应该能看到类似于下面的输出，包含脚本返回代码和脚本输出：

```
[2015-01-19 22:32:34.180] [I] XMLReturnCode is:
<Objs Version="1.1.0.1" xmlns="http://schemas.microsoft.com/powershell/2004/04">
<I132>0</I132></Objs>
```

```
[2015-01-19 22:32:34.180] [I] returnCode is: 0
[2015-01-19 22:32:34.180] [I] Script output is: Successful imported the PowerShellCLI Core Module
Successfully connected to vCenter vcenter05.sunnydale.local
Cluster01 exists
VM Server01 exists
VM Server02 exists
DRS TestRule1 does not already exist
Successfully created DRS Rule TestRule1
0
```

# PowerShell 插件的替代方法

不可否认，即使在实验环境中，由于可用的各种协议和身份验证方法，配置 PowerShell 插件有时也具有挑战性。将其置于具有内部防火墙、安全策略和 Windows 操作系统的企业环境中，确实有产生重大非常头疼问题的空间。本章较之前“配置”部分的注释列出了了一些 URL，说明了可能遇到的某些障碍。

此外，一旦完成 PowerShell 插件的配置，通常还会遇到进一步的问题，如 PowerShell 远程多重身份验证以及使用外部命令和 PowerShell 模块的困难。对这些问题的详细讨论超出了本书的范围，但在面对任何这些挑战时，在工具箱中有一个替代方法是有用的。

本节将演示一种在不使用 PowerShell 插件的情况下在 vRO 中使用 PowerShell 方法。

# 要求

vRO 和 PowerShell 对在不使用 PowerShell 插件的情况下在 vRO 中使用 PowerShell 有如下要求：

- **vRO**: 如本章前面所述，替代方法仅在 vRO 安装在 Windows 上时可用，当使用基于 Linux 的 vRO 设备时则不可用。
- **PowerShell**: vRO Windows 服务器上应提供 v4 版本。

# 配置

对于替代 PowerShell 方法需要配置以下元素：

- **PowerShell**: 确保 PowerShell 具有允许运行脚本的执行策略，按照 PowerShell 插件的配置。
- **vRO**: 对于 vRO，不需要执行列出的任何配置步骤。

