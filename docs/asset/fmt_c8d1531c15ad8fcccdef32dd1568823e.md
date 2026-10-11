
## 描述

`pmntops` 读取便携格式作为输入并产生封装的 PostScript。

如果输入是彩色的 (`PPM`)，则写入一个彩色 PostScript 文件。某些 PostScript 解释器无法处理彩色 PostScript。如果你有其中之一，你需要通过 `pnmptops` 文件运行你的图像。

注意，没有 `pstopp` 工具；这种转换是单向的，因为 `pstopp` 工具将是一个完整的 PostScript 解释器，这超出了此包的范围。然而，如果你愿意安装大型 GhostScript 软件包，可以读取灰度非长度 PostScript 图像数据的 `psiptop` 工具附带了一个 `pstopp` 脚本。

## 选项

`-scale` 标志控制结果的缩放。默认比例为 1，300dpi 打印机使用该比例，因为 Apple Writer 会在 72dpi 屏幕上显示时使输出尺寸与输入相近。要让每个 300dpi 打印机像素获得一个 PxM 像素，请使用 `-scale 2`。

`-turn` 和 `-noturn` 标志控制图像是否旋转 90 度。通常，如果图像宽大于高，它会自动旋转以更好地适应页面。如果指定了 `-turn` 标志，无论形状如何都会旋转；如果指定了 `-noturn` 标志，无论形状如何都不会旋转。

`-rle` 或 `-runlength` 标志指定长度压缩。如果主机到打印机的链路较慢，这可能会很慢；通常打印机的处理时间占主导，因此 `-rle` 会让事情变慢。

`-dpi` 标志设置输出设备的每英寸点数。默认为 300dpi。理论上，`-width` 和 `-height` 标志指定尺寸。`-center` 和 `-nocenter` 标志控制定位。`pmfile` 参数指定输入。

## 缺陷

此程序不是自包含的。要使用它，必须获取 `OTHER.SYSTEMS` 文件列出的 TIFF 软件包并配置 `PBMPLUS` 使用 `libtiff`。有关此配置的详情请参见 `PBM-PLUS` 的 `Makefile`。

## 另请

`tiffopnm(1)`, `pnm(5)`

## 作者

由 Jef Poskanzer 根据 `ras2tiff.c` 派生，版权所有 1990 由 Sun Microsystems, Inc. 版所有。作者：Patrick J. Naughton (`naughton@web.sun.com`)。

1991年1月13日

# pmntoxed

`pmntoxed` -将可移植像素映射图（portable pixmap）转换为 X11 窗口转储

## 概要

```
pmntoxed [-pseudodepth n] [-directcolor][pixfile]
```

## 描述

`pmntoxed` 读取可移植像素映射图作为输入，并产生 X11 窗口转储作为输出。此窗口转储可以使用 `xwud` 工具显示。

通常情况下，`pmntoxed` 为 `PBM` 和 `PGM` 文件生成静态灰度转储文件。对于 `ppm`，如果输入中最多有 256 颜色，它写入伪色（PseudoColor）转储文件，否则写入直接色（DirectColor）转储文件。可以使用 `-directcolor` 标志强制生成直接色转储。可以使用 `-pseudodepth` 标志更改伪色转储的深度，从默认的 8 位/颜色。

## 另请

`xwdtopnm(1)`, `pnm(5)`, `xwud(1)`

## 作者

Copyright© 1989, 1991 Jef Poskanzer.

1991年9月24日

# ppm3d

`ppm3d`-将两个可移植像素映射图转换为红蓝3D眼镜像素映射图

## 概要

```
ppm3d leftfile rightppmfile [horizontal_offset]
```

## 描述

`ppm3d` 读取两个可移植像素映射图作为输入，并产生一个可移植像素映射图作为输出，图像以红/蓝格式水平重叠 `horizontal_offset` 像素。

`horizontal_offset` 默认值为 30 像素。像素映射图必须相同。

## 另请

`ppm(5)`

## 作者

Copyright © 1993 David K. Drum.

1993年11月2日

# ppmbrighten

`ppmbrighten`—根据 HSV 值更改图像的饱和度和亮度

## 概要

```
ppmbrighten [-n] [-s <+ saturation>] [-v <+ value>] <ppmfile>
```

## 描述

`ppmbrighten` 读取可移植像素映射图作为输入，将图像从 RGB 空间转换为 HSV 空间，并按 `<+ value` 的百分比更改亮度；饱和度亦然。使用

```
ppmbrighten -v 100
```

向亮度增加 100%。

`n` 选项将值归一化到 0 和 1 之间（归一化）。

## 另请

`pgmnorm(1)`, `ppm(5)`

## 作者

Copyright 1990 Brian Moffat. Copyright © 1989 Jef Poskanzer.

允许出于任何目的且免费使用、复制和分发此软件及其文档，前提是所有副本中都必须出现上述版权声明，且版权声明和此许可声明均出现在支持文档中。此软件按“原样”提供，不提供任何明示或隐含保证。

## 注意

此程序不改变颜色数量。

1993年11月20日

# ppmchange

`ppmchange`—将可移植像素映射图中某种颜色的所有像素更改另一种

## 概要

```
ppmchange oldcolor newcolor [...] [ppmfile]
```

## 描述

`ppmchange` 读取可移植像素映射图作为输入，并将所有 `oldcolor` 的像素更改为 `newcolor`，其余不变。256 颜色可以通过在命令行指定颜色来替换。

## 第一部分：用户命令

颜色可以通过五种方式指定：

- 指针：`r:g/b`，其中 `r`, `g` 和 `b` 都是4位十六进制数。
- X11风格十六进制描述符：`rgb:g/b`，其中 `r`, `g` 和 `b` 是 0 到 1 之间的浮点数。
- X11风格十进制描述符：`rgb:g/b`，其中 `r`, `g` 和 `b` 是 0 到 1 之间的浮点数。
- 为了后兼容，X11风格十六进制数：`#rgg,#rrggbb,#rrrrggggbb` 或 `#rrrrggbbbb`。
- 为了后兼容，逗号分隔的三元组：`r,g,b`，其中 `r`, `g` 和 `b` 是 0 到 1 之间的浮点数。（这种风格在 MIT 引入 rgb 风格之前）。

## 另请

`pgtop(1)`, `ppm(5)`

## 作者

Wilson H. Bent, Jr. (`wb@usc.edu`)，由 Alberto Accomazzi (`alberto@harvard.edu`) 修改。

1993年12月16日

# ppmdim

`ppmdim`—将可移植像素映射图调至全黑

## 概要

```
ppmdim factor [ppmfile]
```
