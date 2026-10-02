
服务器消息块（SMB）协议使用 NTLM 哈希进行身份验证。

## 21.4.1 哈希传递 (Pass the Hash)

哈希传递（PtH）技术允许攻击者使用用户的 NTLM 哈希而非明文密码来验证远程系统或服务。注意，这不适用于 Kerberos 认证，仅适用于使用 NTLM 认证的服务器或服务。

许多第三方工具和框架使用 PtH 来允许用户同时进行身份验证并获取代码执行。背后的原理与攻击者通过执行连接到受害者的情况大体相同，包括 Metasploit 中的 `PsExec`。大多数用于利用 PtH 构建的工具都会创建一个 Windows 服务（例如 `cmd.exe` 或 PowerShell 实例），并使用命名管道（Named Pipes）与其通信。这涉及到服务控制管理器 API。

该技术要求通过防火墙进行 SMB 连接（通常是端口 `445`），并启用 Windows 文件和打印机共享功能。这些要求在内部企业环境中很常见。

当执行连接时，通常会使用一个名为 `C$` 的特殊管理共享。为了建立此类连接，攻击者必须提供具有本地管理员权限的有效凭据。换句话说，这种横向移动通常需要本地管理员权限。

注意，PtH 是合法地使用了 NTLM 哈希。然而，漏洞在于我们未经授权就获取了本地管理员的密码哈希。

为了演示这一点，我们可以使用来自 Passing-The-Hash 工具包的 `pt-winexec`，就像我们在密码攻击模块中向非域已加入的用户传递哈希一样：

+ 列表 700 - 使用 pt-winexec 传递哈希

```
kali@kali:~ $ pth-winexe -U offsec%aad3b435b5140eead3b435b51404ee:2892d26cdf84d7a70eb3b9f05c425e//10.11.0.22 cmd
E_md4hash wrapper called.
HASH PASS: Substituting user supplied NTLM HASH...
Microsoft Windows [Version 10.0.16299.309]
(c) 2017 Microsoft Corporation. All rights reserved.
C:\Windows\system32>
```

在这种情况下，我们使用 NTLM 认证，仅凭用户的 NTLM 哈希就直接从我们的 Kali Linux 获取了 Windows 10 客户端的代码执行权限。

此方法适用于 Active Directory 域账户以及自 2014 年安全更新后的内置本地管理员账户、其他本地管理员账户。

## 21.4.2 越哈希 (Overpass the Hash)

通过越哈希，可以获取授权票据（TGT）或服务票据，从而允许以该用户的身份访问另一台机器或服务。

为了演示这一点，假设我们已经攻破了一个 Jeff_Admin 用户已通过验证的工作站（服务器），并且该机器现在缓存了他的凭据（因此缓存了 NTLM 密码哈希）。

为了模拟此缓存凭据，我们将以 Office 用户身份登录 Windows 10 机器，并以 Jeff_Admin 身份运行进程，这将触发身份验证。

执行此操作最简单的方法是右键点击任务栏上的记事本图标，然后在弹出窗口记事本图标上按 Shift+右键，得到图 311 所示的选项。

图 311：以不同用户身份启动

从这里开始，我们可以选择“以不同用户身份运行”，并输入用户名“jeff_admin”以及关联的密码，将在该用户的上下文中启动记事本。身份验证成功后，Jeff_Admin 的凭据将缓存在此机器上。

越哈希技术的精髓是将 NTLM 哈希转换为 Kerberos 票据并避免直接使用它。实现此点的一种方法是使用 Mimikatz 的 `sekurlsa::pth` 命令。该命令需要几个参数，并在 Jeff_Admin 用户的上下文中创建一个新的 PowerShell 进程。这个新的 PowerShell 提示符将允许我们在不通过网络进行 NTLM 认证的情况下获取 Kerberos 票据，使得这种攻击不同于传统的哈希传递。

首先，我们通过 `:user;` 和 `:domain;` 将它们分别指定为 jeff_admin 和 corp。我们将使用 `:ntlm;` 指定 NTLM 哈希，最后使用 `:run:` 创建进程（在此例中为 PowerShell）。

```
mimikatz::sekurlsa::pth /user:jeff_admin /domain:corp /ntlm:e2b475c11da2a0748290d877aa96c27 /run:PowerShell.exe
```

```
program: cmd.exe
impers: :no
NTLM: e2b475c11da2a0748290d877aa96c27
PID 4832
```

### 列表 702 - 使用不同用户的 NTLM 密码创建进程

此时，我们拥有了一个新的 PowerShell 会话，允许我们以 Jeff_Admin 的身份执行命令。让我们使用 `klist` 列出 Kerberos 票据：

### 列表 703 - 列出 Kerberos 票据

没有缓存 Kerberos 票据，这是预期的，因为 Jeff_Admin 没有进行交互式登录。然而，让我们通过 `net use` 验证域上的网络共享来生成一个 TGT：

```
| TID 2268
| LSA Process is now R/W |
| LUID 0 | 1197687(00000000124677) | 1_msv1_0 - data @04E0514
```
