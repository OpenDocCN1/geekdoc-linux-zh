
# size

```
size [ -A | -B | --format=compatibility [--help] ]

[ -d | -0 | -x | --radix=number ]

[ --target=bfname -V | --version objfile ]
```

## 描述

GNU `size` 工具列出参数列表中每个对象文件 `objfile` 的段和总大小。默认情况下，会为架构中的每个对象文件或模块生成一行输出。

## 选项

- `-A`, `-B`, `--format compatibility`

使用这些选项之一，你可以选择 GNU 的输出是类似于 System V `size`（使用 `-A` 或 `--format=sys`）还是类似于 Berkeley `size`（使用 `-b` 或 `--format=berkeley`）。默认是类似于 Berkeley 的单行格式。

- `--help`

- `-d`, `-0`, `-x`, `--radix number`

使用这些选项之一，你可以控制每个段的大小以十进制（`-d` 或 `--radix 10`）、八进制（`0` 或 `--radix 8`）或十六进制（`-x` 或 `--radix 16`）给出。在 `--radix number` 中，仅支持三个值（`8`, `10`）。总大小以两种进制给出：使用 `-d` 时为十进制，在使用 `-x` 时为十六进制。

- `--target bfname`

你可以为 `objfile` 指定特定的目标格式。这可能不是必要的；`size` 可以自动识别许多格式。信息详见 `objdump(1)`。

- `-V`, `--version`

显示 `size` 版本信息。

## 另见

`info` 中的 `binutils`；`GNU Binary Utilities`, Roland H. Pesh (1991); `ar(1)`, `objdump(1)`

## 许可

1991 Free Software Foundation 允许分发本手册的副本，前提是保留版权声明和本许可。

允许在上述条件下分发本手册的修改版本，只要整个衍生作品遵循与本许可相同的条款。

## 第一部分 用户命令

允许将本手册翻译成其他语言，遵循上述修改版本的条件，但翻译中可以使用 Free Software Foundation 批准的许可声明代替原始英语。

Cygnus Support, 1991年11月5日

# sldtoppm

`sldtoppm`—将 AutoCAD 转换为可移植位图（pixmap）

## 摘要

```
sldtoppm [--adjust][--dir][--height][ysize s][--info][-lib name][-scale s][--verbose][-width][-xsize s][outfile
```

## 描述

`sldtoppm` 读取 AutoCAD slide 并输出可移植位图。如果没有 slide，则从标准输入读取。如果没有指定输出文件，则写入到标准输出。

## 选项

- `--adjust`

如果使用此，输出将调整为相应的尺寸。

- `--dir`

如果使用此，将从指定的目录读取 slide。

- `--height[ysize s]`

位图的高度将被设置为 `ysize s`。

- `--info`

如果使用此，输出中将包含相关 信息。

- `--lib name`

将从指定的库读取 slide。

- `--scale s`

位图将按比例 `s` 缩放。

- `--verbose`

如果使用此，将在 `stderr` 上打印状态消息。

- `--width`

位图的宽度将被设置为指定的宽度。

- `--xsize s`

位图的宽度将被设置为 `xsize s`。

## 第一部分：用户命令

支持 `WM_SAVE_YOURSELF` 协议的应用程序会在会话管理器发布检查点（checkpoint）或关闭指令时，接收到 `WM_SAVE_YOURSELF` 客户端消息。这允许应用程序保存状态。如果应用程序不支持 `WM_SAVE_YOURSELF` 协议，则代理将向会话管理器提供足够的信息以重启应用程序（使用 `WM_COMMAND`），但不会恢复任何状态。

## 参见

`xsm(1)`

## 作者

Ralph Mor, X 联合会

X Version 11 Release 6

# sort

`sort`—排序文本文件的行

## 概览

```
sort [-cmus] [-t separator] [-o output-file] [-T tempdir] [-bdfWnr]

[+POS1,-POS2] [-k POS1,POS2] [file...]

sort [--help][--version]
```
