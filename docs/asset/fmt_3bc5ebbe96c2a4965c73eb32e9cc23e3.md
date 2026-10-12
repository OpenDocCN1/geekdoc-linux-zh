
$^{619}$ (Microsoft, 2018), https://msdn.microsoft.com/en-us/library/49s2h23\{(v=vs.110).aspx$
$^{620}$ (Microsoft, 2018), https://msdn.microsoft.com/en-us/library/system.directoryservices.directoryentry(v=vs.110).aspx$
$^{621}$ (Microsoft, 2018), https://msdn.microsoft.com/en-us/library/ms679637(v=vs.85).aspx$
$^{622}$ (Microsoft, 2018), https://msdn.microsoft.com/en-us/library/ms679637(v=vs.85).aspx$

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

## 列表 670 - 用于搜索用户的代码片段

我们通过在 `$Searcher` 对象的 `filter` 属性中添加 `samAccountType` 过滤器，然后调用 `FindAll` 方法来执行搜索并找出所有符合配置过滤器的结果。

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

## 列表 671 - 域中的用户

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
