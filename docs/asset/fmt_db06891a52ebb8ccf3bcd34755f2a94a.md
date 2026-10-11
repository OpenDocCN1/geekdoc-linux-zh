
`merge` 将从 `file2` 变为 `file3` 的所有更改合并到 `file1` 中。结果通常进入 `file1`。`merge` 适用于合并对原始文件的修改。假设 `file2` 是原始文件，而 `file1` 和 `file3` 都是对 `file2` 的修改版本。那么 `merge` 就会将它们合并。

如果 `file1` 和 `file2` 在公共的行段上都有更改，则会发生冲突。如果发现冲突，`merge` 通常会输出警告并用 `<<<<<<<< >>>>>>>` 行括起冲突。典型的冲突看起来如下：

```
<<<<<< file A
lines in file A
======
lines in file B
>>>>>> file B
```

如果有冲突，用户应该编辑结果并删除其中一个备选方案。

### 选项

- `-A` 使用 `diff(1)` 的 `-A` 样式输出冲突，如果 `diff3` 支持。这会将从 `file2` 到 `file1` 的所有更改合并到 `file1`，并生成最详细的输出。
- `-E`, `-e` 这些选项指定的冲突样式产生的信息比 `-A` 少。详细信息请参见 `diff(1)`。默认是 `-E`。使用 `-e` 时，`merge` 不会对冲突发出警告。
- `-L label` 此选项可以给出三次，用于在冲突报告中代替相应的索引名的标签。也就是说，`merge -Lx -Ly z` 生成的输出看起来来自文件 `x`、`y` 和 `z`，而不是文件 `a`、`b` 和 `c`。
- `-p` 将结果发送到标准输出，而不是覆盖 `file1`。
- `-q` 静默模式；不对冲突发出警告。
- `-v` 打印 RCS 的版本号。

### 诊断

退出状态：`0` 表示无冲突，`1` 表示某些冲突，`2` 表示出错。

### 标识

作者：Walter F. Tich.

手册页修订版本：5.7；发布日期：1995/06/01。

版权所有 © 1982, 1988, 1989 Walter F. Tich.

版权所有 © 1990, 1991, 1992, 1993, 1994, 1995 Paul Eggert.

### 另请参

`diff(1)`, `diff(1)`, `rmerge(1)`, `co(1)`

### 缺陷

如果二进制文件是文本，合并它们通常没有意义，但 `merge` 会尝试这样做。

GNU, 1995年6月1日

# `mesg`

`mesg`—显示（不显示）来自其他用户的消息

## 语法概要

`mesg [n][y]`

## 描述

用户通过调用 `mesg` 工具来控制对与标准错误输出相关的终端设备的写入权限。如果允许写入权限，如 `talk(1)` 和 `write(1)` 等程序可能会在终端上显示消息。然而，随着用户对安全风险的意识增强，存在一种默认移除写入权限的趋势，至少对于。

## 文件

## 另请参

`talk(1)`, `write(1)`

## 文件

```
/dev/tty
```

## 另请参

`tty(1)`

## 文件

## 另请参

`write(1)`, `talk(1)`

# `mkdir`

## 作者

Copyright © 1989 by Jef Poskaner.

24 January 1989

## `mkdir`—创建目录

## 语法概要

`mkdir [-p] [-m mode] [--parents] [--mode=mode] [--help] [--version] dir..`

## 描述

本手册页描述 GNU 版本的 `mkdir`。`mkdir` 创建每个给定的目录。默认情况下，创建目录的模式是 `0777` 减去设置在 `umask` 中的位。

### 选项

- `-m`, `--mode mode` 设置创建目录的模式为 `mode`，其符号格式类似于 `chmod`，并以默认模式为起点。
- `-p`, `--parents` 确保每个给定的目录存在。为每个参数创建任何缺失的父目录。父目录默认使用 `umask` 修改后的 `u=max`。不要将已存在的参数目录视为错误。
- `--help` 在标准输出上打印用法信息并成功退出。
- `--version` 在标准输出上打印版本信息并成功退出。

GNU File Utilities

# `mkdirhier`

`mkdirhier`—创建目录层次结构

## 语法概要

`mkdirhier directory ...`

## 描述

`mkdir` 命令创建指定的目录。与 `mkdir` 不同，如果指定目录的任何父目录不存在，它也会创建它们。

## 另请参

`mkdir(1)`

# `mkfifo`

`mkfifo`—创建 FIFO（命名管道）

## 语法概要

`mkfifo [-m mode] [--mode=mode] [--help] [--version] filename.`

X Version 11 Release 6

[第 356 页]

## 描述

本手册页文档了 GNU 版本的 `mkfifo`。`mkfifo` 根据给定的名称创建一个 FIFO（先进先出文件）。默认情况下，创建的 FIFO 模式为 `0666`，并减去 `umask` 中设置的位。

### 选项

- `-m`, `--mode` 将创建的 FIFO 模式设置为 `mode`，该模式在 `chmod` 中为符号表示形式，并使用起始点的默认模式。
- `--help` 在标准输出上打印用法信息并成功退出。
- `--version` 在标准输出上打印版本信息，然后成功退出。

GNU 文件工具

# `mkmanifest`

`mkmanifest`—创建一个 shell 脚本来恢复 UNIX 文件名

## 语法

```
mkmanifest [ files ]
```

## 描述

`mkmanifest` 创建一个 shell 脚本，该脚本有助于恢复被 MS-DOS 限制所破坏的 UNIX 文件名。MS-DOS 文件名被限制为八个字符的名称、三个字符的扩展名、大写、不包含设备名，且不包含非法字符。

`mkmanifest` 程序与 `pcomm`、`arc` 和 `mtools` 中使用的方法兼容，这些方法可以将完美的 UNIX 文件名更改以适应 MS-DOS 的限制。

## 示例

假设你想将以下 UNIX 文件拷贝到 MS-DOS 磁盘上（使用 `mcopy` 命令）：

```
very_long_name
2.many.dots
illegal:
good.c
prn.dev
Capital
```

```
mcopy 将名称转换为
very_lon
2xmany.dot
illegalx
good.c
xprn.dev
capital
```

```
命令：
mkmanifest very_long_name 2.many.dots illegal: good.c prn.dev Capital > manifest
```

```
将产生如下：
mv very_lon very_long_name
2xmany.dot 2.many.dots
mv illegal illegal:
mv xprn.dev prn.dev
mv capital Capital
```

[第 357 页]

注意，`good.c` 不需要任何转换，因此它没有出现在输出中。

假设我已将这些文件从磁盘拷贝到另一个 UNIX 系统，现在我想让文件恢复到原始名称。如果文件清单（上述捕获的输出）随这些文件一起发送，可以使用它来转换文件名。

## 缺陷

`mkmanifest` 生成的短名称遵循旧规范（来自 `mtools-2.0.7`），而不是 Windows 95 和 `mtools-3.0` 的规范。

## 参见

`arc(1)`, `pcomm(1)`, `mtools(1)`

## `mknod`

`mknod`—创建特殊文件

## 语法

```
mknod [options] filename [bcu] major minor
mknod [options] filename p
```

## 选项：

```
[-m mode] [--mode=mode] [--help] [--version]
```

## 描述

本手册页描述了 GNU 版本的 `mknod`。`mknod` 根据给定名称创建 FIFO、字符特殊文件或块特殊文件。默认情况下，创建的文件的模式为 `0666` 减去 `umask` 中设置的位。

`filename` 之后的参数指定要创建的文件类型：

`p` 表示 FIFO

`b` 表示块（缓冲）特殊文件

`c` 或 `u` 表示字符（无缓冲）特殊文件

在创建块或字符特殊文件时，必须在文件类型之后给出主设备和次设备号。

### 选项

- `-m`, `--mode` 将创建的文件模式设置为 `node`，该模式在 `chmod` 中为符号表示形式，并使用默认模式作为起点。
- `--help` 在标准输出上打印用法信息并成功退出。
- `--version` 在标准输出上打印版本信息，然后成功退出。

GNU 文件工具

## `mlabel`

`mlabel`—创建一个 MS-DOS 卷标

## 语法

```
mlabel [ -v ] drive: [ new_label ]
```

[第 358 页]

# 第一部分：用户命令

## 描述

`label` 显示当前的卷标（如果存在）。如果没有给出 `new_label`，且既没有设置 `c` 也没有设置 `s` 选项，它将提示用户输入一个新的卷标。如需删除现有的卷标，请在提示符处按回车键。

`label` 支持以下命令行选项：
