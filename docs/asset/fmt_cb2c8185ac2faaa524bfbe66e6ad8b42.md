
## `od` 选项

`-v`, `--output-duplicates` 输出连续的相同行。默认情况下，当省略二或更多连续行时，`od` 只输出第一行，并在后续行上放置一个星号，表示相同的行已编辑。

`-s`, `--strings[bytes]` 代替正常输出，仅输出包含在 ASCII（或格式）字符中的字符串，并以 NUL 终止。如果省略了 `bytes`，默认值为 `3`。

`-w`, `--width[bytes]` 每个输出格式化的输入字节数。它必须是与指定的输出类型大小的倍数。如果省略了 `bytes`，默认值为 `32`。如果未设置此选项，默认值为 `16`。

`-help` 打印用法信息并以非零状态退出。

`-version` 在标准输出上打印信息，然后退出。

接几个选项将旧的、预-POSIX 格式规范映射到相应的 POSIX 格式规范。GNU `od` 接受旧格式和新格式规范的任意组合。

- `a` 输出命名字符，等同于 `a`
- `b` 输出八进制，等同于 `o`
- `c` 输出 ASCII 字符或反斜杠转义，等同于 `c`
- `d` 输出无符号十进制，等同于 `u`
- `f` 输出浮点数，等同于 `f`
- `h` 输出帮助信息，等同于 `help`
- `i` 输出整型，等同于 `I`
- `l` 输出长整型，等同于 `L`
- `o` 输出八进制，等同于 `o`
- `x` 输出十六进制，等同于 `x`
- `traditional` 使用传统格式，等同于上述选项

其语法如下：`od` 允许使用 `offset` 格式的选项，如果用户指定了 `offset`。`+offset` 输出十进制，等同于 `d`。如果指定了 `offset`，则从中开始。

## `passwd`

`passwd`—修改密码

### 概要

`passwd [ name ]`

### 描述

`passwd` 修改指定用户的密码。

### 文件

`/etc/passwd`

### 参见

`chsh(1)`, `chfn(1)`

### 错误

`passwd` 在执行时可能出现错误。

## `paste`

`paste`—合并文件

### 概要

```
paste [-s] [--delim=char] [file_...]
```

### 描述

本手册描述了 GNU 版本的 `paste`。`paste` 以制表符分隔合并行，并以换行符结束。如果没有提供文件，则使用标准输入。

### 选项

- `-s`, `--serial` 将每个文件按行合并。
- `--delim=char` 指定分隔符；默认为制表符。
- `--help` 打印用法信息并以非零状态退出。
- `--version` 在标准输出上打印信息，然后退出。

### 作者

`Coreutils`

## `pbmfilters`

- `pbmclean`: 翻转便携位图中的孤立像素
- `pbmlife`: 在便携位图中应用康威伊生命游戏
- `pbmmake`: 创建指定大小的空白位图
- `pbbmask`: 从普通位图创建掩码位图
- `pbmbscale`: 使用边缘平滑技术放大便携位图
- `pbmreduce`: 读取便携位图并将其缩小为 N 倍
- `pbmtext`: 将文本渲染为位图
- `pbmt0x`: 将便携位图转换为 Gemini 10X 打印机图形
- `pbmt0425`: 在 AT&T 4425 终端上显示 PBM 图像
- `pbmtosscii`: 将便携位图转换为 ASCII 图
- `pbmt0tk`: 将便携位图转换为 Andrew Toolkit 对象
- `pbmtob`: 将便携位图转换为 BitGraph 图形
- `pbmtocemw`: 将便携位图转换为 CMU 窗口管理器位图
- `pbmtopsi`: 将便携位图转换为封装的 PostScript
- `pbmttopson`: 将便携位图转换为 Epson 打印机图形
- `pbmtog3`: 将便携位图转换为 Group 3 文件
- `pbmtogem`: 将便携位图转换为 GEM 图像
- `pbmtogo`: 将便携位图转换为压缩 GraphOn 图形
- `pbmtocol`: 将便携位图转换为 Sun 图标
- `pbmtoil`: 将便携位图转换为 HP Laser Jet 格式
- `pbmtoin03`: 将便携位图转换为 DEC LN03+ Sixel 输出
- `pboltps`: 将便携位图转换为 PostScript
- `pbmtonac`: 将便携位图转换为 MacPaint 文件
- `pbmontogr`: 将便携位图转换为 MGR 位图
- `pbmtopp`: 通过区域平均值将便携位图转换为便携灰度图 `PGM`
- `pbmtop3`: 将便携位图转换为 Atari Degas, `.pi3` 文件
- `pbmtopk`: 将便携位图转换为打包 `PK` 格式字体
- `pbmtplot`: 将便携位图转换为 UNIX `pictot(5)` 文件
- `pbmtoptx`: 将便携位图转换为 Printrix 打印机图形
- `pmttoxbe`: 将便携位图转换为 X11 位图
- `pbmtorinc`: 将便携位图转换为 Zinc 位图
- `pbmpuc`: 创建通用产品代码 `UPC` 位图
- `pcxtome`: 将 PCX 文件转换为便携像素图 `Pixmap`
- `pgmentity`: 对便携灰度图进行 Bentley 化处理
- `pgcrater`: 通过分形灰度创建地形
- `pgmedge`: 对便携灰度图进行边缘检测
- `pgmenance`: 对便携灰度图进行边缘增强
- `pgmhist`: 打印便携灰度图中值的直方图
- `pgmkernel`: 生成卷积核
- `pgmoise`: 创建由白噪声组成的灰度图
- `pgmnorm`: 归化便携灰度图的对比度
- `pgmoil`: 将便携灰度图转换为油画
- `pgmramp`: 生成灰阶阶
- `pgmtexture`: 计算便携灰度图的纹理特征
- `pgmtofs`: 将便携灰度图转换为 Usenix FaceSaver

# 第一部分：用户命令

| 命令 | 说明 |
| :--- | :--- |
| `pgmtolism` | 将便携灰度图转换为 Lisp 机格式 |
| `pgoptbm` | 将便携灰度图转换为便携位图 |
| `pgmtopn` | 将便携灰度图着色为便携像素图 |
| `pgntoybe` | 将便携位图转换为 Bennet Yee “脸”文件 |
| `piittop` | 将 Atari Degas PI1 转换为便携像素图 |
| `pi3topbm` | 将 Atari Degas PI3 文件转换为便携位图 |
| `picctppm` | 将 Macinctoc PICT 文件转换为便携像素图 |
| `pjopp` | 将 HP Paintlet 文件转换为便携像素图 |
| `pktopbm` | 将打包 `PK` 格式转换为便携位图 |
| `pnalias` | 便携任意图 `anymap` 的抗锯齿处理 |
| `pnarith` | 对两个便携任意图进行算术运算 |
| `pmncat` | 拼接便携任意图 |
| `pmncomp` | 将两个便携任意图组合在一起 |
| `pmnconvol` | 对便携任意图进行通用 IIRs 卷积 |
| `pmncrop` | 裁剪便携任意图 |
| `pmncut` | 从便携任意图中剪出一个矩形 |
| `pmndepth` | 读取便携任意图并将其放大为 N 倍 |
| `pmnfile` | 描述便携任意图 |
| `pmnflip` | 对便携任意图执行一次或多次翻转操作 |
| `pnmgamma` | 对便携任意图进行伽马校校正 |
| `pnhist` | 为 PGM 或 PPM 文件绘制直方图 |
| `pindex` | 为一组任意图建立视觉索引 |
| `pminvert` | 反转便携任意图 |
| `pmnargin` | 为便携任意图添加边框 |
| `pmnfililt` | 非线性滤波、平滑、alpha 裁剪平均、最优滤波 |
| `pmnoraw` | 强制将便携任意图转换为原始格式 |
| `pnpad` | 为便携任意图添加边框 |
| `pnpaste` | 在便携任意图中粘贴矩形 |
| `pnmrotate` | 按某些角度旋转便携任意图 |
| `pnmscale` | 缩放便携任意图 |
| `pmshear` | 按某些角度倾斜便携任意图 |
| `pnmsmooth` | 平滑图像 |
| `pntile` | 将便携任意图复制到指定大小 |
| `pntoddif` | 将便携任意图转换为 DDIF 格式 |
| `pntofits` | 将便携任意图转换为 FITS 格式 |
| `pntops` | 将便携任意图转换为 PostScript |
| `pntorast` | 将便携任意图转换为 SGI 图像 |
| `pntosgi` | 将便携任意图转换为 Solitaire 文件 |
| `pntosir` | 将便携任意图转换为 TIFF 文件 |
| `pntotiff` | 将便携任意图转换为 X11 dump 文件 |
| `ppm3d` | 将便携任意图转换为红/蓝像素图 |
| `ppmbrighten` | 改变便携任意图的饱和度 |
| `ppmchange` | 将便携任意图的所有像素更改另一种颜色 |
| `ppmdim` | 降低便携任意图亮度 |

## `pbmfilters`

- `ppmdist`: 简单的灰度分配
