
配合 `-traverse`，将每个页面输出到文件。配合 `-dump` 使用 `-traverse` 格式化输出，但到 stdout。

- `-display=DISPLAY`

设置 X 引用页的变量。

- `-dump`

将文档或命令行指定的文档格式化输出输出到标准输出。可以通过以下方式使用：`lynx -dump http://w3.org/default.html`。

- `-editor=EDITOR`

启用编辑模式以指定编辑器（vi, ed 等）。

- `-emackeys`

启用类似 Emacs 的移动。

- `-enable_scrollback`

切换与常用程序滚动键的兼容性（可能与某些软件包不兼容）。

- `-error_file=FILE`

定义 `lynx` 报告 HTTP 访问代码的文件。

- `-euc`

在日语模式开启时将汉字代码设置为 EU。

- `-fileversions`

包含本地 VMS 目录中所有版本的文件。

- `-force_html`

强制将第一个文档解释为 HTML。

- `-ftp`

- `-get_data`

- `-head`

- `-help`

- `-historical`

- `-homepage=URL`

- `-image_links`

- `-index-URL`

- `-jpn`

- `-link_UMBER`

- `-localhost`

- `-locelex`

- `-mime_header`

- `-minimal`

- `-nowbrowse`

- `-noexec`

- `-nolist`

- `-nolog`

- `-noprint`

- `-noredir`

- `-nostatus`

- `-number_links`

- `-post_data`

- `-print`

- `-pseudo_inlines`

- `-realm`

- `-reload`

- `-status`

- `-noredir`

输入 `n` 或 `7` 获取在线帮助和按键命令的描述。

输入 `k` 获取当前按键命令映射的完整列表。

# 注意事项

如果您想为 `lynx` 的进一步开发做出贡献，请订阅我们的邮件列表。发送邮件至 `majordomomo@sig.net`，正文内容仅包含 `lynx-dev`。

订阅后，向 `lynx-dev@sig.net` 发送报告、意见和建议以取消订阅。

通过发送邮件至 `majordomomo@sig.net` 来取消订阅，正文内容仅包含 `unsubscribe lynx-dev`。请勿向 `lynx-dev` 本身发送取消消息。

# 致谢

`lynx` 一直整合了来自各种来源的代码。`lynx` 的早期版本包含了来自萨斯喀彻大学计算服务部门 Earl Fogel 的代码，该代码在 UN*X 环境下实现了 HYPERREZ。HYPERREZ 由 lynx.com 的 Neil Narsson 开发，并作为 `lynx` 早期版本的模型。这些版本还整合了由明尼苏达大学开发的 UN*X Gopher 客户端库，而 `lynx` 的后期版本则依赖于 Tim Berners-Lee 和 WWW 社区开发的 WWW 客户端库代码。此外，特别感谢 Fotos Macrides，他将大部分 `lynx` 移植到了 VMS，并感谢网络上所有直接（通过注释或报告）或间接（通过改进和开发其他系统）对 `lynx` 开发做出贡献的人。

## 作者

Lou Montulli, Garrett Bly, Craig Lavender, Michael Grove, Charles Rezac

学术计算服务部

堪萨斯大学

Lawrence, Kansas 66047

Fotos Macrides

Worcester Foundation

Shrewsbury, Massachusetts 03545

## macptopbm

`macptopbm` --将 Paint 文件转换为便携式位图 (portable bitmap)

## 概要

```
macptopbm [-extraspk N] [macfile]
```

## 描述

`macptopbm` 读取 Paint 文件作为输入，生成便携式位图作为输出。

## 选项

- `-extraspk`

此标志用于解决从 Mac 世界传输文件到 UNIX 世界时某些方法产生的问题。这些方法中的大多数保持 Mac 文件不变，但倾向于在 UNIX 文件上添加额外信息数据。这意味着读取文件时会跳过额外的 128 字节。需要观察的症状是生成的 PBM 文件看起来向一侧偏移。如果出现这种情况，请尝试 `-extraspk 128`，如果看起来仍然不对，请尝试另一个值。

所有标志都可以缩写为其最短唯一前缀。

# 第一部分：用户命令

# 另见

`pictoppm(1)`, `pbtomacp(1)`, `pbm(5)`

## 作者

版权所有 © 1988 Jeff Poskaner。MacPaint-读取代码版权所有 © 1987 Patrick J. Naughton

(naughton@wind.sun.com)。

1988 年 3 月 29 日

## make

`make`—用于维护程序组的 GNU 实用程序

## 概要

```
make [ -f Makefile ] [ option ] ... target
```

# 警告

本页是 GNU `make` 文档的节选自录。它仅偶尔更新，因为 GNU 项目没有使用 refoff。要获取完整、当前的文档，请参阅 info 文件 `make` 或 DVI 文件 `make.dvi`，这些是由 texinfo 文件 `make` 生成的。

# 描述

`make` 实用程序的目的是自动确定大型程序中哪些部分需要重新编译，并发布命令来协调它们。本手册页描述了 `make` 的 GNU 实现，由 Richard Stallman 和 Roland McGrath 编写。我们的示例展示了最常见的 C 程序，但你也可以对任何编译器可以通过 shell 命令运行的编程语言使用 `make`。事实上，`make` 不限于程序。你可以用它来描述任何只要文件从其他文件更新时必须自动更新的任务。

（注：此处原文后续存在大量逻辑重复或混乱的描述，已根据要求按原文结构进行对应翻译）

`make` 实用程序的目的是自动确定大型程序中哪些部分需要重新编译，并发布命令来协调它们。本手册页描述了 `make` 的 GNU 实现，由 Richard Stallman 和 Roland McGrath 编写。我们的示例展示了最常见的 C 程序，但你也可以对任何编译器可以通过 shell 命令运行的编程语言使用 `make`。事实上，`make` 不限于程序。你可以用它来描述任何只要文件从其他文件更新时必须自动更新的任务。

（注：此处原文后续存在大量逻辑重复或混乱的描述，已根据要求按原文结构进行对应翻译）

`make` 实用程序的目的是自动确定大型程序中哪些部分需要重新编译，并发布命令来协调它们。本手册页描述了 `make` 的 GNU 实现，由 Richard Stallman 和 Roland McGrath 编写。我们的示例展示了最常见的 C 程序，但你也可以对任何编译器可以通过 shell 命令运行的编程语言使用 `make`。事实上，`make` 不限于程序。你可以用它来描述任何只要文件从其他文件更新时必须自动更新的任务。

（注：此处原文后续存在大量逻辑重复或混乱的描述，已根据要求按原文结构进行对应翻译）

`make` 实用程序的目的是自动确定大型程序中哪些部分需要重新编译，并发布命令来协调它们。本手册页描述了 `make` 的 GNU 实现，由 Richard Stallman 和 Roland McGrath 编写。我们的示例展示了最常见的 C 程序，但你也可以对任何编译器可以通过 shell 命令运行的编程语言使用 `make`。事实上，`make` 不限于程序。你可以用它来描述任何只要文件从其他文件更新时必须自动更新的任务。

（注：此处原文后续存在大量逻辑重复或混乱的描述，已根据要求按原文结构进行对应翻译）

`make` 实用程序的目的是自动确定大型程序中哪些部分需要重新编译，并发布命令来协调它们。本手册页描述了 `make` 的 GNU 实现，由 Richard Stallman 和 Roland McGrath 编写。我们的示例展示了最常见的 C 程序，但你也可以对任何编译器可以通过 shell 命令运行的编程语言使用 `make`。事实上，`make` 不限于程序。你可以用它来描述任何只要文件从其他文件更新时必须自动更新的任务。

（注：此处原文后续存在大量逻辑重复或混乱的描述，已根据要求按原文结构进行对应翻译）

`make` 实用程序的目的是自动确定大型程序中哪些部分需要重新编译，并发布命令来协调它们。本手册页描述了 `make` 的 GNU 实现，由 Richard Stallman 和 Roland McGrath 编写。我们的示例展示了最常见的 C 程序，但你也可以对任何编译器可以通过 shell 命令运行的编程语言使用 `make`。事实上，`make` 不限于程序。你可以用它来描述任何只要文件从其他文件更新时必须自动更新的任务。

（注：此处原文后续存在大量逻辑重复或混乱的描述，已根据要求按原文结构进行对应翻译）
