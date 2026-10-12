
769 (Microsoft文档, 2022), https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/get-history?view-powershell-7

770 (Microsoft文档, 2022), https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/clear-history?view-powershell-7

771 (Microsoft文档, 2022), https://docs.microsoft.com/en-us/powershell/module/psredline?view-powershell-7

PWK - Copyright © 2023 OffSec Services Limited. 版权所有。

制作于摩洛哥

# OffSec - 使用 Kali Linux 进行渗透测试

`Enter-PSSession -ComputerName CLIENTWK220 -Credential $cred`
`exit`
`Stop-Transcript`

## 列表 399 - Get-History 的空结果

输出包含了许多对我们来说有趣的命令。

首先，dave 使用 `SecretManagement.keeps` 模块执行了 `Register-SecretVault`，这意味着用户为 KeePass 创建了一个新的密码数据库。在下一行中，dave 使用 `Set-Secret` 在密码管理器中创建了一个名为 Server02 Admin PW、密码为 EarMonitor33# 的秘密条目。正如名称所示，这些可能是另一个系统的凭据。然而，我们应该尝试将此密码用于任何用户，或者在登录 CLIENTWK220 时，它可能被用户使用。现在，我们将记录该密码以继续分析历史记录。

接下来，输出显示 dave 使用了 `Clear-History`，表明在执行该命令后历史记录被清除了。

最后，dave 使用 `Start-Transcript` 创建了一个 PowerShell 会话。此命令创建了记录文件存储的路径。在我们检查它之前，让我们分析下一个。

用户执行了 `Enter-PSSession`，并将本地主机的主机作为 `ComputerName` 的参数，并使用包含用户名和密码的创建的 `$cred` `PSCredential` 对象作为 `-Credential`。创建 `PSCredential` 对象的命令没有包含在历史文件中，因此我们不知道 `Enter-PSSession` 使用了什么用户和密码。

> PowerShell 远程登录默认使用 WinRM 处理如 `Enter-PSSession` 等 Cmdlet。因此，用户需要位于本地组“Windows Management Users”中才能使用这些 Cmdlet。SSH 也可以用于 PowerShell 远程登录。

让我们分析 `C:\Users\Public\Transcripts\transcript01.txt` 中的记录文件，并检查是否能对用户和密码的使用提供更多线。由于 PowerShell 记录在 `Enter-PSSession` 之前开始，它可能包含用于创建存储在 `$cred` 中的 `PSCredential` 对象的明文凭据信息。

```
PS C:\C:\Users\Public\Transcripts\transcript01.txt

type: C:\Users\Public\Transcripts\transcript01.txt

********************************************************************

Windows PowerShell transcript start

Start time: 20220623081143
```

772 (Microsoft文档, 2022), https://docs.microsoft.com/en-us/powershell/module/secretmanagement/enter-psession?view=powershell-7.2
773 (Microsoft文档, 2022), https://docs.microsoft.com/en-us/dotnet/api/system.management.pscredential view=powershell-7
774 (Microsoft文档, 2021), https://docs.microsoft.com/en-us/powershell/scripting/learn/ps101/remoting?view=powershell-7
775 (Wikipedia, 2022), https://en.wikipedia.org/wiki/Secure_Shell
776 (Microsoft文档, 2021), https://docs.microsoft.com/en-us/powershell/scripting/learn-remoting-in-powershell-core?view=powershell-7

PWK - Copyright © 2023 OffSec Services Limited. 版权所有。

493
制作于摩洛哥

# OffSec 使用 Kali Linux 进行渗透测试

用户名: CLIENTWK220\dave
用户身份: CLIENTWK220\dave
配置名称:
机器: CLIENTWK220 (Windows NT 10.0)
主机应用程序: C:\Windows\PowerShell\v1.0\powershell.exe
进程 ID: 16336
PSVersion: 5.1.22000

```
**************************************************

Transcript started, output file C:\Users\Public\Transcripts\transcript01.txt

PS C:\Users\dave> $password = ConvertTo-SecureString "qwertqwert123!" -As -Force

PS C:\Users\dave> $cred = New-Object System.Management.Automation.PSCredential("daveadmin", $password)

PS C:\Users\dave> Enter-PSSession -ComputerName CLIENTWK220 -Credential $cred

**************************************************

Windows PowerShell transcript end

End time: 2022062308221

**************************************************
```

## 列表 400 - 记录文件的内容

列表 400 显示记录文件包含了用于创建变量 `$cred` 的命令，这些命令在历史文件中是缺失的。

为了创建之前讨论的 `PSCredential` 对象，用户首先需要创建一个存储密码的 `SecureString`。然后，用户可以使用用户名和密码创建 `PSCredential` 对象。包含该对象的生成变量可以作为 `Enter-PSSession` 等命令中 `-Credential` 的参数。

让我们复制命令并将其粘贴到我们的 shell 中：

```
PS C:\Users\dave> $password = ConvertTo-SecureString "qwertqwert123!" -As -Force

PS C:\Users\dave> $cred = New-Object System.Management.Automation.PSCredential("daveadmin", $password)

PS C:\Users\dave> Enter-PSSession -ComputerName CLIENTWK220 -Credential $cred
```

列表 400 显示记录文件包含了用于创建变量 `$cred` 的命令，而历史文件中缺失了。

为了创建之前讨论的 `PSCredential` 对象，用户首先需要创建一个 `SecureString` 来存储密码。然后，用户可以使用用户名和密码创建 `PSCredential` 对象。生成的包含该对象的变量可以作为 `Enter-PSSession` 等命令中 `-Credential` 的参数。

让我们复制命令并将其粘贴到我们的 shell 中：

```
PS C:\Users\dave> $password = ConvertTo-SecureString "qwertqwert123!" -As -Force
```
