

## Shell 程序员有用的 UNIX/Linux 工具

### apropos—搜索 whatis 数据库中的字符串

```
apropos keyword ...
```

apropos 搜索一组数据库文件（参见目录 /usr/man/whatis）中系统命令的简短描述，以查找关键字并将结果显示在标准输出上。与 man -k 相同。

**EXAMPLE A.1**

```
1 $ apropos bash
bash (1)          - GNU Bourne-Again Shell

2 $ man -k tcsh
tcsh (1)         - C shell with filename completion and command-line editing
```

**EXPLANATION**

- 1 apropos 搜索关键字 bash 并打印其简短描述。
- 2 man -k 的行为与 apropos 相同。

### arch—打印机器架构（参见 uname -m）

```
arch
```

在当前的 Linux 系统上，arch 打印诸如 i386、i486、i586、alpha、sparc、arm、m68k、mips 或 ppc 之类的内容。

**EXAMPLE A.2**

```
$ arch
i386
```

### at, batch—在稍后时间执行命令

```
at [-csm] [-f script] [-q queue] time [date] [+ increment]
at -l [ job... ]
at -r job...
batch
```

at 和 batch 从标准输入读取命令以在稍后时间执行。at 允许你指定命令应执行的时间，而使用 batch 排队的作业将在系统负载允许时执行。执行的命令从 stdin 或文件在稍后时间读取。除非重定向，否则输出会发送邮件给用户。

**EXAMPLE A.3**

- 1. `at 6:30am Dec 12 < program`
- 2. `at noon tomorrow < program`
- 3. `at 7:45 pm August 9 < program`
- 4. `at now + 3 hours < program`
- 5. `at 8:30am Jan 4 < program`
- 6. `at -r 8388355320.a`

**EXPLANATION**

- 1. 在 12 月 12 日早上 6:30 开始作业。
- 2. 在明天中午开始作业。
- 3. 在 8 月 9 日晚上 7:45 开始作业。
- 4. 三小时后开始作业。
- 5. 在 1 月 4 日早上 8:30 开始作业。
- 6. 删除先前计划的作业 8388355320.a。

### awk—模式扫描和处理语言

```
awk [ -f program-file ] [ -Fc ] [ prog ] [ parameters ] [ filename... ]
```

awk 扫描每个输入文件名中的行，查找与 prog 中指定的任何一组模式匹配的行。

**EXAMPLE A.4**

### banner—制作海报

banner 在标准输出上以大写字母打印其参数（每个最多 10 个字符）。

**EXAMPLE A.5**

```
banner Happy Birthday
```

**EXPLANATION**

以横幅格式显示字符串 Happy Birthday。

### basename—使用目录名提供路径名的部分

```
basename string [ suffix ]
dirname string
```

basename 从 string 中删除以 /（正斜杠）结尾的任何前缀以及 string 中存在的后缀（如果存在），并将结果打印到标准输出。

**EXAMPLE A.6**

```
1  basename /usr/local/bin
2  scriptname=`basename $0`
```

**EXPLANATION**

- 1. 去掉前缀 /usr/local/ 并显示 bin。
- 2. 将脚本 $0 的名称仅分配给变量 scriptname。

### bash—GNU Bourne Again Shell

```
bash [options] [file[arguments]]
sh [options] [file[arguments]]
```

bash 的版权所有 © 1989、1991 由自由软件基金会，Inc. bash 是一个与 sh 兼容的命令语言解释器，执行从标准输入或文件读取的命令。bash 还包含了 Korn 和 C shell（ksh 和 csh）的有用特性。

### bc—处理精密算术

```
bc [ -c ] [ -l ] [ filename... ]
```

bc 是一个交互式处理器，用于一种类似于 C 的语言，但提供无限精度算术。它先读取给定的任何文件，然后读取标准输入。

**EXAMPLE A.7**

```
1 bc << EOF
scale=3
4.5 + 5.6 / 3
EOF
Output : 6.366
--------------------------
2 bc
ibase=2
5
101 (Output)
20
10100 (Output)
^D
```

**EXPLANATION**

- 1 这是一个 here 文档。从第一个 EOF 到最后一个 EOF，输入都提供给 bc 命令。scale 指定小数点右侧的位数。计算结果显示在屏幕上。
- 2 数字基数为 2。数字被转换为二进制（仅 AT&T）。

### bdiff—比较两个大文件

bdiff 比较两个对于 diff 来说太大而无法处理的文件。

### cal—显示日历

```
cal [ month ] year
```

cal 打印指定年份的日历。如果还指定了月份，则仅打印该月份的日历。如果两者均未指定，则打印当前月份的日历。

**EXAMPLE A.8**

- 1. `cal 1997`
- 2. `cal 5 1978`

**EXPLANATION**

- 1. 打印 1997 年的日历。
- 2. 打印 1978 年 5 月。

### cat—连接并显示文件

```
cat [ -bnsuvet ] filename...
```

