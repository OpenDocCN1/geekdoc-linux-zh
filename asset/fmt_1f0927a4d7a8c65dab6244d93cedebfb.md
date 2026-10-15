
## 1. 启动 `libvirtd` 服务
如果它尚未运行，请启动 `libvirtd` 服务：

```
# service libvirtd start
```

## 2. 创建 KVM 客体
以 `root` 用户身份从终端窗口输入以下内容：

```
# /usr/sbin/virt-manager
```

虚拟机管理器窗口将会出现。

## 3. 创建新客体
右键点击 `localhost (qemu)` 并点击“新建”。当创建新虚拟系统的弹出窗口出现时，点击“下一步”。系统要求为你的虚拟机系统命名。

## 4. 虚拟机名称
输入一个代表此虚拟机的名称并点击“下一步”。保持名称简单（单个单词、较短且不含特殊字符），因为该名称将用于文件名和菜单中表示虚拟机。系统询问虚拟化方法。

## 5. 虚拟化方法
选择“完全虚拟化”。你也可以选择使用不同 CPU 架构（`i686`, `X86_64`, `ppc`, `sparc`, `mips` 或 `miscel`）创建客体。系统要求识别安装介质的位置。

## 6. 安装方法
选择 ISO 镜像类型（你可以浏览）或插入了安装介质的 CD 或 DVD 驱动器（例如 Fedora 安装 DVD）。还要识别正在安装的操作系统系统的通用（Linux, UNIX, Windows 或其他）和变体（例如 Fedora, Windows Vista, Sun Solaris）。系统要求分配存储空间。

## 7. 分配存储空间
你可以通过识别文件名和大小来识别或创建虚拟磁盘。无论哪种情况，存储区域都必须大到容纳你安装的客体操作系统。系统要求你设置网络连接。

## 8. 主机网络
识别虚拟网络或共享物理网络设备，为你的客体操作系统提供网络连接。分配内存和 CPU。

## 9. 分配内存
从屏幕显示的总内存中，选择虚拟机内存的数量作为最大值。建议至少为 `256MB`。还要选择虚拟 CPU 的数量（通常不少于主机系统上的逻辑 CPU）。系统要求你检查你的安装信息。

## 10. 开始安装
如果所有信息正确，点击“完成”开始安装过程。

至此，你将像往常为所选操作系统那样运行安装过程。一旦安装完成，你就可以从“虚拟机管理器”启动和关闭新的虚拟环境。

### 总结

在直接为 Linux 和其他 UNIX 系统编写的应用程序、移植到 Linux 的应用程序以及可以在仿真中运行的应用程序之间，有数千个应用程序可供 Fedora 和 RHEL 系统使用。随着 Fedora Core 与 Fedora Extras 以及其他在线软件仓库的合并，可在 Linux 和 RHEL 系统上运行的高质量软件包数量呈指数级增长。

为了简化安装和管理 Linux 应用程序的过程，红帽开发了 RPM 包管理（RPM）格式。使用为 RPM 开发的工具（如 `rpm` 命令），你可以轻松地安装、删除和查询 Linux RPM 包。查找、下载和安装 RPM 包的工具包括 `yum` 实用和 `PackageKit` 窗口。

在 Linux 中运行的应用程序类型中，为 X Window 系统创建的应用程序在 Linux 中使用时具有最高的兼容性和灵活性。然而，通过仿真软件，可以运行为 DOS、Microsoft Windows 95/98/2000/NT/XP/Vista 以及 Macintosh 操作系统设计的应用程序。从长远来看，像 Xen 和 KVM 等虚拟化软件将允许多个操作系统作为客体运行在 Fedora 上。这反过来又为 Fedora 中的这些系统中运行各种应用程序提供了手段。

# 第 6 章 在 Fedora 和 RHEL 上发布

**本章内容**

- 使用 OpenOffice
- 使用商业版
- 创建文字处理器
- 创建文档
- 显示文档
- 图形处理
- 使用扫描仪
- 使用 OpenOffice

为了作为一个桌面系统生存，操作系统必须能够执行至少一项任务：发布文档。在本章中，我描述了用于 Fedora 和 RHEL 的文本和图形界面工具。

> 注意：如果你愿意支付少量费用，Codeavers 提供的 CrossOver 可以让你在桌面上安装并运行不同版本的 Microsoft Office（1997, 2000, XP 和 2003）。更多信息请访问 `codeavers.com/products/cxoffice`

Fedora 和 RHEL 包含了整个 OpenOffice 套件。最新的 OpenOffice 版本（2.4）包含在此发行版中。基于 StarOffice 源码，OpenOffice 包含以下办公应用程序：

- `OpenOffice.writer` — 文字处理应用程序，可以处理来自 Microsoft Word、StarOffice 等的文档。它具有全功能用于使用模板、字体、文档导航、图像和效果以及生成目录。
- `OpenOffice.Calc` — 电子表格应用程序，允许整合来自 Microsoft Excel、StarOffice、Dbase 以及其他表格格式的数据。Calc 的一些实用功能允许你创建图表、设置数据库范围（对排序表格区域），并使用数据工具从不同视图排列数据。
- `OpenOffice.Draw` — 制图应用程序，允许你创建、编辑和对齐对象；它整合纹理；包含颜色并处理对象层。它允许将图像、矢量图形、AutoCAD 以及其他文件格式整合到绘图中。然后，你可以将图形保存为 OpenOffice Drawing 或 StarOffice Draw。
- `OpenOffice.Math` — 计算程序，允许你创建数学公式。
- `OpenOffice.Impress` — 演示应用程序，包含各种幻灯效果。使用 Impress，你可以创建并保存 Microsoft PowerPoint、Draw 和 Impress 格式的演示文稿。
- `OpenOffice.Base` — 低端数据库，类似于 Microsoft Access 数据库。Base 也可以作为其他数据库的前端。

与其他专门为微软文档和数据格式创建的应用程序不同，OpenOffice（尽管完美）在打开和保存许多不同版本的 Microsoft Word（`.doc`）和 Excel（`.xls`）格式方面表现非常好，问题较少。在 OpenOffice.org 中打开的基础样式和格式与其在 Microsoft Office 中的外观通常没有明显不同。事实上，一些旧的

## 第 6 章：在 Fedora 和 RHEL 上发布

在 OpenOffice.org Writer 中编写文档实际上比在最新的 OpenOffice 套书中更好。

注意：Open Office XML（`OOXML`）格式是一部达 6000 页的巨著，代表了微软近期声支持标准文档格式的努力。该格式是 Word 2007 的默认文档类型。然而，开源社区的某些人认为，OOXML 特别要求支持微软产品功能，而没有提供有关如何实现微软专有功能的指导，因此作为一种标准是不可用的。换句话说，不要认为微软声称支持标准，就意味着你能够在其他平台上完全使用微软的文档格式。

要打开 OpenOffice.org Writer、Impress、Calc 以及其他办公应用程序，请点击“应用程序”菜单中的“Office”。然后，选择你想要打开的 OpenOffice.org 应用程序。图 6-1 显示了原始在 Microsoft Word 中创建的文件的 OpenOffice.org Writer 示例。

![](img/6a8f767dda2519b458f97c2e7f586576_292_0.png)

图 6-1：在 OpenOffice.org Writer 中处理 Word 文档。

OpenOffice.org 中的控件与你在 Word 2007 之前找到的控件相似。如果你对那些控件很熟悉，你应该发现很容易过渡到 OpenOffice.org Writer。事实上，你可能会发现它比使用 Microsoft Word 2007 更容易，因为许多人发现过渡到 Word 2007 是困难的。

OpenOffice.org Writer 中的工具栏包含识别文件名以及更改样式、字体类型和字体大小的框。按钮允许你保存和打印文件、更改文本对齐，以及剪切、复制和粘贴文本。换句话说，Writer 包含了几乎你在高级文字处理处理器中预期的所有功能。此外，Writer 还包含一个方便的 PDF 按钮，可以直接将文件输出为 PDF 格式。这对于交换文档或在互联网上发布数据非常有用。

如果你刚开始使用 OpenOffice Writer，这里有一些你可以尝试的特性：

- **向导（Wizards）** — 使用向导编写信函、传真、议程、演示文稿、网页、文档转换器或欧元转换器。选择 `文件 -> 向导`，然后选择上述类型之一。文档转换器向导允许将 Microsoft 或 StarOffice 文档目录转换为 OpenDocument 格式。欧元转换器允许你将包含不同货币的文件转换为欧元。
- **文档样式和格式（Document styles and formatting）** — 使用字符、段落、帧、页面和编号样式窗口创建你的文档格式（选择 `格式 -> 样式和格式`），选择你想要更改的样式类型，在样式框中点击鼠标右键，并选择创建你自己的样式。
