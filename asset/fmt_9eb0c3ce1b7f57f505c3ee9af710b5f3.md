
| Sony | DSC-F1, DSC-F55, DSC-F07, DSC-P30, DSC-P31, DSC-P32, DSC-P5, DSC-P50, DSC-P72, DSC-P92, DSC-S75, DSC-S85, DSC-U20, DSC-V1, Memory Stick, MSAC-SR1, 和 DCR-PC100 |
| Toshiba | PDR-M1 |

## 下载数字照片

新相机更新频繁，因此如果您没有看到您的相机，请检查该页面。以下步骤描述了如何从您的数码相机下载图像：

1. 使用数码相机附带的数据线，将相机连接到计算机的 `USB` 或 `COM` 端口（我发现 `USB` 端口效果更好）。
2. 将您的相机设置为“发送和接收”（`Send and Receive`）模式。
3. 从桌面的主菜单中，显示数码相机窗口。
4. 选择“添加相机”（`Add Camera`）。出现“选择相机”窗口。
5. 点击型号（`Model`）框旁的向下箭头，选择您的相机，并点击“检测”（`Detect`）。
6. 点击“应用”（`Apply`），然后点击“确定”（`OK`）。您的相机应该出现在列表中。
7. 要开始从相机下载图像，点击左侧的相机名称，选择包含图像的文件夹。
8. 选择您感兴趣的图像，并点击“保存”（`Save`）按钮。保存照片窗口允许您选择存储位置。您可以重命名图像或使用相机分配。
9. 选择要删除的图像，点击“删除”（`Delete`）。

## 将相机作为存储设备

某些数码相机可以让看起来像存储设备。通过将数码相机挂载为 `USB` 存储设备，您可以查看、复制、删除和移动相机照片。表 20-4 列出了可以作为 `USB` 存储设备使用的数码相机。

| 品牌 | 支持型号 |
| --- | --- |
| Casio | QV-2400UX, QVv0, QV-3x00, QV-4000, 和 QV-8000 |
| Fuji | FinePix 1300, 1400Zoom, 2300Zoom, 2400Zoom, 2800Zoom, 4200Z, 4500, 4700 Zoom, 4900 Zoom, 6800 Zoom, A101, A201, 和 S1 Pro |
| HP | PhotoSmart 315, 318, 和 C912 |
| Konica | KD200Z, KD400Z, 和 Revio KD303 |
| Kyocera | Finecam s3 |
| Leica | Digilux F |
| Minolta | Dimage 5, Dimage 7, 和 Dimage X |
| Nikon | CoolPix 2500, 885, 5000, 775, 和 995 |
| Olympus | Brio Zoom D-15, C-100, C-200Z, C-220Z, C-27, C-3020Z, C-3042Z, C-4040Zoom, C-700, C-700UZ, C-860L, D-510, D-520Z, E-10, 和 E-20 |
| Pentax | El2000, Optio 330, 和 Optio 430 |
| Sony | DSC-F505, DSC-F505V, DSC-F707, DSC-P51, DSC-P20, DSC-P55, DSC-P71, DSC-S30, DSC-S70, DSC-S75, DSC-S85, MVC-CD300, 和 MVC-FD92 |
| Vivitar | Vivicam 3550 |
| Yashica | Finecam s3 |

## 第四部分 ♦ 运行应用程序

本章检查了 Linux 下基于文本和 GUI 的文档准备软件，并讨论了用于打印和显示文档的工具以及处理图像的软件。

### 使用 OpenOffice.org

有些人认为 `OpenOffice.org` 是微软在桌面市场主导地位的重大威胁。如果你因为需要处理 Microsoft Word 格式的文档而一直没有使用 Linux 作为你的桌面电脑，那么 `OpenOffice.org` 是消除这一障碍的一大步。你可以使用如 `WINE` 这样的程序（其他事情）让你在 Linux PC 上直接运行旧版本的 Microsoft Office，但对于大多数用户来说，没有理由去这样做。在本节中，我们将对所使用的元素进行高层概述，并提供一些细节。

许多 Linux 发行版都包含了整个 `OpenOffice.org` 桌面应用程序套件。有些除了或代替 `OpenOffice.org` 还包含了 `StarOffice` 套件。如果两者都没有，你也可以从其官网 `www.openoffice.org` 下载并安装 `OpenOffice.org`。`StarOffice` 是商业软件，可以在 `www.sun.com` 。

`OpenOffice.org` 与 `StarOffice` 共享源代码，由以下生产力应用组成：

- `Writer` — 一个文字处理程序，可以处理 Microsoft Word、StarOffice 以及其他多种格式的文档。`Writer` 还具有全套功能，用于使用模板、处理字体、导航文档（包括图像和效果）以及生成目录。
- `Calc` — 一个电子表格应用程序，允许你整合来自 Microsoft Excel、StarOffice、Base 以及其他几种电子表格格式的数据。`Calc` 中的某些功能可以允许你创建图表、设置数据库范围（以便于对电子表格区域的数据进行排序），并使用数据向导（`data pilot`）工具从不同的视角安排数据。
- `Draw` — 一个绘图应用程序，允许你创建、编辑和对齐对象；包括纹理和颜色；并处理对象层。它允许将图像、矢量图形、AutoCAD 以及各种其他文件格式整合到你的图中。然后，你可以以 OpenOffice.org 或 StarDraw 格式保存绘图。
- `Math` — 一个计算程序，允许你创建数学公式。
- `Impress` — 一个演示文应用程序，包含多种幻灯片效果。你可以使用 `Impress` 创建并保存 Microsoft PowerPoint、StarDraw 和 Starimress 格式的演示文。

### 第 21 章 处理文字与图像

与其他为了处理微软文档和数据格式而创建的应用不同，`OpenOffice`（尽管并不完美）在打开和保存这些文件时做得非常好，问题较少。在 `OpenOffice` 中打开的基础基础样式和格式通常看起来与在 Microsoft Office 中的显示没有明显区别。在其他情况下，例如项目符号、对齐和缩进，在 `Writer` 中的显示可能与 Word 中完全不同。某些 Word 功能（如宏和脚本功能）在 `Writer` 中可能完全无法工作。

要打开 `OpenOffice.org` 应用程序，请从系统菜单（例如 `K-Menu`）中选择相关项目（如 OpenOffice Writer 图标）。在许多发行版中，系统菜单上还有一个名为 Office（或非常类似的名称）的文件夹。图 21-1 显示了在 `OpenOffice` 中打开编辑的 Microsoft Word 文档。

![](img/a2d958d7eab32ca5b89b2b8af808aa70_578_0.png)

图 21-1：在 `OpenOffice.org` 中处理 Microsoft Word 文档。

`Writer` 中的控件与你在 Word 中找到的相似。工具栏包含更改样式、字体类型和大小的框。按钮允许你保存和打印文件；更改文本对齐；以及剪切、复制和粘贴文本。换句话说，`Writer` 包含了你在高级文字处理器中需要几乎的所有内容。此外，`Writer` 还包含一个方便的 `PDF` 按钮，可以直接将文件输出为 `PDF` 格式，这对于交换文档或在互联网上放置数据非常有用。

尽管本书无法涵盖所有的 `OpenOffice.org` 应用程序，但你可以直接从 `KNOPPIX` 或大多数其他提供 KDE 或 GNOME 桌面的 Linux 发行版中尝试它们。

## 其他文字处理器

如果你的发行版不包含 `OpenOffice.org` 套件，或者你只是想尝试其他的，你还有一些其他选择：

- `StarOffice` — `StarOffice` 生产力套件包含文字处理、电子表格、演示图形、电子邮件、新闻、图表和图形应用程序。它是为了在 Linux 系统上运行而创建，但在所有环境中运行。它可以导入和导出多种微软文件格式。`StarOffice` 属于 Sun Microsystems，该公司将其作为商业产品销售。
- `AbiWord` — `AbiWord` 文字处理器（`abiword` 命令）是非商业软件，是 AbiSource 项目（`www.abisource.com`）产生的第一个应用程序。除了处理其自身格式（`.abw` `.zabw`）的文件外，`AbiWord` 还可以导入 Microsoft Word 和其他格式的文件。
