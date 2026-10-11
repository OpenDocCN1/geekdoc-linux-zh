

```powershell
$SearchString = "LDAP:///"

$SearchString += $PDC + "/"

$DistinguishedName = "DC=$($domainObj.Name.Replace('.',' ,DC='))"

$SearchString += $DistinguishedName

$Searcher = New-Object System.DirectoryServices.DirectorySearcher([ADSI]$SearchString)

$objDomain = New-Object System.DirectoryServices.DirectoryEntry

$Searcher.SearchRoot = $objDomain

$Searcher.filter = "samAccountType=805306368"

$Searcher.FindAll()
```

**列表 670 - 用于搜索用户的代码片段**

我们通过在 $Searcher 对象的 `filter` 属性中添加 samAccountType 过滤器，然后调用 `FindAll` 方法来执行搜索并找出所有符合配置过滤器的结果。

运行此脚本时，它应该枚举域中的所有用户：

| 路径 | 属性 |
| :--- | :--- |
| LDAP:///CN=Administrator, CN= Users, DC=corp, DC=com | {admincount... |
| LDAP:///CN=Guest, CN= Users, DC=corp, DC=com | {iscritical... |
| LDAP:///CN=Default Account, CN= Users, DC=corp, DC=com | {iscritical... |
| LDAP:///CN=krbtgt, CN= Users, DC=corp, DC=com | {msds... |
| LDAP:///CN=Offsec, OU=Admins, OU=CorpUsers, DC=corp, DC=com | {givenname... |
| LDAP:///CN=Jeff_Admins, OU=CorpUsers, DC=corp, DC=com | {givenname... |
| LDAP:///CN=Adam, OU=Normal, OU=CorpUsers, DC=corp, DC=com | {givenname... |
| LDAP:///CN=iis_service, OU=ServiceAccounts, OU=CorpUsers, DC=corp, DC=com | {givenname... |
| LDAP:///CN=sql_service, OU=ServiceAccounts, OU=CorpUsers, DC=corp, DC=com | {givenname... |

**列表 671 - 域中的用户**

这是一个很好的信息，但我们应该对其进行一些整理。由于用户对象的属性存储在 `Properties` 字段中，我们可以实现一个双重循环，将每个属性打印在单独的一行上。

完整的 PowerShell 脚本将收集所有用户及其属性：

```powershell
$domainObj = [System.DirectoryServices.ActiveDirectory.Domain]::GetCurrentDomain()

$PDC = ($domainObj.PdcRoleOwner).Name

$SearchString = "LDAP:///"

$SearchString += $PDC + "/"
```

[^623]: [Microsoft, 2018](https://docs.microsoft.com/en-us/dotnet/api/system.directoryservices.directorysearcher.findall?view=netframework-4.8).

```powershell
$DistinguishedName = "DC=$($domainObj.Name.Replace('.',' ,DC='))"

$SearchString += $DistinguishedName

$Searcher = New-Object System.DirectoryServices.DirectorySearcher([ADSI]$SearchString)

$objDomain = New-Object System.DirectoryServices.DirectoryEntry

$Searcher.SearchRoot = $objDomain

$Searcher.filter="samAccountType=805306368"

$Result = $Searcher.FindAll()

Foreach($obj in $Result)
{
    Foreach($prop in $obj.Properties)
    {
        $prop
    }

    Write-Host "--------------------------"
```

**列表 672 - 枚举所有用户的 PowerShell 脚本**

检索到的信息可能非常令人不知所措，因为用户对象有许多属性。下面的列表显示了 Jeff\_Admin 用户属性的部分视图。

| 属性 | 值 |
| :--- | :--- |
| givenname | {Jeff_Admin} |
| samaccountname | {jeff_admin} |
| cn | {Jeff_Admin} |
| pwdlastset | {13162329100859206} |
| whencreated | {05/02/2018 18.33.10} |
| badpwdcount | {0} |
| displayname | {Jeff_Admin} |
| lastlogon | {0} |
| samaccounttype | {805306368} |
| countrycode | {0} |
| objectguid | {130 114 89 75 220 233 3 76 170 206 193 232 122 112 176 32} |
| usnchanged | {12938} |
| whenchanged | {05/02/2018 19.20.52} |
| name | {Jeff_Admin} |
| objectsid | {1 5 0 0 0 0 0 0 5 21 0 0 0 195 240 137 95 239 58 38 166 116 233} |
| logoncount | {0} |
| badpasswordtime | {0} |
| accountexpires | {9223372036854775807} |
| primarygroupid | {513} |
| objectcategory | {CN=Person,CN=Schema,CN=Configuration,DC=corp,DC=com} |
| userprincipalname | {jeff_admin@corp.com} |
| useraccountcontrol | {66048} |
| admincount | {1} |
| dscoreregulationdata | {05/02/2018 19.20.52, 01/01/1601 00.00.00} |
| distinguishedname | {CN=Jeff_Admin,OU=Admins,OU=CorpUsers,DC=corp,DC=com} |
| objectclass | {top, person, organizationalPerson, user} |
| usncreated | {12879} |
| memberof | {CN=Domain Admins, CN= Users, DC=corp, DC=com} |
| adspath | {LDAP://CN=Jeff_Admin, OU=Admins, OU=CorpUsers, DC=corp, DC=com} |
| ... | ... |

**列表 673 - 所有用户及相关属性**

根据上述输出，Jeff\_Admin 账户是域管理员组（Domain Admins）的成员。使用我们的 DirectorySearcher 对象，我们可以使用过滤器来定位特定组（如域管理员）的成员，或者使用过滤器专门搜索 Jeff\_Admin 用户。

在 filter 属性中，我们可以设置我们想要的对象类型的任何属性。例如，我们可以使用 name 属性为 Jeff\_Admin 用户创建过滤器，如下所示：

```powershell
$Searcher.filter="name=Jeff\_Admin"
```

**列表 674 - 过滤结果仅保留 Jeff\_Admin**

虽然这个脚本乍一看可能令人生畏，但它非常灵活，可以修改以协助其他 AD 枚举任务。

## 21.2.2.1 练习

- 1. 修改 PowerShell 脚本，使其仅返回域管理员组的成员。
- 2. 修改 PowerShell 脚本，使其返回域中的所有计算机。
- 3. 添加一个过滤器，使其仅返回运行 Windows 10 的计算机。

## 21.2.3 解决嵌套组

接下来，让我们使用新开发的 PowerShell 脚本来解析我们在 net.exe 中遇到的嵌套组。

第一项任务是定位域中的所有组并打印它们的名称。为此，我们将创建一个过滤器，提取所有 objectClass 设置为 "Group" 的记录，并且我们将仅打印每个组的 name 属性，而不是所有属性。

[^624]: [Microsoft, 2018](https://docs.microsoft.com/en-us/windows/win32/ad/object-class-and-object-category).

列表 675 显示了修改后的脚本，并高亮显示了更改部分。

```powershell
$domainObj = [System.DirectoryServices.ActiveDirectory.Domain]::GetCurrentDomain() 

$PDC = ($domainObj.PdcRoleOwner).Name 

$SearchString = "LDAP://" 

$SearchString += $PDC + "/" 

$DistinguishedName = "DC=$($domainObj.Name.Replace('.',' ,DC='))" 

$SearchString += $DistinguishedName 

$Searcher = New-Object System.DirectoryServices.DirectorySearcher([ADSI]$SearchString) 

$objDomain = New-Object System.DirectoryServices.DirectoryEntry

$Searcher.SearchRoot = $objDomain  
$Searcher.filter="(objectClass=Group)"  
$Result = $Searcher.FindAll()  
Foreach($obj in $Result)  
{  
$obj.Properties.name  
}
```

**列表 675 - 用于枚举所有域组的修改版 PowerShell 脚本**

执行时，脚本输出域中所有组的列表。列表 676 中显示的截断输出揭示了组 Secret_Group、Nested_Group 和 Another_Nested_Group：

```text
...  
Key Admins  
Enterprise Key Admins  
DnsAdmins  
DnsUpdateProxy  
Secret_Group  
Nested_Group  
Another_Nested_Group
```

**列表 676 - 枚举域组的截断输出**

现在，让我们尝试通过为 name 属性设置适当的过滤器来列出 Secret_Group 的成员。

此外，我们将只显示 member 属性以获取组成员。实现此功能的修改后的 PowerShell 脚本显示在列表 677 中，并高亮显示了更改部分：

```powershell
$domainObj = [System.DirectoryServices.ActiveDirectory.Domain]::GetCurrentDomain()  
$PDC = ($domainObj.PdcRoleOwner).Name  
$SearchString = "LDAP://"  
$SearchString += $PDC + "/"  
$DistinguishedName = "DC=$($domainObj.Name.Replace('.',' ,DC='))"  
$SearchString += $DistinguishedName  
$Searcher = New-Object System.DirectoryServices.DirectorySearcher([ADSI]$SearchString)  
$objDomain = New-Object System.DirectoryServices.DirectoryEntry  
$Searcher.SearchRoot = $objDomain  
$Searcher.filter="(name=Secret_Group)"  
$Result = $Searcher.FindAll()  
Foreach($obj in $Result)
{
    $obj.Properties.member
}
```

**列表 677 - 用于枚举组成员的 PowerShell 脚本**

修改后的脚本将转储 DistinguishedName 组成员的名称：

```text
CN=Nested_Group,OU=CorpGroups,DC=corp,DC=com
```

**列表 678 - 组 Secret_Group 的成员**

根据此输出，Nested_Group 是 Secret_Group 的成员。为了枚举其成员，我们必须重复上述步骤以列出 Nested_Group 的成员。我们可以通过替换过滤器条件中的组名来实现：

```powershell
...
$Searcher.SearchRoot = $objDomain
$Searcher.filter="(name=Nested_Group)"
...
```

**列表 679 - 获取 Nested_Group 的成员**

此更新脚本生成列表 680 中显示的输出：

```text
CN=Another_Nested_Group,OU=CorpGroups,DC=corp,DC=com
```

**列表 680 - 组 Nested_Group 的成员**

这表明 Another_Nested_Group 是 Nested_Group 的唯一成员。我们需要再次修改并运行脚本，替换过滤器条件中的组名。

```powershell
...
$Searcher.SearchRoot = $objDomain
$Searcher.filter="(name=Another_Nested_Group)"
...
```

**列表 681 - 获取 Another_Nested_Group 的成员**

下一次搜索的输出显示在列表 682 中。

```text
CN=Adam,OU=Normal,OU=CorpUsers,DC=corp,DC=com
```

**列表 682 - 组 Another_Nested_Group 的成员**

最后，我们发现域用户 Adam 是 Another_Nested_Group 的唯一成员。这结束了所需枚举以解开嵌套组，并展示了如何利用 PowerShell 和 LDAP 来执行这种类型的查找。

## 21.2.3.1 练习

- 1. 重复枚举以揭示 Secret_Group、Nested_Group 和 Another_Nested_Group 之间的关系。
- 2. 本节中展示的脚本要求我们在每次迭代时更改组名。调整该脚本，以便在事先不知道组名的情况下，通过编程方式解开嵌套组。

