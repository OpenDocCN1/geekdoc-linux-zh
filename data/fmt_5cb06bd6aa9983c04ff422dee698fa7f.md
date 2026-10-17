
$domainObj = [System.DirectoryServices.ActiveDirectory.Domain]::GetCurrentDomain()

$PDC = ($domainObj.PdcOwner).Name

$SearchString = "LDAP://"

$SearchString += $PDC + " /"

$DistinguishedName = "DC=$($domainObj.Name).Replace('.','DC=')"

$SearchString += $DistinguishedName

```
```powershell

$Searcher = New-Object System.DirectoryServices.DirectorySearcher([ADSI]$SearchString)

$objDomain = New-Object System.DirectoryServices.DirectoryEntry

$Searcher.SearchRoot = $objDomain

```
### 列表 669 - 创建 DirectorySearcher

通过我们的 `DirectorySearcher` 对象，我们可以执行搜索。然而，如果没有任何过滤器，我们将接收整个域中的所有对象。

设置过滤的一种方法是通过 `samAccountType` 属性，这是一个用户、计算机和组对象都拥有的属性。请参阅链接引用获取更多示例，但在这种情况下，我们可以向 `filter` 属性提供 `0x03000000`（十进制 503530638）来枚举域中的所有用户，如列表 670 所示：

```powershell

$domainObj = [System.DirectoryServices.ActiveDirectory.Domain]::GetCurrentDomain()

$PDC = ($domainObj.PdcOwner).Name

$SearchString = "LDAP://"

$SearchString += $PDC + " /"

$DistinguishedName = "DC=$($domainObj.Name.Replace('.','DC='))"

$SearchString += $DistinguishedName

$Searcher = New-Object System.DirectoryServices.DirectorySearcher([ADSI]$SearchString)

$objDomain = New-Object System.DirectoryServices.DirectoryEntry

$Searcher.SearchRoot = $objDomain

$Searcher.filter="samAccountType=80530638"

$Searcher.FindAll()

```

### 列表 670 - 搜索用户的代码段

我们通过 `$Searcher` 对象的 `.filter` 属性添加了 `samAccountType` 过滤器，并调用了 `FindAll` 方法进行搜索并找到符合配置过滤器的结果。

运行此脚本时，它应该枚举域中的所有用户：

| 路径 | 属性 |
|---|---|
| LDAP://CN=Administrator,CN=DC=corp,DC=com | {admincount...} |
| LDAP://CN=Guest,CN=DC=corp,DC=com | {iscritical...} |
| LDAP://CN=DefaultAccount,CN=DC=corp,DC=com | {iscritical...} |
| LDAP://CN=krbtgt,OU=DC=corp,DC=com | {msd-...} |
| LDAP://CN=WebJeff,OU=Admins,OU=CorpUsers,DC=corp,DC=com | {givenname} |
| LDAP://CN=Jeff_Admin,OU=Admins,DC=corp,DC=com | {givenname} |
| LDAP://CN=Adam,OU=Normal,OU=CorpUsers,DC=corp,DC=com | {givenname} |
| LDAP://CN=is_service,OU=ServiceAccounts,OU=CorpUsers,DC=corp,DC=com | {givenname...} |

### 列表 671 - 域中的用户

这些信息很有用，但我们应该对其进行清理。由于用户对象的属性存储在 `Properties` 字段中，可以使用一个简单的循环来单独打印每个属性。完整的 PowerShell 脚本将收集所有用户及其属性：

```powershell

$domainObj = [System.DirectoryServices.ActiveDirectory.Domain]::GetCurrentDomain()

$PDC = ($domainObj.PdcOwner).Name

$SearchString = "LDAP://"

$SearchString += $PDC + " /"

$DistinguishedName = "DC=$($domainObj.Name.Replace('.','DC='))"

$SearchString += $DistinguishedName

$Searcher = New-Object System.DirectoryServices.DirectorySearcher([ADSI]$SearchString)

$objDomain = New-Object System.DirectoryServices.DirectoryEntry

$Searcher.SearchRoot = $objDomain

$Searcher.filter="samAccountType=80530638"

$Result = $Searcher.FindAll()

foreach($obj in $Result) {

  foreach($prop in $obj.Properties) {

    $prop

  }

}

Write-Host "----------------------------------"

```

### 列表 672 - 枚举所有用户的 PowerShell 脚本

由于用户对象具有许多属性，检索的信息可能会让人眼 overwhelming。下面的列表显示了 Jeff_Admin 属性的部分视图。

| 属性 | 值 |
|---|---|
| admincount | {1} |
| accountcontrol | {6604} |
| badpasswordcount | {0} |
| badpasswordtime | {0} |
| cn | {Jeff_Admin} |
| created | {05/02/2018 18:33:10} |
| displayname | {Jeff_Admin} |
| lastlogon | {0} |
| samAccountType | {80530638} |
| countrycode | {0} |
| objectid | {15002100195240975338661233} |
| logoncount | {0} |
| primarygroup | {513} |
| objectcategory | {CN=Person,CN=Schema,CN=Configuration,DC=com} |
| userprincipalname | {jeff_admin@corp.com} |
| dscorepropagationdata | {05/02/2018 19.20.52, 01/01/1601 00.00.00} |
| distinguishedname | {CN=Jeff_Admin,OU=Admins,OU=CorpUsers,DC=corp,DC=com} |
| objectClass | {top, person, organizationalPerson, user} |
| uncreated | {12879} |

### 列表 673 - 所有用户及其属性

根据上述信息，Jeff Admin 账户是域管理员组的成员。使用我们的 `DirectorySearch` 对象，我们可以使用过滤器来定位特定组（如域管理员），或者使用过滤器专门搜索 Jeff Admin 用户。

在 `filter` 属性中，我们可以设置任何定义的对象类型。例如，我们可以使用 `name` 属性为 Jeff_Admin 创建过滤器，如下：

```powershell

$Searcher.filter="name=Jeff_Admin"
```
