
# 第24章：Linux 中的文本处理

`nroff` 命令使用 `groff`。如果 `.B -T` 选项带有除 `.B ascii` 和 `.B latin` 以外的参数，它将被忽略。
... Some lines deleted here

## SEE ALSO
`groff` (1),
`groff` (1).

`man` 手页的标记后文本文件的一个有趣特性是换行的方式。格式化 `groff`（`man` 命令使用 `groff` 处理标记后的文本文件）会填充行并使所有内容呈现出来。大多数命令必须独占一行，且每个命令以句号开头。然而，你可以在文中嵌入一些 `groff` 控制命令；这些嵌入命令以反斜杠开头。

以下是 `man` 手页标记后文本文件的总结：

- `.B` 开启粗体
- `.I` 开启斜体
- `.B` 开启粗体并切换到
- `.I` 开启开启
- `.SH` 是新章节的开始
- `.TH` 指明文档标题

## 编写一个示例的 man 手页

当你使用 `man` 命令查看 `man` 手页后，你应该查看生成 `man` 命令输出的原始源文件。在你的 Linux 系统中，`man` 手页源码位于几个目录中。这些目录名在 `/etc/man.config` 文件中定义。

`nroff` `man` 手页的源文件是 `/usr/man/man1/nroff.1`。你应该查看此文件以查看 `man` 手页最终呈现的形式，如图 24-5 所示。以下是你可以查看 `gnroff` `man` 手页源码的方法：

```
cd /usr/man/man1

more nroff.1
```

... Some lines deleted here

```
.TH NROFF 1 "26 June 1995" "Groff Version 1.1"

.SH NAME

nroff \ emulate nroff command with groff

.SH SYNOPSIS

nroff

  [

  .B -h

  ]

  .B -f

  ]

    ... Some lines deleted here

  [

  .I file.

  ]

.SH DESCRIPTION

The

  nroff

  script emulates the
```

假设你正在编写一个名为 `satview` 的程序。

```
.TH SATVIEW 1 "May 25, 1998" "Satview Version 4.0"
.SH NAME
satview - 查看卫星图像。
.SH SYNOPSIS
satview [-p projection] [-m] [-z zoomlevel]
.SH DESCRIPTION
satview 显示来自文件的图像。
.B -p projection（可以是 Lambert Conformal 或 Polar Stereographic）。默认是 Conformal。
.B -m 地图。
.B -z zoomlevel 设置缩放级别（可以是 2、4 或 8）。默认缩放级别为 1。
.TP 包含数据的文件。
.SH FILES
.TP /etc/awips/satview.rc Satview 的初始化命令
.SH SEE ALSO
exrad(1), contour(1)
.SH Bugs
当缩放级别大于 2 时，地图没有正确对齐。
```

实际上，`man` 手页的标记后文本文件的一个有趣特性是换行的方式。

## 测试并安装 man 手页

当你准备 `man` 手页时，你希望确保其格式正确。为了查看格式化输出，你应该使用以下命令：

```
groff -Tascii -man satview.1 | more
```
