
## 选项

- `f` `problem-report`：指定一个已包含完整报告的文件。`cvbug` 将发送文件内容而不调用编辑器。如果 `--problem-report` 值为空，则 `cvbug` 从标准输入读取。

- `t` `mail-address`：更改中央支持站点用于问题报告的邮件地址。默认邮件地址是默认 `site` 使用的地址。请使用 `site` 参数。

- `P`：在标准输出上打印环境变量 `PR` 指定表单。如果 `PR` 未设置，则打印空白 `PR` 模板。不发送邮件。

- `L`：打印可用类别的列表。不发送邮件。

- `request-id`：向支持站点发送邮件，或者如果指定，则请求你的 `submitter ID`。如果你不属于 `site`，请使用 `net` 作为 `submitter ID`。

- `v`：显示 `cvbug` 版本号。

## 环境

环境变量 `EDITOR` 指定了调用模板的编辑器。默认是 `vi`。

如果环境变量 `PR` 已设置，则其值被用作问题报告编辑会话的文件名。你可以利用此从一个部分填充的表单开始（例如标识字段已完全的表单）。

# 如何填写问题报告

问题报告必须采用特定格式，以便程序于管理。请记住以下准则：

对于后续邮件，请使用与自动回复中相同的主题行。它由 `PR` 编号和原始概要行组成。这允许支持站点接收针对特定 `PR` 的多封邮件并自动记录。

请在主题（`subject`）或摘要（`synopsis`）行中尽可能准确。

主题和摘要行不保密。这是因为开放缺陷列表（`open-bugs lists`）是从这些内容编译的。避免在其中包含机密信息。

参见 GNU Info 文件 `cvbug`、`cvbug.info` 或文档《Reporting Problems With cvbug》获取有关报告问题的详细信息。

# 如何提交测试用例、代码等

在提交 `PR` 时提交较小的代码示例。联系支持站点获取有关提交较大的测试用例和问题源码的说明。

# 文件

- `/tmp/ps$` 用于编辑会话的 `PR` 副本

- `/tmp/ps$` 空 `PR` 表单副本，用于测试目的

- `/tmp/piaass$` 用于被拒绝的 `PR` 的文件

# EMACS 用户界面

一个用于 `cvbug` 且具有字段值补全功能的 EMACS 接口是 `cvbug` 分发的一部分（通过 `M-x cbug` 调用）。参见 `cvbug-info` 或发行版根目录下的 ASCII 文件 `INSTALL` 以获取配置和安装信息。EMACS LISP 模板文件为 `cvbug-el.in`，并安装为 `cvbug-el`。

# 安装与配置

参见 `cvbug.info` 或 `INSTALL` 获取安装说明。

# 另另

使用 `cvbug` 报告问题（也安装为 GNU Info 文件 `cvbug.info`）。

`gnats(1)`, `query-pr(1)`, `edit-pr(1)`, `gnats(8)`, `queue-pr(8)`, `at-pr(8)`, `mkcat(8)`, `mkdist(8)`

## 作者

`Jeffrey Osier`, `Bertrand Kehoe`, `Jason Merrill`, `Heinz G. Seidl` (`Cygnus Support`)。

## 复制

版权所有 (`c`) 1992, 1993 Free Software Foundation, Inc.。允许制作并分发本手册的逐字副本，前提是所有副本上必须保留版权公告和本许可声明。

在满足逐字复制条件的情况下，允许复制并分发本手册的修改版本，前提是生成的作品按照与本公告相同的条款进行分发。

在上述适用于修改版本的条件下，允许复制并分发本手册到其他语言的翻译，但本许可声明可以包含在自由软件基金批准的翻译中，而不是原始版本。

版本，1993年2月

# cvbtbatch

`cvbtbatch`—将 Usenet 批文件转换为 INN 格式。

# 摘要

```
cvbtbatch [ -w items ]
```

# 第八部分：管理与特殊命令

## 描述

`-w` 标志显示每行输出的开头。该标志的项必须从 `newsfeeds(5)` 中指定的 `w` 标志项中选择。它们可以从以下集合中选择：

| | | |

|---|---|---|

| b | 字节大小 |

| f | 文章的完整路径 |

| m | 文章的 Message-ID |

| n | 文章的相对路径 |

如果输入文件由一系列 Message-Ids 组成，则使用带有 `-s` 标志的 `grephistory(1)` 并管道至 `cvbatch`。

# 历史

由 `Rich Salz` (`rsalz@ouenet.uu.net`) 为 InterNetNews 编写。

# 查看

`grephistory(1)` `newsfeeds(5)`

# cytune

`cytune`—调整 Cylades 驱动程序参数。

# 摘要

```
cytune [-q [-i interval]] ([-s value];[-S value])
[-gG] ([-t timeout];[-T timeout]) tty ...
```

## 描述

`cytune` 查询并修改 Cylades 驱动程序的中断阈值。Cylades 上的每条串口线都有一个 12 字节的输入 FIFO（以及另一个 12 字节的输出 FIFO。“阈值”指定了在触发中断之前 FIFO 中必须有多少多少个字符。当打开 Cylades `tty` 时，此阈值将根据波特设置为默认值：

| 波特 | 阈值 |

|---|---|

| 50–480 | 10 |

| 9600 | 8 |

| 19200 | 4 |

| 38400 | 2 |

| 57600–150000 | 1 |

如果阈值设置过低，大量的中断会导致机器负担并降低整体吞吐量。如果阈值设置过高，FIFO 缓冲区可能会溢出，导致字符丢失。然而，较慢的机器可能无法处理输入负载，需要将阈值上调。

如果在编译 Cylades 驱动程序时定义了 `ENABLE MONITORING`，则可以使用 `cytune` 命令配合 `-q` 选项报告监控间隔内的中断和监控间隔内传输的字符。它还会报告 FIFO 的状态。报告发生中断时 FIFO 中的最大字符数、FIFO 中字符的瞬时计数以及现在 FIFO 中的字符数。输出可能如下：

```
dev/cubC0: 830 ints, 9130 chars; fifo: 11 threshold, 11 max, 11 now
166.258886 interrupts/second, 1828.65821 characters/second
```

此输出表明，在监控期间，中断总是在一个字符时间时间内处理的，因为 `max` 从未超过过阈值。这是好事，你可能可以这样运行，并可以使用输出的大量样本。如果你运行 FIFO，你将丢失字符，因为 Cyclades 硬件似乎不支持从 DCE 到 DTE 的 RS-232 硬件流控信号线。

`cytune` 在查询模式下并在以 `SIGINT` 结束时会生成摘要报告。如果 Cylades 驱动程序在定义 `ENABLE MONITORING` 时编译，可以使用 `cytune` 命令配合 `-q` 选项报告监控间隔内的中断和监控间隔内传输的字符。它还会报告 FIFO 的状态。报告发生中断时 FIFO 中的最大字符数、FIFO 中字符的瞬时计数以及现在 FIFO 中的字符数。输出可能如下：

```
dev/cubC0: 830 ints, 9130 chars; fifo: 11 threshold, 11 max, 11 now
166.258886 interrupts/second, 1828.65821 characters/second
```

此输出表明，在监控期间，中断总是在一个字符时间时间内处理的，因为 `max` 从未超过过阈值。这是好事，你可能可以这样运行，并可以使用输出的大量样本。如果你运行 FIFO，你将丢失字符，因为 Cyclades 硬件似乎不支持从 DCE 到 DTE 的 RS-232 硬件流控信号线。

`cytune` 在查询模式下并在以 `SIGINT` 结束时会生成摘要报告。如果 Cylades 驱动程序在定义 `ENABLE MONITORING` 时编译，可以使用 `cytune` 命令配合 `-q` 选项报告监控间隔内的中断和监控间隔内传输的字符。它还会报告 FIFO 的状态。报告发生中断时 FIFO 中的最大字符数、FIFO 中字符的瞬时计数以及现在 FIFO 中的字符数。输出可能如下：

```
dev/cubC0: 830 ints, 9130 chars; fifo: 11 threshold, 11 max, 11 now
166.258886 interrupts/second, 1828.65821 characters/second
```

此输出表明，在监控期间，中断总是在一个字符时间时间内处理的，因为 `max` 从未超过过阈值。这是好事，你可能可以这样运行，并可以使用输出的大量样本。如果你运行 FIFO，你将丢失字符，因为 Cyclades 硬件似乎不支持从 DCE 到 DTE 的 RS-232 硬件流控信号线。
