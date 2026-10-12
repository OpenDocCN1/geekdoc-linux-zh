
此输出揭示了任何人都可以编辑 `/etc/passwd` 文件！这很重要，因为它允许攻击者轻松地提升权限或创建账户。尽管这些工具执行了自动化检查，但请注意每个系统都是不同的，且更改会被这些工具捕获。

### 18.2.1 练习

1. 使用本节介绍的工具和命令检查 Windows 和 Linux，以熟悉技术。
2. 不同的 `windows-privesc-check` 选项。

## 18.2 Windows 权限提升

在本节中，我们将讨论 Windows 权限、完整性机制以及利用内核漏洞、UAC 绕过和未引号路径来提升权限。

### 18.2.1 理解 Windows 权限和完整性级别

在 Windows 系统上，为了使权限生效，Windows 使用称为令牌的对象。一旦用户通过身份验证，Windows 就会生成包含各种信息的令牌，描述用户的上下文。最后，这些令牌需要唯一标识。这是通过安全标识符 `SID` 实现的，它是分配给每个对象（如用户或组）的唯一值。这些 `SID` 由 Windows 本地体系生成并维护。除了权限外，Windows 还实现了所谓的完整性机制。这是通过为应用程序进程和安全对象分配完整性级别来实现的核心组件。简单来说，这描述了操作系统对运行的应用或安全对象的信任程度。例如，配置的完整性级别决定了可以执行哪些操作，API 也可以被特定的完整性级别阻止。

从 Vista 开始，进程运行在四个完整性级别上：

- 系统完整性进程：`SYSTEM` 权限
- 高完整性进程：管理员权限
- 中完整性进程：标准用户权限
- 低完整性进程：通常用于沙箱的高度限制权限

### 18.2.2 用户账户控制 (UAC) 简介

用户账户控制 `UAC` 是微软在 Windows Vista 和 Windows Server 2008 中引入的访问控制系统。虽然 `UAC` 已经被讨论和研究了很长时间，但重要的是，微软并不认为它是一个安全边界。相反，`UAC` 强制应用程序在非管理员账户的上下文中运行，除非管理员授权提升。它会阻止未经授权的应用程序在没有权限的情况下运行，并阻止更改设置。通常情况下，`UAC` 的效果是任何想要执行对系统产生潜在影响的操作的操作都无法静默执行。至少在-UAC 有两种不同的模式：凭据提示和许可提示。程序相当简单。当标准用户想要执行管理任务（如安装新应用程序）且启用了 `UAC` 时，用户将看到凭据提示。

# 攻击性安全

## 使用 Kali Linux 进行渗透测试 2.0

会弹出一个确认提示。在这种情况下，用户只需确认应完成任务，无需重新输入用户凭据。

例如，在下面的示例中，标准用户账户下运行的 Windows 命令处理器正尝试执行特权操作。`UAC` 根据其通知设置⁵⁰（在此情况下为“始终通知”）运行，暂停目标进程 `cmd.exe`，并提示管理员用户名和密码以执行请求的特权操作。

![](img/f99f528ca9845f4c256ce54e882b1345_539_0.png)

图 275：请求管理员密码的 UAC 对话

当以管理员用户登录时，该账户将有两个安全令牌：一个运行在中等完整级别，另一个运行在高完整级别。`UAC` 充当这两个完整级别之间的隔离机制。

为了查看完整级别的运作，让我们先以管理员用户登录，打开命令提示符并运行 `whoami /groups` 命令：

```
c:\Users\admin>whoami /groups

GROUP INFORMATION
--------------------
Group Name                     Type                SID               Attributes
=================================================================
Everyone                       Well-known group S-1-1-0     Mandatory group,
AUTHORITY\Local account and member Well-known group S-1-5-114 Group used for de-identification
```

⁵⁰ (Microsoft, 2018), https://docs.microsoft.com/en-us/windows/security/identity-protection/user-account-control/how-user-account-controls

| Name | Alias | SID | Attributes |
| --- | --- | --- | --- |
| BUILTIN\Administrators | | S-1-5-32-54 | 用于管理任务的组 |
| BUILTIN\Users | | S-1-5-32-54 | 强制性组 |
| NT AUTHORITY\INTERACTIVE | Well-known group | S-1-5-4 | 强制性组 |
| CONSOLE LOGON | Well-known group | S-1-2-1 | 强制性组 |
| NT AUTHORITY\Authentic Users | Well-known group | S-1-5-11 | 强制性组 |
| NT AUTHORITY\Organization | Well-known group | S-1-5-15 | 强制性组 |
| NT AUTHORITY\Local account | Well-known group | S-1-5-113 | 强制性组 |
| LOCAL | Well-known group | S-1-2-0 | 强制性组 |
| NT AUTHORITY\Local Authentication | Well-known group | S-1-5-64-10 | 强制性组 |
| Mandatory Label\Medium Level | Label | S-1-16-8192 | |

#### 555 - 检查完整级别

如输出行所示，此提示符目前运行在中等完整级别上。

让我们尝试使用此命令提示符更改管理员的密码：

```
C:\Users\admin> net user admin Ev!pass
System error 5 has occurred.
```

拒绝访问。

尽管我们已以管理员用户登录，请求仍被拒绝了。

为了更改用户密码，即使我们以管理员账户登录，也必须切换到高完整级别。例如，一种方法是使用 `powershell.exe` 配合 `Start-Process cmd.exe -Verb "Run as administrator"`：

```
C:\Users\admin>powershell.exe Start-Process cmd.exe -Verb runas
```

#### 557 - 使用命令生成具有高完整性的 cmd.exe 进程

在提交此操作并接受 `UAC` 提示后，我们将看到一个新的高完整性 `cmd.exe` 进程。

让我们使用 `whoami /groups` 参数检查完整级别以更改密码：

```
C:\Windows\System32> whoami /groups
GROUP INFORMATION
```

| Name | Type | SID | Attributes |
| --- | --- | --- | --- |
| Everyone | Well-known group | S-1-5-1 | 强制性组 |
| NT AUTHORITY\Local account and member | Well-known group | S-1-5-114 | 强制性组 |
| BUILTIN\Administrators | Alias | S-1-5-32-54 | 强制性组 |
| BUILTIN\Users | Alias | S-1-5-32-54 | 强制性组 |
| NT AUTHORITY\INTERACTIVE | Well-known group | S-1-5-4 | 强制性组 |
| CONSOLE LOGON | Well-known group | S-1-2-1 | 强制性组 |
| NT AUTHORITY\Authenticated Users | Well-known group | S-1-5-11 | 强制性组 |
| NT AUTHORITY\This Organization | Well-known group | S-1-5-15 | 强制性组 |
| NT AUTHORITY\Local account | Well-known group | S-1-5-113 | 强制性组 |
| NT AUTHORITY\Local Authentication | Well-known group | S-1-2-0 | 强制性组 |
| Mandatory High Mandatory Level | Well-known group | S-1-16-8192 | 强制性组 |
