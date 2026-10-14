

## 19.3 使用 GIMP 编辑图像

```
@sf(Debian): 'gimp'
@sf(Debian): 'gimp-manual'
@sf(WWW): http://www.gimp.org/
```

GIMP（GNU Image Manipulation Program，GNU 图像处理程序）是一款功能全面的图像编辑和处理程序，可让你以复杂的方式绘制、绘图、创建和编辑图像。使用 GIMP，你还可以转换图像文件、润饰和编辑照片图像，以及浏览图像集合。

GIMP 附带了数百种工具、滤镜、字体和其他好东西。以下是其功能的 partial 列表：

- 包含完整的绘画工具套件，包括画笔、铅笔、喷枪和克隆。
- 支持自定义画笔和图案。
- 包含完整的图像选择、变换和操作工具套件，包括渐变编辑器、颜色混合和特殊效果。
- 包含动画支持。
- 允许使用图层和通道。
- 允许大尺寸图像，其大小仅受可用磁盘空间限制。
- 提供高质量的抗锯齿。
- 提供完整的 Alpha 通道支持。
- 支持命令脚本。
- 允许多次撤销和重做，仅受可用磁盘空间限制。
- 允许同时打开多个图像。
- 支持所有流行的文件格式，包括 GIF、JPEG、PNG、XPM、TIFF、TGA、MPEG、PS、PDF、PCX 和 BMP。
- 允许轻松添加超过 100 个插件，用于新的文件格式和新的效果滤镜。

GIMP 在 X 下运行，可通过运行 gimp 或从窗口管理器的菜单中选择它来启动。启动后，GIMP 看起来像这样：

![](img/8bf3d083d04b4cc3d79bd39657ac711a_296_0.png)

> *注意：* 要学习 GIMP 的基础知识，请参阅 *GIMP 用户手册* 以及 Web 上 http://www.gimp.org/ 的其他文档和资源。你也可以在系统上安装手册；它包含在 Debian `gimp-manual` 包中。

[ < ] [ > ]   [ << ] [ Up ] [ >> ]   [Top] [Contents] [Index] [ ? ]

## 19.4 交互式图像编辑器和工具

Linux 可用的图像编辑软件应用程序种类繁多——制作和编辑图像的方式与可用于此目的的工具一样多。

下表列出了一些其他流行的制作和编辑图像的工具和应用程序——包括 CAD 工程软件——你可能想要探索。列表并不详尽。

| TOOL | DESCRIPTION |
|------|-------------|
| bitmap | 使用 bitmap 编辑器编辑位图文件，这些文件用于 X Window System 中的图标和瓷砖图案。{@sf{Debian}}: `xbase-clients` |
| drgeo | drgeo 是一个用于绘制交互式几何图形的程序。{@sf{Debian}}: `drgeo` {@sf{WWW}}: http://members.xoom.com/FeYiLai/dr_geo/doctor_geo.html |
| dia | 使用 dia 绘制简单的图表和示意图。它以自己的格式保存文件，但你可以将文件导出为 EPS（参见 PostScript 部分）；然而，如果你计划再次编辑图表文件，请确保保留 `.dia` 文件，因为截至本文撰写时，dia 无法导入 EPS 文件。{@sf{Debian}}: `dia` {@sf{WWW}}: http://www.lysator.liu.se/~alla/dia |

electric 使用 electric 设计电子电路的图像。{@sf{WWW}}: http://www.gnu.org/software/electric/electric.html

freedraft FREEdraft 是一款用于精确绘图和草图的 2-D 机械 CAD 工具。{@sf{WWW}}: http://www.freeengineer.org/Freedraft/

gnuplot gnuplot 是一款功能强大的非交互式函数绘图工具。给定一个数据文件和一个公式，gnuplot 可以制作图表和图形。{@sf{Debian}}: `gnuplot` {@sf{WWW}}: ftp://ftp.gnu.org/pub/gnu/gnuplot/

ivtools ivtools 软件套件包括 idraw，这是一款矢量图形编辑器。{@sf{Debian}}: `ivtools-bin` {@sf{WWW}}: http://www.vectaport.com/

kali 使用 kali 绘制图案和镶嵌，包括壁纸图案和无限或递归瓷砖，风格类似于 M.C. Escher。{@sf{Debian}}: `kali`

moonlight Moonlight Creator 是用于建模、照明和渲染 3-D 场景的 X 客户端。{@sf{Debian}}: `moonlight` {@sf{WWW}}: http://www.cybersociety.com/moonlight/

sced sced 是用于创建 3-D 场景的工具。{@sf{Debian}}: `sced` {@sf{WWW}}: http://www.cs.wisc.edu/~schenney/sced/sced.html

xfig 使用久负盛名的 xfig 应用程序绘制图形——复杂的图表、平面图、地图、流程图等。它以自己的格式保存文件（默认情况下扩展名为 `.fig`）；通常的做法是导出为 EPS。{@sf{Debian}}: `xfig` {@sf{WWW}}: http://xfig.org/

xmorph xmorph 是一个将两幅图像融合（有时称为“扭曲”）在一起的工具，从而制作出新图像。图像必须采用 TrueVision Targa 文件格式，且每个文件的大小、形状和像素数相同（另请参阅 Morphing Two Images Together）。{@sf{Debian}}: `xmorph` {@sf{WWW}}: http://www.colorado-research.com/~gourlay/software/

xpaint xpaint 是一款简单的“画图”工具，早于 GIMP，包含你对画图程序所期望的所有基本功能。如果你不需要 GIMP 的高级功能，请考虑改用体积更小的 xpaint。{@sf{Debian}}: `xpaint` {@sf{WWW}}: http://www.danbbs.dk/~torsten/xpaint/index.html

