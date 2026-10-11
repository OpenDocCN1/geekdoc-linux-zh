
Meterpreter 还有一个用于权限提升的命令 `getsystem`，它使用不同的技术尝试获取 SYSTEM 权限，前提是你是以管理员权限运行的。你也可以使用 Meterpreter 会话配合后利用工具进行本地权限提升。一旦实现了这一点，你就应该对目标系统拥有完全控制权。始终，使用 Meterpreter 这种强大工具的最佳起点是 `help` 命令。你可以使用 Meterpreter 的 `keyscan_start` 命令启动其按键记录器。要查看记录器运行时用户按下的按键，你需要使用 `keyscan_dump` 命令。

# 哈希转储 (Hash Dumping)

Meterpreter 的 `hashdump` 命令非常有用，因为它会转储 SAM 的内容。将其视为 Linux 或 UNIX 系统上的 `/etc/passwd` 和对应的 `/etc/shadow` 文件，Meterpreter 可以自动检索所需的密钥和 syskey 值。

## 第 13 章 » Microsoft Windows

Meterpreter 有加载其他工具的能力——例如加载 mimikatz。Mimikatz 允许你从 Windows 系统的不同区域获取明文密码，一旦加载了 Mimikatz（github.com/gentilkiwi/Mimikatz），你就可以使用 Meterpreter 命令 `sspkg` 获取最近登录机器的用户明文密码，因为它们会残留在内存某处（通过 Heartbleed 转储内存则不同）。Meterpreter 本身具有许多值得进一步探索的功能。你可以在此处查看更多 Meterpreter 命令：www.offensive-security.com/metasploit-unleashed/meterpreter-basics。你通常需要运行任何 SYSTEM shell。

# 传递哈希 (Passing the Hash)

UNIX 类系统中，用户的密码哈希可以在 `/etc/shadow` 文件中找到。在 Windows 机器，必须使用如 Mimikatz 之类的工具从内存中转储。

> 注意：你可以传递密码哈希来访问 Windows 系统上的账户，使用一种被称为“哈希攻击”的技术：google.com/archive/p/passing-the-hash/

通常，为了使用哈希，需要对其进行破解并推导出明文密码，以便配合用户名登录。在 Windows 中，某些情况下，可以直接使用哈希而无需破解即可作为相应用户进行身份验证。在 Windows 域中，用户可能需要访问文件服务器，与其使用密码身份验证，可以使用用户的哈希自动完成。实现这种可能的技术是 Kerberos，作为新型技术语言管理器（NTLM）的身份验证系统。NTLM 构建并极大改进了语言管理器（LANMAN）的安全性，后者的版本发布于 1994 年；它是一个网络操作系统。

这背后的逻辑可能是：“如果用户拥有密码副本，他们就可以访问域。这是 Windows 的一个固有问题：如果用户拥有哈希，他们就可以访问域。”这就是为什么我们可以在不知道密码的情况下使用哈希访问目标机器。

## 第 13 章 - Microsoft Windows

UNIX 类系统中，用户的密码哈希可以在 `/etc/shadow` 文件中找到。在 Windows 机器，必须使用如 Mimikatz 之类的工具从内存中转储。

> 注意：你可以传递密码哈希来访问 Windows 系统上的账户，使用一种被称为“哈希攻击”的技术：google.com/archive/p/passing-the-hash/ 通常，为了使用哈希，需要对其进行破解并推导出明文密码，以便配合用户名登录。在 Windows 中，某些情况下，可以直接使用哈希而无需破解即可作为相应用户进行身份验证。

当涉及到 Windows 权限提升时，有很多获取 SYSTEM 的简单方法。以下是相关选项：

| Name | Required | Description |
| :--- | :--- | :--- |
| HOSTS | yes | 目标主机 |
| RPORT | 445 | SMB 端口 |
| SERVICE_DESCRIPTION | no | 服务描述 |
| DISPLAY_NAME | no | 显示名称 |
| SERVICE_NAME | no | 服务名称 |
| SHARE | yes | 共享 |
| authentication | no | 身份验证 |
| SMBUser | no | 用户名 |

一旦你获得了足够的管理员权限，就有许多简单方法可以获取 SYSTEM，例如使用 `sc.exe` 服务控制创建一个以 LOCAL SYSTEM 身份运行的任务。你也可以与此服务控制进行交互，并指示它通过网络远程设置服务。你经常需要获取 SYSTEM，在这里我们演示如何将管理员凭据转换为 SYSTEM shell，以下是 `sc.exe` 使用命令的概述：

```
也可以通过 sc.exe \<ip> <cmd> 远程使用，如下
sc query - 列出服务
sc qc <service> - 查询配置（显示登录用户）
sc stop/pause/continue <service> - 停止/暂停/继续服务
sc control - 发送控制（继续后）
sc config VulnService binpath=c:\lol.exe - 重配置漏洞服务
```

# 权限提升 (Privilege Escalation)

当涉及到 Windows 权限提升时，漏洞（正如 UNIX 类一样）针对内核或用户空间。这里是一些可以检查的历史漏洞，它们将用户提供 SYSTEM 权限：

- MS11-046: AFD 权限提升
- MS14-058: 内核利用
- MS15-078: 内核提升
- MS16-035: 登录服务

破解管理员账户也是可行方法，类似于直接从数据泄露中获取凭据。你还应该检查配置的文件权限，正如你在 Linux 中看到的那样。有一个名为 PowerUp 的工具，它是 PowerSploit 的一部分，可以自动执行权限提升过程（github.com/PowerShellMafia/PowerSploit/tree/master/Privesc）。PowerUp 利用常见的权限不当的服务；一旦获得了受限的本地访问，它通常可以获得 SYSTEM 等高权限访问。

> 由于 AMSI 的启用以及针对攻击者常用例程的改进检测工具，PowerShell 对攻击者来说不再那么有用。由于 .NET 框架，工具作者更倾向于使用 C#（读作 "C-Sharp"），因为它可以在大多数 Microsoft 桌面和服务器上快速混淆和重新编译。许多用 PowerShell 编写的工具现在已迁移到 C# 或其他语言。

## 第13 章 - Microsoft Windows 509

```
sc enumdepend <Service> - 列出服务依赖
sc \ip> create <service> binpath=c:\blah.exe start=auto 创建远程服务
```

你可以通过 `binpath` 创建并执行服务。为了最大限度地利用服务进行权限提升，你必须编写一个实际的服务与控制器通信。然而，微软提供了许多可以轻松修改的示例。Hacker House 提供了一个 SYSTEM 服务项目（github.com/hackerhouse-opensource/backdoors/blob/master/SYSTEMservice.tg），它绑定到本地的 1337 端口，允许你轻松地使用该端口打开 SYSTEM 权限。你可以使用 Visual Studio Community 根据自己的需求对其进行轻松编辑，由于它是编译后的代码，你需要确保目标系统已安装了适用于 Visual Studio 2015、2017 和 2019 的 Microsoft C++ Redistributable。它包含 `CppWindowsService.exe`，当使用以下选项运行时，它将创建一个简单的服务。记住在完成后使用 `-remove` 卸载该服务！

```
.CppWindowsService.exe -install
```

CppWindowsService 已安装。

```
net start CppWindowsService
```

CppWindowsService 示例服务正在启动。

CppWindowsService 示例服务已启动。

```
C:\tools\Windows_Tradecraft_Tools\netcat\nc.exe 127.0.0.1 1337
```

Microsoft Windows [Version 6.3.9600]

(c) 2013 Microsoft Corporation. 保留所有。

```
C:\WINDOWS\system32>
```

```
whoami
nt authority\system
```

## 替代的载荷交付方法
