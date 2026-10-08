

## 1542

## 选项

-c 计数字节数。
-C 与 -m 相同。
-l 计数行数。
-m 计数字符数。
-w 计数由空白字符或换行符分隔的单词数。分隔符是来自 `isspace()` 定义的任何编码的扩展 UNIX 代码 (EUC) 字符。

如果不指定任何选项，默认使用 -wc（计数行数、单词数字节数）。

## 操作数

file 输入文件名。如果未指定 `fileoperands`，则使用标准输入。

## 示例

以下示例使用不带选项的 `wc` 命令显示文件 `kookaburra-1` 中的行数、单词数和字符数。

```
castle kookaburra-1
9 47 264 kookaburra-1
cast
```

kookaburra-1 文件包含 99 行、47 个单词和 264 个字符。接下来的示例使用 `wc` 命令显示目录中以 `kook` 开头的所有文件的计数。

```
castle kook*
9 47 264 kookaburra-2
9 47 264 kookaburra-2
18 94 528 total
cast
```

## 用法

参见 `LARGE(5)` 了解 `wc` 在遇到大于或等于 2 Gbytes (31 bytes) 文件时的行为描述。

## 环境变量

参见 `environ(5)` 了解以下影响 `wc` 执行的环境变量描述：`LC_TYPE`、`LC_MESSAGES` 和 `NLPATH`。

## 退出状态

0 成功完成。
>0 发生错误。

## what

## 属性

参见 attributes(5) 了解以下属性的描述：

| 属性类型 | 属性值 |
|---|---|
| Availability | SUNwcs |
| CSI | Enabled |

## 相关

cksum(1), isspace(3), iswalpha(3), isspace(3), setlocale(3), attributes(5), environ(5), largefile(5)

## what — 从文件中提取 SCCS 版本信息

## 概要

/usr/ccs/bin/what [-s] filename...

## 描述

使用 `what` 命令打印源代码控制系统 (SCCS) 文件的标识字符串。`what` 命令搜索每个文件名中出现的模式 @(#，该模式是 SCCS get 命令（如 sccs-get(1)）替换 %Z% ID 关键字的结果，并打印其之后的内容，直到遇到 *、换行符、\ 或空字符。

## 选项

- -s 在首次出现该模式后停止。

## 示例

例如，如果文件 `program.c` 中的 C 程序包含行 `char sccsid[] = "@(#)identification information`，并且 `program.c` 编译生成 program.o 和 a.out，则以下命令将列出 @(#) 之后的字符串。

```
castle% what program.c program.o a.out
program.c:
    identification information
program.o:
    identification information
a.out:
    identification information
castle%
```

以下示例使用 `whatis` 命令列出该命令的所有手册页。

## whence 1545

```
castle% whatis chown
chown (1) - 修改所有所有
chown (1b) - 修改所有者
chown (1m) - 修改所有者
chown (2) - 修改文件的所有者和组
castle%
```

要显示特定章节的手册页，
man -s section-number command

## 文件

```
/usr/share/man/index
```

目录和关键字数据库。

## 属性

参见 attributes(5) 了解以下属性的描述：

| 属性类型 | 属性值 |
| - | - |
| Availability | SUM/Doc |
| CSI | Enabled |

## 相关

- apropos(1), man(1), catman(1M), attributes(5)

## whence — 用于获取/设置 Shell 变量的内置函数

## 概要

```
whence [-pv] name...
```

## 描述

参见 typeset(1)。

## whereis — 定位命令的二进制文件、源码和手册页

## 概要

```
/usr/ucb/whereis [-bmsu] [-BMS directory... -f] filename...
```

## whereis

## 描述

whereis 为指定文件定位源、二进制和手册章节。提供的名称首先删除前导路径名组件以及任何形式为 .ext,.c 的（单个）后缀扩展。由于使用源码控制产生的 s 前缀也会被删除。whereis 然后尝试在标准位置查找所需的程序：

- /usr/bin
- /usr/bin
- /usr/sbin
- /usr/games
- /usr/hosts
- /usr/include
- /usr/local
- /usr/etc
- /usr/lib
- /usr/share/man
- /usr/src
- /usr/ucb

## 选项

- -b 仅搜索二进制文件。
- -B 更改或限制 whereis 搜索二进制文件的地方。
- -f 终止最后一个目录列表并指示文件名开始。你必须与 -B、-M 或 -S 选项配合使用此选项。
- -m 仅搜索手册章节。
- -M 更改或限制 whereis 搜索章节的地方。
- -s 仅搜索源码。
- -S 更改或限制 whereis 搜索源码的地方。
- -u 搜索非常常源码。如果一个文件不具备每个请求类型的条目，则该文件是不寻常的。因此，whereis -u 请求当前目录下没有文档的文件。

## 示例

以下示例找到所有名为 libc 的文件的位置。

```
castle@ whereis libc
libc:/usr/lib/libc.so /usr/lib/libc2.so /usr/lib/libc2.a
/usr/lib/libc.a
castle@
```

以下示例找到 /usr/ucb 中所有在 /usr/src/cmd 中有源码且在 /usr/share/man/man 中未文档的文件。

```
castle@ cd /usr/ucb
castle@ whereis -M /usr/share/man/man1 -S /usr/src/cmd -f
Mail:/usr/ucb/Mail
adplot:/usr/ucb/adplot
arch:/usr/bin/arch /usr/ucb/arch
```

## which

```
atoplot: /usr/ucb/atoplot
basename: /usr/bin/basename /usr/ucb/basename
bgplot: /usr/ucb/bgplot
biff: /usr/ucb/biff
cc: /usr/ucb/cc
chown: /usr/bin/chown /usr/ucb/chown
clear: /usr/bin/clear /usr/ucb/clear
...（未列出的更多行）
castle%
```

## 文件

- /usr/src/*
/usr/(doc,man)/*
/etc, /usr/(lib,bin,ucb,old,new,local)

## 属性

参见 attributes(5) 了解以下属性的描述：

| 属性类型 | 属性值 |
| Availability | SUNwcpu |

## 相关

chdir(2), attributes (5)

## 缺陷

由于它使用了 chdir(2)

## which — 定位命令；显示其路径

## 概要

```
which [filename]
```

## 描述

which 命令打印可执行文件的完整路径。它在 PATH 环境变量中搜索可执行文件并返回找到的。

注意 — 如果文件名是别名，which 将找不到它。

## 示例

以下示例显示 ls 命令的路径。

```
castle% which ls
/usr/bin/ls
```

以下示例显示 grep 命令的路径。

```
castle% which grep
/usr/bin/grep
```

## 文件

- /usr/bin/which

## 属性

参见 attributes(5) 了解以下属性的描述：

| 属性类型 | 属性值 |
| Availability | SUNwcs |

## 相关

attributes(5)

## 退出状态

0 如果找到了可执行文件。
>1 如果未找到可执行文件。

