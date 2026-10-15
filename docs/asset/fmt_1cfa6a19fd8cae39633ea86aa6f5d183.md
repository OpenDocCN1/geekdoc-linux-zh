
Unix 两个文本处理程序，`nroff` 和 `troff`。当你需要将格式化文本输出到行打印机或行显示运行时，使用 `nroff` 程序；当你想将文本发送到激光打印机、点阵显示器或字字机时，使用 `troff`。

`nroff` 的输入文件包含文本，其中穿插着以点开头并包含两个字母命令的行。`nroff` 还允许你将一个宏定义为一组输入行，并有三个主要的宏包可以自动化复杂的格式功能。

使用 `nroff` 和 `troff` 而不是商业字处理器的主要优点是它们的输入文件是简单的文本文件。这允许你使用许多 Unix 工具（`grep`、`diff` 等）处理你的文件，而这在字处理器使用的专用格式中是无法实现的。

参见 `eqn`, `LATEX`, `groff`, `me macros`, `mm macros`, `ms macros`, `pic`, `soelim`, `tbl`, `TEX`, `TEXInfo`, `troff`

# 空参数 (null argument)

一种没有值但为了让参数按其正确位置被解析所需的命令行参数。当你使用显式选项时，不需要空参数。

# 空字符 (null character)

一种用于指示字符字符串结束、文件结束或空指针的特殊值。按照惯例，该字符由全零表示。

# 空设备 (null device)

Unix 空设备，也称为位桶（bit bucket），是 `/dev/null`。当你将输出发送到空设备时，它会被丢弃。

# 空字符串 (null string)

不包含任何字符的字符串；长度为零的字符串。

# 数字缓冲区 (numbered buffer)

在 `vi` 编辑器中，用于存储从文件中删除文本的九个存储区域之一；当进行第十次删除时，第一个缓冲区会被覆盖。

# `od`

一个用于对文件进行八进制、进制、十六进制或 ASCII 转储的命令。

## 语法 (Syntax)

以下是使用 `od` 的语法：

```
od [options][filename]offset
```

## 选项和参数 (Options and Arguments)

`od` 命令将以八进制格式对指定的文件进行转储，除非使用了其中一个选项。除非指定了偏移量，否则文件从开始处转储；偏移量通常是八进制字节；如果你想指定十进制偏移量，请使用它，或者使用 `b` 指定该偏移量代表 512 字节的块。表 O.1 列出了你可以配合 `od` 使用的选项。

另参见 `bc`, `dd`, `hexdump`, `more`

### 表 O.1：配合 `od` 使用的选项

| 选项 | 说明 |
| --- | --- |
| `-a` | ASCII, 文本 |
| `-b` | 八进制, 字节 |
| `-B` | 短型, 八进制 |
| `-c` | ASCII, 字节 |
| `-C` | 扩展 ASCII |
| `-d` | 无符号短型, 十进制 |
| `-D` | 无符号长型, 十进制 |
| `-e` | 双精度浮点数 |
| `-f` | 单精度浮点数 |
| `-F` | 双精度浮点数；同于 `-e` |
| `-h` | 短型, 十六进制 |
| `-H` | 长型, 十六进制 |
| `-1` | 短型, 有符号十进制 |
| `-I` | 长型, 有符号十进制 |
| `-p` | 偶奇校验 |
| `-P` | 奇偶校验 |
| `-s` | 接受字符串 |
| `-v` | 显示所有数据 |

# `olwm`

由 Sun Microsystems 开发的 Open Look 窗口管理器名称。

另参见 `mwm`, Open Look

# `onintr`

用于在 shell 脚本中管理中断的 shell 关键字。你可以通过三种不同的方式使用 `onintr`：命令`onintr label`标签类似于 `goto`，并跳转到以`label!`开头的行；命令`onintr -`允许脚本忽略中断；而不带参数的`onintr`命令则重新开启中断处理。

# Open 桌面 (Open Desktop)

来自 SCO 的图形用户界面 (GUI) 提供了在桌面上访问系统实用程序功能、SCO 和 DOS。文件、目录和程序由图标表示并在窗口中显示。

另参见 `OpenServer`

# 打开的文件 (open file)

任何当前正在使用的文件都被称为“已打开”（open）或“可用于打开”（open for use）。

# OpenGL

Open Graphics Library（开放图形库）的缩写；一组最初由 Silicon Graphics 开发的图形库，现在由 IBM、Intel、Microsoft 以及许多公司支持。

OpenGL 让开发者能够为运行了 X Window 系统程序员分级交互式图形系统 (PHiGS) 扩展的工作站创建 3D 图形应用程序。

另参见 `X Window`

# Open Look

由 AT&T 和 Sun Microsystems 开发的基于 X Window 的图形用户界面 (GUI)。Open Look 被用作 Sun 工作站上的标准窗口管理器，但其采用程度不如 OSF 的 Motif 广泛。

另参见 `olwm`

# OpenServer

SCO 提供的一组可扩展的 Unix 产品集，包括桌面系统、主机系统和企业系统。它们基于 `svr3.2`，但包含了许多重要的 `svr4` 增强功能。桌面系统是一个单用户多任务系统，包含 DOS 仿真、Microsoft Windows 3.1、TCP/IP 连接、内置的万维网浏览器、图形新闻阅读器和电子邮件支持。

企业级和主机系统为基于 Intel 的平台提供高性能的可扩展服务器，支持超过 8,000 个应用程序，具有广泛的网络支持、UPS 和高级的电源管理支持。

另参见 `sysadmsh`

# 开放系统 (open system)

一个用于描述不依赖于任何特定厂商专有系统而是遵循已知公共标准的硬件和软件的术语。

# `openwin`

用于在运行 Solaris 的系统中启动 X Window 系统和 OpenWindows 窗口管理器的命令。

## 语法 (Syntax)

该命令的语法为：

```
openwin [options]
```

## 选项和参数 (Options and Arguments)

表 O.2 列出了配合 `openwin` 命令使用的选项。

另参见 `xrdb`

### 表 O.2：配合 `openwin` 使用的选项

| 选项 | 说明 |
| --- | --- |
| `-banner` | 显示 OpenWindows 启动幅。 |
| `-noauth` | 降低安全级别。 |
| `-includedemo` | 将演示目录添加到路径中。 |
| `-nobanner` | 禁用 OpenWindows 启动幅，使启动速度略快。 |

# OpenWindows

Solaris 可用的基于 Open Look 的图形用户界面 (GUI)。OpenWindows 包含一组名为 DeskSet 的应用程序，用于执行常见的日常任务。

另参见 `o1wm`

# `/opt`

一个通常用于包含附加应用程序的根目录。

另参见 `/bin`

# `OPTARG`

一个包含选项参数的环境变量。

另参见 `OPTIND`

# `OPTIND`

一个包含下一个要处理参数索引的环境变量。

# 普通文件 (ordinary file)

不是特殊文件或目录的文件。

# 孤儿文件 (orphaned file)

文件名丢失的文件。

# 孤儿进程 (orphan process)

父进程已死亡的进程。

# OSF/1

由 Open Software Foundation 开发的操作系统。

# OSx

AT&T 的一个 Unix 版本。

# `pack`

一个用于压缩文件以占用更少磁盘空间的命令。

# `page`

`more` 命令的系统别名。

# `pagesize`

一个 BSD 命令，以字节为单位显示系统内存的页大小。

# 参数 (parameter)

在编程中，参数（通常译为形参或参数）是指从主机环境传递给程序或函数的变量，并持有一个常量值。

# 参数替换 (parameter substitution)

shell 用于将参数引用替换为其值的机制。

# 父目录 (parent directory)

文件系统中位于当前目录上方的目录；只有根目录没有父目录。两个点 `..` (dot dot) 是父目录名的简写，你可以使用：

```
cd ..
```

来切换到父目录，而无需输入（甚至记住）它的名称。

# 父 PID (parent PID)

参见 `PPID`

# 父进程 (parent process)

派生其他进程的进程。每个都可以识别其父进程，因为 `PPID` 存储在进程表中。

# `passwd`

用于维护用户登录密码的命令。

## 语法 (Syntax)

使用 `passwd` 的语法简单：

```
passwd
```

`passwd` 命令提示你输入旧密码，然后输入你想要使用的新密码，最后要求你再次确认新密码。只有你的系统管理员可以在不知道当前密码的情况下更改你的密码。
