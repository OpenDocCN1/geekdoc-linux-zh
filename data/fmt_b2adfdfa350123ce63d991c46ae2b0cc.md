
## 缺陷

如果 `PPM_MAXVAL` 大于 `255`，整数可能会溢出。

## 作者

Graeme W. Gill (`graeme@lamtab.edu.au`)。

1998年2月5日

## `pnmoraw`

`pnmoraw`—强制将便携任意映射（portable anymap）作为输入并以纯文本（非原始）格式输出

### 概要

`pnmoraw [pnmfile]`

### 描述

`pnmoraw` 读取便携任意映射作为输入并以纯文本（非原始）格式输出。如果你没有定义 `BPMPUS_RABBITS` 编译选项，这基本上是没用的。

# 第一部分：用户命令

## 参见

`pnmf(5)`

## 作者

版权 Copyright © 1991 by Jef Poskanzer.

1991年1月8日

## `pnmpad`

`pnmpad`—为便携任意映射添加边框

### 概要

`pnmpad [-white|-.black] [-l] [-r] [-t] [-b] [pnmpfile]`

### 描述

`pnmpad` 读取两个便携任意映射作为输入，并输出具有指定尺寸额外边框的便携任意映射。边框颜色可以设置为黑色或白色（默认黑色）。

## 参见

`pnmake(1)`, `pnmpaste(1)`, `pnm(5)`

## 作者

版权 Copyright © 1990 by Angus Duggan. Copyright © 1989 by Jef Poskanzer.

## `pnmpaste`

`pnmpaste`—粘贴到便携任意映射中

### 概要

`pnmpaste [-replace|-.or] [-and] [-xor] pnmpfile x y [intfile]`

### 描述

`pnmpaste` 读取两个便携任意映射作为输入，将第一个映射插入第二个映射的指定位置，并产生与输出大小相同的便携任意映射。如果未指定第二个映射，则从 stdin 读取。`x` 和 `y` 可以为负值，分别相对于映射的右侧和底部。该工具在 `pnmcut` 中非常有用。例如，如果你想编辑大图像的一部分，但你的编辑器无法处理大图像，你可以剪切感兴趣的部分，编辑它，然后将其粘贴回去。另一个配套工具是 `pnmmask`。

可选标志指定执行粘贴时使用的操作。默认是 `-replace`。只有当两个图像都是位图时才允许其他逻辑操作。操作中白色为 TRUE，黑色为 FALSE。所有标志均可缩写为唯一的前缀。

## 参见

`pnmcut(1)`, `pnmvert(1)`, `pnmith(1)`, `pnm(5)`, `pnmmask(1)`

## 作者

版权 Copyright © 1989 by Jef Poskanzer.

1991年2月21日

## `pnmrotate`

`pnmrotate`—按某些角度旋转便携任意映射

### 概要

```
pnmrotate [-antialias] angle [pnmfile]
```

### 描述

`pnmrotate` 读取便携任意映射作为输入，按指定的角度旋转，并输出便携任意映射。如果输入文件是彩色，输出也是彩色；否则为灰度。角度以度（浮点数）计，逆时针测量。角度可以是负的，但应在 -90 到 90 之间。此外，对于大于 45 度的旋转，如果使用 `pnmip` 可能会获得更好的结果。旋转算法是 Alan Paech 的三倾斜法。每种倾斜通过遍历源像素并将分数分配到像素来实现。这避免了锯齿边缘和类似的伪影。然而，这意味着图像中的原始颜色或灰阶被修改了。如果你需要保持相同的颜色，可以使用 `-antialias` 标志。这在不改变值的情况下进行倾斜。如果你想要抗锯齿且不在乎精确颜色，但需要有限的颜色，可以将结果通过 `pnmquant`。所有标志均可缩写为唯一的前缀。

## 参考文献

*A Fast Algorithm for General Rotation* by Alan Paech, Graphics Interface '86, pages 77–81.

## 参见

`psear(1)`, `pnmip(1)`, `pnm(5)`, `pnmquant(1)`

## 作者

版权 Copyright © 1989 by Jef Poskanzer.

1991年1月12日

## `pnmscale`

`pnmscale`—缩放便携任意映射

### 概要

```
pnmscale s [pnmfile]

pnmscale s -xwidth-height s [pnmfile]

pnmscale s -xwidth-height s [pnmfile]

pnmscale -xsize x y [pnmfile]

pnmscale -pixels n [pnmfile]
```

# 第一部分：用户命令

### 描述

`pnmscale` 读取便携任意映射作为输入，按指定的因子或因子进行缩放，并输出便携任意映射。如果输入文件是彩色，输出也是彩色；否则为灰度。你可以放大（缩放因子 > 1）也可以缩小（缩放因子 < 1）。你可以指定一个维度为像素比例，另一个维度将相应缩放。你可以指定一个维度为比例，另一个维度将不缩放。你可以使用特殊的 `-resize` 标志，它在不改变比例的情况下将图像适应到指定的尺寸。或者，你可以使用 `-pixels` 标志，在不改变比例的情况下将图像适应到指定的像素。所有标志均可缩写为唯一的前缀。如果放大三倍或以上，可能应该添加 `pnmmooth` 步骤；否则你会在结果图像中看到原始像素的锯齿。

## 参见

`pnmreduce(1)`, `pnlarge(1)`, `pnmmooth(1)`, `pnm(5)`

## 作者

版权 Copyright © 1989 by Jef Poskanzer.

1991年1月12日

## `pnmsear`

`pnmsear`—按某些轴倾斜便携任意映射

### 概要

`pnmsear [-noantialias] angle [pnmfile]`

### 描述

`pnmsear` 读取便携任意映射作为输入，按指定的角度倾斜，并输出便携格式。如果输入文件是彩色的，输出也是彩色；否则为灰度。角度以度（浮点数）计，测量为：

```
+-++--+
|   ||   |
| OLD|\/NEW \
|!an||
|   | +gle+-+
```

如果角度为负，则向相反方向倾斜：

```
+-+ -an--+
|  gl/ |
| OLD|/ NEW /
|   | +gle+-+
```
