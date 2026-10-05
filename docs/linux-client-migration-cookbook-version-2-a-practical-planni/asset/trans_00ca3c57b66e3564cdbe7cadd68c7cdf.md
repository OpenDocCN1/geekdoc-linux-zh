

![](img/23b949da14ff7bab8762f0f0361af394_307_0.png)

图 C-1 Progression Desktop 中性化过程

## GUI

GUI 允许用户通过“下一步-下一步-完成”风格的向导界面进行迁移。用户会看到一系列问题，询问应该捕获并存储 Windows 桌面上的哪些系统设置、应用程序设置和文件以便迁移。例如，在第 281 页的图 C-2 中了检测到的应用程序列表，用户正在选择迁移 Microsoft Outlook、AOL Instant Messenger、Microsoft Internet Explorer 和 Microsoft Word 的设置。

![](img/23b949da14ff7bab8762f0f0361af394_308_0.png)

图 C-2 Windows 上的存储存储

接下来，在 Linux 桌面上，用户界面会询问将这些设置应用于哪些目标应用程序和位置。在第 282 页的图 C-3 中，应用程序正在请求图 C-2 中存储的设置。用户已选择将 Microsoft Internet Explorer 映射到 Mozilla Firefox，将 AOL Instant Messenger 映射到 GAIM，将 Microsoft Outlook 映射到 Novell，将 Microsoft Word 映射到 OpenOffice.org Writer。

附录 C 使用 Versora Progression Desktop 自动化桌面迁移 281

## Progression Desktop

应用程序设置目标地

请选择您希望应用设置的应用程序。您可以使用下拉菜单为可以应用到多个目标的应用程序选择合适的目标。

如果您不想迁移某个应用程序，可以选择该应用程序的“不迁移”选项。

| 应用程序 | 目标 |
| :--- | :--- |
| AOL | AOL Instant Messenger |
| GAIM | |
| Microsoft | MSN Messenger |
| Microsoft | Excel |
| Microsoft | OpenOffice.org Calc |
| Microsoft | Outlook |
| Microsoft | PowerPoint |
| Microsoft | OpenOffice.org Writer |

返回
继续

![](img/23b949da14ff7bab8762f0f0361af394_309_0.png)

### Linux 上的 Progression Desktop 设置

使用 GUI 进行迁移是最简单的。然而，由于此选项需要一些设置，它最适合较小的群体。对于较大的群体，您应该考虑命令行。

### 命令行

模板在 XML 文件中定义，它们告诉 Progression Desktop 需要捕获哪些项目以及将它们放在何处。由于并非所有系统都提供 GUI，命令行界面允许您自动化迁移。这种方法也适用于没有 GUI 或不想要 GUI 的环境。

所有平台通用的通用迁移步骤为：

- 1. 创建模板。
- 2. 创建平台中性包（Platform Neutral Package）。
- 3. 应用平台中性包。

## 桌面架构

Progression Desktop 的主要设计目标之一是可扩展性。由于对于每个常用和目标数据集，在 Windows 和 Linux 中都有许多独特的应用程序选择，Progression Desktop 需要能够迁移到几种不同的配置。例如，运行 Microsoft Outlook 的用户可能想要迁移到 Evolution，而另一个用户可能从 Mozilla Mail 迁移到 Thunderbird。为了实现这一目标并在 Windows 和 Linux 上运行，Progression Desktop 利用了基于插件的架构和运行在 .NET 上的 XML 数据文件。为此开发的三项主要技术是 PNP 文件格式、设置包（Settings Packages）以及作为转换（Transforms）和附件（Accessories）的插件。

## PNP 文件

Progression Desktop 将提取的设置存储在平台中性包（简称 PNP）中。PNP 文件是标准的 Zip 文件，可以使用您喜欢的 Zip 编辑器（如 FileRoller、Ark 或 WinZip）打开。第 285 页的图 C-4 显示了