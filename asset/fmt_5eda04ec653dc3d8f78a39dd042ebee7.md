
*列表 121 - 创建并执行独立载荷*

值得注意的是，像这样的独立载荷可能很容易被 IDS 检测到。具体来说，生成的脚本相当大，大约有 300 行代码。此外，它还包含一些硬编码字符串，这些字符串可以很容易地用于创建恶意活动签名。虽然任何特定签名的识别超出了本模块的范围，但足以说，像这样的明文恶意代码很可能成功率较低，并很可能被防御性软件解决方案捕获。

我们可以尝试通过利用 PowerShell 执行 Base64 编码命令的能力来克服这个问题。要生成一个独立的编码载荷，我们使用 `-ge` 选项，并再次将输出重定向到文件：

---
<sup>95</sup> (Microsoft, 2019), https://docs.microsoft.com/en-us/powershell/
<sup>96</sup> (besimorhino/powercat, 2017), https://github.com/besimorhino/powercat/blob/master/powercat.ps1
<sup>97</sup> (besimorhino, 2018), https://github.com/besimorhino
<sup>98</sup> (SS64, 2019), https://ss64.com/ps/source.html
<sup>99</sup> (Wikipedia, 2019), https://en.wikipedia.org/wiki/Payload_(computing)

## 4.3.8.1 练习

- 1. 使用 `PowerShell` 和 `powercat` 从你的 Windows 系统向你的 Kali 机器创建一个反向 Shell。
- 2. 使用 `PowerShell` 和 `powercat` 在你的 Windows 系统上创建一个绑定 Shell，并从你的 Kali 机器连接到它。你还能使用 `powercat` 在本地连接到它吗？
- 3. 使用 `powercat` 生成一个编码后的有效载荷（payload），然后通过 `powershell` 执行它。让反向 Shell 发送到你的 Kali 机器，同时在你的 Windows 系统上创建一个编码后的绑定 Shell，并使用你的 Kali 机器连接到它。

### 4.4 Wireshark

一名合格的安全渗透测试人员应精通网络基础。网络嗅探器（如行业标准工具 Wireshark<sup>100</sup>）是学习网络协议、分析网络流量以及调试网络服务的必备工具。在本节中，我们将讨论一些 Wireshark 的基础知识。

#### 4.4.1 Wireshark 基础

Wireshark 使用 `Libpcap` <sup>101</sup>（在 Linux 上）或 `Winpcap` <sup>102</sup>（在 Windows 上）库来捕获网络数据包。

在使用嗅探器分析网络流量时，收集数据中的大量“噪声”很容易让人眼花缭乱。为了便于分析，我们可以应用捕获过滤器（capture filters）<sup>103</sup>和显示过滤器（display filters）<sup>104</sup>。如果在 Wireshark 会话期间应用捕获过滤器，则不符合过滤器条件的数据包将被丢弃，剩余的数据将被传递到*捕获引擎*。捕获引擎随后解析传入的数据包，对其进行分析，最后在显示输出之前应用任何额外的*显示过滤器*。

以下图表展示了这一过程：

![](img/ec25e59d75726b7041242a56d3376832_95_0.png)

*图 11：从线路到 Wireshark*

使用任何网络嗅探器（包括 Wireshark）的秘诀在于学会如何使用捕获和显示过滤器来剔除多余的数据。幸运的是，Wireshark 的图形界面使得可视化和处理各种过滤器变得相对容易。

#### 4.4.2 启动 Wireshark

在以下示例中，我们将在匿名 FTP 登录期间捕获网络流量。在我们的 Kali 系统上，我们使用命令行启动 Wireshark，如列表 125 所示，或者通过应用程序菜单启动，它位于嗅探与欺骗（Sniffing & Spoofing）子菜单下。

```
kali@kali:~$ sudo wireshark
```
*列表 125 - 从终端运行 wireshark*

#### 4.4.3 捕获过滤器

当 Wireshark 加载时，我们会看到一个基本窗口，其中可以选择要监控的网络接口，并设置显示过滤器和捕获过滤器。如上所述，我们可以使用捕获过滤器通过丢弃不符合过滤器的流量来减少捕获的流量，并将注意力集中在我们要分析的数据包上。请注意，任何被捕获过滤器排除的流量都会丢失，因此，如果你担心可能会丢失数据，最好定义较广泛的捕获过滤器。

我们首先选择要监控的接口并输入捕获过滤器。在这种情况下，我们使用网络过滤器（net filter）<sup>105</sup> 仅捕获 `10.11.1.0/24` 地址范围内的流量：

![](img/ec25e59d75726b7041242a56d3376832_97_0.png)

*图 12：为 tap0 设置捕获过滤器*

也可以通过导航到 `Capture > Capture filters` 来选择预定义的捕获过滤器，我们也可以点击 `+` 号添加我们自己的捕获过滤器。设置好捕获过滤器后，我们可以双击可用接口列表中的网络接口（`tap0`）开始捕获。

#### 4.4.4 显示过滤器

现在 Wireshark 正在捕获本地网络上的所有流量，我们可以登录到 FTP 服务器并检查流量：

```
kali@kali:~$ ftp 10.11.1.13

Connected to 10.11.1.13.

220 Microsoft FTP Service

Name (10.11.1.13:kali): anonymous

331 Anonymous access allowed, send identity (e-mail name) as password.

Password: anonymous

230 Anonymous user logged in.

Remote system type is Windows_NT.

ftp> quit

221
```
