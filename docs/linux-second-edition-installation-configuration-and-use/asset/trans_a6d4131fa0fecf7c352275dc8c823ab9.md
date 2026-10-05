
在此处，可以设置多种额外的选项（颜色/黑白、压缩因子）。因此，xv 是一个图像处理和转换的极其强大的工具。

-   xv 拥有一份 100 页的手册，在大多数发行版中以 PostScript 文件 (xvdocs.ps) 的形式提供。

## Electric Eyes (电子眼)

GNOME 程序 Electric Eyes 通过命令 `ee` 启动。控制可以通过上下文菜单（鼠标右键）或通过 `EDIT | SHOW EDIT WINDOW` 显示的对话框进行。在当前版本中，该程序易于使用（另参见 HTML 格式的帮助文本），但它仍然远未 xv 的替代品（如 RedHat 手册中所誉的）。

![](img/b30873dd3d753687a59253fb9ad26a0b_544_0.png)

图 15.8 用 Electric Eyes 显示的 Linux 标志。

## xpcd, hpctoppm (Photo CD)

读取 Photo CD 上图片最简单的方法是使用 xpcd 程序。此前，必须像常一样使用 `mount` 命令将 CD 挂载到文件系统中。然后，执行 `xpcd /cdrom` 显示 CD 的内容列表。随后，你可以查看各种分辨率的单张图片，并将其保存为 JPEG、PPM 或 TIFF 格式。要将多个文件自动转换为 PPM 格式，也可以使用 `hpctoppm` 命令。

## 518 工具与实用程序

![](img/b30873dd3d753687a59253fb9ad26a0b_545_0.png)

图 15.9 Photo CD 的内容。

## 其他图像处理和图形转换程序

如果你认为 xv 和 ee 的图像处理功能不够灵活，那么你应该看一看 gimp 程序。该程序在第 20 章从 659 页开始有详细描述。

另一方面，如果你面临的是奇特的图形格式，或者你想将一整组文件转换为另一种脚本形式（无需用户交互），还有其他替代方案：Image Magick 程序包同时提供了单命令和交互式界面。转换时，使用了一种专有的中间格式 (MIFF)。

NetPBM 软件包（以前称为 Portable Bitmap Utilities）也采用了类似的方法。在这里，PBM 格式被用作中间格式。例如，你需要将数百个 MS Windows 位图转换为 PostScript 格式，这些实用程序就是正确的选择。

## 15.4 显示文档和图形

### 显示 PostScript 文件 (ghostview, kghostview, gv)

原则上，ghostview 只是已经介绍过的 `gs` (GhostScript) 程序的图形用户界面。ghostview 可以同时处理多达数百页的 PostScript 图形和文档。如果文档符合 PostScript 标准，你可以在页码之间自由跳转。否则，文件只能按顺序读取（即一页一页地读取，而无法跳过页面或返回）。

取决于发行版的不同，ghostview 编译时使用了不同的部件库。这导致 ghostview 的按钮和滚动条看起来与图 15.10 所示的不同。然而，这种差异仅涉及视觉效果；程序的功能保持不变。

## 显示文档和图形 519

![](img/b30873dd3d753687a59253fb9ad26a0b_546_0.png)

图 15.10 来自 LaTeX2 用户指南的一页，用 ghostview 显示。

通常，调用 ghostview 时不带任何参数，或者带上要查看的文件名。该程序是完全由菜单驱动的。为了打开新文件，会显示一个窗口，允许用鼠标轻松选择。在图像区域的任意一点点击鼠标都会打开一个一个小窗口，其中包含鼠标指针周围区域的放大图。你可以通过鼠标中键点击数字来切换到另一个显示的页面。

作为鼠标控制的快速替代方案，提供了一些键盘快捷键，其中最重要的总结在下表中。

| PgUp, PgDn | 上一页 / 下一页 |
| :--- | :--- |
| Spacebar, ← | 下一页 |
| ↑ | 旋转视图 90 度 |
| Backspace, Del | 上一页 |
| +, - | 更改缩放因子 |
| O | 打开新文件 |
| Q | 退出程序 |
| R | 重新打开修改过的页面 |
| H, L | 图像区域向左/右移动 |
| U, D | 图像区域向上/下移动

ghostview 允许你从文档中提取单页或页面区域并将其存储在单独的文件中。为了这样做，在按住鼠标的同时移动鼠标标记所需的区域，然后执行 `SAVE | MARKED PAGES` 命令。

## 520 工具与实用程序

如果你非常看重高质量的呈现（并愿意付出更长的计算时间和更高的内存消耗作为回报），你应该激活抗锯齿功能。这意味着 PostScript 表示将先以更高的分辨率生成，然后降低为灰度级。要做到这一点，你可以在启动 ghostview 时选择选项 `-sDEVICE=x11alpha`，或者通过以下行扩展 `~/.XXdefaults`：

```prolog
! activate Ghostview antialiasing in ~/.XXdefaults
Ghostview*arguments: -sDEVICE=x11alpha
```

关于处理 ghostview 的详细信息，以及所有命令选项和键盘快捷键的摘要，可以在正文中找到。

## ghostview

KDE 版本的 ghostview 称为 ghostview，其实质上更更容易的操作令人印象深刻。（不过，老练 ghostview 用户会怀念他们常用的快捷键。）

## gv, ggv

gv 程序是另一个 ghostview 变体。该程序看起来比 ghostview 更现代，但不提供任何本质的附加功能。RedHat Linux 目前仅随带 gv。ghostview 仅仅是 gv 的链接。最后，它是 gv 的 GNOME 变。

## 查看 DVI 文件 (xdvi, kdvi)

原则上，xdvi 对 *.dvi 文件的操作与 ghostview 对 PostScript 文件的操作相同。xdvi 允许在屏幕上查看 *.dvi 文件并正反翻页。xdvi 使用 *.dvi 文件作为唯一参数启动。随后，可以使用 `NEXT`、`PREVIOUS` 等来翻阅文档。当你按住鼠标移动图像区域时，会显示鼠标指针下方矩形区域的放大。下表提供了控制 xdvi 的最重要的快捷键。

| xdvi 快捷键 | |
| :--- | :--- |
| PgUp/PgDn | 上一页/下一页 |
| Spacebar ← | 下一页 |
| Backspace, Del | 上一页 |
| ↑, ←, → | 移动图像区域 |
| G | 转到指定的页码 |
| V | 切换显示图形 |

## 显示文档和图形 521

![](img/b30873dd3d753687a59253fb9ad26a0b_548_0.png)

图 15.11 用 dvdi 和 kdvi 显示的用户指南的一页。

你可以自由选择 dvdi 或 ghostview 来处理 LaTeX 。这两个程序都有优势：在使用 LaTeX 源文件时，dvdi 通常显示得更快；在使用 PostScript 文件时，ghostview 提供了更好的图像质量。

在 LaTeX 发行版中，可以通过文件 `/usr/lib/texmf/xvdi/` 配置 xvdi。该文件有四个项目：`mfmode` 指定打印机，`pixelsInch` 指定 DPI 分辨率，`shrinkFactor` 指定缩小因子以及纸张。前两个设置应与 dvips 生成 PostScript 文件时使用的参数匹配。这样你就可以避免创建必要的位图字体文件，这在时间和磁盘空间上都是浪费。

分辨率和打印机必须匹配（参见 MakeTeXPK 或第 623 页）。xvdi 显示的页面太大。如果你在 300 dpi 的激光打印机上打印 *.dvdi 文件，以下设置是合理的：

```prolog
xvdi*mfmode: cx
dxvdi*pixelsInch: 300
dxvdi*shrinkFactor: 4
dxvdi*paper: a4
```

如果你想检查以 1270 dpi 进行像素排版的结果，可以使用以下设置：

```prolog
Dvi*mfmode: linoone
dxvdi*pixelsInch: 1270
dxvdi*shrinkFactor: 16
dxvdi*paper: a4
```
