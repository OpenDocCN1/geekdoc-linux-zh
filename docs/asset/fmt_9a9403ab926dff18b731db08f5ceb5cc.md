
```text
# wine /bin/mspaint.exe
err: module:PE fixup imports Module (file) MFC42.DLL (which is needed by Z:\a\mspaint.exe) not found
```

这表明您需要 `mfc42.dll` 文件才能运行 `mspaint.exe`。

4. 接下来，从 Windows 分区复制必要的 DLL 文件。例如：

```text
# cd /usr/share/wine-c/windows/system
# cp /mnt/win/windows/system/mfc42.dll mfc42.dll
```

5. 安装好适当的 DLL 文件后，再次输入 `wine /bin/mspaint.exe`，MS Paint 窗口就会打开。图 5-3 显示了在 Red Hat Linux 中运行的 Paint 窗口示例。

![](img/27a85d56d393921ced6412ae6e8336bf_228_0.png)

在图 5-3 中，Paint 显示的是我从 Red Hat Linux 文件系统打开的位图图像。选择“文件”→“打开”。在“打开”对话框中，您可以看到应用程序如何查看其可用的位置。C:、D:、E:、F: 和 Z: 驱动器都代表表 5-5 中显示的位置。（示例中的计算机没有软驱，否则您还会看到 A:。）

## 寻找适用于 WINE 的 Windows 应用程序

经过测试可在 WINE 下运行的应用程序在 Wine 应用程序数据库 (`http://appdb.codeweavers.com`) 中维护。该数据库分为以下类别：

- 教育软件和计算机培训
- 游戏
- 多媒体
- 网络与通信
- 办公效率
- 编程/软件工程
- 参考、文档和信息
- 科学、技术和数学
- 特殊用途
- 实用工具

数百个应用程序已提交至该数据库。经过测试的软件包大多数是游戏。在大多数情况下，列出应用程序的人会描述其测试平台以及使其运行的任何经验。列表托管商 `codeweavers.com` 要求您创建登录帐户以访问数据库。

## 使用 ARDI Executor 运行 Macintosh 应用程序

除了让您在 PC 上运行许多流行的 Macintosh 应用程序外，来自 ARDI 公司的 ARDI Executor (`www.ardi.com`) 还允许您使用 Mac 格式的软盘和各种 Mac 驱动器。请访问 `www.ardi.com/executor.php` 了解有关 ARDI Executor 的更多信息。

ARDI 还在其兼容性数据库中维护一份兼容 Mac 软件的列表。上面列出了数百个 Mac 应用程序。每个应用程序都有颜色编码（绿、黄、橙、红或黑），以指示软件在 ARDI 下运行的效果。绿色和黄色分别表示完全可用和基本可用。橙色表示大多不可用。红色表示应用程序完全无法运行，黑色表示因为需要 ARDI 中未实现的功能而无法运行。粗略看来，所列应用程序中约有三分之二为绿色或黄色。

## 总结

在直接为 Linux 和其他 UNIX 系统编写的应用程序、移植到 Linux 的应用程序以及可在仿真环境中运行的应用程序之间，有数百个应用程序可供 Red Hat Linux 使用。互联网上有数十个下载 Linux 应用程序的位置，还有更多可以在光盘上购买。

为了简化安装和管理 Linux 应用程序的过程，Red Hat 开发了 Red Hat 软件包管理器 (`RPM`)。使用为 `RPM` 开发的工具（如 `rpm` 命令），您可以轻松地安装、删除和查询 Linux `RPM` 包。

在可在 Linux 中运行的应用程序类型中，为 X Window System 创建的应用程序在 Linux 中使用时提供了最大程度的兼容性和灵活性。然而，使用仿真软件，可以运行针对 DOS、Windows 95/98/2000/NT/XP 和 Macintosh 操作系统的应用程序。

### 第 6 章：使用 Red Hat Linux 进行出版

本章内容

- 使用 OpenOffice
- 使用商业文字处理器
- 使用 Groff 和 LaTeX 创建文档
- 创建 DocBook 文档
- 使用 Red Hat Linux 打印文档
- 使用 ghostscript 和 Acrobat 显示文档
- 处理图形
- 使用由 SANE 驱动的扫描仪

要作为桌面系统生存，操作系统必须至少能很好地执行一项任务：生成文档。Word（现捆绑在 Microsoft Office 中）之所以成为 Microsoft 在桌面上成功的基石，紧随 Windows 之后，绝非偶然。Red Hat Linux 包含用于生成文档、处理图像、扫描和打印的工具。您期望出版系统执行的几乎所有任务，都可以用 Red Hat Linux 完成。

OpenOffice 是一个功能强大的开源办公套件，首次作为 Red Hat Linux 发行版的一部分提供。基于 Sun Microsystems 的 Star Office，OpenOffice 包括文字处理器、电子表格、演示文稿管理器和其他个人效率工具。

Linux 的第一批文档和图形工具大多构建在较旧的基于文本的工具之上。最近，增加了更复杂的工具用于写作、排版和集成图形。尽管历史悠久，许多较旧的出版工具（如 Groff 和 LaTeX）仍被技术社区的人们使用。

在本章中，我将介绍适用于 Red Hat Linux 的基于文本和基于 GUI 的文档准备软件。我还将介绍用于打印和显示文档的工具，以及用于处理图像的软件。

## 使用 OpenOffice

有人称 OpenOffice 对微软在桌面市场的统治地位构成了重大威胁。如果处理 Microsoft Word 格式文档的需求曾阻止你将 Linux 用作桌面计算机，那么 OpenOffice 就是消除这一障碍的重要一步。

> **注意：** 如果你愿意支付几美元，来自 `Codeweavers.com` 的 `CrossOver Office` 让你能够从 Linux 桌面安装并运行较旧版本的 Microsoft Office（97、2000、XP 等）。请参阅第 5 章了解更多信息或访问 `www.codeweavers.com/products/office`。

Red Hat Linux 包含完整的 OpenOffice 桌面应用程序套件。基于 Sun Microsystems 的 StarOffice 源代码，OpenOffice 由以下办公生产力应用程序组成：

- **OpenOffice Writer** — 一种文字处理应用程序，可处理来自 Microsoft Word、StarOffice 以及其他多种的文件格式文档。Writer 还提供了一整套用于使用模板、处理字体、导航文档、插入图像和效果以及制作目录的功能。

- **OpenOffice Calc** — 一种电子表格应用程序，可将来自 Microsoft Excel、StarOffice、Dbase 以及其他多种电子表格格式的数据合并。Calc 中的一些不错功能让你可以创建图表、设置数据库范围（以便轻松对电子表格区域中的数据进行排序），并使用数据透视表从不同角度排列数据。

- **OpenOffice Draw** — 一种绘图应用程序，可让你添加、编辑和对齐对象；合并纹理；包含纹理和颜色；并处理对象的图层。它可将图像、矢量图形、AutoCAD 以及多种其他文件格式合并到你的绘图中。然后，你可以将绘图保存为 OpenOffice Drawing 或 StarDraw 格式。

- **OpenOffice Math** — 一种计算程序，可让你创建数学公式。

- **OpenOffice Impress** — 一种演示应用程序，包含多种幻灯片效果。使用 Impress，你可以创建并保存 Microsoft PowerPoint、StarDraw 和 StarImpress 格式的演示文稿。

与其他为处理 Microsoft 文档和数据格式而创建的应用程序不同，OpenOffice（虽然不完美）能够以更少的问题打开和保存这些文件。在 OpenOffice 中打开的基本样式和格式通常看起来与在 Microsoft Office 中显示时没有明显差异。

启动 Writer、Impress 和 Calc 的图标就在 Red Hat 桌面面板上（只需点击即可启动）。或者，要打开这些和其他 OpenOffice 应用程序，请点击主菜单中的 Office。然后选择要打开的 OpenOffice 应用程序。图 6-1 显示了 OpenOffice Writer 显示并处理最初由 Microsoft Word 创建的文档文件的示例。

![](img/27a85d56d393921ced6412ae6e8336bf_232_0.png)

**图 6-1：** 在 OpenOffice Writer 中处理 Microsoft Word 文档。
