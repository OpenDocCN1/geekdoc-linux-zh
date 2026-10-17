
此脚本输出修改后的行，紧接着输出原始行（原始行未被替换命令修改）。

## 总结

虽然本章仅触及了 `sed` 处理文本的表面，但你已经看到了这个小工具的威力。本章快速回顾了正则表达式及其在 `sed` 中的用法，以及数值和基于模式范围的使用。你回顾了一些最常用的 `sed` 命令，包括替换、打印、删除和转换。章节最后对保留缓冲区进行了简要讨论，它赋予了 `sed` 记忆能力。

# 实用单行命令

### 输出文件的前 10 行（类似于 'head'）
```bash
sed 10q file.txt
```

### 输出文件的双倍间距版本
```bash
sed 'G' file.txt
```

### 输出文件的行数
```bash
sed -n '=$' file.txt
```

### 输出文件的最后一行
```bash
sed '$!d' file.txt
```

### 输出长度大于 30 个字符的行
```bash
sed -n '/.\{30}/p' file.txt
```

### 输出非空行
```bash
sed '/^$/' file.txt
```

### 删除文件开头所有的空行
```bash
sed './,$!d' file.txt
```

# 参考

“On the Early History and Impact of Unix Tools to Build the Tools for a New Millennium,” 出自 *Netizens: An Anthology*, 作者为 Ronda 和 Michael Hauben，1996 年6 月 12 日。访问 `http://www.columbia.edu/~rh120/ch001j,c11`。
“Sed... The Stream Editor” 访问 `http://www.cornerstonemag.com/sed`.

# 使用 awk 进行文本处理

- 本章内容
- `awk` 简介
- 简单的 `awk` 脚本编写
- `awk` 中的复杂应用
- `awk` 中的条件和循环结构
- `awk` 内置函数

## 引言

`awk` 编程语言是一种脚本语言，可以用于从非常简单的单行应用到大型应用程序的各种场景。`awk` 是一门通用语言，但在它最初的任务——文本处理方面表现得出色。本章将带您领览 `awk` 编程语言，通过大量示例阐明开发者可以如何使用它。`awk` 接手了 `sed` 未完成的工作，但二者各有千秋的优势。

# 简史

`awk` 的第一个版本于 1977 年由 Alfred Aho、Peter Weinberger 和 Brian Kernighan 发布（它的名字是这三位作者名字首字母的组合）。它的第一次集成是到第 7 版 AT&T UNIX 中（因为当时这三位创建者都在贝尔实验室工作）。`awk` 在其生命周期中经历了各种变化。它的语法和表示法既借鉴了 `shell` 脚本语言，也借鉴了 `C` 语言。

# 464 GNU/Linux 应用程序编程

# awk 结构

`awk` 程序的高级结构在概念上非常简单（见图 24.1）。

```bash
awk ' BEGIN {

  pattern { actions }

  ...

 END { }

 }' <filenames>
```

图 24.1 `awk` 程序的结构。

`awk` 程序的结构可以分为三部分。`BEGIN` 部分在从输入文件（s）中读取第一行之前执行，`END` 部分在处理完输入文件（s）的最后一行 之后执行。在可选的 `BEGIN` 和 `END` 部分之间是 `awk` 的模式/动作（pattern/action）部分。对于指定的每个输入文件，每个模式都会按顺序进行比较，如果模式匹配成功，则执行与其相关的动作。

本章将对 `awk` 的讨论分为两个部分。在第一部分，你将查看可以在命令行中指定的简单 `awk` 程序，然后你将学习构建更复杂的 `awk` 程序用于脚本编写。

# 命令行 awk

你可以从查看一些展示其行为的简单 `awk` 脚本开始。你使用文件 `missiles.txt` 中的下述数据（该文件包含有关冷战核武器投送平台的数据）。这些数据（列表 24.1）以 `:` 分隔，包含五个字段（文件名、长度、重量、范围和速度）。

列表 24.1 用于 `awk` 脚本的导弹数据（这些信息也可以在战略航空司令部网站 `http://www.strategic-air-command.com` 以及光盘-ROM 上的 `./source/missiles.txt` 查看）

```bash
Thor:65:109330:1725:10250

Snark:67:48147:6325:650
```

# 第 24 章 使用 awk 进行文本处理 465

```
Jupiter:55:110000:1976:9022
Atlas:75:260000:6300:17500
Titan:98:221500:6300:15000
Minuteman III:56:65000:6300:15000
Peacekeeper:71:195000:6000:15000
```

你可以像 `sed` 一样通过输出行，但将搜索表达式作为模式，并将 `print` 命令作为动作：

```bash
# awk '/Thor/{print}' missiles.txt

Thor:65:109330:1725:10250
```

如果没有模式，你只需输出整个文件：

```bash
# awk '{print}' missiles.txt

Thor:65:109330:1725:10250

Snark:67:48147:6325:650

Jupiter:55:110000:1976:9022

Atlas:75:260000:6300:17500

Titan:98:221500:6300:15000

Minuteman III:56:65000:6300:15000

Peacekeeper:71:195000:6000:15000
```

与其输出整行，不如你可以输出选定的字段。`awk` 会自动将行（亦称为记录）拆分为由冒号分隔的字段。因此，如果你想输出 Thor 导弹的行和范围，可以如下操作：

```bash
# awk -F:/Thor/{print $1 ": $5}' missiles.txt

Thor:10250
```

注意，你通过 `-F` 命令行选项指定了分隔符。每个字段都被解析为一个 `$` 变量。第一个字段定义为 `$1`，第二个定义为 `$2`，以此此类推。整个记录被定义为 `$0`。
你可以简单地在 `print` 命令中包含更多文本来使你的输出更合理（该命令实际上是一行）：

```bash
# awk -F:/Thor/{print "Missile " $1 " has a range of " $5 miles"}' missiles.txt

Missile Thor has a range of 10250 miles
```

在数据上进行进行算术运算也是可能的。考虑这个示例，它输出了范围在 12000 或以上的导弹：

```bash
# awk -F:'$5 >12000 { print $1 } missiles.txt

Atlas

Titan

Minuteman III

Peacekeeper
```

在这个示例中，你的模式是测试 `$5`（范围字段）是否大于 12000。当此测试满足时，你的动作是输出第一个字段（导弹名称）。
`awk` 提供了许多非常有用的内置变量。例如，如果你想知道记录数，可以使用带有内置变量（记录数）的可选 `END` 部分：

```bash
# awk 'END { print NR } missiles.txt
```

注意，你在最后输出了 `NR`，因此它是文件中记录的总数。如果你在每行都输出 `NR`，那么它就是该行的行号，例如：

```bash
# awk -F:'{ print NR, $0 } missiles.txt

1 Thor:65:109330:1725:10250

2 Snark:67:48147:6325:650

3 Jupiter:55:110000:1976:9022

4 Atlas:75:260000:6300:17500

5 Titan:98:221500:6300:15000

6 Minuteman III:56:65000:6300:15000

7 Peacekeeper:71:195000:6000:15000
```

你可以以 `sed` 相同的方式输出，但包含一个搜索表达式作为模式，并将 `print` 命令作为动作：

```bash
# awk '/print}' missiles.txt

Thor:65:109330:1725:10250

Snark:67:48147:6325:650

Jupiter:55:110000:1976:9022

Atlas:75:260000:6300:17500

Titan:98:221500:6300:15000

Minuteman III:56:65000:6300:15000

Peacekeeper:71:195000:6000:15000
```

如果没有模式，你只需输出整个文件：

```bash
# awk '{print}' missiles.txt

Thor:65:109330:1725:10250

Snark:67:48147:6325:650

Jupiter:55:110000:1976:9022
