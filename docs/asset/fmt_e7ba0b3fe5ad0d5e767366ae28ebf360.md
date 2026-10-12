
³⁷¹ (Wikipedia, 2022), https://en.wikipedia.org/wiki/Privilege_escalation

³⁷² (Wikipedia, 2022), https://en.wikipedia.org/wiki/Windows_Task_Scheduler

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

# OffSec

虽然使用技术攻击向量来实现权限提升很常见，但查看用户留下的信息通常就足够了。一个例子是用户在 PowerShell 中存储了密码。对于攻击者来说，这可能是一个通往更高权限的金矿。

在本学习单元中，我们将讨论 Windows 权限和访问控制机制的工作原理。然后，我们将探索在系统上建立态势感知的方法。这些方法提供了关于目标系统的关键信息，如现有用户、活跃的网络连接和运行的应用程序。接下，我们将检查 Windows 中可以搜索敏感信息的各种区域。最后，我们将审查自动化工具。

## 16.1.1 理解 Windows 权限和访问控制机制

Windows 操作系统上的权限指的是服务账户执行系统相关本地操作的权限（例如修改文件系统或添加用户）。为了授予或拒绝这些权限，Windows 需要控制机制来识别操作来源，并确定操作所需的权限是否足够。

在本节中，我们将涵盖四个不同的概念和机制：安全标识符（SID）。⁷³³ 访问令牌（access token）。⁷³⁴ 强制完整控制（Mandatory Integrity Control）。⁷³⁵ 以及用户账户控制（User Account Control）。⁷³⁶

Windows 使用 SID 来标识实体。SID 是分配给每个由 Windows 识别的实体或主体（如用户和组）的唯一值。本地账户和组由本地安全机构（LSA）⁷³⁷ 生成，域用户和域组也是如此。

> ³⁷⁰ (Wikipedia, 2022), https://en.wikipedia.org/wiki/Privilege_escalation

³⁷¹ (Wikipedia, 2022), https://en.wikipedia.org/wiki/Windows_Task_Scheduler

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

# OffSec

使用 Kali Linux 进行渗透测试

线程根据模拟身份的令牌（impersonation token）而不是进程的主令牌与对象进行交互。

除了 SID 和令牌外，Windows 还实现了所谓的强制性完整性控制（Mandatory Integrity Control）。它使用*完整性级别*（integrity levels）来控制对可安全对象的访问。我们可以将这些级别视为 Windows 对运行中的应用程序或可安全对象的信任层级结构。

当启动进程或创建对象时，它们将接收执行此操作的完整性级别。一个例外是，如果可执行文件具有低完整性级别，则进程的完整性级别也将较低。低完整性级别的进程无法向高级别的对象写入，即使权限通常允许它们这样做。

从 Windows Vista 开始，进程运行在四种完整性级别上：

- System（系统）：内核、...

- High（高）：特权用户

- Medium（中）：标准用户

- Low（低）：非常受限的权限，通常用于沙箱[^privesc_win_sandbox]进程或存储临时数据的目录

| 列表 375 - 完整性级别 |

我们可以通过 Explorer^740 显示当前用户 `whoami/groups` 的进程完整性级别，对于页面我们使用 `icacls.`^741。

例如，下图显示了 Process Explorer 中 Windows 系统上的两个 PowerShell 进程。一个作为普通用户，另一个作为管理员用户。

| | | | | | | | |

|---|---|---|---|---|---|---|

| powershell.exe | <0.01 | 51308 K | 66092 | 56396 Windows PowerShell Medium |

| powershell.exe | <0.01 | 51356 K | 65998 | 10836 Windows PowerShell High |

图 236：Power 的不同完整性级别

PowerShell 进程具有高和中完整性级别。查看列表 375，我们可以推断出*高完整性级别进程由管理员用户启动，而*中*完整性级别进程由普通用户启动。

最后，我们需要考虑的另一个安全技术是用户账户控制（UAC）。UAC 是 Windows 的安全功能，通过以标准用户权限运行大多数应用程序和任务来保护操作系统，即使启动它们的用户是管理员。第一个用户在成功登录后获得两个令牌。第一个令牌是标准令牌（*过滤后的管理员令牌*），用于执行非特权操作。第二个令牌是管理员令牌。当用户想要执行特权操作时将使用它。利用这一点，需要确认 UAC 同意提示^742。

这就结束我们对 Windows 权限和访问控制机制的介绍。我们现在应该对 SID、访问令牌、完整性和 UAC 有了基本的了解。

^739 (Microsoft Documentation, 2021), https://docs.microsoft.com/en-us/windows/32/secauthz/impersonation-tokens

^740 (Microsoft Documentation, 2022), https://docs.microsoft.com/en-us/sysinternals/downloads/process-explorer

^741 (Microsoft Documentation, 2022), https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/icacls

^742 (Microsoft Documentation, 2022), https://docs.microsoft.com/en-us/windows/security/identity-protection/user-account-control/how-user-account-controls

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

# OffSec

使用 Kali Linux 进行渗透测试

Windows 提供了许多其他机制来控制对可安全对象的访问。我们将在模块中进行讨论和演示。

## 16.1.2 态势感知

现在我们已经对 Windows 权限有了基本的了解，我们将涵盖在系统上获取态势感知的各种方法。假设我们使用客户端攻击或利用漏洞访问了一个非特权用户。在提升我们的权限之前，我们必须获取有关我们所处系统的信息。

这是更好地理解被攻破机器的性质并发现可能的权限提升向量的关键步骤。然而，缺乏经验的渗透测试通常会跳过或最小化这一步，因为发现和解释大量信息并没有攻击服务或机器那样有趣。经验丰富的渗透测试人员知道，通过尽可能地收集信息，可以获得有关目标系统的价值信息，并利用这些信息创建各种可操作的向量来提升他们的权限。

我们应该始终获取的一些信息：

- 用户名和主机名

- 当前用户所属的组

- 现有的用户和组

- 操作系统、版本和架构

- 网络信息

- 已安装的应用程序

- 运行中的进程

> 列表 376 - 为了获取态势感知应该收集的信息

在执行枚举步骤获取这些信息后，我们将对目标系统有一个实实的了解。

让我们开始收集 CLIENTWK220 系统上的信息。在这个例子中，我们假设之前通过客户端攻击在端口 4444 上启动了一个绑定 shell（bind shell）。

> 如果本节或后续章节中到绑定 shell 的连接断断，可能需要 1 分钟才能再次被访问。

现在我们演示如何从列表 376 获取信息。为此，我们将使用 netcat 连接到目标系统并输入 `whoami` 来获取第一部分信息：我们的用户名和主机名。

```
kali@kali:~$ nc 192.168.50.220 4444
Microsoft Windows [Version 10.0.22000.318]
(c) Microsoft Corporation. All rights reserved.

C:\Users\dave>whoami
whoami
clientwk220>dave
C:\Users\dave>
```

> 列表 377 - 连接到绑定 shell 并获取用户名和主机名

列表 377 的输出显示我们以用户 dave 的身份执行了命令。此外，输出包含了系统的主机名 clientwk220。此主机名意味着我们的绑定 shell 运行在客户端而不是服务器上。

主机名通常可以用于推断机器的作用和类型。例如，如果它是用于 Web 服务器的 WEB01 或用于 SQL^743 服务器的 MSSQL0。
