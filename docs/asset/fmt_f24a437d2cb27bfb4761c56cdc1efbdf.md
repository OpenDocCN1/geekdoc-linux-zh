
包含另一个 Makefile。参见第 3.3 节 [包含 Makefile]。

`override` variable-assignment

定义一个变量，覆盖命令行中的任何定义。参见第 6.7 节 [override 指令]。

`export`

告诉 make 将所有变量导出到子进程。参见第 5.7.2 节 [子进程间的通信]。

166

GNU make

`unexport` variable

告诉 make 是否将特定变量导出到子进程。参见第 5.7.2 节 [子进程间的通信]。

`private` variable-assignment

不允许此赋值被依赖项继承。参见第 6.13 章 [抑制继承]。

`vpath` pattern

指定匹配 `%` 模式的文件的搜索路径。参见第 4.4.2 节 [vpath 指令]。

`vpath`
移除之前在任何 vpath 中指定的路径
以下是内置函数的摘要（参见第 8 章 [函数]）：

`$(from,to,text)`
将 text 中的 from 替换为 to。参见第 8.2 节 [字符串替换与分析]。

`$(pattern,replacement,text)`
将 text 中匹配 pattern 的部分替换为 replacement。参见第 8.2 节 [字符串替换与分析]。

`$(strip string)`
删除字符串中的多余字符。参见第 8.2 节 [字符串替换与分析]。

`$(findstring,text)`
在 text 中查找 find。参见第 8.2 节 [字符串替换与分析]。

`$(filter pattern,...,text)`
选择 text 中匹配 pattern 单词之一的单词。参见第 8.2 节 [字符串替换与分析]。

`$(filter-out pattern,...,text)`
选择 text 中不匹配任何 pattern 单词的单词。参见第 8.2 节 [字符串替换与分析]。

`$(sort list)`
对 list 中的单词按字母顺序排序并去重。参见第 8.2 节 [字符串替换与分析]。

`$(word n,text)`
提取 text 的第 n 个单词（从 1 开始）。参见第 8.2 节 [字符串替换与分析]。

`$(words text)`
计算 text 中单词的数量。参见第 8.2 节 [字符串替换与分析]。

## 附录 A：快速参考

`($wordlist s,e,text)`
返回 text 中从 s 到 e 的单词列表。
见第 8.2 节 [字符串替换与分析函数]，第 84 页。

`($firstword names...)`
提取 names 中的第一个单词。
见第 8.2 节 [字符串替换与分析函数]，第 84 页。

`($lastword names...)`
提取 names 中的最后一个单词。
见第 8.2 节 [字符串替换与分析函数]，第 84 页。

`($dir names...)`
提取每个文件名的目录部分。
见第 8.3 节 [文件名函数]，第 87 页。

`($notdir names...)`
提取每个文件名的非目录部分。
见第 8.3 节 [文件名函数]，第 87 页。

`($suffix names...)`
提取每个文件名的后缀（最后一个 '.' 及其后续字符）。
见第 8.3 节 [文件名函数]，第 87 页。

`($basename names...)`
提取每个文件名的基名（不带后缀的名字）。
见第 8.3 节 [文件名函数]，第 87 页。

`($addsuffix suffix,names...)`
在 names 中的每个单词后添加后缀。
见第 8.3 节 [文件名函数]，第 87 页。

`($addprefix prefix,names...)`
在 names 中的每个单词前添加前缀。
见第 8.3 节 [文件名函数]，第 87 页。

`($join list1,list2)`
合并两个并行的单词列表。
见第 8.3 节 [文件名函数]，第 87 页。

`($wildcard pattern...)`
查找匹配 shell 文件名模式（不是 '%' 模式）的名字。
见第 4.3.3 节 [wildcard 函数]，第 24 页。

`($realpath names...)`
对于 names 中的每个文件，展开为不包含任何 . 或 .. 组件的绝对路径，但保留符号链接。
见第 8.3 节 [文件名函数]，第 87 页。

`($abspath names...)`
对于 names 中的每个文件，展开为不包含任何 . 或 .. 组件的绝对路径，但保留符号链接。
见第 8.3 节 [文件名函数]，第 87 页。

`$(error text...)`
当此函数被求值时，`make` 会生成带有该消息的致命错误。
见第 8.12 节 [控制 Make 的函数]，第 96 页。

`$(warning text...)`
当此函数被求值时，`make` 会生成带有该信息的警告。
见第 8.12 节 [控制 Make 的函数]，第 96 页。

`$(shell command)`
执行 shell 命令并返回其输出。
见第 8.13 节 [Shell 函数]，第 97 页。

`$(origin variable)`
返回一个描述 `make variable variable` 如何定义的字符串。
见第 8.10 节 [origin 函数]，第 94 页。

`$(flavor variable)`
返回一个描述 `make variable variable` 作用域（flavor）的字符串。
见第 8.11 节 [flavor 函数]，第 95 页。

`$(foreach var, words, text)`
对 words 中的每个单词进行界定并求值 text，然后合并结果。
见第 8.5 节 [foreach 函数]，第 90 页。

`$(if condition, then-part [,else-part])`
求值条件；如果非空，则替换为 then-part 的扩展，否则替换为 else-part 的扩展。
见第 8.4 节 [条件判断函数]，第 89 页。

`$(or condition[1], condition[2], condition[3...])`
逐个求值每个条件；替换第一个空的扩展。如果所有扩展都为空，则替换为空字符串。
见第 8.4 节 [条件判断函数]，第 89 页。

`$(and condition[1], condition[2], condition[3...])`
逐个求值每个 conditionN；如果任何扩展结果为空字符串，则替换为最后一个 `condition` 的扩展。
见第 8.4 节 [条件判断函数]，第 89 页。

`$(call var,param...)`
求值 var，并将其中任何对 $(1), $(2) 的引用替换为第一个、第二个等 param 值。
见第 8.7 节 [call 函数]，第 91 页。

`$(eval text)`
求值 text，然后将结果作为 make 命令读取。扩展为空字符串。
见第 8.9 节 [eval 函数]，第 93 页。

`$$(file filename,text)`
展开参数，然后使用模式 op 打开文件 filename 并写入该文件。
见第 8.6 节 [file 函数]，第 91 页。

`$$(value var)`
求值变量 var 的内容，但不对其进行扩展。
见第 8.8 节 [value 函数]，第 93 页。

以下是自动变量的摘要。完整信息请见第 10.5.3 节 [自动变量]，第 120 页。

- `$$` 目标名称。
- `$%` 当目标是归档成员时，目标目标成员名称。
- `$<` 第一个依赖项的名字。
- `$?` 所有比目标新的依赖项名称，用空格隔开。对于归档成员的依赖项，仅使用命名的成员（见第 11 节 [存档]，第 129 页）。
- `$^` 所有依赖项的名字，用空格隔开。对于归档成员的依赖项，仅使用命名的成员（见第 11 节 [存档]，第 129 页）。'$$' 的值。
- `$*` 匹配的通配（见 10.5.4 节 [模式匹配]，第 122 页）。
- `$$(D)` 目录部分。
- `$<` 目录部分。
- `$<D)` 目录部分。
- `$(F)` 目录部分。
- `$+F)` 目录部分。

这些变量被 GNU make 特殊使用：

`MAKEFILES` 每次调用 make 时读取的 Makefile。
见第 3.4 节 [wildcard 函数]，第 14 页。

`VPATH` 在当前目录未找到文件的搜索目录。
见第 4.4.1 节 [所有依赖的搜索路径]，第 25 页。

`SHELL` 系统默认解释器，通常为 '/bin/sh'。可以在 Makefile 中设置 SHELL 来更改运行规则。
见第 5.3.2 节 [选择 Shell]，第 45 页。

`MAKESLL` 仅在 MS 上使用的命令解释器名称。此值高于 SHELL。
见第 5.3 节 [MAKESLL 变量]，第 44 页。

`MAKE` 被调用的名称。在规则中使用此变量有特殊含义。
见第 5.7.1 节 [变量工作原理]，第 51 页。

`MAKELEVEL` 递归层数（子 make 数量）。
见第 5.7.2 节 [变量/递归]，第 52 页。

`MAKEFLAGS` 使用 make 的标志。可以在环境变量或 Makefile 中设置。
见第 5.7.3 节 [向子 make 传递选项]，第 54 页。
不建议在规则行中直接使用 MAKEFLAGS：其内容可能无法为 shell 正确引用。始终通过递归 make 从环境中获取这些值。

`GNUMAKEFLAGS` 被 make 解析的其他标志。可以在环境变量或 Makefile 中设置。GNU make 从不设置此变量。只有当你想在 POSIX 的 make 中设置 GNU make 特有的标志时才需要此变量。此变量会被 GNU make 读取而被其他实现忽略。如果你使用 GNU make，则不需要；直接使用 MAKEFLAGS。

`MAKEDGOALS` 命令行给出 make 的目标。设置此变量对 make 的操作没有影响。
见第 9.2 节 [指定目标的参数]，第 99 页。

`CURDIR` 设置为当前工作目录的路径（在处理所有 -C 选项后）。设置此变量对 make 的操作没有影响。
见第 5.7 节 [递归使用 make]，第 50 页。

`SUFFIXES` 在 make 读取任何 Makefile 之前的默认后缀列表。

`LIBPATTERNS` 定义 make 搜索的库的命名及其顺序。
见第 4.4.6 节 [链接库的目录搜索]，第 28 页。

## 附录 B：Make 生成的错误

以下是你可能会看到的 make 常见错误列表，以及关于这些错误含义及其如何修复的信息。

有时 make 错误并不是致命的，特别是在配方行带有 `-` 前缀且使用了 `-k` 命令行选项的情况下。致命错误以字符串 `***` 为前缀。

错误信息均以程序名称（通常为 'make'）作为前缀；或者如果在 Makefile 中发现错误，则显示包含问题的文件名和行号。

在下表中，省略了这些前缀。

- * [foo] 错误 NW
- * [foo] 信号描述

这些错误并不是真正的 make 错误。它们意味着作为配方一部分调用的 make 程序返回了非零代码（'Error NW'），make 将其解释为失败，或者它以其他异常方式（带有信号类型）退出。参见第 49 页第 5.5 节“配方中的错误”。

如果消息后面没有 `***`，说明子进程失败了，但 Makefile 前加了 `-` 特殊字符，因此 make 忽略了该错误。

`'missing separator. Stop.'`（缺少分隔符。停止。）

`'missing separator (did you make TAB instead of 8 spaces)?'`（缺少分隔符（你使用的是 TAB 而不是 8 个空格吗）？）

这意味着 make 无法理解它刚刚读取的 Makefile 行。GNU make 寻找各种分隔符（`;` `=`、配方前缀字符等）来指示它正在解析什么类型的行。此消息意味着它没有找到有效的分符。

导致此信息的常见原因之一是你（可能是你那热心的编辑器，MS-Windows 编辑器就是如此）尝试使用空格而不是制表符来插入配方行。在这种情况下，make 将使用上述错误的第二种形式。记住，配方中的每一行必须以制表符开头（除非使用了 `;RECIPEPREFIX:`，参见第 73 页第 6.4 节[特殊变量]）。参见第 21 页第 4.1 节[规则语法]。

`'recipe commences before first target. Stop.'`（配方在第一个目标之前开始。停止。）

`'missing rule before recipe. Stop.'`（配方之前缺少规则。停止。）

这意味着 Makefile 的开头似乎配方的一部分：它以配方前缀字符开头，并且看起来不是合法的 make 指令（例如变量赋值）。配方必须始终与目标关联。

如果行的第一个空白字符是分号，则生成第二种形式；make 将其解释为你遗漏了规则的“目标：依赖”部分。参见第 21 页第 4.1 节[规则语法]。

`'No rule to make target 'xxx'.'`（没有制作目标 'xxx' 的规则。）
`'No rule to make target 'xxx', needed by 'yyy'.'`（没有制作 'yyy' 需要的目标 'xxx' 的规则。）

这意味着 make 决定需要构建一个目标，但在 Makefile 中没有找到任何如何操作的指令，无论是显式的还是隐式的（包括默认规则数据库中的）。

如果你想构建一个文件，你需要在 Makefile 中添加一条规则，描述如何构建该目标。导致此问题的其他可能来源是 Makefile 中的拼写错误（如果文件名错误）或源码树损坏（如果该文件不应该被构建，而是依赖项）。

`'No targets specified and no makefile. Stop.'`（未指定目标且未找到 make。停止。）
`'No targets. Stop.'`（没有目标。停止。）

前者意味着你没有在命令中提供任何要构建的目标，且 make 找不到任何可读取的 Makefile。后者意味着找到了某个 Makefile，但它不包含任何默认目标也没有命令行指定的目标。GNU make 在这些情况下无作为。参见第 99 页第 9.1 节[指定 Makefile 的参数]。

`'Makefile 'xxx' was not found.'`（未找到 Makefile 'xxx'。）
`'Included makefile 'xxx' was not found.'`（未找到包含的 Makefile 'xxx'。）

未指定的（第一种形式）或（第二种形式） Makefile。

`'warning: overriding recipe for target 'xxx''`（警告：覆盖目标 'xxx' 的配方）
`'warning: ignoring old recipe for target 'xxx'.'`（警告：忽略目标 'xxx' 的旧配方。）

GNU make 允许每个目标指定一个配方（双冒规则除外）。如果你为一个已经定义的目标提供配方，则会发出此警告，且第二个配方将覆盖第一个。参见第 35 页第 4.10 节[一个目标的多个规则]。

`'Circular xxx <- yyy dependency dropped.'`（循环依赖 xxx <- yyy 已被丢弃。）

这意味着 make 检测到依赖图中存在环：在追踪目标 xxx 的依赖项 yyy 及其依赖项后，其中一个依赖 xxx。

`'Recursive variable 'xxx' references itself. Stop.'`（递归变量 'xxx' 引用自身。停止。）

这意味着你定义了一个普通的（递归）make 变量，它在展开时会引用自己 (xxx)。这是不允许的；请使用展开型变量（`:=` 或 `::`）或使用追加运算符（`+=`）。参见第 59 页第 6 章[如何使用变量]。

`'Unminated variable reference. Stop.'`（未终止的变量引用。停止。）

这意味着你在变量或函数引用中忘记提供正确的右括号或大括号。

`'insufficient arguments to function 'xxx'. Stop.'`（函数 'xxx' 参数不足。停止。）

这意味着你没有为该函数提供所需的参数数量。请查看函数的文档获取参数描述。参见第 83 页第 8 章[转换文本的函数]。

## 附录 C：复杂的 Makefile 示例

这是该 GNU 程序的 Makefile。这是一个中等复杂的 Makefile。第一行使用 `#!` 设置以允许 Makefile 被直接执行。

# 你可能添加到 DEFS 中的内容：

- `-DSTC_HEADERS` 如果你有 ANSI C 头文件和库。
- `-DPOSIX` 如果你有 POSIX.1 头头文件和库。
- `-DBSD42` 如果你有 sys/dir.h（除非你使用了 -DPOSIX）、sys/file.h 以及 'struct stat' 中的 st_blocks。
- `-DUSG` 如果你有 System V/ANSI C 字符串和内存函数及头文件，sys/sysmacros.h，没有 valloc，cntnl.h，getcwd，没有 valloc，ndir.h（除非你使用了 -DDIRENT）。
- `-DNO_MEMORY_H` 如果使用了 US 或 STDC_HEADERS 但没有包含 memory.h。
- `-DDIRENT` 如果你拥有 dirent.h 而不是 ndir.h。
- `-DSIGYPE=int` 如果你的信号处理函数返回 int 而不是 void。
- `-DNO_MTIO` 如果你缺少 sys/mtio.h (magntap ioctls)。
- `-DNO_REMOTE` 如果你没有远程 shell 或 resex。
- `-DUSE_REXEC` 使用 resex 进行远程磁带操作，而不是 forking rash 或 remh。
- `-DVPRINT_MISSING` 如果你缺少 fprint 函数（但有 dopprnt）。
- `-DDOPPRINT_MISSING` 如果你缺少 dopprnt 函数。还需要定义 -DVPRINT_MISSING。
- `-DFTIME_MISSING` 如果你缺少 ftime 系统调用。
- `-DSTRSTR_MISSING` 如果你缺少 strstr 函数。
- `-DVALLOC_MISSING` 如果你缺少 valloc 函数。
- `-DMKDIR_MISSING` 如果你缺少 mkdir 和 rmdir 系统调用。
- `-DRENAME_MISSING` 如果你缺少 rename 系统调用。
- `-DFTRUNCATE_MISSING` 如果你缺少 ftruncate 系统调用。
- `-DV7` 用于 Version 7 Unix（已久未测试）。
- `-DEMUL_OPEN3` 如果你缺少 3 参数版本的 open，并想通过你已有的系统调用来模拟它。
- `-DNO_OPEN3` 如果你缺少 3 参数的 open 并且想要禁用 tar -k 选项而不是模拟 open。
- `-DXENIX` 如果你有 sys/inode.h 且需要包含 94。

# 附录 C：复杂的 Makefile 示例

```make

```
