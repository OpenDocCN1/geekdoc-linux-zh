

## vim-minimal — (Version 5.3, 445K)

VIM（Visual editor iMproved）是 vi 编辑器的更新和改进版本。Vi 是 UNIX 的第一个真正的基于屏幕的编辑器，至今仍非常流行。VIM 通过添加新功能改进了 vi：多窗口、多级撤销、块高亮等。vim-minimal 包包含 VIM 的精简版本，该版本安装到 /bin/vi 中，以便在仅存在根分区时使用。

## Emulators

本节包含与仿真其他操作系统相关的软件包。

### dosemu — (Version 0.99.10, 1,812K)

Dosemu 是一个 DOS 仿真器。安装 dosemu 后，通过输入 dos 命令启动 DOS 仿真器。如果你使用 DOS 程序并希望在 Red Hat Linux 系统上运行它们，则需要安装 dosemu。你可能还需要安装 dosemu-freedos 包。

### dosemu-freedos — (Version 0.99.10, 8,194K)

通常，dosemu DOS 仿真器要求系统具有某种版本的 DOS，或者系统分区是用 DOS 格式化并安装的。如果你的系统不符合上述任一要求，你可以改用 dosemu-freedos 包，该包包含一个 hdmage 文件，将安装在 /var/lib/dosemu 目录中。hdmage 文件已可使用 FreeDOS 启动。你需要编辑 /etc/dosemu.conf 文件，将该映像添加到 dosemu 使用的磁盘“驱动器”列表中。如果你在安装 dosemu 包，并且系统上没有可用的 DOS 版本，且系统分区不是用 DOS 格式化并安装的，则应安装 dosemu-freedos。

### xdosemu — (Version 0.99.10, 26K)

## Engineering

本节包含与工程技术相关的软件包。

### bc — (Version 1.05a, 128K)

bc 包包含 bc 和 dc。Bc 是一种任意精度数值处理算术语言。Dc 是一种交互式任意精度基于栈的计算器，可用作文本模式计算器。如果需要其数字处理功能或想使用其文本模式计算器，请安装 bc 包。

### gnuplot — (Version 3.7, 918K)

Gnuplot 是一个命令行驱动的交互式函数绘图程序，特别适合科学数据表示。Gnuplot 可用于以二维和三维以及多种不同格式绘制函数和数据点。如果需要用于科学数据表示的图形软件包，请安装 gnuplot。

### units — (Version 1.0, 25K)

Units 可将一个单位的数量转换为另一个单位，或告诉你将一个单位转换为另一个单位需要执行什么数学运算。Units 只能处理乘法尺度变化（即，它无法告诉你如何将摄氏度转换为华氏度，后者除了乘法转换外还需要额外的加法步骤）。Units 是一个方便的小程序，包含大量转换，从天文单位到秒差距，从汤匙到杯。你可能不需要安装它，但有时会派上用场。

### xlispstat — (Version 3.52.9, 2,871K)

xlispstat 包包含 XLISP-PLUS，即 X Window 系统的 Lisp 编程语言实现。XLISP-PLUS 还包含用于执行高级统计计算的扩展。如果需要带有统计扩展的 X 版 Lisp 编程语言，请安装 xlispstat 包。

## File

本节包含与文件操作相关的软件包。

### bzip2 — (Version 0.9.0b, 233K)

Bzip2 是一种可自由获得、无专利、高质量的数据压缩程序。Bzip2 可将文件压缩到最佳技术能力的 10% 到 15% 以内。然而，bzip2 的额外好处是其压缩速度约为那些技术的两倍，解压缩速度约为六倍。Bzip2 不是最快的压缩实用程序，但它在速度和压缩能力之间取得了平衡。如果需要高质量的压缩实用程序，请安装 bzip2。

### file — (Version 3.26, 206K)

file 命令用于根据文件中包含的数据类型来识别特定文件。File 可识别许多不同的文件类型，包括 ELF 二进制文件、系统库、RPM 包和不同的图形格式。由于 file 命令是一个非常有用的实用程序，你应该安装 file 包。

### fileutils — (Version 4.0, 1,283K)

fileutils 包包含许多 GNU 版本的常用流行文件管理实用程序。Fileutils 包含以下工具：
- chgrp（更改文件组所有权）
- chown（更改文件所有权）
- chmod（更改文件权限）
- cp（复制文件）
- dd（复制和转换文件）
- df（显示文件系统的磁盘使用情况）
- dir（提供简要目录列表）
- dircolors（ls 命令彩色版本的设置程序）
- du（显示磁盘使用情况）
- install（复制文件并设置权限）
- ln（创建文件链接）
- ls（以颜色列出目录内容）
- mkdir（创建目录）
- mkfifo（创建 FIFO，即命名管道）
- mknod（创建特殊文件）
- mv（重命名文件）
- rm（删除/移除文件）
- rmdir（删除空目录）
- sync（同步内存和磁盘）
- touch（更改文件时间戳）
- vdir（提供长目录列表）

你应该安装 fileutils 包，因为它包含许多你会经常使用的文件管理实用程序。

