
| sesio0_username | sesio1_time | sesio0_idle_time |
| :--- | :--- | :--- |
| 192.168.1.111 CLIENT25$ | 6 | 6 |
| DC01 | | 0 |
| 192.168.1.111 offsec | | |

列表 685 - 使用 `Get-NetSession` 枚举活动会话

由于 Offsec 用户在来自 192.168.1.111 (Windows 10) 的域控制器上有一个活动会话，从两个 API 获取的信息最终是相同的，因为我们只针对单台机器，而这台机器恰好也是我们执行脚本的机器。在真实的 Active Directory 基础设施中，使用每个 API 获得的信息可能会不同，并且无疑会有更多帮助。

现在我们已经枚举组成员关系并确定哪些机器当前已登录，我们拥有了开始渗透用户账户的基本技能，最终目标是获取域管理员权限。

## 2.2.4.1 练习题

- 1. 下载并使用 PowerShell，在 Offsec 账户上下文中执行与学生 VM 相同的枚举。
- 2. 使用 Jeff_Admin 账户登录学生 VM，并使用 Jeff_Admin 账户通过远程桌面登录到域控制器。接下来，在学生 VM 上执行 `Get-LoggedOn` 函数，以发现 Jeff_Admin 账户上下文中域控制器上的登录用户。
- 3. 重复使用 `System.Net.Client` 类中的 `DownloadString` 方法进行枚举，以便从 Kali 系统下载 PowerShell 并在内存中执行它，而不保存到硬盘。

## 通过服务主体名称 (SPN) 进行枚举

我们已经枚举了域用户，以寻找属于高价值组成员的登录账户。攻击域用户账户的另一种方案是针对所谓的服务账户 629，它们也可能是高价值组的成员。

当执行一个应用程序时，它必须在操作系统用户的上下文中运行。如果用户启动应用程序，则由该用户账户定义上下文。然而，由系统启动的服务使用基于服务账户的上下文。

换句话说，它使用了一组预定义的服务账户：LocalSystem、630 LocalService、631 和 NetworkService 632。对于更复杂的应用程序，可以使用域用户账户来提供所需的上下文，同时访问域内部的资源。

> 管理服务账户（Managed Service Accounts）634 随 Windows Server 2008 R2 引入，为需要与 Active Directory 深度集成的复杂应用程序设计。像 SQL 和 Microsoft Exchange 635 等较大的应用程序通常需要服务器冗余但不保证可用性，而管理服务账户 636 是随着 Windows Server 2012 引入的，但这要求域控制器运行 Windows Server 2012 或更高版本。由于由于，许多组织仍然依赖基础服务账户。

通过枚举域中的 SPN，我们可以获取运行在集成 Active Directory 的服务器上的应用程序 IP 地址和端口号，从而减少对范围端口扫描的需求。

由于信息注册并存储在 Active Directory 中，因此存在于域控制器上。为了获取数据，我们将查询域控制器寻找特定的服务主体名称。

629 (Microsoft, 2017), https://msdn.microsoft.com/en-us/library/windows/desktop/ms68605(v=vs.8).aspx
630 (Microsoft, 2018), https://msdn.microsoft.com/en-us/library/windows/desktop/ms68419(v=vs.8).aspx
631 (Microsoft, 2018), https://msdn.microsoft.com/en-us/library/windows/desktop/ms68188(v=vs.8).aspx
632 (Microsoft, 2018), https://msdn.microsoft.com/en-us/library/windows/desktop/ms684272(v=vs.8).aspx
633 (Microsoft, 2017), https://msdn.microsoft.com/en-us/library/windows/desktop/ms67794(v=vs.8).aspx
634 (Microsoft, 2019), https://blogs.technet.com/asks/2009/09/10/
635 (Microsoft, 2018), https://security.org/page_id
636 (Microsoft, 2012), https://technet.com/windows-service-accounts
637 (Sean Metcalf, 2017), http://adsecurity.org/page_id

通过枚举域中的 SPN，我们可以获取运行在集成 Active Directory 的服务器上的应用程序 IP 地址和端口号，从而减少对范围端口扫描的需求。

由于信息注册并存储在 Active Directory 中，因此存在于域控制器上。为了获取数据，我们将查询域控制器寻找特定的服务主体名称。

```powershell
$domainObj = [System.DirectoryServices.ActiveDirectory]::GetCurrentDomain()

$PDC = $domainObj.Name

$Searcher = New-Object System.DirectoryServices.DirectorySearcher("LDAP://$"

$Searcher.Filter = "serviceprincipalname=*"

$Result = $Searcher.FindAll()

foreach($obj in $Result) {

    $obj.Properties

}
```
