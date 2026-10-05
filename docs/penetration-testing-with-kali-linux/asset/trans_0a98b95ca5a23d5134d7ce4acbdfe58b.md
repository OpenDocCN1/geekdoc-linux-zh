

# OffSec

```
C:\Users\dave> powershell
powershell
Windows PowerShell
Copyright (C) Microsoft Corporation. All rights reserved.
```

安装最新版本的 PowerShell 以获取新功能和改进！
https://aka.ms/PSWindows

```
PS C:\Users\dave> Get-LocalUser
Get-LocalUser
```

| Name | Enabled | Description |
| --- | --- | --- |
| Administrator | False | 用于管理计算机/域的内置账户 |
| dave | True | |
| daveadmin | True | 由系统管理的用户账户。 |
| Guest | False | 访客内置账户 |
| offsec | True | |
| steve | True | |

## 列表 379 - 在 CLIENT220 上显示本地用户

输出显示了若干项可以帮助我们概述系统的项目。第一点是内置的 Administrator 账户被禁用了。接下来是两个名为 steve 和 dave 的普通用户。此外，我们还识别出另外两个用户 daveadmin 和 BackupAdmin。这两个用户名都包含 "admin"，这意味着他们可能是管理员用户，从而成为我们的目标。

我们也可以假设 daveadmin 是特权账户。他们既有一个非特权账户，还有一个用于管理任务的特权账户。出于安全考虑，他们不会使用特权账户浏览互联网。

在做出进一步假设之前，让我们列出 CLIENT220 上剩余的组。我们可以在 PowerShell 中在 Get-LocalGroup 命令之间进行选择。

```
PS C:\Users\dave> Get-LocalGroup
Get-LocalGroup
```

| Name | Description |
| --- | --- |
| Administrators | 此组的成员是所有工作站的管理员 |
| BackupUsers | |
| helpdesk | |
| Administrators 拥有完全访问权限 |

## 列表 380 - 在 CLIENT220 上显示本地组

输出显示了非标准组 admin、BackupUsers 和 helpdesk。admin 组可能对我们感兴趣，因为它包含 "admin"，并且带有一个自定义描述，指示其成员被允许进入二楼的所有工作站。然而，我们目前还没有关于哪些部门在这些机器的进一步信息。

另一个有趣的发现是 BackupUsers 组，因为他们拥有在文件系统中执行操作的广泛权限，这使得他们成为极有价值的目标。

在非标准组中，有几个我们应该分析的内置组，例如 Administrators、Backup Operators、Remote Desktop Users 和 Remote Management Users。Backup Operators 的成员可以捕获并恢复计算机上的所有文件，即使是他们没有权限访问的文件。我们不能将其与示例中的 BackupUsers 等非标准组混淆。Remote Desktop Users 的成员可以使用 RDP 访问系统，而 Remote Management Users 的成员可以使用 WinRM 访问。对于本示例，让我们查看 admin 和 Administrators 的成员。我们可以通过 Get-LocalGroupMember 实现，并将组名作为参数。

```
PS C:\Users\dave> Get-LocalGroupMember admin
Get-LocalGroupMember admin
```

| ObjectClassName | PrincipalSource |
| --- | --- |
| User | CLIENT220\daveadmin Local |

```
PS C:\Users\dave> Get-LocalGroupMember Administrators
Get-LocalGroupMember Administrators
```

| ObjectClassName | PrincipalSource |
| --- | --- |
| User | CLIENT220\Administrator Local |
| User | CLIENT220\daveadmin Local |
| User | CLIENT220\backupadmin Local |
| User | CLIENT220\offsec Local |

## 列表 381 - 显示组 admin 的成员

381 显示只有 daveadmin 是 admin 组的成员。然而，admin 未列在本地 Administrators 组中。我们知道该组的成员是二楼工作站的管理员。我们目前收集的信息无法直接操作，但当我们深入渗透网络并识别出留在二楼的系统时，这些信息可能会变得有用。

输出还显示，在被禁用的本地 Administrator 账户中，用户 daveadmin 和 BackupAdmin 是本地 Administrators 组的成员。因此，我们识别出了两个非常有价值的目标。

虽然了解哪些用户是特权用户至关重要，但理解哪些用户可以使用 RDP 对我们来说也同样重要。获取其中一个用户的凭据可能会让我们获得 GUI 访问，这通常会极大地提高我们与系统交互的。

我们已经收集了关于目标系统用户和组的大量信息。让我们简要总结一下目前已知的信息。

我们的 bind shell 运行在名为 CLIENTWK220 的机器上，用户为 dave。该用户属于名为 helpdesk 的组。此外还有另一个用户 daveadmin，这可能是该人的特权账户，dave 可能用于日常工作。用户 daveadmin 属于名为 admin 的组，其描述表明它对二楼的所有工作站拥有管理权限。此外，daveadmin 和 BackupAdmin 是本地账户。接下来，我们将收集有关实际机器、配置和架构的信息。我们可以使用 systeminfo 来收集这些信息。

```
PS C:\Users\dave> systeminfo
systeminfo
Host Name:               CLIENTWK220
OS Name:                Microsoft Windows 11 Pro
OS Version:             10.0.22000 N/A
System Type:           x64-based PC
```

列表 382 显示我们的 shell 运行在 Windows 11 上。要获取准确的版本，可以使用版本号并查看现有操作系统。在我们的情况下，版本 22000 是 64 位的。此外，输出包含了我们的 shell 运行在 64 位应用程序上的信息。

 使用 Kali Linux 进行渗透测试

这些信息，我们可以识别新服务或访问其他网络。这些信息可能无法引导我们获取权限，但对于理解机器的目的和获取其他系统的向量至关重要。渗透测试中获取所有机器的权限很少是一个目标。我们将面临许多挑战。对于所有网络接口，可以使用 ipconfig /all。

```
PS C:\Users\dave> ipconfig /all
ipconfig /all

Windows IP Configuration:
| Host Name:                   clientwk220 |
| Primary DNS Suffix:           Hybrid |
| Node Type:                    No |
| IP Routing Enabled:           No |
| WINS Proxied:                 No |

Ethernet adapter0:
| Connection-specific DNS Suffix: vmx3 |
| Description:                   00-50-56-8A-80-16 |
| DHCP Enabled:                  Yes |
| Autoconfiguration Enabled:      fe80::c7a:96e:1f98:babb%6(Preferred) |
| Link-local IPv6 Address:        192.168.50.220(Preferred) |
| IPv4 Address:                   255.255.255.0 |
| Default Gateway:                192.168.50.254 |
| DHCPv6 IAID:                    22491508 |
| DHCPv6 Client ID:               00-01-00-2A-B3-F7-25-00-50-56-8A-80-16 |
| DNS Servers:                    8.8.8.8 |
| Netbios over Tcpip:             Enabled |
```

## 列表 383 - 关于操作系统和架构的信息

输出显示了一些重要信息。例如，系统没有配置通过 DHCP 获取 IP 地址，而是手动设置的。此外，它包含了 DNS 服务器、网关、子网掩码和 MAC 地址。当我们尝试移动到其他系统或网络时，这些信息将非常有用。

