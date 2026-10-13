
理解如何设置和运行 Microsoft Windows 应用程序的最佳方法是体验在 WINE 中运行一个简单的 Microsoft Windows 辅助程序的过程。要执行此步骤，你需要以下内容：

- 在你的 Fedora Core 或 RHEL 系统中安装了 `wine` 包。
- 访问 Microsoft Windows 组件，包括你想运行的可执行程序和运行它所需的 DLL 文件。

如果你有双启动系统（Fedora Core 和 Microsoft Windows），执行此操作的最佳方法是拥有 Windows 分区。为了本过程，我们假设你有一个从 `/mnt/win` 访问的 Windows 系统。如果不是这种情况，你需要找到从另一台计算机上的 Windows 系统拷贝文件的方法。

### 步骤

1. 使分区永久可用，请在 `/etc/fstab` 中添加以下行：

```
/dev/hda1 /mnt/win vfat 0 0
```

上述项目会在每次 Fedora Core 启动时自动挂载该分区到 `/mnt/win`。

2. 将 `mpaint.exe` 程序拷贝到 Linux 可访问的位置。例如，对于描述的 Windows 分区，你可以输入：

```
# cp /mnt/win/Program Files/Accessories/mspaint.exe /bin/
```

3. 以 `mspaint.exe` 作为参数运行 `wine` 命令，查看它可以运行或需要某些 DLL 文件。

```
# wine /bin/mspaint.exe
err: module:PE_fixup_imports Module (file) MFC42.DLL (which is needed by Z:\a\mspaint.exe) not found
```

这意味着你需要 `mfc42.dll` 文件来运行 `mspaint.exe`。

4. 接下来，从 Windows 分区拷贝所需的 DLL 文件。例如：

```
# cp /mnt/win/windows/system/mfc42.dll /usr/share/wine-c/system/
```

5. 安装正确的 DLL 后，再次输入 `wine /bin/mspaint.exe`，Microsoft 画画窗口就会打开。图 5-4 显示了在 Fedora Core 中运行的窗口示例。

在图 5-4 中，Paint 显示了一张从 Fedora Core 文件系统打开的位图。选择文件 → 打开。在打开对话框中，你可以看到应用程序查看其可用位置的方式。`C:`; `D:`; `E:`; `F:`; 和 `Z` 代表表 5-5 所示的位置。（示例中的计算机没有软盘，否则你还会看到 `A:` 驱动器。）

![](img/8aa80810fdd3df400bb7ee72b296baad_252_0.png)

## 第二部分：使用 Fedora 和 RHEL

![](img/8aa80810fdd3df400bb7ee72b296baad_253_0.png)

图 5-4：在 Red Hat Linux 中通过 WINE 运行画。

## 为 WINE 使用 Microsoft Windows 应用程序

经过测试可以在 WINE 下运行的应用程序维护在 Wine 数据库（http://appdb.codewavers.com）中。该数据库分为以下几类：

- 教育软件与计算机化培训
- 游戏
- 多媒体
- 网络与通信
- 办公生产力工具
- 编程 / 软件工程
- 参考、文档与信息
- 科学、技术与数学
- 特殊用途
- 工具程序

数百个应用程序已提交到该数据库。测试过的软件包大多数是游戏。在大多数情况下，列出应用程序的人会描述他或她测试的内容，以及在运行该程序时遇到的任何经验。列表的托管网站 `codewavers.com` 要求您创建登录以访问数据库。

另一个关于 WINE 应用程序信息的网站是 Frank's Corner (`www.frankcorner.org`)。该网站提供了许多关于如何在 WINE 中运行图形、多媒体、办公、游戏和其他应用程序的实用技巧。

## 第 5 章：访问与运行应用程序 231

## 使用 ARDI Executor 运行 Macintosh 应用程序

除了让 PC 运行许多旧版 Macintosh 应用程序之外，来自 ARDI, Inc. 的 ARDI Executor (`www.ardi.com`) 还允许您使用 Mac 格式软磁盘和各种 Mac 驱动器。可以通过 `www.ardi.com/executor.php` 获取更多关于 ARDI Executor 的信息。

ARDI 还在其兼容性数据库中维护了一个兼容 Mac 软件列表。列出了数百个 Mac 应用程序。每个应用程序都用代码（绿色、黄色、橙色、红色或黑色）标记该软件在 ARDI 下的运行情况。绿色和黄色分别代表可用和基本可用。橙色表示大部分不可用。红色表示应用程序完全无法运行，黑色表示它无法运行，因为需要 ARDI 中未实现的功能。一眼看上去，列出的应用程序约三分之二是绿色或黄色。

> 参考：由于 Mac OS X 基于类 Linux 操作系统，Linux 和 Mac 将拥有更多跨平台的应用程序。第 26 章将详细讨论 Mac OS X 与 Linux 系统的互操作。

### 总结

在直接为 Linux 和其他 UNIX 系统编写的应用程序、移植到 Linux 的应用程序以及可以在仿真环境中运行的应用程序之间，有数百个应用程序供 Fedora Core 和 RHEL 系统使用。互联网上有几十个地方可以下载 Linux 应用程序，还有更多可以通过 CD 购买的。

为了简化安装和管理 Linux 应用程序的过程，红帽开发了 RPM 包管理器（RPM）。使用为 RPM 开发的工具（如 `rpm` 命令），你可以轻松地安装、删除和查询 Linux RPM 包。

在 Linux 可运行的应用程序类型中，为 X Window 系统创建的应用程序在 Linux 中使用时具有最高的兼容性和灵活性。然而，通过仿真软件，可以运行为 DOS、Microsoft Windows 95/98/2000/NT/XP 以及 Macintosh 操作系统设计的应用程序。

# 第 6 章

## 使用 Fedora 和 RHEL 进行发布

本章内容：

- 使用 OpenOffice.org
- 使用商业文字处理器
- 使用 Groff 和 LaTeX 创建文档
- 创建 DocBook 文档
- 使用 Linux 打印文档
- 使用 ghostscript 和 Acrobat 显示文档
- 处理图形
- 使用 SANE 驱动的扫描仪

要作为一个桌面系统生存下去，操作系统必须能够很好地完成至少一项任务：生成文档。并非偶然，在 Windows 之后，Microsoft Word（通常包含在 Microsoft Office 中）是微软桌面端成功的基础。Fedora 和 RHEL 包含了生成文档、处理图像、扫描和打印的工具。你期望一个发布系统能做的几乎所有事情，都可以通过 Fedora 和 RHEL 实现。

OpenOffice.org 是一个强大的开源套件，作为 Fedora 和 RHEL 发行版的一部分提供。OpenOffice.org 包含文字处理器、电子表格、演示文稿管理器和其他个人生产力工具。在许多情况下，OpenOffice.org 可以作为 Microsoft Office 的无缝替代。

Linux 第一批文档和图形工具大多是基于旧的文本文本工具构建的。最近，增加了更复杂的用于写作、页面格式化和集成图形的工具。尽管年代久远，许多旧的出版工具（如 Groff 和 LaTeX）仍然被技术社区的人们使用。

在本章中，我描述了用于 Fedora 和 RHEL 的基于文本和基于 GUI 的文档准备软件。我还描述了用于打印和显示文档的工具，以及处理图像的软件。

## 使用 OpenOffice

有些人认为 OpenOffice.org 是微软在桌面市场主导地位的重大威胁。如果需要处理 Microsoft Word 格式文档的需求阻碍了你将 Linux 作为你的桌面电脑，那么 OpenOffice.org 是消除这一障碍的一大步。

> 注意：如果你愿意花几美元，来自 Codewea.com 的 CrossOffice 让你从 Linux 桌面安装并运行不同版本的 Microsoft Office（97, 2000, XP 等）。更多信息请参阅第 5 章，或检查 `www.codeweavers.com/products/cxoffice`。

Fedora 和 RHEL 包含了整个 OpenOffice.org 套件。基于 StarOffice，OpenOffice.org 由由以下应用程序组成：

- `Writer`：文字处理应用程序，可以处理 Microsoft Word、StarOffice 等其他格式的文档。`Writer` 包含了高级文字处理器预期的几乎功能。此外，`Writer` 有一个方便的 PDF 按钮可以直接将文件输出为 PDF 格式。
