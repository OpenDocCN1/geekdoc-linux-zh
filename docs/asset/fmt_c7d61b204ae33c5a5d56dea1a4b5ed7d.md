
`cut -d - -f4 project | sort | uniq -c | awk '{printf "%s: %s\n",$2,$1}' > pnum`

# 提取 prog_num，输出交给 sort 去重

# 并获取程序/项目的计数。

# 输出文件为程序员编号，后跟计数

3. 按 `Esc` 切换到命令模式。
4. 输入 `wq` 写入文件并退出 `vi`。

## 运行 shell 脚本

你可以在系统上的几乎任何 shell 中运行 shell 脚本。在书中，使用 Bourne Again Shell (`Bash`)，它在 Linux 系统中非常常用。正如你之前学到的，脚本是包含命令的文本文件。在不同的

# 第 5 章 B 节 高级文件处理

在 shell 中，在具体用法、语法以及与命令相关的选项方面往往存在一些不兼容之处。使用 `Bash` shell 的优势在于它比原始的 Bourne shell 接受更多命令结构的变；`Bash` 是 Bourne 和 Korn shell 的免费衍生版本。

当你创建一个要在 `Bash` 中运行的 shell 脚本时，可以通过输入 `sh`（调用 Bash shell 解释器）然后输入脚本名称来立即运行脚本，如下：

```
sh testscript
```

使用 `sh` 的另一个优势是你可以配合几个调试选项来帮助排查脚本中的问题（在第 6 章了解更多关于调试选项）。在本章首次接触 shell 脚本时，你只需使用 `sh` 来运行脚本。

运行 shell 脚本的另一种方法（你将在第 6 章中详细学习）是通过 `x` 权限赋予其可执行权限，然后在运行脚本名称之前输入 `./` 来手动运行脚本。此外，当你编写脚本时，建议指定脚本要使用的 shell。你可以通过在脚本的第一行包含一条语句——例如对于 Bash shell 使用 `#!/bin/bash`——来实现。第 7 章将展示当你的 shell 脚本变得更加高级时如何实现这种做法。

现在，你可以使用 `sh` 命令运行 `pact` 脚本，并使用 `less` 命令显示 `pnum` 的内容。

运行你之前创建的 `pact` 脚本：

- 1. 在 `sh` 命令提示符后，输入 `sh pact` 并按回车。
- 2. 输入 `less pnum` 并按回车，查看由 `pact` 脚本创建的 `pnum` 文件的内容。
- 3. 你会看到这些程序员编号和计数字段：
```
101:1
102:2
103:2
104:1
105:2
106:1
107:1
109:1
110:2
112:1
```
- 4. 如必要，按 `q` 退出文本显示并返回命令行。

![](img/b5f7722b7c2983a215c7726aaada19f9_195_0.png)

现在你有一个包含程序员编号和每个程序员正在进行的项目数量的文件。接下来，创建一个脚本文件 `pname`，以从程序员文件中提取程序员名称和编号，并将输出重定向到文件 `pnn`。

## 运行 shell 脚本

创建另一个脚本文件：

- 1. 在 `$` 命令提示符后，输入 `vi pumname` 并按回车。
- 2. 输入 `a` 切换到插入模式，然后输入以下文本，并在每行结束按回车：

```
=====================================================

# Script Name: pumname

# By: 你的缩写

# Date: Jan 2004

# Purpose: Extract Programmer Numbers and Names

=====================================================

cut -d: -f1-4 programmer | sort -t: +0 -1 | uniq > pnn

# 以上命令截取了第 1 到第 4 个字段。

# 输出通过管道按程序员编号进行排序。

# 排序后的输出通过管道交给 uniq 以去

# 重。

# uniq 将输出重定向到 pnn。
```

- 3. 按 `Esc` 切换到命令模式。
- 4. 输入 `wq` 保存文件并退出 `vi`。
- 5. 运行 shell 程序并使用 `less` 命令显示 `pnn` 的内容，输入 `sh pumname` 并按回车。
- 6. 输入 `less pnn` 并按回车。

- 7. 你看到程序员名称和编号，且消除了重复：
```
101:Johnson:John:K
102:King:Mary:K
103:Brown:Gretchen:K
104:Adams:Betty:C
105:Utley:Amos:V
106:Wilson:Patricia:F
107:Culligan:Thomas:F
108:Mitchell:Hillary:N
109:Arbuckle:Margaret:F
110:Ford:Terrence:H
111:Greene:Sarah:L
112:Rose:Richard:P
113:Daniels:Allan:S
114:Edwards:George:J
```

- 8. 如必要，按 `q` 退出文本显示。

现在你可以创建一个脚本文件 `joinall` 来合并 `pnn` 和 `pumname` 文件，并将输出重定向到 `patrec`。

# 第 5 章 B 节 高级文件处理

创建一个合并两个文件的脚本：

- 1. 在 `$` 命令提示符后，输入 `vi joinall` 并按回车。
- 2. 输入 `a` 切换到插入模式，然后输入以下文本，并在每行结束按回车：

```
=====================================

# Script Name: Joinall

# By: 你的缩写

# Date: Jan 2004

# Purpose: Join pnum and pnn to create a report file

=====================================

# 合并包含未分配程序员的文件。

# 你通过将程序员名称 (pnn) 文件

# 首先放在 join 序列中来实现。

join -t: -al1 -j2 pnum > pactrep

=====================================
```

- 3. 按 `Esc` 切换到命令模式。
- 4. 输入 `wq` 保存文件并退出 `vi`。

- 5. 运行 `joinall` 并使用 `less` 显示 `pactrep` 的内容，输入 `sh joinall` 并按回车。
- 6. 输入 `less pactrep` 并按回车。
- 7. 你看到程序员名称，包括未分配的程序员：
```
101:Johnson:K:1
102:King:Mary:2
103:Brown:Gretchen:2
104:Adams:Betty:1
105:Utley:Amos:2
106:Wilson:Patricia:1
107:Culligan:Thomas:1
108:Mitchell:Hillary:1
109:Arbuckle:Margaret:1
110:Ford:Terrence:2
111:Greene:Sarah:1
112:Rose:Richard:1
113:Daniels:Allan:1
114:Edwards:George:1
```
- 8. 如必要，按 `q` 退出。

# 整合以生成报告

开发应用程序的一种有效方法是将小脚本合并到一个较大的脚本文件中。由于你已经执行了各个脚本并测试了准确性，现在可以将它们按顺序放在一个脚本文件中以生成最终的程序员项目报告。

## 整合以生成报告

使用编辑器创建 shell 脚本 `practity`。使用 `:r` 命令获取 `pact`、`pumname` 和 `joinall` 脚本并将它们放入 `practity` shell 脚本中。然后你可以使用 `dd` 命令删除注释指定的行。

创建一个最终的 shell 脚本：

- 1. 在 `$` 命令提示符后，输入 `vi practity` 并按回车。
- 2. 输入 `a` 切换到插入模式，然后输入以下文本，并在每行结束按回车：

```
#############################################

# Script Name: practity

# By:         你的缩写

# Date:       Jan 2004

# Purpose: Generate Programmer Activity Status Report

#############################################
```

- 3. 按 `Esc` 切换到命令模式。
- 4. 获取三个脚本文件，输入 `:r pact` 并按回车。将光标移动到文件末尾，输入 `:r pumname` 并按回车。将光标移动到文件末尾，输入 `:r joinall` 并按回车。
- 5. 删除指定的行。例如，你可以将光标移动到每个以 `#` 开头的行，然后输入 `dd`。对文件中剩余的注释行执行相同操作。

脚本中应剩下这四行：
