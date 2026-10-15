
> 列表 75 - 发现存在漏洞的 nmap SMB NSE 脚本

我们找到了一些有趣的 `nmap` NSE 脚本，它们可以执行各种任务，如通过 SMB 进行操作系统发现和枚举。

> SMB 发现脚本仅在目标上启用了 SMBv1 时才有效，而这在现代 Windows 版本中并不是默认情况。然而，许多遗留系统仍在运行 SMBv1，我们已经在 Windows 主机上启用了此特定版本以模拟此类场景。

让我们在 Windows 11 客户端上尝试 `smb-os-discovery` 模块。

```
kali@kali:~$ nmap -v -p 139,445 --smb-os-discovery 192.168.50.152

PORT    STATE     REASON

139/tcp open netbios-ssn syn-ack

445/tcp open microsoft-ds syn-ack

OS detection: Windows 11 (build 10.0.22631)

CPE: cpe:/2.5:a:microsoft:windows:11:10.0:22631:*:*:*:*:
```

# OffSec

同样，我们可以像之前做的那样，从 Windows 11 客户端获取目标的 SMTP 信息。

```
PS C:\Users\student> Test-NetConnection -Port 25 192.168.50.8
```

```
ComputerName : 192.168.50.8

RemoteAddress : 192.168.50.8

RemotePort : 25

InterfaceAlias : Ethernet0

SourceAddress : 192.168.50.152

TestSucceeded : True
```

> *列表 B1 - 通过 PowerShell 进行端口扫描*

遗憾的是，通过 `Test-NetConnection` 无法无法与 SMTP 服务进行完全交互。尽管如此，如果尚未启用，我们可以安装微软版本的 Telnet 客户端，如下所示：

```
C:\Windows\system32> dism /online/Enable-Feature/FeatureName:TelnetClient
```

> *列表 B2 - 安装 Telnet 客户端*

我们应该注意，安装 Telnet 需要管理员权限，如果我们以低权限用户身份运行，可能会面临挑战。但是，我们可以从我们另一台开发机器上的 `c:\system32\telnet.exe` 获取 Telnet 二进制文件，并将其传输到正在测试的 Windows 机器。

一旦在测试机器上启用了 Telnet，我们连接到目标机器并从 Kali 进行枚举。

```
C:\Windows\system32>telnet 192.168.50.8 25

220 mail SMTP Postfix (Ubuntu)

VRFY goofy

550 5.1.1 <goofy>: Recipient address rejected: User unknown in local recipient table

252 2.0.0 root
```

> *列表 83 - 在 Windows 上通过 telnet 与 SMTP 服务交互*

该输出描述了另一个示例，即当 Kali 不可用时，我们可以从被攻主机上执行的枚举。

## 6.3 SNMP 枚举

多年来，我们发现许多网络管理员并不十分了解简单网络管理协议（SNMP）。这导致了 SNMP 配置错误，从而引发严重的信息泄露。

SNMP 基于 UDP，这是一种简单且无状态的协议，因此容易受到 IP 欺骗和重放攻击。此外，常用的 SNMP 协议 1、2 和 2c 不提供流量加密，这意味着 SNMP 信息和凭据可以在局域网内被拦截。传统的 SNMP 协议还有弱的身份验证方案，并且通常配置有默认的 `public` 和 `private` 团体字（community strings）。

直到最近，提供认证和加密的 SNMPv3 只支持 DES-56，这被证明是一种容易被暴力破解的弱加密方案。较新的 SNMPv3 实现支持 AES-256 加密方案。

由于上述所有内容都适用于一个定义上用于“管理网络”的协议，SNMP 是我们的另一个易于枚举的协议之一。

几年前，OffSec 对一家为大量企业客户、银行和其他类似组织提供网络集成服务的公司进行了内部渗透测试。我们发现了一个大型 B 类网络，其中有数千个正在运行的系统，并连接了数千台 Cisco 路由器。他们向我们解释说这些路由器中的每一个都是其客户的网关，用于管理和配置。

通过对 Cisco 默认凭据进行快速扫描，发现了一个低端 Cisco ADSL 路由器。进一步挖掘在路由器配置文件中发现了一组复杂的 SNMP 公有和私有团体字。结果证明，这些公共和私有团体字被用于每一个网络设备，涵盖整个 B 类范围以及更远——简单的管理，对吧？

企业路由硬件的一个有趣点点是，这些设备通常支持通过私有 SNMP 团体字访问来读写配置文件。由于我们现在已经了所有网关路由器的私有团体字，通过编写简单的脚本使用 SNMP 和 TFTP 协议复制该网络上所有的路由器配置，我们不仅攻破了整个网络集成公司的基础设施，还攻破了他们客户的基础设施。

现在我们对 SNMP 有了基本的了解，可以探索它的主要功能之一：SNMP MIB 树。

SNMP 管理信息库（MIB）是一个包含通常与网络管理相关的信息的数据库。数据库被组织成树形，分支代表不同的组织或网络功能。树的叶节点（或最终终端）对应于特定的变量值，外部用户可以访问并探测。IBM Knowledge Center 包含了关于 MIB 树的丰富信息。

例如，MIB 值对应特定的 Microsoft Windows SNMP 参数，并包含比基于网络的信息更多的内容：

> 374 (IBM, 2022), https://www.ibm.com/support/knowledgecenter/ssw_aix_71/programming/mib.html

### 表 2 - Windows MIB 值

| OID | 名称 |
| :--- | :--- |
| 1.3.6.1.2.25.1.6.0 | 系统进程 |
| 1.3.6.1.2.25.4.2.1 | 运行中的程序 |
| 1.3.6.1.2.25.4.2.4 | 进程路径 |
| 1.3.6.1.2.25.2.3.1.4 | 存储单元 |
| 1.3.6.1.2.25.6.3.1.2 | 软件名称 |
| 1.3.6.1.2.25.4.1.1 | 用户账户 |
| 1.3.6.1.2.25.1.1.1.2 | 端口 |

要扫描端口，可以使用 `nmap` 并使用 `-U` 参数，通过特定的选项显示。

```
kali@kali:~# nmap -U -p 161 192.168.50.151 -o output.txt

Starting Nmap for 192.168.50.151

...

Nmap scan for 192.168.50.151 completed in 12.45 seconds

Host is up.

161/udp open
```

# OffSec

## 列表 89 - 使用 snmpwalk 列举 Windows 进程

该命令返回一个字符串数组，每个字符串包含一个运行进程的名称。这些信息可能非常有价值，因为可能会揭示存在漏洞的应用程序，甚至指示目标主机上运行的是哪种防病毒软件。

同样，我们可以查询该机器上安装的所有软件：

```
kali@kali:~$ snmpwalk -c public -v1 192.168.50.151 1.3.6.1.2.1.25.6.3.1.2

iso.3.6.1.2.1.25.6.3.1.2 = STRING: "Microsoft C++ 2019 Minimum Runtime - 14.27.29016"

iso.3.6.1.2.1.25.6.3.1.2 = STRING: "VM Tools"

iso.3.6.1.2.1.25... = STRING: "Microsoft C++ 2019 X64 Additional Runtime - 14.27.29016"

iso.3.6.1.2.1.25.6.3.1.4 = STRING: "Microsoft C++ 2015-2019 Redistributable (x86) - 14.27.29016"

iso.3.6.1.2.1.25.6.3.1.5 = STRING: "Microsoft C++ 2015-2019 Redistributable (x64) - 14.27.29016"

iso.3.6.1.2.1.25.6.3.1.6 = STRING: "Microsoft C++ 2019 X86 Additional Runtime - 14.27.29016"
```
