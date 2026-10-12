
LDAP://DC1.corp.com/CN=Microsoft,Program Data,DC=corp,DC=com

LDAP://DC1.corp.com/CN=NTQuotes,DC=corp,DC=com

LDAP://DC1.corp.com/CN=Managed Service Accounts,DC=corp,DC=com

LDAP://DC1.corp.com/CN=Keys,DC=corp,DC=com

![](img/987dc9f6ebd8893c565a1d124d7724e6_699_0.png)

1028 (Microsoft), https://learn.microsoft.com/en-us/dotnet/api/system.directoryservices.directorysearcher?view=dotnet-plat-ext-0

1029 (Microsoft), https://learn.microsoft.com/en-us/dotnet/api/system.directoryservices.directorysearcher.findall?view=dotnet-plat-ext-0.7#system-directoryservices-directorysearcher-findall

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

LDAP://DC1.corp.com/CN=WinsockServices,CN=System,DC=corp,DC=com
LDAP://DC1.corp.com/CN=RpcLinks,CN=System,DC=corp,DC=com
LDAP://DC1.corp.com/CN=FileLinks,CN=System,DC=corp,DC=com
LDAP://DC1.corp.com/CN=VolumeTable,CN=FileLinks,CN=System,DC=corp,DC=com
LDAP://DC1.corp.com/CN=ObjectTable,CN=FileLinks,CN=System,DC=corp,DC=com

## 列表 729 - 使用我们的脚本搜索 AD

如截断的列表 729 所示，脚本并没有产生大量文本。事实上，我们正在接收整个域中的所有对象。这证明了脚本正按预期工作。

过滤输出相当简单，有几种方法可以实现。一种方法是设置一个过滤器来筛选 `samAccountType`，这是一个应用于所有用户、计算机和组的属性。

官方文档显示了 `samAccountType` 属性的不同值，但我们将从 0x3000000（十进制 50336638）开始，这将列举域中的所有用户。要在我们的脚本中实现过滤器，我们可以简单地将过滤器添加到 `DirectorySearcher` 过滤器中，如下所示：

```
$PDC = [System.DirectoryServices.Directory]::GetCurrentDomain().PdcOwner.Name

DN = (([adsi]).distinguishedName

$LDAP = "LDAP://$DN$"
```

## 列表 730 - 使用 samAccountType 属性过滤普通用户账户

运行我们的脚本会显示域中的所有用户：

```
PS C:\Users\stephanie> enumeration.ps1
```

| Path | Properties |
|---|---|
| LDAP://DC1.corp.com/CN=Administrator,CN=Users,DC=corp,DC=com | {logoncount, objectcategory, description...} |
| LDAP://DC1.corp.com/CN=Guest,CN=Users,DC=corp,DC=com | {logoncount, objectcategory, description...} |
| LDAP://DC1.corp.com/CN=krbtgt,CN=Users,DC=corp,DC=com | {logoncount, objectcategory, description...} |
| LDAP://DC1.corp.com/CN=dave,CN=Users,DC=corp,DC=com | {logoncount, objectcategory, description...} |
| LDAP://DC1.corp.com/CN=stephanie,CN=Users,DC=corp,DC=com | {logoncount, objectcategory, description...} |
| LDAP://DC1.corp.com/CN=jeff,CN=Users,DC=corp,DC=com | {logoncount, objectcategory, description...} |
| LDAP://DC1.corp.com/CN=jeffadmin,CN=Users,DC=corp,DC=com | {logoncount, objectcategory, description...} |
| LDAP://DC1.corp.com/CN=service,CN=Users,DC=corp,DC=com | {logoncount, objectcategory, description...} |
| LDAP://DC1.corp.com/CN=pete,CN=Users,DC=corp,DC=com | {logoncount, objectcategory, description...} |
| LDAP://DC1.corp.com/CN=jen,CN=Users,DC=corp,DC=com | {logoncount, objectcategory, description...} |

1033 (Microsoft), https://learn.microsoft.com/en-us/windows/win32/adschema/samaccounttype

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

## 列表 731 - 在域上注册 samAccountType 过滤器

这非常有用，但我们需要进一步开发。在枚举 AD 时，我们对每个对象的属性感兴趣，它们存储在 `Properties` 字段中。我们可以从新的搜索中获取结果，并通过嵌套循环遍历每个对象找到每个属性。

```
$domainObj = [System.DirectoryServices.ActiveDirectory]::GetCurrentDomain()

$POC = $domainObj.PdcRoot.Name

$DN = (([adsi]).distinguishedName

$LDAP = "LDAP://$POC/$DN"
```

```
$dentry = New-Object System.DirectoryServices.DirectoryEntry($LDAP)

$dsearcher = New-Object System.DirectoryServices.DirectorySearcher($dentry)

$dsearcher.filter="samAccountName=8053368"

$result = $dsearcher.FindAll()
```

## 列表 732 - 添加嵌套循环以使每个属性单独打印

```
foreach($obj in $result) {

  foreach($prop in $obj.Properties) {

    $prop

  }

}

Write-Host "-----------------"
```

这个完整的脚本将搜索 AD 并根据我们选择的 `samAccountType` 过滤结果，将结果放入 `$result` 变量。然后它根据两个 `foreach` 循环进一步处理结果。第一个循环提取 `$result` 中的对象并放入 `$obj` 变量。第二个循环提取每个对象的所有属性并存储在 `$prop` 变量中。脚本将打印 `$prop` 并在输出。

虽然脚本运行不需要 `Write-Host`，但它会在每个对象之间打印一行。这有助于输出变得易读。

脚本将输出大量信息，取决于域用户数量。下面的列表提供了 `jeffadmin` 属性的部分视图：

```
PS C:\Users\stephanie> .enumeration.ps1

...

logoncount {173}

cepage {0}

objectcategory {CN=Person,CN=Schema,CN=Configuration,DC=corp,DC=com}

dpropagationatime {(9/3/2022 6:25:58 AM, 9/2/2022 11:26:49 PM, 1/1/1661)}
```
