

![](img/ec25e59d75726b7041242a56d3376832_531_0.png)

# 使用 Kali Linux 2.0 进行渗透测试

### 列表 153 - 运行 unix_privesc_check

该脚本会对常见文件的权限执行多项检查。例如，以下摘录揭示了可被非 root 用户写入的配置文件：

```
"""
Checking for writable config files
####################################
Checking if anyone except root can change /etc/passwd
WARNING: /etc/passwd is a critical config file. World write is set for /etc/passwd
Checking if anyone except root can change /etc/group
Checking if anyone except root can change /etc/fstab
Checking if anyone except root can change /etc/profile
Checking if anyone except root can change /etc/sudoers
Checking if anyone except root can change /etc/shadow
"""
```

**列表 154 - unix_privesc_check 可写配置文件**

此输出显示系统上的任何人都可以编辑 /etc/passwd 文件！这非常严重，因为它允许攻击者轻松提升其权限<sup>493</sup>或在目标上创建用户账户。我们将在本模块的后文中演示这一过程。

尽管这些工具执行了许多自动检查，但请记住，每个系统都是不同的，且独特的、一次性的系统更改通常会被这类工具遗漏。因此，注意那些只能通过手动检查发现的独特配置非常重要。<sup>494</sup>

## 18.1.2.1 练习

-   使用本节中介绍的工具和命令检查你的 Windows 和 Linux 客户端，以熟悉手动本地枚举技术。
-   尝试不同的 windows-privesc-check 和 unix_privesc_check 选项。

# 18.2 Windows 权限提升示例

在本节中，我们将讨论 Windows 权限、完整性机制以及用户帐户控制（UAC）。我们将演示 UAC 绕过技术，并利用内核驱动漏洞、不安全的文件权限和未加引号的服务路径来提升目标上的权限。

## 18.2.1 理解 Windows 权限和完整性级别

Windows 操作系统中的权限<sup>495</sup>指的是特定账户执行系统相关本地操作的许可。这包括修改文件系统、添加用户、关闭系统等操作。

为了使这些权限生效，Windows 操作系统使用称为访问令牌的对象。<sup>496</sup> 一旦用户完成身份验证，Windows 就会生成一个分配给该用户的访问令牌。令牌本身包含各种信息，有效地描述了给定用户的安全上下文，包括用户权限。

最后，鉴于令牌中包含的信息，这些令牌必须是可唯一识别的。这是通过使用安全标识符或 SID<sup>497</sup>实现的，SID 是一个唯一值，分配给每个对象（包括令牌），例如用户或组账户。

这些 SID 由 Windows 本地安全机构生成和维护。<sup>498</sup>

除了权限之外，Windows 还实施了一种称为完整性机制的东西，<sup>499</sup> 这是 Windows 安全架构的核心组件，通过为应用程序进程和可保护对象<sup>501</sup> 分配完整性级别<sup>500</sup>来工作。简而言之，这描述了操作系统对运行中的应用或可保护对象的信任程度。例如，配置的完整性级别决定了应用程序可以执行的操作，包括从本地文件系统读取或写入的能力。API 也可以从特定的完整性级别中被阻止。

从 Windows Vista 开始，进程运行在四个完整性级别上：

-   系统完整性进程：SYSTEM 权限
-   高完整性进程：管理权限
-   中完整性进程：标准用户权限
-   低完整性进程：通常用于沙箱化<sup>502</sup>进程的高度受限权限

### 18.2.2 用户帐户控制 (UAC) 简介

用户帐户控制（UAC）<sup>503</sup>是微软在 Windows Vista 和 Windows Server 2008 中引入的一种访问控制系统。虽然 UAC 已经讨论和研究了相当长的时间，但重要的是要强调，微软并不认为它是一个安全边界。相反，UAC 强制应用程序和任务在非管理员帐户的上下文中运行，直到管理员授权提升的访问权限。它将阻止安装程序和未经授权的应用程序在没有管理员帐户权限的情况下运行，并阻止更改系统设置。一般来说，UAC 的效果是，任何希望执行可能具有系统级影响的操作的应用程序，都不能静默地执行。至少在理论上是如此。

同样重要的是强调，UAC 有两种不同的模式：凭据提示和同意提示。区别相当简单。当标准用户希望执行管理任务（例如安装新应用程序）且 UAC 已启用时，用户将看到凭据提示。换句话说，需要管理员用户的凭据才能完成任务。然而，当管理员用户尝试执行相同操作时，他或她会遇到同意提示。在这种情况下，用户只需确认应完成任务，无需重新输入用户凭据。

例如，在下图中，在标准用户帐户下运行的 Windows 命令处理程序试图执行特权操作。UAC 根据其通知设置<sup>504</sup>（在此情况下为“始终通知”）进行操作，暂停目标进程 **cmd.exe** 并要求输入管理员用户名和密码以执行请求的特权操作。

![](img/ec25e59d75726b7041242a56d3376832_533_0.png)

*图 275. 请求管理员密码的 UAC 对话框*

即使登录为管理员用户，该账户也将有两个安全令牌，一个以中完整性级别运行，另一个以高完整性级别运行。UAC 充当这两个完整性级别之间的分离机制。

要查看完整性级别的实际运行情况，让我们首先以 admin 用户身份登录，打开命令提示符，并运行 **whoami / groups** 命令：

```
c:\Users\admin> whoami / groups

GROUP INFORMATION
------------------

Group Name                        Type            SID             Attributes
================================= ============== =============================
Everyone                          Well-known group S-1-1-0        Mandatory group,
NT AUTHORITY\Local account and   Well-known group S-1-5-114      Group used for d
```

---
<sup>493</sup> (Raj Chandel, 2018), https://www.hackingarticles.in/editing-etc-passwd-file-for-privilege-escalation/
<sup>494</sup> (G0tm1rk, 2011), https://blog.g0tm1rk.com/2011/08/basic-linux-privilege-escalation/
<sup>495</sup> (Microsoft, 2018), https://msdn.microsoft.com/en-us/library/windows/desktop/aa379306(v=vs.85).aspx
<sup>496</sup> (Microsoft, 2018), https://docs.microsoft.com/en-us/windows/win32/secreccauit/access-tokens
<sup>497</sup> (Microsoft, 2018), https://docs.microsoft.com/en-us/windows/win32/secauthz/security-identifiers
<sup>498</sup> (Microsoft, 2018), https://docs.microsoft.com/en-us/windows/win32/secauthz/lsa-authentication
<sup>499</sup> (Microsoft, 2007), https://msdn.microsoft.com/en-us/library/bb625957.aspx
<sup>500</sup> (Microsoft, 2007), https://msdn.microsoft.com/en-us/library/bb625963.aspx
<sup>501</sup> (Microsoft, 2018), https://docs.microsoft.com/en-us/windows/win32/secauthz/securable-objects
<sup>502</sup> (Wikipedia, 2019), https://en.wikipedia.org/wiki/Sandbox_(software_development)
<sup>503</sup> (Microsoft, 2017), https://docs.microsoft.com/en-us/windows/security/identity-protection/user-account-control-overview
<sup>504</sup> (Microsoft, 2018), https://docs.microsoft.com/en-us/windows/security/identity-protection/user-account-control/how-user-account-control-works

