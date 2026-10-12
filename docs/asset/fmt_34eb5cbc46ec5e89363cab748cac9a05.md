
```
12:00:00 AM {52775}

changed (4)

instancetype {jeffadmin}

name badpasswordtime

pwdlastlistset {133086595469025897,133086334888894042}

objectclass {top, person, organizationalPerson, user}

badwdcount {0}

samaccountcount {8053368}

lastlogontimestamp {133084432186976}

created {12821}

objectguid {14 171 158 148 92 27 70 39}

memberof {CN=Administrators,CN=Builtin,DC=corp,DC=com}

whencreated {9/12/2022 11:26:48 PM}

adspath {LDAP://DC1.corp.com/CN=jeffadmin,CN=Users,DC=corp,DC=com}

useraccountcontrol {66048}

country {jeffadmin}

primarygroupid {513}

whenchanged {9/19/2022 6:42:22 AM}

locktime {0}

lastlogon {13308831228837545}

distinguishedname {CN=jeffadmin,CN=Users,DC=corp,DC=com}

adminaccount {1}

samaccountname {jeffadmin}

objectsid {1 5 0 0 0 0 5 21 0 0 30 221 116 118 148 92 27 70 39}

accountexpires {92233726385478507}
```

我们可以对任何类型的对象进行过滤。在示例中，我们有两个更改。首先，我们更改了过滤器以使用 `name` 属性来显示 `jeffadmin` 的信息。此外，我们添加了 `member` 属性以只显示 `jeffadmin` 成员的组：

```powershell
$dsearcher = New-Object System.DirectoryServices.DirectorySearch($direntry)

$dsearcher.filter="name=jeffadmin"

$result = $dsearcher.FindAll()

foreach($obj in $result) {

    foreach($prop in $obj.properties) {

        $prop.memberof

    }

    Write-Host "------------------------------------------------"

}
```

列表 734 - 在过滤器中添加 `name` 属性并在嵌套循环中仅添加 `memberof` 属性

# OffSec

```
PS C:\Users\stephanie\.enumeration.ps1

CN=Domain Admins,CN=Users,DC=corp,DC=com

CN=Administrators,CN=Built,DC=corp,DC=com
```

用于仅显示 `jeffadmin` 及其所属组的脚本

这确认了 `jeffadmin` 是 `Domain Admins` 组的成员。

我们可以使用此脚本枚举 AD（活动目录）中我们可用的任何对象。然而，在当前状态下，我们需要根据想要枚举的内容对脚本本身进行进一步的编辑。

相反，我们可以让脚本变得更加灵活，允许我们通过命令行添加所需的参数。例如，我们可以让脚本接受我们想要枚举的 `samAccountType` 作为命令行参数。

```powershell
function LDAPSearch {

    param (

        [string]$LDAPQuery

    )

    $PDC = [System.DirectoryServices.ActiveDirectory.Domain]::GetCurrentDomain().PdcRoleOwner.Name

    $DistinguishedName = =([adsis]').distinguishedName

    $DirectoryEntry = New-Object
    System.DirectoryServices.DirectoryEntry("LDAP://$PDC/$DistinguishedName")
    $DirectorySearcher = New-Object
    System.DirectoryServices.DirectorySearcher($DirectoryEntry,$LDAPQuery)

    return $DirectorySearcher.FindAll()

}
```

在最顶端，我们使用自定义的名称调用函数，在此例中为 `LDAPSearch`。它随后动态获取所需的 LDAP 连接字符串并将其添加到 `$DirectoryEntry` 变量中。

之后，将 `DirectoryEntry` 和 `$LDAPQuery` 参数传递给 `DirectorySearcher`。最后，运行搜索并将输出添加到一个数组中，根据我们的需要将该结果显示在终端中。

要使用该函数，让我们先将其导入内存。

```powershell
PS C:\Users\stephanie Import-Module \.function.ps1
```

在 PowerShell 中，我们现在可以使用 `LDAPSearch`（我们定义的函数命令）从 AD 中获取信息。为了重复我们之前执行的枚举部分，我们可以再次对特定的 `samAccountType` 进行过滤：

## 使用 Kali Linux 进行 OffSec 渗透

```powershell
PS C:\Users\stephanie LDAPSearch -LDAPQuery "(samAccountType=805306368)"
```
