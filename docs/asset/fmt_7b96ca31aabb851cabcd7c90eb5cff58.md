
macOS Sierra 的另一个重大变化是系统范围支持标签窗口。标签页（`Tabs`）允许你在单个窗口内多个内容面板之间切换，而不是采用传统的 OS X 拥有独立应用程序窗口的方法。所有应用程序，即使是未为 macOS Sierra 更新的第三方应用程序，都可以利用标签窗口。

`iCloud Drive` 现在会同步用户“桌面”和“文档”文件夹的所有内容。随着更多项目被安全地存储在 `iCloud` 中，不再需要将这些项目永久存储在 Mac 计算机的本地硬盘上。为此，macOS Sierra 还包含“优化存储”（`Optimized Storage`），这是一套自动释放本地硬盘空间的存储管理技术。

几项新的 macOS Sierra 功能改进了 Apple 设备之间的集成。你现在：

- 使用 `Apple Watch` 解锁 `Mac`
- 在 `Mac` 上使用 `Apple Pay`
- 使用通用剪贴板（`Universal Clipboard`）在 Apple 设备之间复制和粘贴

最后，几个内置的 macOS Sierra 应用了更新，以提供与其 `iOS 10` 对应的功能的功能。这包括许多应用程序的改进，例如 `iTunes`、音乐、信息、备忘录和照片。

### 更多信息

macOS Sierra 新功能的完整列表可以在 `www.apple.com/macos/sierra/` 找到。

### 通过标准集成

macOS 的成功很大程度上归于 Apple 对行业标准格式和开源软件的采用。采用通用标准可以节省工程时间，并允许与其他平台进行更流畅的集成。当 Apple 开发者必须为新功能设计技术时，Apple 通常会将速度发布给开发者社区，从而培养出新标准。一个例子是 `Bonjour` 网络发现，由 Apple 开创并维护为一种行业标准协议多播 DNS (`mDNS`)，供他人开发和使用。以下是 macOS 支持的一些通用标准的示例：

- 连接标准——通用串行总线 (`USB`)、`IEEE 1394` (`FireWire`)、雷电 (`Thunderbolt`)、蓝牙无线，以及 `IEEE 802` 系列以太网和 `Wi-Fi` 标准
- 文件系统标准——文件分配表 (`FAT`)、新技术文件系统 (`NTFS`)、`ISO 9660` 光盘格式、通用磁盘格式 (`UDF`) 以及由 `NextStore` 文件系统维护的 `XFS` 文件系统
- 网络标准——动态主机配置协议 (`DHCP`)、域名系统 (`DNS`)、超文本传输协议 (`HTTP`)、互联网访问协议 (`IMAP`)、简单邮件传输协议 (`SMTP`)、文件传输协议 (`FTP`)、`Web` 分布式访问与验证 (`WebDAV`) 以及连接 `SMB` 的服务器块/通用互联网文件系统 (`SMB/CIFS`)
- 应用和开发标准——单 Unix 规范 v3 (`SUSv3`)、可移植操作系统接口 (`POSIX`)、`C` 和 `C++`、`Ruby`、`Python`、`Perl` 和 `Swift`
- 文档标准——`ZIP` 文件归包、富文本格式 (`RTF`)、便携文档格式 (`PDF`)、标签图像文件格式 (`TIFF`)、联合图像专家组 (`JPEG`)、可移植网络图形 (`PNG`)、高级音频编码 (`AAC`) 以及影像专家组 (`MPEG`) 系列媒体标准

### 参考文献 1.2 选择安装方法

你想完成多少课程取决于你 Mac 的状态。你可以阅读整个课程，但你可能不想在你运行的 Mac 上尝试这里的所有技术。

> 提示：如果你不知道你的 Mac 运行的是哪个版本的 macOS，只需从 `Apple` 菜单中选择“关于本机”。

你的 Mac 可能属于以下大类别之一。

### 运行 macOS Sierra 且无重大问题

如果是这样，你可以阅读整个课程，但你可能不想在你运行的 Mac 上尝试这里的所有技术。

请确认您的 Mac 和 Mac 操作系统符合升级到 macOS Sierra 的要求。如果您不确定规格，请使用“系统报告”（`System Profiler`）或“系统信息”（`System Information`）进行查询。

`系统报告`（适用于 `OS X Snow Leopard 10.6`）和 `系统信息`（适用于 `OS X Lion 10.7` 及更高版本）位于 `/Applications/Utilities` 文件夹中。在任一个应用程序中，您都可以通过选择并查看“硬件”部分的各个区域来验证 Mac 电脑的规格。

![](img/054d569616d6bf404cc0816f583e361a_28_0.png)

在安装 macOS Sierra 之前，请记录 Mac 电脑的内存容量和序列号。此外，检查 `SATA`/`SATA Express` 或存储部分查看系统磁盘（通常命名为 `Macintosh HD`）的可用空间。

### MacBook Pro

## 硬件概览：

| 属性 | 值 |
| --- | --- |
| 型名称 | MacBook Pro |
| 型号标识符 | MacBookPro10,1 |
| 处理器名称 | Intel Core i7 |
| 速度 | 2.3 GHz |
| 核心数 | 4 |
| L2 缓存（每核心） | 256 KB |
| L3 缓存 | 6 MB |
| 内存 | 16 GB |
| BOOT RAM 版本 | MBP101.0EE.B02 |
| SMC 版本（系统） | 2.335 |
| 序列号（系统） | C02HV144DB02 |
| 硬件 UUID | 48FA7891-D176-52A4-9EF2-04BC144DB002 |

升级到 macOS Sierra 有以下通用要求：

- `OS X Lion 10.7.5` 或更高版本
- `2 GB` 内存
- `8.8 GB` 可用存储空间
- `Apple ID`（某些功能需要）
- 兼容的互联网提供商（某些功能需要）

除此之外，您还需要确认您的 Mac 是否受支持。获取 Mac 电脑的序列号后，可以在 Apple 支持技术网站（`http://support.apple.com/specs/`）上进行比对。访问该网站，在“搜索规格”字段中输入 Mac 序列号，并点击“搜索”按钮。

搜索结果将返回 Mac 的型号名称。请注意，之前的截图显示 Mac 被识别为 `MacBookPro10,1`。虽然 `MacBookPro10,1` 是一个特定的标识符，但它并不是 Apple 用于技术规格的名称。在 Apple 支持技术网站上输入此 Mac 电脑的序列号将返回用于技术规格的官方型号：“MacBook Pro (Retina, 15-inch, Mid 2012)”。

macOS Sierra 支持以下 Mac 机型：

- `MacBook`（2009 年末或更新型号）
- `MacBook Pro`（2010 年中期或更新型号）
- `MacBook Air`（2010 年末或更新型号）
- `Mac mini`（2010 年中期或更新型号）
- `iMac`（2009 年末或更新型号）
- `Mac Pro`（2010 年中期或更新型号）

### macOS Sierra 功能要求

macOS Sierra 的某些功能要求超出了最低系统要求。许多此类功能依赖于其他设备或服务。例如，为了利用 `Handoff` 功能（如您的 Mac 处理 `iPhone` 蜂窝电话或短信的能力），您需要一台支持 `Handoff` 的 `iPhone`。另一个例子是 `Siri` 或 `Spotlight` 需要宽带网络访问。

Mac 可能需要特定的硬件来支持新功能。例如，“连续互”（`Handoff`、即时热点和通用剪贴板）需要配备 `蓝牙 4.0` 的 Mac 电脑。另一个新功能“自动解锁”需要飞行时间计算，这在配备最新 `802.11ac Wi-Fi` 的 Mac 电脑上可行。访问 `https://www.apple.com/macos/how-to-upgrade` 了解更多关于 macOS Sierra 的特定要求。

### Mac 要求

Mac 电脑带有专门为它们设计的 Mac 操作系统版本。某些 Mac 电脑可能包含额外的捆绑软件。本文假设您使用的是标准版本的 macOS Sierra。如果您使用的是编写本文时尚未发布的特定 Mac macOS 版本，细节可能会有所不同。另一个考虑因素是，macOS 版本不支持比它们新的 Mac 电脑。也就是说，您可能会遇到比您正尝试安装的 macOS Sierra 版本更高的 Mac。如果发生这种情况，安装可能会无法启动 Mac 或拒绝安装。请使用 macOS 恢复。

更多信息：请参阅 Apple 支持文章 `HT20431`，“随 Mac 发布的 OS X 版本”以及 `HT20168`，“使用随 Mac 附的 OS X 版本”。

### 准备升级

尽管您可以在未完成某些步骤的情况下启动 macOS 升级，但通过采取四个关键步骤可以减少升级问题或数据丢失的概率：

1. 验证应用程序兼容性。
2. 备份重要文件和文件夹。
3. 记录设置。
4. 检查 Apple 软件更新。

注意：这似乎是常识，但您不希望在升级过程中断电。升级期间请连接 AC 电以确保升级成功。

### 验证应用程序兼容性
