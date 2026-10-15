
该命令可用的选项见表 H.4。

`history` 还是 Korn shell 命令，用于列出最后16条命令；`history` 是 Korn shell 中 `fc -1` 的别名。

参见 `fc`, `history`, `.history`, `history file`

# 第二章

表 H.4: `history` 的可用选项

| 选项 | 描述 |
|---|---|
| `-h` | 打印不带事件编号的历史列表。 |
| `-r` | 按逆序打印历史列表，最旧的命令在前。 |
| `n` | 仅显示最后 n 条命令，而不是由 变量设置的数量。 |

# `.history`

历史文件的文件名，该文件存储了用户在登录系统期间输入的所有命令；当用户在会话结束注销时，该文件会被删除或清空。

另参见 `history`

# `HISTSIZE`

一个 Korn shell 环境变量，用于指定可以访问多少条历史命令；默认值为 128 条命令。

另参见 `history`

# `home`

屏幕左上角的初始光标位置。

# `home`

一个 C shell 变量，包含你家目录的完整路径。字符 `~` (`~`) 是你家目录名称的简写符号。

另参见 `HOME`

# `HOME`

一个 Bourne shell 和 Korn shell 变量，包含你家目录的完整路径。波浪字符 (`~`) 是你家目录名称的简写符号。

# `/home`

一个 SVR4 根目录，包含用户家目录和文件。

# `home directory`

一个包含特定用户 ID 文件的目录。你的家目录名称存储在 `passwd` 文件中，当你登录时，你的当前目录始终被设置为你的家目录。家目录通常是你个人目录结构的起点，你可以根据喜好让它变得极其简陋或极其复杂。

作为快捷方式，你可以使用波浪字符 (`~`) 作为你家目录名称的符号。你家目录的完整路径存储在 `home` 或 `HOME` 变量中，取决于你使用哪种 shell。

另参见 `cd`, `pwd`

# `home page`

在万维网上的初始起始页面。首页可以由个人、非营利组织或公司准备，是通往其他 Web 页面或互联网资源的方便跳板。

另参见 `HTML`, `HTTP`, `SGML`, `URL`

# `HoneyDanBer UUCP`

由 Peter Honeyman、David Nowitz 和 Brian D. Redman 开发的 UUCP 版本，它取代了原始的 AT&T 版本。也称为基础网络工具（Basic Networking Utilities），有时简称为 BNU。

# `host`

网络化或分布式处理环境中的中央或控制计算机，提供其他计算机或终端通过网络访问的服务。

互联网上可以访问的大型系统也称为主机（host）。有时称为主机系统或主机计算机。

# `hostid`

一个打印主机系统十六进制 ID 数字的命令。该命令位于 `/usr/uc/hostid`。

另参见 `hostid`。

# `hostname`

一个设置或打印当前主机名称的命令。语法为：`hostname [newhost]`

其中 `newhost` 是要为主机使用的新名称；你必须是超级用户才能更改此名称。

另参见 `hostid`。

# `hp`

一个 SCO 命令，用于处理惠普（HP）2640 系列终端上的特殊功能，以便在这些终端上显示准确的 `nroff` 输出。

# `HP-UX`

用于惠普公司计算机的 Unix 版本。`HP-UX` 包含 BSD 扩展，包括网络命令、Korn shell 和一个版本的 `emacs`。VUE（视觉用户环境）是 HP 的图形用户界面（GUI），具有不同任务的独立工作空间、拖放功能、一个文本编辑器、彩色图标编辑器以及其他生产力工具。

`HP-UX` 还包括 SAM（系统管理管理器），用于常见的管理任务，如添加新用户、安装和配置外设、管理进程和调度作业。无盘计算机（无论是客户端还是服务器）都可以从服务器启动并支持本地挂载的文件系统，因此每个客户端都可以访问自己的数据文件，并与他人共享文件。

# `HTML`

超文本标记语言（Hypertext Markup Language）的缩写。一种用于创建万维网页面和其他超文本文档的标准超文本语言。

当你访问 HTML 文档时，你会看到文本、图形以及指向其他文档或其他互联网资源的链接的混合。当你选择链接时，相关的文档会自动打开，无论该文档位于何处。超文本文档通常具有 `.html` 或 `.htm` 文件扩展名。

`HTML` 对万维网的发展至关重要；然而，它通过浏览器提供的功能正变得越来越局限。这导致了其他的发展，例如 Java，它可以提供 3D 交互应用程序。

*另参见首页, `HTTP`, `SGML`, `URL`*

# `HTTP`

超文本传输协议（Hypertext Transfer Protocol）的缩写。用于管理超文本文档之间链接的协议。

`HTTP` 是当你选择超文本链接时打开相关文档的机制，无论相关文档位于何处。

另参见首页, `HTML`, `SGML`, `URL`

# `Hurd`

自由软件基金（FSF）的一个项目，旨在为许多不同的硬件平台开发和分发免费版本的 Unix。`Hurd` 仍处于开发的早期，`Hurd`（或有时称为 HURD）被认为是 GNU 所有软件、编译器、编辑器、实用程序以及操作系统的集合。

# `hwconfig`

一个 SCO 命令，列出包含在 `/usr/adm/hwconfig` 中的配置信息。

## 语法

该命令的语法为：

```
hwconfig [options]
```

信息显示在以下列：

- `magic_char`
- `device_name`
- `base+finish`
- `vec`
- `dma`
- `rest`

其中 `magic_char` 是百分号 (`%`)，`device_name` 是设备驱动程序的名称，`base+finish` 是驱动程序工作空间的起始和结束地址，`vec` 是中断向量，`dma` 是 DMA 通道号，`rest` 是参数=值对列表。

# 选项和参数

`hwconfig` 的可用选项见表 H.5。

# 表 H.5: `hwconfig` 的可用选项

| 选项 | 描述 |
| --- | --- |
| `-c` | 检查冲突。 |
| `-f filename` | 使用文件名而非 `/usr/adm/hwconfig`。 |
| `-h` | 使用带有头的长格式。 |
| `-l` | 使用长格式，默认设置。 |
| `Param` | 显示参数的值。有效的系统参数名，`base`, `offset`, `vec`, `dma`, `unit`, `type`, `ports`, `ids`, `cyls`, `secs`, `drvr`。 |
| `param=value` | 显示参数等于 value 的信息。 |
| `-q` | 静默模式；与 `-c` 使用时仅显示冲突。 |

# 超文本标记语言 (Hypertext Markup Language)

参见 `HTML`

# 超文本传输协议 (Hypertext Transfer Protocol)

参见 `HTTP`

# `iconv`

用于将文件从一种字符集转换为另一种字符集的命令。
语法为：

```
iconv -f char-set1 -t char-set2 filename
```
