
|  |  | `convert` |
|  |  | `gimp` |
|  |  | `xv` |
| `.tiff24` | Tagged file Format (24-bit) | `convert` |
|  |  | `xv` |
| `.tim` | PSX TIM | `convert` |
| `.ttf` | TrueType font file | `convert` |
| `.txt` | text file bitmap | `pbmtext` |
|  |  | `convert` (read-only) |
| `.uil` | Motif UIL icon | `ppmtoiuil` |
|  |  | `convert` |
| `.upc` | Universal Product Code | `pbmupc` |
| `.uyvy` | 16-bit YUV format | `convert` |
| `.vicar` |  | `convert` (read-only) |
|  |  | `xv` |
| `.viff` | Khoros Visualization image | `convert` |
| `.x10bm` | X10 bitmap | `pbmtox10bm` |
| `.xbm` | X11 bitmap | `pbmtoxbm` |
|  |  | `xbm topbm` |
|  |  | `convert` |
|  |  | `xv` |
| `.xim` | Xim file | `ximtoppm` |
| `.xpm` | X11 pixmap | `ppmtoxpm` |
|  |  | `xpmtoppm` |
|  |  | `convert` |
|  |  | `gimp` |
|  |  | `xv` |
| `.xv` | xv thumbnail | `xvminitoppm` |
| `.xvpic` | xv thumbnail file | `xvpictoppm` |
| `.xwd` | X11 Window Dump | `ppmtoxwd` |
|  |  | `xwdtopnm` |
|  |  | `convert` |
|  |  | `gimp` |
|  |  | `xv` |
| `.ybm` | Bennet Yee face file | `pbmtoybm` |
|  |  | `ybmtopbm` |
| `.yuv` | Abekas YUV file | `ppmtoyuv` |
|  |  | `yuvtoppm` |
|  |  | `convert` |
| `.zeiss` | Zeiss confocal file | `zeisstoppm` |
| `.zinc` | Zinc bitmap | `pbmtozinc` |

## 转换和查看图形

系统上安装的程序有多种方式可以将图形文件转换为不同格式。本小时讨论的若干绘画或绘图程序可以转换图形，并且表 16.1 中的许多程序也可以作为管道命令中的过滤器（详见第 6 小时，“使用 Shell”，具体细节）来转换图形。

你可以使用这些命令的不同组合来转换文件。OpenLinux 用户，例如图形艺术家或系统管理员，出于不同的原因转换文件。艺术家或普通用户可能希望导入或导出图形以供不同的绘图程序使用。系统管理员可能会寻找转换图形以节省磁盘空间的附带好处。在某些情况下，节省的空间相当可观。请看以下示例：

```
# xwd >graphic.xwd
# xwdtopnm <graphic.xwd | convert - graphic.jpg
xwdtopnm: writing PPM file
# ls -l graphic.*
-rw-r--r-- 1 bball users 11003 Jan 27 14:21 graphic.jpg
-rw-r--r-- 1 bball users 851523 Jan 27 14:17 graphic.xwd
```

第一条命令使用 `xwd` 客户端在你选择一个窗口并按下鼠标左键后创建 X11 窗口转储图形文件（`.xwd`）。窗口转储文件使用 `xwdtopnm` 命令转换为 `.pnm` 格式，并且输出流被送入 `convert` 命令以创建 `.jpg` 图形文件。`convert` 命令后面的连字符（`-`）指定应使用标准输入代替输入文件名。正如你所见，`.jpg` 图形文件比 X11 窗口转储图形文件小 77 倍以上！

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_388_0.png)

> 文件压缩的结果和效益因图形文件大小和压缩设置而异。详见 `convert` 手册页。

还有许多未列在表 16.1 中的图形程序可用于修改图形图像。例如，`pnrotate`、`pnmsmooth` 和 `pnmscale` 命令可旋转、平滑和调整图形图像大小。你可以使用多种此类程序不仅转换图形，还更改其外观或方向。

如果你使用管道转换图形，也可以通过应用这些过滤器程序在飞行中更改图像。例如，如果你有一个 `.xpm` 格式的图形文件，但想快速将其上下翻转并保存为 `.gif` 格式，请应用诸如 `pnmtflip` 命令之类的过滤器程序：

```
# xpmtoppm penguin.xpm | pnmtflip -topbottom | convert - penguin.gif
```

这里，文件 `penguin.xpm` 从 `.xpm` 格式转换为 `.ppm` 格式。`xpmtoppm` 命令的输出被送入 `pnmtflip` 命令，该命令使用 `-topbottom` 选项将图形文件上下翻转。`pnmtflip` 命令的输出被送入 `convert` 命令，该命令读取标准输入并将图形流保存为 `.gif` 格式。

不同过滤器的组合可实现不同的效果。有关其他效果，请参阅诸如 `pnmcrop`、`pnminvert`、`pnmrotate`、`pnmscale`、`pnmsmooth` 或 `pnmtile` 等命令。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_389_0.png)

> 并非所有随 Linux 发行版提供的图形转换程序都读取标准输入并写入标准输出。在命令行上使用管道进行实验之前，请先阅读任何所需转换程序的手册页。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_389_1.png)

> 在丢弃原始文件之前，请预览或打印转换结果，以确保你获得想要的效果，并且生成的图形文件不会出现图像质量损失。

如果你尝试复杂的管道，请使用 `convert` 命令，即 ImageMagick 软件包中的七个程序之一（稍后在“使用 ImageMagick 进行图形编辑”部分讨论），以便更轻松地进行文件转换。此命令位于 `/usr/bin` 目录下，可转换超过 75 种不同的图形文件格式（甚至包括一些未列在表 16.1 中的格式）。

`convert` 程序通常通过识别命令行上的不同文件扩展名来工作，如以下示例所示：

```
# xwd >graphic.xwd
# convert graphic.xwd graphic.tiff
```

这里，`xwd` 客户端用于创建 X11 窗口转储图形文件。`convert` 命令随后通过在命令行上第二个或输出文件上指定 `.tiff` 扩展名来创建 `.tiff` 文件。有关使用 `convert` 命令的详细信息，请参阅 ImageMagick 和 `convert` 命令手册页。

## 使用 GIMP 进行图形编辑

您可以在命令行更改或操作图形，但如果使用 X11，使用图像处理程序交互式地处理文件会更有趣。Linux 上最好的最新图形工具之一是 Spencer Kimball 和 Peter Mattis 开发的 GNU 图像处理程序，即 GIMP。

这个功能强大且复杂的程序，如图 16.1 所示，具有许多功能。如果您在其他操作系统上使用过商业软件图像编辑程序（如 Adobe Photoshop），您会欣赏 GIMP 的工具和滤镜。GIMP 具有以下功能：

- 9 个程序操作菜单
- 21 种不同的编辑工具
- 81 个画笔
- 168 个图案
- 123 种不同的插件滤镜和工具，用于创建图像效果或执行操作
- 导入和导出 24 种不同的图形格式
- 多个图像窗口，便于剪切粘贴或对文件进行多视图显示
- 每个图像都有多层，以便叠加效果
- 多级撤销，便于在出错时恢复
- 六个浮动窗口和对话框，用于选择工具、画笔、颜色或图案

新术语 您需要近 23 兆字节的硬盘空间来安装 GIMP 及其软件库、支持文件和相关目录。主要的 GIMP 文件安装在 `/usr/X11R6/share/gimp` 和 `/usr/X11R6/lib/gimp/X.X` 目录下，其中 `X.X` 是当前版本（本文撰写时为 1.0）。库目录包含 GIMP 的插件，它们是由 GIMP 从不同菜单运行的编译模块，可创建效果或更改图像或图像选择。

该程序有 11 种不同的命令行选项（例如 `-help` 显示选项列表），但不支持 X11 Toolkit 选项，例如几何设置。当您在命令行指定图形文件时，GIMP 会尝试根据文件的扩展名加载和解释文件。启动 GIMP 很简单；只需输入以下内容：

```
# gimp &
```
