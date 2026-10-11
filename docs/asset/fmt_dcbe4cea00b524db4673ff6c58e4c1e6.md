
# DESCRIPTION

`pbmtoplot` 读取可移植位图作为输入并生成一个 UNIX plot 文件。

注意，没有 `pbmptok` 工具；这种转换是单向的。

# Part I: User Commands

# SEE ALSO

`pbm(5)`, `plot(5)`

# AUTHOR

Copyright © 1990 by Arthur David Olson.

1990 年 9 月 1 日

# pbmtoptx

`pbmtoptx`—将可移植位图转换为 Printronix 打印机图形

## SYNOPSIS

`pbmtoptx [pbmfile]`

## DESCRIPTION

`pbmtoptx` 读取可移植位图作为输入并生成一个 Printronix 打印机图形文件作为输出。

注意，没有 `pxtopbtbm` 工具；这种转换是单向的。

## SEE ALSO

`pbm(5)`

## AUTHOR

Copyright © 1988 by Jef Poskanzer

1988 年8 月 31 日

# pbmtox10bm

`pbmtox10bm`—将可移植位图转换为 X10 位图

## SYNOPSIS

`pbmtox10bm [pbmfile]`

## DESCRIPTION

`pbmtox10bm` 读取可移植位图作为输入并生成一个 X10 位图作为输出。维护这种旧格式是为了兼容性考虑。

注意，没有 `x10pbtopbm` 工具，因为 `xbbtopbm` 可以同时读取 X11 和 X10 位图。

## SEE ALSO

`pbmxm(1)`, `xbbtopbm(1)`, `pbm(5)`

## AUTHOR

Copyright © 1988 by Jef Poskanzer.

1988 年8 月 31 日

# pbmtoxbm

`pbmtoxbm`—将可移植位图转换为 X11 位图

## SYNOPSIS

`pbmtoxbm [pbmfile]`

## DESCRIPTION

`pbmtoxbm` 读取可移植位图作为输入并生成 X11 位图。

## SEE ALSO

`pbmx10bm(1)`, `xbtopbm(1)`, `pbm(5)`

## AUTHOR

Copyright © 1988 by Jef Poskanzer.

# pgmtoybm

`pgmtoybm`—将可移植位图转换为 Bennett Yee “脸”文件

## SYNOPSIS

`pgmtoybm [pbmfile]`

## DESCRIPTION

`pgmtoybm` 读取可移植位图作为输入并生成被 Bennett Yee (`bsy@cmu.edu`) 接受的输出文件。

## SEE ALSO

`ybtopbm(1)`, `pbm(5)`, `face(5)`, `xbm(1)`

## AUTHORS

Copyright © 1991 by Jamie Zawinski and Jef Poskanzer.

# pbmtozinc

`pbmtozinc`—将可移植位图转换为 Zinc 位图

## SYNOPSIS

`pbmtozinc [pbmfile]`

## DESCRIPTION

`pbmtozinc` 读取可移植位图作为输入并生成 Zinc 格式的位图作为输出。

## SEE ALSO

`pbm(5)`

# pbmupc

`pbmupc`—创建通用位图

## SYNOPSIS

`pbmupc [-s1|s2]`

## DESCRIPTION

`pbmupc` 生成通用位图。`pbmupc` 生成一个位图。

## OPTIONS

- `-s1`... 默认设计尺寸为 1。TFM 参数以设计尺寸的倍数形式给出。
- `-p num` 设置字体的前 `num` 个字体参数。前几个参数是字体的斜率、字间距、词间距、词收缩性、x 高、四格宽和句后间距。数学和符号字体有许多参数；请参见《The TexBook》获取列表。对于未指定的参数，选择了合理的默认值。
- `-C comments` 设置 TFM 文件中的编码注释。
- `-F family` 设置 TFM 文件中的字体注释。
- `-f optfile` 读取文件 `optfile`，该文件应包含一行：

```
filename xoff horiz vert width height depth
```

由 `filename` 参数指定的 PBM 文件将按照指定的属性连续插入字体中。如果省略了上述任何项或用 `+` 替换，将根据位图的大小计算默认值。`-w`,`-h`,`-d`,`-l`,`-v`,`-x` 和 `-y` 的设置不影响通过这种方式创建的字符。可以通过包含以 `+` 开头的行和新数字来更改字符编号。以 `w` 或 `i` 开头的行将被忽略。
- `-c num` 将下一个遇到的位图的字符编号设置为 `num`。
- `-w width` 将下一个字符的 TFM 宽度设置为 `width`（设计尺寸的倍数）。
- `-h height` 将下一个字符的 TFM 高度设置为 `height`（设计尺寸的倍数）。
- `-d depth` 将下一个字符的 TFM 深度设置为 `depth`（设计尺寸的倍数）。
- `-ital` 将下一个字符的斜体修正设置为 `ital`（设计尺寸的倍数）。
- `-h horiz` 将下一个字符的水平间距设置为 `horiz`（像素）。
- `-v vert` 将下一个字符的垂直间距设置为 `vert`（像素）。
- `-x xoff` 将下一个字符的水平偏移设置为 `xoff`（像素）。
- `-y yoff` 将下一个字符的垂直偏移设置为 `yoff`（像素，从顶行开始）。

# pgmenhance

## 作者

John Walker

Autodesk SA Avenue des Champs-Montants14b

CH-2074 MARIN

Suisse/Schweiz/Svizzera/Sviza/Switzerland

Usenet: `kelvin@Autodesk.com`

传真: 038/33 88 15

语音: 038/33 76 33

许可为了任何目的使用、复制、修改和分发此软件及其文档，无需任何费用，且无任何条件或限制。本软件按“原样”提供，不提供任何明示或隐含保证。

插件：如果你喜欢这类内容，可能也知道 James Gleick 编写 MS-DOS 的“Chaos—The Software”，可以在您的当地商店以 59.95 美元的价格或直接从 Autodesk, Inc. 购买。收件：Science Series, 2320 Marlin Way, Wausalty, CA 94965, USA。电话：800-688-2344（免费热线），或在美国境外拨打 (415) 332-2344 分机 4886。传真：415-289-4718。“Chaos—The Software”包含一个更全面的分形生成器，可以创建三维景观以及云层和行星，外加五个探索 Chaos 其他方面的模块。超过 200 页的用户指南包含了 James Gleick 的引言，以及 Rudy Rucker 对每个程序的数学和算法的详细解释。

1991年10月1日

# pgmedge

`pgmedge`—便携灰度图的边缘检测

## 概要

`pgmedge [pgmfile]`

## 描述

`pgmedge` 读取便携灰度图作为输入，勾勒边缘轮廓，并将便携灰度图作为输出。将结果通过传输到 `pgmtopbm`——通过调整阈值值可以得到边缘效果。

所使用的边缘检测技术是取两个相互垂直 90 度的梯度算子进行勾股达和。更多细节请参阅 Gonzalez 和 Wintz 著的《数字图像处理》第7章。

## 参见

`pgmenhance(1)`, `pgmtopbm(1)`, `pgm(5)`, `pbm(5)`

## 作者

版权 © 1991 由 lef Poskaner 所有。

1990年2月4日

# pgmenhance

`pgmenhance`—便携灰度图的边缘增强

## 概要

`pgmenhance [-N][pgmfile]`

## 描述

`pgmancement` 读取便携灰度图作为输入，增强边缘，并将便携灰度图作为输出。

边缘增强技术取自 Philip R. Thompson 的程序，该程序取自 Dot Diffusion、D. E. Knuth 发表在《ACM Transaction on Graphics》第6卷第4期（1987年10月）的《Digital Haltones》第6节，该节又源自 J. F. Jarvis 等人1976年发表的两篇论文。

## 选项

可选的 `-n` 标志应该是 1 到 9 之间的数字。1 是最低级别的增强，9 是最高级别；默认值为 9。

## 参见

`pgmedge(1)`, `pgm(5)`, `pbm(5)`

## 作者

版权 © 1989 由 J Poskanzer 所有。

1989年1月13日

# pgmhist

`pgmhist`—打印便携灰度图中值的直方图

## 概要

`pgmhist [pgmfile]`

## 描述

`pgmhist` 读取便携灰度图作为输入并打印灰度值的直方图。

## 参见

`pgmnorm(1)`, `pgm(5)`, `pgmhist(1)`

## 作者

版权 © 1989 由 J Poskanzer 所有。

1989年2月28日

# 第一部分：用户命令
