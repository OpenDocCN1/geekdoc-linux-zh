
# OffSec

使用 Kali Linux 进行渗透测试

`DirectorySearch` 类通过 LDAP 查询活动目录（AD）。在创建 `DirectorySearcher` 实例时，我们必须以 `SearchRoot` 属性的形式指定我们想要查询的 AD 服务。根据微软文档，该属性指示了搜索在 AD 层次结构中开始的位置。由于 `DirectoryEntry` 封装了指向层次结构顶部的 LDAP 路径，我们将将其作为一个变量传递给 `DirectorySearcher`。

`DirectorySearcher` 文档列出了 `FindAll()`，它会返回在 AD 中找到的所有条目的集合。

让我们将这两个类实现到脚本中。下面的代码显示了脚本的相关部分：

```powershell
$PDC =
[System.DirectoryServices.ActiveDirectory.Domain]::GetCurrentDomain().PdcOwner.Name
$DN = (($adsi').distinguishedName
$LDAP = "LDAP://$PDC\$DN"

$directory = New-Object System.DirectoryServices.DirectoryEntry($directory)
$dirsearcher = New-Object System.DirectoryServices.DirectorySearch($directory)
$dirsearcher.FindAll()
```

列表 728 - 将 Directory 和 DirectorySearch 添加到脚本

如列表 728 所示，我们添加了 $directory 变量，它封装了我们的 LDAP 路径。$dirsearcher 变量包含了 $directory 变量，并使用该信息作为 `SearchRoot`，指向层次结构的顶部，`DirectorySearch` 将在那里运行 `FindAll()`。

现在，由于我们开始搜索 AD 而没有对结果进行过滤，它将产生大量的输出。不过，让我们运行它：

PS C:\Users\stepanie\.enumeration.ps1

```text
Path
----
LDAP://DC1.domain.com/DC=dc,DC=com
LDAP://DC1.domain.com/CN=Users,DC=dc,DC=com
LDAP://DC1.domain.com/CN=Computers,DC=dc,DC=com
LDAP://DC1.domain.com/OU=Domain Controllers,DC=dc,DC=com
LDAP://DC1.domain.com/CN=System,DC=dc,DC=com
LDAP://DC1.domain.com/CN=FoundAndAbandoned,DC=dc,DC=com
LDAP://DC1.domain.com/CN=Infrastructure,DC=dc,DC=com
LDAP://DC1.domain.com/CN=SecurityPrincipals,DC=dc,DC=com
LDAP://DC1.domain.com/CN=Program Data,DC=dc,DC=com
LDAP://DC1.domain.com/CN=Microsoft,CN=Program Data,DC=dc,DC=com
LDAP://DC1.domain.com/CN=NTQuotes,DC=dc,DC=com
LDAP://DC1.domain.com/CN=Managed Service Accounts,DC=dc,DC=com
LDAP://DC1.domain.com/CN=Keys,DC=dc,DC=com
```

1029 (Microsoft), https://learn.microsoft.com/en-us/dotnet/api/system.directoryservices.directorysearcher?view=dotnet-plat-6.0

1029 (Microsoft), https://learn.microsoft.com/en-us/dotnet/api/system.directoryservices.directorysearcher.findall?view=dotnet-plat-ext-7.0#system-directoryservices-directorysearcher-findall

PWK - © 2023 OffSec Services Limited. 版权所有。

# OffSec 使用 Kali Linux 进行渗透测试

LDAP://DC1.corp.com/CN=WinsockServices,CN=System,DC=corp,DC=com evenLDAP://DC1.corp.com/CN=RpcServices,CN=System,DC=corp,DC=com
LDAP://DC1.corp.com/CN=FileLinks,CN=System,DC=corp,DC=com
LDAP://DC1.corp.com/CN=VolumeTable,CN=FileLinks,CN=System,DC=corp,DC=com
LDAP://DC1.corp.com/CN=ObjectTable,CN=FileLinks,CN=System,DC=corp,DC=com

> 列表 729 - 使用我们的脚本搜索 AD

如列表 729 的截断列表所示，脚本并没有产生大量文本。事实上，我们正在接收整个域中的所有对象。这至少证明了脚本按预期工作。

过滤输出非常简单，有几种方法可以实现。其中一种方法是使用过滤器来筛选 `samAccountType` 属性，该属性应用于所有用户、计算机和组对象。

官方文档揭示了 `samAccountType` 属性的不同值，但我们将从 0x30000000（十进制 805306368）开始，它识别域中的所有用户。要在我们的脚本中实现过滤器，我们只需如下所示将过滤器添加到 `DirectorySearcher` 过滤器中：

```powershell
$PDC =
[System.DirectoryServices.ActiveDirectory.Domain]::GetCurrentDomain().PdcOwner.Name
$DN = ($AD).distinguishedName
LDAP = "LDAP://$PDC\$DN"
```

```powershell
$directoryentry = New-Object System.DirectoryServices.DirectoryEntry($LDAP)
$dirsearcher = New-Object System.DirectoryServices.DirectorySearcher($directoryentry)
$dirsearcher.filter="samAccountType=805306368"
$dirsearcher.FindAll()
```

> 列表 730 - 使用我们的脚本搜索 AD

过滤输出非常简单，有几种方法可以实现。其中一种方法是使用过滤器来筛选 `samAccountType` 属性，该属性应用于所有用户、计算机和组对象。

官方文档揭示了 `samAccountType` 属性的不同值，但我们将从 0x30000000（十进制 805306368）开始，它识别域中的所有用户。要在我们的脚本中实现过滤器，我们只需如下所示将过滤器添加到 `DirectorySearcher` 过滤器中：

| 路径 | 属性 |
|---|---|
| LDAP://DC1.domain.com/DC=dc,DC=com | |
| LDAP://DC1.domain.com/CN=Users,DC=dc,DC=com | |
| LDAP://DC1.domain.com/CN=Computers,DC=dc,DC=com | |
| LDAP://DC1.domain.com/OU=Domain Controllers,DC=dc,DC=com | |
| LDAP://DC1.domain.com/CN=System,DC=dc,DC=com | |
| LDAP://DC1.domain.com/CN=FoundAndAbandoned,DC=dc,DC=com | |
| LDAP://DC1.domain.com/CN=Infrastructure,DC=dc,DC=com | |
| LDAP://DC1.domain.com/CN=SecurityPrincipals,DC=dc,DC=com | |
| LDAP://DC1.domain.com/CN=Program Data,DC=dc,DC=com | |
| LDAP://DC1.domain.com/CN=Microsoft,CN=Program Data,DC=dc,DC=com | |
| LDAP://DC1.domain.com/CN=NTQuotes,DC=dc,DC=com | |
| LDAP://DC1.domain.com/CN=Managed Service Accounts,DC=dc,DC=com | |
| LDAP://DC1.domain.com/CN=Keys,DC=dc,DC=com | |

