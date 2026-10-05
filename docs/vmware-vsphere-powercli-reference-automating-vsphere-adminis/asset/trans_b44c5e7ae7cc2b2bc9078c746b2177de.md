
能够输出命令结果固然，但并不非常有用。要对这些信息进行操作，必须提取值并将其存储在对象中。这是一个简单的文本到对象的转换，是许多 PowerShell 操作的一部分。9.1 是此类操作的一个示例，它使用 `Where-Object` 和正则表达式来简化数据收集和对象创建的功能。

# 列表 9.1 将文本转换为对象

```powershell
$searchString = "(\S+)\\s+(\d+)\\s+(\d+)\\s+(\d+)\\s+(\d+)\\s+(\S+)"
$splat = @{
  'Computer' = $vm.Guest.IPAddress[0]
  'Credential' = $creds
  'ScriptText' = "df"
}
Invoke-SSH @splat | Where-Object { $_ -match $searchString }
ForEach-Object {
  New-Object PSObject -Property @{
    "FileSystem" = $matches[1]
    "lBlocks" = [int64]$matches[2]
    "Used" = [int64]$matches[3]
    "Available" = [int64]$matches[4]
    "PercentUsed" = [Decimal]$matches[5]
    "MountPoint" = $matches[6]
  }
} | Where-Object { _.Available -lt (50MB/1KB) }
ForEach-Object {
  Write-Warning "卷 $($_.MountPoint) 的可用空间不足"
}
```

列表 9.1 看起来有点吓人，请放松。一切很快就会变得清晰。当在 `Where-Object` 脚本块中使用 `-match` 运算符时，你可以使用正则表达式。正则表达式是一种便于进行高级模式识别和提取数据的规则。在这种情况下，列表 9.1 使用数据列之间的空格来分隔数据。简单的分组有许多益处：它极其快速且灵活，会自动过滤掉任何不符合预期模式的行。为了为了更好地了解所使用的规则，请查看表 9.2。数据解析后，使用 `New-Object`  cmdlet将其组织成适当的对象。从那里开始，通过简单的 PowerShell 操作即可找到任何可用空间小于 50 MB 的分区。

![](img/62596f5acc979040608a4e5111beb7d6_328_0.png)

# 第 9 章 • 高级虚拟机功能

# 表 9.2 正则表达式参考表

| 字符 | 定义 | 示例 |
|---|---|---|
| (dot) | 匹配任意字符。 | "pos.*" 匹配 pos 或 posh 但不匹配。 |
| + | 前一个项目必须匹配一次或多次。 | "pos.*+" 匹配 posh 或 poshable 但不匹配。 |
| * | 前一个项目必须匹配零或多次。 | "pos.**" 匹配 po 和 poss 但不匹配 pos。 |
| () | 创建子集或组。 | "po (sh)*" 匹配 po 并创建两个组：po 和 sh。 |
| [] | 匹配括号内的任意字符。 | "po[os]*" 匹配 po 和 po。 |
| \s | 单个空白字符。 | "pos\s" 匹配 po sh 但不匹配 pos。 |
| \S | 单个非空白字符。 | "po\S*" 匹配 po 和 posh 但不匹配 po。 |
| \w | 单个单词字符（字母、数字、下划线）。 | "po\w*" 匹配 posh 但不匹配 po$5。 |
| \d | 单个数字字符。 | "pos\d*" 匹配 pos5 但不匹配 pos。 |

起初看起来很困难，但使用简单的正则表达式对于从 SSH 等基于文本的工具获取有用对象非常重要。许多在线工具可以帮助开发正则表达式，但基本的列匹配可以使用子组和空白分隔符 `\s|\S` 即可完成。或者，你也可以通过 SSH 传递命令处理更多的解析工作。采用哪种方法取决于你的熟悉程度。这没有标准的方法，请随时使用任何技能或工具来满足需求。

# 使用 Windows 原生工具

与 Windows 系统交互有两种主要方式：Windows 管理规范 (WMI) 和 PowerShell Remoting。WMI 允许 VBScript 或 Windows PowerShell 等脚本语言在本地和远程管理 Windows 系统。WMI 预装在 Windows 2000 及更新操作系统中。PowerShell 与远程系统交互的新方式随 PowerShell 2.0 或更高版本发布。这两种方法的缺点是网络连接不能被公司防火墙拦截，并且远程系统必须配置并运行相关服务。WMI 是一个使用 WMI 查询语言 (WQL) 管理系统信息的接口，而 PowerShell Remoting 类似于远程 shell。

# WMI

WMI 是微软对基于 Web的企业管理 (WBEM) 的实现，这是一项开发用于企业环境中访问管理信息的标准的行业倡议。WMI 非常强大但难以理解。很多时候，找到正确的信息需要在大量的 WMI 类集合中进行挖掘。对 WMI 的深入研究超出了本书的范围。学习 WMI 的良好起点是微软 MSDN 库。你可以通过 http://microsoft.com/en-us/ 访问它。

![](img/62596f5acc979040608a4e5111beb7d6_328_0.png)
