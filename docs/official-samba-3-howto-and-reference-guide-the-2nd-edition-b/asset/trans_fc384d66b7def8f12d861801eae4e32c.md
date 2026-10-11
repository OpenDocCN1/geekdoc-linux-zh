
## 21.10.12 如何确认 cupsaddsmb 是否成功完成

在**所有**字段中，你*必须*始终检查该工具是否成功完成。你至少需要在输出中看到以下三条消息：

1.  *打印机驱动程序 infotec_2105 安装成功。*（用于 W32X86 == Windows NT/200x/XP 架构）。
2.  *打印机驱动程序 infotec_2105 安装成功。*（用于 WIN40 == Windows 9x/Me 架构）。
3.  *成功将 [printerXYZ] 设置为驱动程序 [printerXYZ]。*

这些消息在一般输出中可能不容易被识别。如果你运行 **cupsaddsmb** 并附带 *-a* 参数（该参数试图为下载准备*所有活动*的 CUPS 打印机驱动程序），你可能会错过某些单个打印机驱动程序安装过程中出现的问题。重定向输出将帮助你事后分析结果。

如果你得到以下信息：

```
SetPrinter call failed!
result was WERR_ACCESS_DENIED
```

这意味着你可能已将该打印机的*使用客户端驱动程序*设置为“是”。将其设置为“否”将解决问题。请参考 *smb.conf* 手册页以了解关于*使用客户端驱动程序*的解释。

> **注意**
>
> 如果你不运行 **cupsaddsmb** 的详细模式，就不可能看到任何诊断输出。因此，我们强烈建议不要使用默认的静默模式。它会向你隐藏任何可能出现的问题。

## 21.10.13 在 Samba PDC 上运行 cupsaddsmb

无法在 Samba PDC 上运行标准的 **cupsaddsmb** 命令吗？你是否一次又一次地被要求输入密码凭据，而命令却始终无法启动？请尝试以下变体之一：

```
root# cupsaddsmb -U MIDEARTH\\root -v printername
root# cupsaddsmb -H SAURON -U MIDEARTH\\root -v printername
root# cupsaddsmb -H SAURON -U MIDEARTH\\root -h cups-server -v printername
```

（注意有两个反斜杠：第一个是用来“转义”第二个的）。

## 21.10.14 cupsaddsmb 流程图

图 21.16 展示了关于 **cupsaddsmb** 命令的流程、命令流和数据流的图表。再次注意：cupsaddsmb 并非设计用于且不能与原始打印队列配合使用！

![](img/86d74c6cc862465e3a42e6dc3c90935a_450_0.png)

## 21.10.15 在客户端安装 PostScript 驱动程序

**cupsaddsmb** 完成后，你的驱动程序已准备好供客户端使用。以下是通过 Point n Print 下载并安装驱动程序的步骤：从 Windows 客户端浏览到 CUPS/Samba 服务器：

-   在网络邻居中打开 Samba 的**打印机**共享。
-   右键单击问题打印机。
-   从打开的上下文菜单中选择**安装…**或**连接…**（取决于你使用的 Windows 版本）。

几秒后，客户端的*本地打印机*文件夹中应该会有一台新打印机。在 Windows XP 上，它将遵循*打印机名称*在*SambaServer*上的命名约定。[在我当前的情况下，它是 kde-bithop 上的 infotec_2105。] 如果你想测试并发送第一个任务，例如从 Kwinword 应用程序，新打印机将出现在可用打印机下拉列表中的 **\\SambaServer\\PrinterName** 条目中。

**cupsaddsmb** 仅可靠地工作与 CUPS 版本 1.1.15 或更高版本以及 Samba 版本 2.2.4 或更高版本。如果不工作，或者自动打印机驱动程序下载不成功，你仍然可以手动在客户端上安装 CUPS 打印机 PPD，覆盖在 Adobe PostScript 驱动程序之上。然后将客户端的打印机队列指向 Samba 打印机共享，用于 UNC 类型的连接：

```
C:\> net use lpt1: \\sambaserver\printershare /user:ntadmin
```

如果你希望使用 CUPS 网络 PostScript RIP 功能。（请注意，用户 "ntadmin" 需要是一个有效的 Samba 用户，并具备访问打印机共享所需的权限。）这以传统的 LanMan 方式（不使用 MS-RPC）设置打印机连接。

## 21.10.16 避免客户端上关键的 PostScript 驱动程序设置

打印工作了，但仍有问题。大多数任务打印良好，有些则完全无法打印。有些任务在字体方面有问题，看起来不太好。有些任务打印快速，有些则慢得要死。如果你遵循几条准则，可以大大减少甚至完全消除许多这些问题。请记住，如果你的打印设备不支持 PostScript，你是在使用客户端驱动程序设置产生的输出来处理你的 CUPS 主机上的 Ghostscript 安装。好好对待它：

-   避免 PostScript 输出选项：优化速度设置。相反，使用优化可移植性（Adobe PostScript 驱动程序）。
-   不要使用页面独立性：否设置。相反，使用页面独立性：是（CUPS PostScript 驱动程序）。
-   推荐 TrueType 字体下载选项：原生 TrueType 优于自动和轮廓：你应当完全避免位图（Adobe PostScript 驱动程序）。
-   选择 TrueType 字体：作为软字体下载到打印机，优于默认的替换为设备字体（对于异国字体，你可能需要改回去以获得任何打印输出，Adobe）。
-   有时你可以选择 PostScript 语言级别：如果有问题，请尝试 2 而不是 3（最新的 ESP Ghostscript 包非常完美地处理 3 级 PostScript；Adobe）。
-   对 PostScript 错误处理程序回答“是”（Adobe）。

## 21.11 使用 rpclient 手动安装 PostScript 驱动程序文件

当然，你可以自己运行嵌入到 cupsaddsmb 便利工具中的所有命令，逐一上传并为未来客户端下载准备驱动程序文件。

1.  准备 Samba（应有一个名称为打印机名称的 CUPS 打印队列。我们现在提供驱动程序）。
2.  将所有文件复制到 /print8/。
3.  运行 `rpclient addriver`（针对你想支持的每个客户端架构）。
4.  运行 `rpclient setdriver`。

我们现在将执行此操作。首先，阅读 `rpclient` 的手册页以获得初步概念。查看所有与打印相关的子命令：**enumprinters**、**enumdrivers**、**enumports**、**adddriver** 和 **setdriver** 是最有趣的几个。`rpclient` 实现了 MS-RPC 协议的重要部分。你也可以用它来查询（除了命令外） Windows NT（或 200x/XP）PC。MS-RPC 被 Windows 客户端等用于从 Point'n'Print 功能中受益。Samba 现在也可以模拟这一点。

### 21.11.1 检查 rpclient 手册页

首先让我们检查 `rpclient` 的手册页。以下是两个相关段落：

**adddriver** `<arch>` `<config>` 执行 **AddPrinterDriver()** RPC 以在服务器上安装打印机驱动程序信息。驱动程序文件应已存在于由 **getdriverdir** 返回的目录中。`arch` 的可能值与 **getdriverdir** 命令相同。`config` 参数定义如下：

```
Long Printer Name:\
Driver File Name:\
Data File Name:\
Config File Name:\
Help File Name:\
Language Monitor Name:\
Default Data Type:\
Comma Separated list of Files
```

任何空字段应输入字符串“NULL”。

Samba 不需要支持打印监视器概念，因为这些仅适用于可以使用双向链接进行通信的本地打印机。此字段应为 "NULL"。在远程 NT 打印服务器上，在添加驱动程序之前，必须已安装该驱动的打印监视器，否则 RPC 将失败。

**setdriver** *<printername> <drivername>* 执行 **SetPrinter()** 命令以更新与已安装打印机关联的打印机驱动程序。打印机驱动程序必须已正确安装在打印服务器上。

另请参阅 **enumprinters** 和 **enumdrivers** 命令，以获取已安装打印机和驱动程序的列表。

### 21.11.2 理解 rpcclient 手册页

手册页没有清楚地说明*确切*格式，因为你需要处理一些包含空格的参数。以下是更好的描述。我们对命令进行了换行，并用“\\”标示了断点。通常你应在一行内输入命令，而不进行换行：

```
adddriver "Architecture" \
"LongPrinterName:DriverFile:DataFile:ConfigFile:HelpFile:\LanguageMonitorFile:DataType:ListOfFiles,Comma-separated"
```

手册页所表示的简单 *<confiig>* 关键字实际上由八个冒号分隔的字段组成。最后一个字段可以包含多个（在某些非常疯狂的情况下，甚至 20 个不同的额外）文件。这起初听起来可能令人困惑。手册页所称的 "LongPrinterName" 实际上应称为 "Driver Name"。你可以随意命名，只要你随后在 **rpcclient ... setdriver** 命令中使用此名称即可。出于实用原因，许多人将驱动程序命名与打印机相同。

这并不简单。我听到你在问：“现在我如何知道哪些文件是 Driver File”、“Data File”、“Config File”、“Help File” 以及 “Language Monitor File”？为了找到答案，你可能想查看具有共享打印机的 Windows NT 系统向我们呈现文件的方式。请记住，整个流程必须由 Samba 团队通过监听线缆上 Windows 计算机引起的流量来开发。我们现在也可以转向 Windows 系统，并从 UNIX 工作站访问它。我们将使用 **rpcclient** 对其进行查询，看看它告诉我们的内容，并尝试更清楚地理解手册页。

### 21.11.3 通过查询 Windows 系统生成示例

我们可以对 **rpcclient** 运行 **getdriver** 或 **getprinter** 子命令（在 3 级详细程度下）来针对它。只需坐在安装了 Samba 实用程序的 UNIX 或 Linux 工作站前，然后键入以下命令：

