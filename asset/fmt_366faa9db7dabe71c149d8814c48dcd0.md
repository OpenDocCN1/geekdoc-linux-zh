
为了便于管理各种对象并辅助管理工作，系统管理员通常会将这些对象组织到组织单元（Organizational Units, OUs）中¹¹⁰⁰⁸

OU 类似于文件文件夹，因为它们是存储域内对象的容器。计算机对象代表已加入域（域的一部分）的实际服务器和工作站；AD 对象代表可以用于登录加入域计算机的账户。此外，所有 AD 对象都包含属性，这些属性根据对象的类型而异。例如，用户对象可能包括由于名字、用户名、电话号码等属性。

AD 依赖于多个组件和通信服务。例如，当用户尝试登录域时，请求会发送到域控制器（DC）。¹¹⁰⁹ DC 会检查用户是否允许登录域。一个或多个 DC 充域的核心和枢纽，存储所有的对象及其属性。由于 DC 是域的中心组件，我们在枚举 AD 时将特别关注它。

对象可以分配给 AD 组，以便管理员将这些对象作为一个单元进行管理。例如，某组中的用户可以获得文件服务器的访问权限，或获得域内各种客户端的管理员权限。攻击者通常针对高权限组。

域管理员（Domain admins）¹¹¹⁰ 是域中权限最高的对象之一。如果攻击者攻破了该组的成员（通常称为 AD 管理员），他们实质上获得了对域的完全控制。

这种攻击向量可能会扩展到单个域之外，因为一个 AD 实例可以托管一个域或域森林中的多个域。虽然森林中的每个域都有一个域管理员组，但企业管理员（Enterprise Admins）组的成员被授予了对森林中所有域的完全控制权，并对所有 DC 拥有管理员权限。这显然是攻击者的一个高价值目标。

我们将在本模块中利用这些和其他概念，专注于 AD 极其重要的方面。这门重要的学科可以提高我们在攻击阶段的成功率。我们将使用多种工具进行手动枚举。

# OffSec

## 使用 Kali Linux 进行渗透测试

该域。我们将为用户提供 `/u`，为域名提供 `/d` 并输入密码，在此例中，密码为 `LegionTeamBenzoin!!`

```
kali@kali:~ xfreedp /u:stephanie:d:corp.com /v:192.168.50.75
```

列表 711 - 使用 "`xfreedp`" 连接到 Windows 11 客户端

AD（活动目录）包含的信息非常多，以至于很难确定从何处开始枚举。但每个 AD 安装从根本上说都包含用户和组，我们将从这里开始。

为了收集用户信息，我们将使用 `net.exe`¹1012，它是所有 Windows 操作系统上默认安装的。更具体地说，我们将使用 `net user` 子命令¹1013。虽然我们可以使用此工具列出机器上的账户，但我们将使用 `/domain` 来打印出域中的用户。

```
C:\Users\stephanie>net user /domain
请求将在域 corp.com 的域控制器上处理。
```

\DC1.com 的用户账户

| Administrator | dave | Guest |
| :--- | :--- | :--- |
| iis_service | jeff | jeffadmin |
| jen | krbtgt | pete |
| stephanie | | |
| 命令已成功完成。 | | |

列表 712 - 运行 "`net user`" 显示域中的用户

此命令的输出将取决于组织的大小。有了用户列表后，我们现在可以查询有关单个用户的信息。

管理员往往倾向在用户名上添加前缀或后缀，以通过其功能识别账户。根据列表 711 中的输出，我们应该检查 `jeffadmin` 用户，因为它可能是一个管理账户。

让我们使用 `net.exe` 和 `/domain` 标志来检查用户：

```
C:\Users\stephanie>net user jeffadmin /domain
请求将在域 corp.com 的域控制器上处理。
```

| 用户名 | jeffadmin |
| :--- | :--- |
| 全名 | |
| 注释 | |
| 用户注释 | 000 (系统默认) |
| 账户/区域代码 | |
| 账户活动 | 是 |
| 账户过期 | 从不 |
| 密码最后设置 | 2022/9/2 下午 4:26:48 |
| 密码过期 | 从不 |
| 密码可更改性 | 2022/9/3 下午 4:26:48 |
| 需要密码 | 是 |
| 用户可以更改密码 | 是 |
| 允许的工作站 | 所有 |
| 登录脚本 | |
| 用户配置文件 | |
| 主目录 | |
| 最后登录 | 2022/9/20 上午1:36:09 |
| 允许的登录时间 | 所有 |
| 本地组成员身份 | *Administrators |
| 全局组成员身份 | *Domain Users *Domain Admins |

命令已成功完成。

列表 713 - 针对特定用户运行 '`net user`'

根据输出，`jeffdavid` 是 Domain Admins 组的一部分，这是我们应该注意的。如果我们能够攻破此账户，我们将提升为域管理员。

我们还可以使用 `net.exe` 通过 `net group` 来枚举域：

```
C:\Users\stephanie>net group /domain
请求将在域 corp.com 的域控制器上处理。
```

+ 组账户 \DC1.corp.com
* 可复制的域控制器
* Debug
* Development Department
* DnUpdateProxy
* Domain Admins
* Domain Computers
* Domain Controllers
* Domain Guests
* Domain Users
* Enterprise Admins
* Enterprise Key Admins
* Enterprise Read-only Domain Controllers
* Group Policy Creator Owners
* Key Admins
* Management Department
* Protected Users
* Read-only Domain Controllers
* Sales Department
* Schema Admins

命令已成功完成。

列表 714 - 运行 "`net group`" 显示域中的组

![](img/987dc9f6ebd8893c565a1d124d7724e6_692_0.png)

输出包含了域中很长的组列表。其中一些是默认安装的¹⁰⁵。其他的，如上面高亮的的，是自定义组。让我们先枚举一个自定义组。我们将使用 `net.exe` 来枚举组成员，这次关注 Sales Department（销售部）。

```
PS C:\Tools> net group "Sales Department" /domain
请求将在域 corp.com 的域控制器上处理。
```

| 组名 | Sales Department |
| :--- | :--- |
| 注释 | |
| 成员 | pete stephanie |

命令已成功完成。

列表 715 - 运行 '`net group`' 显示特定组中的成员

这显示 `pete` 和 `stephanie` 是 Sales Department 的成员。尽管这看起来不多，但通过枚举获得的每一条小信息都可能具有价值。在现实世界的场景中，我们可能会枚举每个组并编目录结果。这需要良好的组织，但我们有比 `net.exe` 更灵活的替代方案。

## 2.2.2 使用 PowerShell 和 .NET 枚举活动目录

有几种工具可以用来枚举活动目录。PowerShell cmdlet（如 `ADUser`¹⁰⁶）效果良好，但它们仅作为远程服务器管理工具 (RSAT)⁷ 的部分默认安装在域控制器上。RSAT 在客户端上很少，我们必须安装它。在客户端上，我们有比 `net.exe` 更灵活的替代方案。

在枚举活动目录之前，我们必须理解它。在开始之前，让我们讨论一下。为了枚举活动目录，我们首先需要管理员权限。在客户端上，我们有比 `net.exe` 更灵活的替代方案。

在实际场景中，我们使用 PowerShell 来枚举。在。。。。。。。。。。。。。。。我们将使用 .NET 来枚举。在。在。上。。。。。。。。。。。。。。。。。。。根据 Microsoft 的文档¹⁰⁰，LDAP 格式如下：

```
LDAP://[DistinguishedName]
```

列表 716 - LDAP 格式

# OffSec

## 使用 Kali Linux 进行渗透测试

`stephanie` 域用户。我们知道 `stephanie` 是 `corp.corp` 域中的一个用户对象。据此，其 DN（区分名称）（尽管我们还无法确定）可能如下：

```
CN=Stephanie, CN=Users, DC=corp, DC=com
```

列表 717 - 区分名称（Distinguished Name）示例
