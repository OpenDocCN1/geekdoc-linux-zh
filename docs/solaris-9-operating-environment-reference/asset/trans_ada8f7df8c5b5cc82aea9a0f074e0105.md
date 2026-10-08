

# sccsdiff

# 1225

# 参见

bdiff(1), diff(1), sccs(1), sccs-admin(1), sccs-cdc(1), sccs-get(1),
sccs-help(1), sccs-prs(1), sccs-prt(1), sccs-rmdel(1), sccs-sccsd(1),
sccs-unset(1), what(1), sccsfile(4), attributes(5), XPG4(5)

# 诊断

使用 SCCS help 命令获取解释（参见 sccs-help(1)）。

# 警告

以 ASCII SOH 字符（二进制 001）开头的行无法放入 SCCS 文件，除非对 SOH 进行了转义。SOH 字符对 SCCS 有特殊含义（参见 sccsfile(4)）并产生错误。

# sccsdiff — 比较 SCCS 文件的两个版本

# 概要

```
/usr/ccs/bin/sccsdiff [-p] -r sid -r sid [diff-options]
s.filename
```

# 描述

参见 sccs-sccsdiff(1)。

# sccs-get, get — 获取 SCCS 文件的版本

# 概要

```
/usr/ccs/bin/get [-begkmpst] [-p] [-sequence] [-c date-time |
[-date-time] [-G-file] [-i sid-list] [-isid-list] -r[sid]
-x sid-list [-xid-list] s.filename...
/usr/pg4/bin/get [-begkmpst] [-p] [-a sequence] [-c date-time |
[-date-time] [-G-file] [-i sid-list] [-isid-list] -r sid [-rsid]
-x sid-list [-xid-list] s.filename ...
```

# 描述

使用 SCCS get 根据指定的选项从 SCCS 历史文件中检索工作副本。

对于每个 `s.filename` 参数，get 会显示 SCCS 增量 ID (sid) 和检索的行数。如果你使用目录名代替 `s.filename`，get 命令将适用于该目录下的所有文件。不可读的文件会产生错误；程序将继续处理下一个文件（如果有）。`s.filename` 使用连字符 (`-`) 表示从标准输入读取文件名，每行一个。检索的文件名通常与 `s.filename` 相同，但去掉前缀，被称为 g-file。对于处理的每个文件，get 会向标准输出响应 sid 和检索的行数。

# sccs-get, get

# 选项

-a sccs-get(1); -r 是你指定版本的更简单方法。当同时使用 -a 和 -r 时，-a 覆盖 -r。

-b 创建一个新分支。配合 -e 选项指示该增量应被检入新分支。它不是增加要检入的版本级别，而是初始化一个新分支（如果当前级别没有现有分支），或者增加 sid 的分支部分（如果 `s.file` 中未设置 b 标志，则忽略此选项）。

-c date-time 获取在 `date-time` 参数指定的日期和时间之前检查的最新版本。`date-time` 格式为 `yy[mm[dd[[hh:mm[ss]]]]`。省略单位默认使用最大可能值；-c 等同于 -c。任何非数字字符都可以分隔 `date-time` 规范。

-e 获取用于编辑的版本。对 `s.file` 加锁，以便其他人无法更改你已检出的版本。如果文件中设置了 e 标志，则锁是建议性的：get 会发出警告信息。允许对不同的 sids 并发使用 `get -e`；然而，如果目录中存在可写版本，get 将不会检出该文件的版本。文件中存储的所有 SCCS 保护措施（包括发布周期和授权用户列表）都会被遵守。

-g 获取 SCCS 版本 ID 而不检索版本本身。用于验证特定 sid 的存在性。

-G-file 使用 g-file 作为检索版本的名称。

-i sid-list |isid-list 指定包含在检索版本中的增量列表。所包含的增量将记录在标准输出的逗号分隔的 sid 列表中。要指定增量范围，请在列表中两个 sid 之间使用连字符 (`-`) 分隔符。

-k 抑制 ID 关键字的扩展。-k 由 -e 隐含。

-l[p] 获取增量表（版本日志）的摘要，并将其写入带有 l 前缀的列表文件（称为 l.file）。当你使用 -lp 时，将摘要写入标准输出。

-m 在每个检索到的行之前加上该行被添加到文件的增量 sid。sid 用制表符 (Tab) 与行隔开。

-n 在每行之前加上 n ID 关键字和制表符。当你同时使用 -m 和 -n 选项时，ID 关键字位于 sid 和文本行之前。

-p 将检索版本的文本写入标准输出。将所有通常发送到标准输出的消息重定向到标准错误。

-s 抑制通常写入标准输出的所有输出。然而，致命错误信息（始终始终发送到标准错误）不受影响。

-t 获取给定发布中最近创建（顶部）的增量，例如 -rl。

# /usr/ccs/bin/get

-r[sid] 获取与指定的 sid (增量) 对应的版本。

给定增量的 sid 是十进制数字，由两个字段组成：发布(release)和级别(level)，对于分支增量，还有分支(branch)和序列(sequence)字段。例如，如果 sid 是 1.2，则 1 是发布号，2 是级别号。如果 sid 是 1.2.3.4，则 3 是分支号，4 是序列号。

使用 get 获取版本无需指定 sid。当你省略 -r 或同时省略发布和级别时，get 会检索最高的发布和级别。如果该标志在 `s.file` 中设置为某个 sid 且你省略了 sid，get 将检索该标志指示的默认版本。

当你指定了发布但省略级别时，get 将检索该发布中最高的级别。如果该发布不存在，get 将从下一个最高的现有发布中检索最高级别。

分支的情况也是如此，如果你指定了发布、级别和分支，get 将检索该分支中最高的序列。

# /usr/xpg4/bin/get

-r sid -sid-list 与 /usr/ccs/bin/get 相同，但 sid 是强制性的。

-x sid-list -xsid-list

# 输出

# /usr/ccs/bin/get

The /usr/ccs/bin/get 命令具有以下输出格式：
"%s\n%d lines\n", sid, number-of-lines

# /usr/xpg4/bin/get

The /usr/xpg4/bin/get 命令具有以下输出格式：
"%s\n%d lines\n", sid, number-of-lines

# 1228

# 用法

# ID 关键字

在没有 -e 或 -k 的情况下，get 通过文本中的指定值来扩展以下 ID 关键字：

-A datawhat(1) 的简写表示，格式为 `%Y%Y %m%m %d%d`。

-B 分支部分。

-C 当前行号。用于程序输出“不应发生”的错误。它不用于在行产生序列号。

-D 当前日期，格式为 `yy/mm/dd`。

-E 增量创建的日期，格式为 `yy/mm/dd`。

-F SCCS 文件名。

-G 增量创建的日期，格式为 `mm/dd/yy`。

-H 当前日期，格式为 `mm/dd/yy`。

-I 检索版本的 sid，格式为 `%R%.%L%.%B%.%S`。

-L sid 部分。

-M 模块名，即文件中 m 标志的值（参见 sccs-admin(1) 或去掉前缀的 s.file 名称）。

-P 完全限定的 s文件名。

-Q s.file 中 q 标志的值。

-R 发布部分。

-S sid 序列部分。

-T 当前时间，格式为 `hh:mm:ss`。

-U 增量创建的时间，格式为 `hh:mm:ss`。

-W datawhat 的简写表示，格式为 `%Z%Y%M %I`。

-Y 模块类型，即 `s.file` 中 t 标志的值。

-Z 四字符字符串：`#` (# 被 what 识别)。

# ID 字符串

下表解释了如何确定检索和创建增量的 SCCS 标识字符串。

| 指定 SID (1) | 选项 (2) | 其他条件 | 检索的 SID | 创建增量的 SID |
|---|---|---|---|---|
| 无 (3) | 否 | R 默认为 mR | mR.mL | mR.(mL+1) |
| 无 (3) | 是 | R 默认为 mR | mR.mL | mR.(mL.(bB+1) |

