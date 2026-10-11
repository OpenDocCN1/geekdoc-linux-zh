
Floyd-Steinberg 总是给出最好的结果；然而，好的并不总是你想要的。例如，阈值法可以在配合 `pnmconv` 工具的管道中使用，用于边缘检测和峰值检测等任务。使用类似报纸效果的聚类抖动是一种有用的特殊效果。`-value` 标志更改 Floyd-Steinberg 和简单阈值法的阈值值。它应该是一个 0 到 1 之间的实数。大于 0.5 意味着图像更暗；低于 0.5 意味着图像更亮。

希尔伯特曲线方法对于处理无法清晰渲染单个像素的显示设备（如激光打印机）之前的图像有用。这种抖动方法可以比激光打印机通常使用的抖动产生更好的结果。`-clump` 标志更改一个簇中的像素数量。较小的簇尺寸意味着图像灰色较少，但颗粒感更强。PGM 图像必须缩放以适应激光打印机（对于 400dpi 的 AN 为 2400 × 3000 像素），然后在转换为 PostScript 文件之前抖动为 PBM 图像。打印管道可能像这样：`pnmscale -ysize 2400 3000 image.pgm | pgmtobpm | pnmconv -scale 0.25 image.pgm`

所有标志都可以缩写为其最短前缀。

# 参考文献

这里你需要的参考文献是 Ulrich Lithner 的《Digital Haltoning》，MIT Press, ISBN 0-262-21009-6。希尔伯特曲线空间填充方法取自 Luiz Velelho 的《Digital Haltoning with Space Filling Curves》，Computer Graphics 第 25 卷第 4 期，SIGRAF '91 会议，第81页。ISBN 0-89791-436-8

# 另请

`preduce(1)`, `pgm(5)`, `pbm(5)`, `pnmconv(1)`, `pnmscale(1)`, `pnmtops(1)`

## 作者

> Copyright© 1991 by Jef Poskanen.

1991年1月11日

# 第一部分：用户命令

# pgmtoppm

`pgmtoppm`—将便携灰度图（pgm）彩色化携像素图（ppm）

# 语法

```
pgmtoppm colorspec [file]
pgmtoppm colorspec1-colorspec2 [file]
pgmtppm—map map [file]
```

## 描述

`pgmtoppm` 读取便携灰度图作为输入，通过将灰度值乘以指定的颜色或颜色进行着色，并产生便携像素图作为输出。

如果只指定了一种颜色，黑色 PPM 文件将保持为白色，而 PPM 文件中的黑色将变为 PPM 文件中指定的颜色。如果指定了两种颜色（用连字符分隔），则黑色映射到第一种颜色，白色映射到第二种颜色。

颜色可以通过五种方式指定：

- 名称，假设调用了指向 X11 风格颜色名称的指针，

- X11 风格的十六进制格式：`rgb:rgb`，其中 r、g 和 b 分别是 1-4 位的十六进制数。

- X11 风格的小数格式：`rgb:r/g/b`，其中 r、g 和 b 是于 0 到 1 之间的浮点数。

- 为了向后兼容，旧的 X11 风格十六进制数：`#rgb`, `#rrggbb`, 或 `#rrrrbb`。

- 为了向后兼容，用冒号分隔的数字三：`r,g,b`，其中 r、g 和 b 是于 0 到 1 之间的浮点数。（这种样式在 MIT 提出类似的 rgb 样式之前添加的）。

此外，`-map` 标志标记要使用的整个调色板。该映射是一个 PPM 文件；可以是任何形状，重要的是里面的颜色及其对应关系。在这种情况下，黑色映射到映射文件中的第一种颜色，白色映射到最后一种。

# 另请

`rgbbtoppm(1)`, `pptnpoppm(1)`, `pgmtorb3(1)`, `ppm(5)`, `ppm(5)`

## 作者

> Copyright© 1991 by Jef Poskanen.

1991年1月11日

## pi1toppm

`pi1toppm`—将 Atari Degas PI1 转换为便携像素图（ppm）

# 语法

```
pi1toppm [file]
```

## 描述

`pi1toppm` 读取 Atari Degas PI1 作为输入并产生便携像素图。

# 另请

`pi1topit(1)`, `ppm(5)`, `pi3topbm(1)`, `pbntopit(1)`

## 作者

> Copyright© 1991 by Steve Belczyk (seb@gte.com) and Jef Poskanen.

1990年7月19日

## pi3topbm

`pi3topbm`—将 Atari Degas PI3 转换为便携位图（pbm）

# 语法

```
pi3topbm [pi3file]
```

## 描述

`pi3topbm` 读取 Atari Degas PI3 文件作为输入。产生便携位图。

# 另请

`pbmtop3(1)`, `ppm(5)`, `pictoppm(1)`, `pptopit(1)`

## 作者

Copyright© 1988 by David Beckeyer (david) and Diomidis. Spinellis.

1990年3月11日

## pictoppm

`pictoppm`—将 Macintosh PICT 文件转换为便携像素图（ppm）

# 语法

```
pictoppm [-verbose][-fullres][-noheader][-quickdraw][-fontdir] [pictfile]
```

# 描述

`pictoppm` 读取 PICT 文件（版本 1 或 2）并输出像素图。作为扫描图像转换为可在 UNIX 上显示的内容的的第一步。

## 选项

- `-fullres` 强制任何 PICT 文件以其最小分辨率输出。PICT 图像可能指示保持其大小。

- `-noheader` 跳过所有 PICT 文件中的文件头。当 PICT 数据存储在数据分支时有用。

- `-quickdraw` 执行 quickdraw 操作。

- `-verbose` 开启详细模式，打印 pictoppm 黑客真正关心的信息。

# Bug

PICT 文件是一种通用绘制格式。`pictoppm` 不支持所有的绘制命令，但对任何矩形、多边形和文本有完全支持。它用于扫描图像的某些绘制转换。每个像素至少使用六字节内存。大型位图 PICT 文件可能会耗尽内存。

# format

`fontdir` 有内置字体，你的本地安装程序可能提供了额外的字体。你可以指向指定的更多字体。文件中的每行都是注释行，必须以 `#` 开头。字体信息由四个字段组成。第一个是字体编号，第二个是像素字体大小第三第三是字体样式，第四个是包含字体的 BDF 文件名。BDF 格式由 X Window 系统定义，此处未描述。

字体编号指示字形。这里是已知字体编号及其字形。

| 数字 | 字形 |
| :--- | :--- |
| 0 | Chicago |
| 1 | Application font |
| 2 | New York |
| 3 | Geneva |
| 4 | Monaco |
| 5 | Venice |
| 6 | London |
| 7 | Athens |
| 8 | San Francisco |
| 9 | Toronto |
| 11 | Cairo |
| 12 | Los Angeles |
| 20 | Times Roman |
| 21 | Helvetica |
| 22 | Courier |
| 23 | Symbol |
| 24 | Talesien |

字体样式表示字体的变体。多个变体适用于一个字体，字体样式是变体编号的和：

- 1 加粗 (Boldface)

- 2 斜体 (Italic)

- 4 下划线 (Underlined)

- 8 空心 (Outlined)

- 16 投影 (Shadow)

- 32 紧凑 (Condensed)

- 64 扩展 (Extended)

显然，字体定义与 Macintosh 密切相关。更多字体编号和字体信息可以在 Macintosh 文档中找到。

# 另请

Inside Macintosh 第1卷和第5卷，`pptoptict(1)`, `ppm`

## 作者

Copyright © 1993 by George Phillips.

## pjtoppm

`pjtoppm`—将 HP PaintJet 文件转换为便携像素图（ppm）

# 语法

```
pjtoppm [paintjet]
```

# 描述

`pjtoppm` 读取 HP PaintJet 文件作为输入并将其转换为便携像素图。这是一个为了节省时间的快速方案，它只处理 paintjet 命令的一个子集。特别是，它只会处理足够转换大多数栅格图像文件的命令。

# 参考文献

PaintJet XL Color Graphics Printer User’s Guide

# 另请

`pjttop(1)`

## 作者

Copyright© 1991 by Christos Zoulas.

1991年7月14日

## pkptobm

`pkptobm`—将打包 (PK) 格式字体转换为便携位图（pbm）

# 语法
