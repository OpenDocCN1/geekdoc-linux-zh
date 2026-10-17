
\DC01.corp.com 的组账户

- `Another_Nested_Group`
- `Cloneable Domain Controllers`
- `DnsAdminProxy`
- `Domain Admins`
- `Domain Computers`
- `Domain Controllers`
- `Domain Guests`
- `Domain Users`
- `Enterprise Admins`
- `Enterprise Key Admins`
- `Enterprise Read-only Domain Controllers`
- `Group Policy Creator Owners`
- `Key Admins`
- `Nested_Group`
- `Protected Users`
- `Read-only Domain Controllers`
- `Schema Admins`
- `Secret_Group`

命令成功完成。

从列表 664 中的突出输出中，我们注意到自定义组 `Secret_Group`、`Nested_Group` 和 `Another_Nested_Group`（以及随后包含的所有成员）可以被添加为另一个的成员。这被称为嵌套组。

虽然嵌套看起来很复杂，但它的扩展性良好，为即使是 AD 实现提供了灵活性和成员自定义。遗憾的是，`net.exe` 命令行工具无法列出嵌套组，只能列出直接的用户成员。由于此和其他局限性，我们将探索一种在现实环境中更有效、更灵活的替代方案。

# 21.2.1.1 练习

- 1. 连接到你的 Windows 10 环境并使用 `net.exe` 查找域中的用户和组。如果你能看到任何有趣的用户或组。

# 21.2.2 一种现代方法

有几种现代工具能够枚举 AD 环境。PowerShell 命令行（如 `Get-ADUser`608）运行良好，但它们默认只安装在域控制器上

608 (Microsoft, 2018), https://docs.microsoft.com/en-us/powershell/module/adsadministration/get-aduser?view=win10

（作为 RSAT⁶⁰⁹ 的一部分），它们可以安装在 Windows 7 及之后的 Windows 工作站上，并且使用需要管理员权限。

然而，可以使用 PowerShell（Windows 首选的管理脚本语言）来枚举 AD。在本节中，我们将开发一个脚本，尽管这不像运行类似 `net.exe` 命令那样简单，但该脚本将非常灵活，允许我们根据需要添加功能和特性。在构建脚本的过程中，我们将讨论许多与当前任务相关的技术细节。一旦脚本完成，我们就可以复制并粘贴它在评估期间使用。

总体而言，此脚本将查询网络以获取主域控制器和模拟器的名称、域，搜索 Active Directory 并过滤输出以显示用户账户，并清理输出以提高可读性。

> 主域控制器模拟器是域控制器执行的五个操作主角色之一（或 FSMO 角色）⁶⁰。从技术上讲，该属性称为 `PdcRoleOwner`，具有此属性的域控制器始终拥有有关用户登录和验证的最新信息。

此脚本依赖于少数组件。具体而言，我们将使用 `DirectorySearcher`⁶¹ 对象通过轻量级目录访问协议 (LDAP)⁶² 查询 Active Directory，LDAP 是一种域控制器理解的网络协议，也用于与第三方应用程序通信。

LDAP 是 Active Directory 服务接口 (ADIS)⁶³ 提供程序（一种 API），支持对 Active Directory 进行搜索功能。这将允许我们使用 PowerShell 与域控制器交互并提取有关对象的非权限信息。

我们的脚本将围绕一个非常特定的 LDAP 提供程序⁶⁴ 开发，它将作为 `DirectorySearcher` .NET 类的输入。它的路径原型如下：

```
LDAP://HostName=:DistinguishedName
```

列表 665 - LDAP 提供程序路径格式

要创建此路径，我们的目标主机（域）和区分名称 (DN)⁶⁵ (Microsoft, 2018), https://msdn.microsoft.com/en-us/library/directorysearcher(vs=110).⁶¹ (Microsoft, 2018), https://msdn.microsoft.com/en-us/library/fsmo-roles-in-domain.⁶² (Microsoft, 2018), https://msdn.microsoft.com/en-us/library/domain(vs=110).⁶³ (Microsoft, 2018), https://msdn.microsoft.com/en-us/library/search(vs=110).⁶⁴ (Microsoft, 2018), https://msdn.microsoft.com/en-us/library/pdcroleowner(vs=110).⁶⁵ (Microsoft, 2018), https://msdn.microsoft.com/en-us/library/name(vs=110).

PWK 2.0

Copyright © Offensive Security Ltd. 保留所有权利。

227# 攻击性安全

使用 Kali Linux 2.0

首先，让我们使用 PowerShell 命令发现域的主机和区分名称。具体而言，我们将使用 `System.DirectoryServices` 命名空间的 `Domain` 类。`Domain` 类包含一个名为 `GetCurrentDomain`⁶⁷ 的方法，它可以获取当前登录的域对象。调用该方法及其输出显示如下：

```
PS C:\Users\offsec.corp> [System.DirectoryServices.Domain]::GetCurrentDomain()
```

| Forest | corp.com |
| DomainControllers | {DC01.corp.com} |
| Children | {} |
| DomainMode | Unknown |
| DomainModeLevel | 7 |
| Parent | |
| PdcRoleOwner | DC01.corp.com |
| RidRoleOwner | DC01.corp.com |
| InfrastructureRoleOwner | DC01.corp.com |
| Name | corp.com |

列表 666 - 来自 System.DirectoryServices 的 Domain 类

根据此输出，域名为 "corp.com"，主域控制器名称为 "DC01.corp"⁶⁸。

我们可以以此程序化构建 LDAP 提供程序路径。让我们在简单的 PowerShell 脚本中使用 `Name` 和 `PdcRoleOwner` 来构建以下内容：

```powershell
$domainObj = [System.DirectoryServices.ActiveDirectory.Domain]::GetCurrentDomain()
$PDC = ($domainObj.PdcRoleOwner).Name
$SearchString = "LDAP://"
$SearchString += $PDC + " /"
$DistinguishedName = "DC=$($domainObj.Name.Replace('.','DC='))"
$SearchString += $=$DistinguishedName
$SearchString
```

列表 667 - 构建 LDAP 提供程序路径

在此脚本中，`$domainObj` 将存储域对象，`$PDC` 将存储 PDC 的名称，`$SearchString` 将构建根路径。注意 `DistinguishedName` 将

# 攻击性安全

由我们的域名（'corp.com'）拆分为单个域名组件（DC），从而生成的区分名称（DistinguishedName）为 'DC=corp,DC=com$，如脚本输出所示：

```
LDAP://DC01.corp.com/DC=com
```

列表 668 - 完整的 LDAP 提供程序路径

这是对域控制器执行 LDAP 查询时所需的完整 LDAP 提供程序路径。

现在我们可以使用 LDAP 提供程序路径实例化 `DirectorySearcher` 类。要使用 `DirectorySearcher` 类，我们必须指定 `SearchRoot`（搜索根），它是 Active Directory 层次结构中搜索开始的节点。

搜索根的形式为从 `DirectoryEntry` 类实例化的对象。当向构造函数传递任何参数时，`SearchRoot` 将指示每个搜索都从 Active Directory 返回结果。列表 669 显示了实现此目的脚本相关部分：

```powershell
```
