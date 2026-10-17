
`SYSLOG_LEVEL`—发送消息的 syslog 级别。

然后，编辑 `portsentry.conf`。`README.install` 解释了不同的设置。

添加任何你希望 PortEntry 忽略的主机到 `portsentry.ignore`。

最后，编译程序：

```
make linux
make install
```

这将把程序和配置文件放在 `/usr/local/psionic/portsentry` 中。要启动 PortSentry，进入此目录并输入：

```
./portsentry <option>
```

选项在 `README.install` 中有详细解释。你一次只能使用一个选项，但如果你想同时监控 TCP 和 UDP 端口，可以加载多次 PortSentry。例如，若要在 TCP 和 UDP 端口上都使用高级扫描（最安全），请输入：

```
./portsentry -atcp
./portsentry -autp
```

# 业务应用程序

对于我们的目的而言，业务应用程序是指运行在个人 PC 上并执行业务功能的程序。最最销的软件标题加载了各种业务应用程序。例如，销量最畅销的 Microsoft Office 是一系列常用业务应用程序的组合，包括文字处理器 `Word`、电子表格 `Excel` 和演示文软件 `PowerPoint`。

某些版本的 Microsoft Office 包含电子邮件和日历程序 `Outlook` 以及数据库 `Access`。这两个应用程序在其他章节中都有介绍。

财务程序如 Intuit 的 Quicker 和 Microsoft Money 也是必重要的业务程序。图形程序如 Adobe Photoshop、Corel Draw 和 Microsoft Visio 完善了这一业务程序列表。

## 6.1 Microsoft Office

凭借 95% 的市场份额，Microsoft Office 是生产力套件中的“重量级选手”。如果你从别人那里得到一个文档、电子表格或演示文稿，它很有可能是一个 Microsoft Office 文件。

因此，为了让 Linux 在桌面端流行起来，它必须有一个与 Microsoft Office 相似的程序，并且必须能够读写 Office 文件。

Linux 有几个与 Microsoft Office 相似的程序。它们大部分都有 Windows 版本。但没有一个是 Microsoft Office 的完整、无缝替代品。每个程序都有需要考虑的优缺点。

处理 Office 文件是一个大问题。由于每个 Office 应用程序都使用专有格式，因此在其他程序打开它们之前，必须对文件格式进行反向工程。Office 应用程序彼此以及与 Windows 操作系统紧密集成，这一事实使得问题更加复杂。目前，没有任何 Linux 应用程序 100% 兼容 Office 文件，但某些比其他的要好。

## 6.2 Corel WordPerfect Office

虽然它的市场份额远不及 Microsoft Office，但 Corel WordPerfect Office 是市场上第二种受欢迎的生产力套件。它具有与 Microsoft Office 相同的所有功能，包括文字处理 `WordPerfect`、电子表格 `Quatro Pro`、演示 `Presentations`、日历 `CoreCENTRAL` 和 Web 发布 `Trellix`。豪华版还带有一个数据库 `Paradox`、更多字体、更多剪贴画、游戏《铁路大亨》以及服务器版 `http://www.corel.com/Office2000/index.htm`。Linux 版的 WordPerfect `WP` 与 Windows 版本代码相同，因此版本看起来几乎完全一样。Core 决定使用 `WINE` 库来实现低级兼容。`WP Office` 自带一个服务器。标准版带有 100 多种字体。服务器还允许通过将字体拷贝到目录来使用 Windows 和 TrueType 字体！`WP Office` 拥有任何 Linux 中效果最好的字体。加载 `WP Office` 程序大约需要 30 秒到 2 分钟。加载 `WINE` 仅需几秒钟。一旦程序加载，在良好的电脑上响应是合理的。请注意，`WP Office` 不适用于低端系统。为了获得良好的性能，你必须拥有 Pentium 200 或更好的处理器、64MB 内存和 540MB 空闲磁盘空间。Core 花了大量时间让 `WP Office` 能够读写 Office文档。`Word`、`Excel` 和 `PowerPoint` 文档导入 `WP Office` 并没有太大困难。在本章后面的部分，我们将讨论导入导出 MS Office 文件。`WP Office` 还具有导出 HTML、XML、RDF 和 TIFF 等便携格式的能力。HTML 是网页使用的标准格式。`WP Office` 允许将文档、电子表格和演示文稿直接导出为 HTML 发布在网页上，无需单独的 HTML 编辑器。XML 与 HTML 类似，但用户可以定义自己的数据格式。Adobe 的 PDF（文档格式）允许文档在不同平台上看起来完全相同。它是分文档和法律摘要的流行方式。最后，RTF（富文本格式）最早被 Microsoft Word 用于将 Word 文档导出到其他文字处理器。它不支持现代文字处理器的高级功能，但所有主要的文字处理器都支持它。`WP Office` 也有一些缺点。在某些 Linux 发行版上存在安装问题。它似乎在 Red Hat、Mandrake 和 Core Linux 上安装良好，但在其他发行版（包括 SuSE Linux）上存在问题。许多这些问题都有解决方法。更多信息请查看 Core 支持页面 `http://corel.com/support/wp2000-linux.htm`。运行 `WP Office` 还会导致稳定性问题。`WINE` 仍在开发，尚未稳定。幸运的是，`WP Office` 的崩溃不会导致整个桌面崩溃。只需确保开启了自动保存功能：前往工具 -> 设置 -> 文件 -> 文档，勾选定时文档备份并设置分钟数即可。

## 6.3 其他商业生产力套件

59

![](img/a1ad58e4259f15e8b2826ecf57a28362_74_0.png)

**图 6.1** 设置自动保存功能。在这种情况下，设置为每 10 分钟保存一次。

Linux 版 `WP Office` 缺少了大多数办公套件常见的两个功能：互联网集成和与个人数字助理（PDA）的热同步（HotSync）。`WP Office` 没有内置的 Web 浏览器或电子邮件。Netscape 捆绑 `WP Office` 并不是什么大问题，但有时在不打开另一个应用程序的情况下查看邮件或网页会更方便。

HotSync 将 Windows 版 `WP Office` 和所有版本的 Star Office 连接起来。如果与 PDA 同步日历对你很重要，你可能想要考虑 Linux 的 Star Office。

### 6.21 Linux 版 WordPerfect 8

WordPerfect 8 `WP8` 仍然可以从 Core 网站下载。虽然它作为版本 9 兼容 Microsoft Office，但它仍然保留了版本 9 的大部分功能。它的运行速度也快得多，因为它使用的是原生代码而非 `WINE`。它是低端系统的极佳选择，因为它可以在带有 16MB 内存的旧 486 电脑上运行。

`WP8` 提供免费版和完整的商业包，零售价约为 50 美元，尽管它的售价通常更低。个人版是一个功能齐全的程序。完整版包含了个人版未包含的额外图形、剪贴画和字体 `http://corel.com/products/wp8/`。

## 6.3 其他生产力套件

Lotus SmartSuite 还没有推出 Linux 版的官方计划，但我对 Lotus 决定将 SmartSuite 移植到 Linux并不并不意外，因为他们已经注意到母公司 IBM 正在向 Linux 开发投入大量资源。

### 6.3.1 Star Office

Sun 的 Star Office 对 Microsoft 文件支持非常出色。它提供了与文字处理 `Writer`、电子表格 `Calc`、演示文稿 `Impress`、图形 `Draw`、电子邮件 `Mail`、日历管理 `Schedule` 和数据库 `Base` 等效的程序。它还集成了一个 Web 浏览器。虽然它的功能没有像 Microsoft Office 那么丰富，但它提供了所有功能，如页眉、页脚和模板。

### Star Office 最大的缺点可能是它的体积和速度。它需要 60MB 的磁盘空间和至少 32MB 的内存才能获得体面的性能。即使在快速系统上，它的加载也需要时间。Star Office 确实具有 HotSync 功能，这是其他 Linux 办公套件所不具备的。如果将 PDA 与你的办公套件同步对你很重要，Star Office 提供了最好的支持。

Star Office 还内置了一个桌面。在 Windows 机器上，它用自己的桌面替换默认的 Windows 桌面。可以从 Sun 网站免费下载 Star Office，或者以约 40 美元的价格通过 CD 购买 `http://www.sun.com/staroffice/`。
