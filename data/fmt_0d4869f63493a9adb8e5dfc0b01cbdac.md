
### 单击 New Type
单击 `New Type`。会出现一个对话框，允许你添加有关辅助应用程序及其可以处理的数据的信息。

### 输入数据描述
输入数据的描述、`MIME` 类型以及包含该类型数据的文件的后缀（如果有）。

> 注意：添加后缀时，不要包含点 。

### 选择处理应用程序
选择处理该数据类型应用程序。如果应用程序需要终端窗口运行，请键入 `xterm -e`，后跟你需要输入的命令行。这将在 `xterm` 窗口中执行命令，根据需要读取数据。

### 完成
完成后单击 `OK`。

下次你在 Mozilla 中打开你刚刚添加类型的数据时，弹出窗口会询问你是否要使用你刚刚输入的应用程序打开数据。

## 添加插件

在随 Red Hat Linux 提供的 Mozilla 版本中，可用的插件并不多。要查看与你的 Mozilla 浏览器关联的插件列表，请选择 帮助 → 关于插件。你可能会看到一个插件：Plugger。如果未安装 Plugger，你可以从 CD #3 安装它。Plugger (http://frederik.hubbe.net/plugger.html) 是一个多媒体插件，通过依赖外部程序播放数据来处理 QuickTime、MPEG、MP2、AVI、SGI-movie、Tiff、DL、IFF-anim、MIDI、Soundtracker、AU、WAV 和 Commodore 64 音频文件。最近，Plugger 还增加了对显示各种 Microsoft 文件类型的支持。

以下是一些可与 Red Hat Linux 配合使用的 Mozilla 免费插件列表。

- **Adobe Acrobat Plug-in** (www.adobe.com/support/downloads) — 显示来自 Adobe Systems 的 PDF（便携式文档格式）文件。
- **Cult3D Plug-in** (www.cult3d.com) — 在网页上显示高质量、交互式实时 3D 图像。该插件来自 Cycore Computers。（单击 Download 找到插件。有可用的 cult3D RPM 需要定制才能在 Mozilla 中工作。）
- **DjVu Plug-in** (djvu.sourceforge.net) — 显示 DjVu 图像压缩技术中的图像。该插件来自 AT&T。
- **Real Audio** (www.real.com) — 播放 Real Audio 和视频内容。（要在 Mozilla 中使用 Real Play 插件，你需要 RealPlayer 和 realplay-npplugin RPM，可通过搜索 rpmfind.net 获得）。
- **Macromedia Flash Player** (www.macromedia.com/) — 显示多媒体矢量图形和动画。该插件来自 Macromedia, Inc。Flash Player 可用于 Red Hat Linux，但 Macromedia 的 Shockwave 插件尚未适用于 Linux。
- **Xswallow** (www.csn.ul.ie/~coa1an/docs/Xswallow.html) — 允许 X 窗口程序用作内联查看器。

未来可能会为 Red Hat Linux 添加更多插件供使用。Mozilla 现在提供了一个很棒的新网站，用于获取可在 Mozilla 中运行的 Linux 插件：

http://plugindoc.mozdev.org/linux.html。该网站包含下载插件的链接和安装说明。

当你下载插件时，请遵循随插件提供的安装说明。如果插件以 RPM 文件形式提供，请像在 Red Hat Linux 中安装任何其他软件包一样安装它（`rpm -iv package` 命令）。否则，可能只需将插件文件（一个 `.so` 文件）复制到系统插件目录（可能是 `/usr/lib/mozilla/plugins`）或你的个人插件目录（可能是 `$HOME/.mozilla/plugins`）。重新启动 Mozilla 后，插件将自动从这些位置拾取。

> **注意：** CrossOver Plugin 是一款商业产品，可让你在 Mozilla 中使用许多 Windows 插件。有关详细信息，请参阅本章后面“添加 CrossOver Plugin”部分。

## 使用 Mozilla Navigator 控件

如果您以前使用过网络浏览器，控件可能与您预期的一样：位置框、前进/后退按钮、文件和编辑菜单等等。然而，Mozilla 中有一些控件您可能不习惯看到。以下是一些示例：

- **使用侧边栏** — 按 `F9` 功能键打开或关闭侧边栏。点击“相关内容”、搜索、书签或历史记录标签（或按前面所述添加自己的标签）。添加自己的书签、从历史记录列表返回页面，或搜索网页内容。
- **发送网页内容** — 您可以发送一封包含当前网页（文件 → 发送页面）或当前网页的 URL（文件 → 发送链接）的电子邮件给选定的收件人。
- **搜索互联网** — 您可以以多种不同的方式搜索关键词短语。选择 工具 → 搜索网络 以打开一个可让您搜索互联网的 Netscape 网站。或者在位置框中输入一个或多个关键词，然后点击搜索。当然，您也可以按前面所述使用侧边栏进行搜索。
- **查看页面信息** — 您可以通过选择 查看 → 页面信息 来查看网页的位置、其各个组件的位置、页面修改日期以及其他信息。图 9-4 显示了网页的页面信息窗口。点击链接标签可查看该页面上指向网络上其他内容的链接。点击安全标签可查看页面上使用的验证和加密信息。

![](img/27a85d56d393921ced6412ae6e8336bf_332_0.png)

**图 9-4：** 通过选择页面信息显示有关网页的信息。

## 改进 Mozilla 浏览

使用 Mozilla 访问的每个网站都不会表现良好。有些网站不遵循标准，使用难以阅读的字体，选择使内容难以看清的颜色，或要求您使用特定类型的浏览器来查看其内容。为了改善浏览体验，您可以向 Mozilla 添加一些东西。

### 添加 CrossOver 插件

QuickTime 5 电影、Shockwave Director 多媒体内容以及各种 Microsoft 电影、文件和数据格式在 Mozilla Navigator 中根本无法原生播放。CodeWeavers（www.codeweavers.com）基于 WINE 构建的软件创建了 CrossOver 插件。尽管它花费几美元（一次性用户许可证为 24.95 美元），CrossOver 插件让您可以在 Linux 中播放一些否则无法使用的内容。

安装 CrossOver 插件后，您会看到一个不错的插件设置窗口，可让您选择性地安装 QuickTime 6、Windows Media Player 6.4、Shockwave 8.5、Flash 6 以及 Microsoft Word、Excel 和 PowerPoint 查看器的插件。您还可以安装其他多媒体插件，以及与这些插件一起使用的各种字体。

> **提示：** 尽管我在 Red Hat Linux 早期版本中运行 CrossOver 插件运行良好，但在撰写本文时，它在当前版本的 Red Hat Linux 中尚未正常工作。请与 CodeWeavers 确认他们是否已修正 CrossOver 插件以在最新版 Red Hat Linux 中运行。

### 添加首选项工具栏

您是否遇到过要求您使用特定类型或版本的浏览器，或字体和颜色使页面难以阅读的网页？Mozilla 首选项工具栏可让您尝试欺骗网站，使其认为您正在运行不同的浏览器。它还可让您选择可能改善难以阅读页面上的颜色、字体和其他属性的设置。

您可以从 Mozdev.org 网站（prefbar.mozdev.org）安装这个不错的小工具栏。点击安装链接；然后安装后，重新启动 Mozilla。图 9-5 显示了已安装在 Mozilla 中的首选项工具栏示例。

![](img/27a85d56d393921ced6412ae6e8336bf_333_0.png)

**图 9-5：** 使用 Mozdev.org 首选项工具栏即时更改颜色、字体和浏览器类型。

默认按钮集可让您执行以下操作：

- **颜色** — 在默认颜色和网页上设置的颜色之间切换。
- **图像** — 在显示的页面上切换图像是否加载。
- **JavaScript** — 允许或禁止 JavaScript 内容在 Mozilla Navigator 中播放。
- **清除缓存** — 删除内存和磁盘上的所有缓存内容。
- **终止 Flash** — 终止当前页面上的所有嵌入式 Flash 内容。
- **真实 UA** — 选择将浏览器识别为其自身（当前版本的 Mozilla）或以下任一：Mozilla 1.0（在 Windows 98 中）、Netscape Navigator 4.7（在 Macintosh 中）、Netscape 6.2（在 Linux 中）、Internet Explorer 5.0（在 Macintosh 中）或 Internet Explorer 6.0（在 Windows XP 中）
