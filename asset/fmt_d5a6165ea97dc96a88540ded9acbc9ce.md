
### 控制面板
如果应用程序为 Windows 控制面板设置了小部件，您可以打开一个 Windows 控制面板，然后选择该小部件以从那里启动应用程序。要启动 Windows 控制面板，请输入以下内容：

```
$ wine control
```

### WINE 文件系统浏览器
如果您安装了 `wine-core` 包，您可以启动 `winefile` 命令以查看 Wine File 窗口。此窗口显示与您为 WINE 配置的驱动器相关的文件系统树结构。选择包含您要启动的应用程序的驱动器号，浏览到该应用程序，然后双击以启动它。

正如前面所述，就像您启动应用程序安装程序一样，您也可以从命令行启动安装在您的文件系统上的 Windows 应用程序。同样，您可以使用驱动器号来表示您要启动的应用程序的位置。但是，为了正确解释应用程序的路径，您通常应该用引号将其包围：

```
$ wine "C:\program files\appid\app.exe"
```

作为 Windows 文件路径，您使用反斜杠 (`\`) 而不是斜杠 (`/`) 来分隔子目录。除了使用双引号外，您还可以在每个空格或反斜杠前添加一个额外的反斜杠。

一旦您有了用于运行 Windows 应用程序的有效 `wine` 命令行，您就可以将该命令添加到您的 Fedora 桌面上的启动器中。有关将应用程序启动器添加到您的面板、菜单或桌面区域的信息，请参阅第 3 章。

### 调整和配置 WINE
由于您使用 WINE 运行的 Windows 应用程序期望在 Linux 系统上找到 Windows 资源，这些资源要么由 WINE 提供，要么需要映射到现有的 Linux 系统。例如，某个应用程序可能需要 WINE 未包含的特定 DLL 文件。或者，您可能需要在 WINE 期望找到 COM 或 LPT 端口的地方映射它们。

以下是一些帮助调整 WINE 配置的技巧：

- **Windows 版本** — 不同版本的 Windows 为应用程序运行提供了不同的环境。WINE 默认模拟 Windows XP，但允许您为每个应用程序让 WINE 运行多达十几个不同的 Windows 版本。从 WINE 配置窗口中，选择“应用程序”标签页并选择“添加应用程序”按钮。从您的文件系统中选择您想要的 Windows 应用程序，然后选择您希望其运行的 Windows 版本。

- **更改注册表项** — 当您需要更改 Windows 注册表项时，WINE 提供三个可供操作的文件：`system.reg`、`user.reg` 和 `userdef.reg`。所有这些文件都在用户的 `$HOME/.wine` 目录中。您可以使用 `wineregfix` 创建实用工具来更新您的注册表，但通常您不再需要这样做，因为这应该会自动发生。

- **配置端口** — 与 Windows 驱动器号一样，您可以将串行端口和并行端口的链接添加到您的 `$HOME/.wine/dosdevices` 目录中。例如，要为您的第一个并行端口 (`LPT1`) 和串行端口 (`COM1`) 添加条目，您可以从您的 `$HOME/.wine/dosdevices` 目录运行以下命令：

```
$ ln -s /dev/lp0 lpt1
$ ln -s /dev/ttyS0 com1
```

- **添加 DLL** — WINE 提供了功能性 Windows 系统所需的许多基本库（DLL 文件）。然而，您的应用程序可能需要的一些 DLL 可能未包含在内，或者包含的一些 DLL 可能无法为您的应用程序正常工作。使用 Windows 配置窗口（库标签页），您可以替换 WINE 提供的 DLL，或者添加您从安装的应用程序中获取的其他 DLL。

- **图形设置** — 您可以从 Windows 配置窗口上的“图形”标签页更改与您的图形显示相关的设置。特别是，您可以更改您的 Windows 应用程序在您的 Linux 桌面上被管理的紧密程度。

- **添加字体** — 要为您的 WINE 安装添加字体，请将 TrueType 字体（`.ttf` 文件）复制到您的 WINE 虚拟驱动器上的 `c:/windows/fonts` 目录中。

有关配置 WINE 以在 Linux 中运行 Windows 应用程序的更多信息，请参阅 Wine 用户指南（`http://www.winehq.org/docs/en/wineusr-guide.html`）。

### 查找更多用于 WINE 的 Windows 应用程序
有关已在 WINE 中测试运行的 Windows 应用程序的信息，请参阅 Wine 应用程序数据库（`http://appdb.winehq.org`）。CodeWeavers 也维护自己的应用程序数据库，其中包含已在 WINE 下测试运行的应用程序。有关运行 Windows 应用程序的信息，请参阅 CodeWeavers 兼容性中心（`http://www.codeweavers.com/compatibility`）。在那里，您可以查看 CodeWeavers 自己的包含超过 3,300 个 Windows 应用程序的应用程序数据库。

另一个关于 WINE 应用程序信息的网站是 Frank's Corner (`http://www.frankscorner.org`)。该网站提供了大量关于让图形、互联网、多媒体、办公、游戏和其他应用程序在 WINE 中运行的良好技巧。

> **注意：** 第 25 章涵盖了 Linux 中的虚拟化。使用虚拟化，您可以在您的 Linux 系统上运行托管的 Windows、Linux、UNIX 或其他操作系统。

### 总结
在直接为 Linux 和其他 UNIX 系统编写的应用程序、已移植到 Linux 的应用程序以及可以在模拟中运行的应用程序之间，有数千种应用程序可供 Fedora 系统使用。随着 Fedora 存储库的发展，可在 Fedora 上运行的高质量软件包数量正在迅速增长。

为了简化和安装 Linux 应用程序的过程，Red Hat 开发了 RPM 包管理（RPM）格式。使用为 RPM 开发的工具，例如 `rpm` 命令，您可以轻松地安装、删除 Linux RPM 包并对其进行查询。用于查找、下载和安装 RPM 包的工具有 `yum` 实用程序和 `PackageKit` 窗口。

在可以在 Linux 中运行的应用程序类型中，为 X 窗口系统创建的应用程序在 Linux 中使用时提供了最高程度的兼容性和灵活性。然而，使用模拟软件，可以运行旨在用于 DOS、Microsoft Windows `95/98/2000/NT/XP/Vista/7` 和 Macintosh 操作系统的应用程序。此外，如第 25 章所述，Xen 和 KVM 等虚拟化软件允许多个操作系统作为来宾在 Fedora 上运行。反过来，这提供了在 Fedora 上的那些系统中运行各种应用程序的手段。

# 第 6 章 使用 Fedora 进行出版

**本章内容**

- Linux 下的桌面出版
- 试用图形化文本编辑器
- 使用 OpenOffice.org
- 使用 Ghostscript 和 Acrobat 显示文档
- 使用 Groff 和 LaTeX 创建文档
- 创建 DocBook 文档
- 使用 Scribus 进行页面排版
- 处理图形
- 捕获屏幕图像
- 使用 Inkscape 制作矢量图形
- 使用由 SANE 驱动的扫描仪
- 在 Web 上进行发布

作为一个桌面系统想要生存下来，操作系统必须至少能很好地完成一项任务：生成文档。在 Windows 之后，微软的 Word（捆绑在 Microsoft Office 中）成为微软在桌面市场成功的基础，这绝非偶然。Fedora 包含了用于生成文档、处理图像、扫描和打印的工具。几乎你可以期望一个出版系统所做的任何事情，你都可以使用 Fedora 来完成。

本章介绍了流行的 Linux 办公套件（如 OpenOffice.org 和 KOffice），用于创建文档、演示文稿和电子表格。在页面排版方面，Scribus 是一个出色的应用程序，可用于创建宣传册和小册子。在处理图像方面，我们将介绍 GNU 图像操作程序（GIMP）。在处理矢量图形方面，我们将描述 Inkscape 矢量图形编辑器。

为了显示你创建的内容，有几种不同的查看器可用于显示 PDF 和 PostScript 格式的输出。对于 PDF，有 Evince 查看器和 Adobe Reader。要显示 PostScript 文件，可以使用 Ghostview。

如果你想在网上发布内容，有各种工具，从编写基本的 HTML 文档到创建网络照片网站，再到实现完整的内容管理系统都有。打包用于 Linux 以管理你自己网站软件包括 MediaWiki（维基）、WordPress（博客）、Drupal（内容管理）和 Gallery（照片网站）等。

### Linux 下的桌面出版
