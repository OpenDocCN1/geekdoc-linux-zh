
`foreach_1` 脚本调用另一个名为 `command` 的程序，其命令行参数保证包含 2 个参数。如果调用 `foreach_1` 时参数少于 20 个，它将用零填充命令行，以完成 `command` 所需的 20 个参数。提供超过 20 个参数会导致其显示用法信息并返回错误状态 1。

`foreach` 结构遍历每个命令行参数对应的命令。每次循环时，`foreach` 将命令行中的下一个参数值赋值给变量 `argument`。脚本将这些值中的每一个赋值给 `buffer` 的一个元素。变量 `count` 维护缓冲区数组的索引。使用后置运算符 `@ count++` 增加计数。`exec` 内置命令（bash 和 tcsh；第 491 页）调用 `command` 而不会启动新进程。（一旦调用 command，运行例程的进程就不再需要，因此不需要新进程）

# while

`while` 结构的语法

```bash
while (expression)
  commands
end
```

只要表达式为真，该结构就会持续循环执行命令。如果表达式在第一次求值时为假，则该结构永远不会执行命令。

```bash
tcsh $ cat while_1

#!/bin/tcsh

# while 控制结构的演示。

# 此例程计算 1 到 n 之间的数字和，
# n 是命令行上的第一个参数。
#

set limit = $argv[1]
set index = 1
set sum = 0

#

while ($index <= $limit)
  @ sum += $index
  @ index++
end

#

echo "The sum is $sum"
```

此程序计算包含 n 在内的所有整数之和，其中 n 是行首参数。`+=` 运算符将 `sum + index` 的值赋值给 `sum`。

# break and continue

你可以使用 `break` 或 `continue` 语句中断 `foreach` 或 `while` 结构。这些语句在转移控制权之前会执行行内的剩余命令。`break` 语句将控制转移到 `end` 语句，终止循环执行。`continue` 语句将控制转移到 `end` 语句，继续执行循环。

# switch

`switch` 结构类似于 bash 的 `case` 结构（第 459 页）：

```bash
switch ( test-string )
  case pattern:
    commands
    breaksw

  case pattern:
    commands
    breaksw

  ...

  default:
    commands
    breaksw

endsw
```

`breaksw` 语句将控制转移到 `endsw` 语句之后的语句。如果省略了 `break`，控制权将回落到下一个命令。你可以在 `pattern` 中使用表 11-2 中列出的任何特殊字符，但管道符号 (`|`) 除外。

```bash
tcsh $ cat switch_1

#!/bin/tcsh

# switch 控制结构的演示
# 此例程测试第一个命令行参数
# 是否为大写或小写任意组合的
# yes 或 no。
#

# 测试 argv[1] 是否存在
if ($#argv != 1) then
    echo "Usage: switch_1 [yes|no]"
    exit 1
else
# argv[1] 存在，根据其值设置 switch
    switch ($argv[1])
    # YES 的情况
        case [yY][eE][sS]:
            echo "Argument one is yes."
            breaksw

    # NO 的情况
        case [nN][oO]:
            echo "Argument one is no."
            breaksw

    # 默认情况
        default:
            echo "Argument one is neither."
            breaksw

    endsw
endif
```

# Builtins（内置命令）

内置命令是 shell 的一部分。当你输入命令时，它要么是 shell 内置命令，要么是可执行程序。如果是内置命令，shell 会直接执行它，而无需搜索路径。

下表描述了 tcsh 可用的内置命令。

| Builtin | Function |
| :--- | :--- |
| `%job` | `fg` 的别名。该作业是要带到前台的任务 (272)。 |
| `%job` | `bg` 的别名。该作业是将放入后台的任务 (273)。 |
| `@` | 类似于 `echo`，但不会显示参数之间的空格。参阅“数值变量” (358)。 |
| `alias` | 创建并显示别名 (347)。 |
| `hashstat` | 报告 tcsh 哈希机制的效率。 |
| `bg` | 将挂起的任务移到后台 (273)。 |
| `bindkey` | 控制按键映射。 |
| `bindkey` | 不带任何参数时，`bindkey` 列出所有可用按键 (353)。 |
| `bindkey -l` | 列出所有可用命令及简短描述 (353)。 |
| `bindkey -e` | 将行编辑器置于 emacs 模式 (353)。 |
| `bindkey -v` | 将行编辑器置于 vi 模式 (353)。 |
| `bindkey` | 将编辑器绑定命令。 |
| `cd` 或 `chdir` | 工作目录 (82)。 |
| `dirs` | 显示目录栈 (274)。 |
| `echo` | 显示其参数。你可以使用 `-n` 选项 (361) 或在末尾使用 `-x` (487) 来防止 `echo` 在行尾显示换行符。 |
| `eval` | 扫描并评估命令。当你在命令前加上 `eval` 时，该命令会被扫描两次。 |
| `exec` | 在同一个 shell 中用另一个程序覆盖当前执行的程序 (491)。 |
| `exit` | 退出 Tc Shell。如果后面跟着数字，`tcsh` 将该数字作为退出状态返回 (479)。 |
| `fg` | 将任务移到前台 (271)。 |
| `glob` | 类似于 `echo`，但不会显示参数之间的空格。 |
| `history` | 显示最近命令的列表 (344)。 |

- `jobs`: 显示作业列表（暂停的命令和后台运行的命令）。
- `kill`: 终止作业或进程（第 497 页）。
- `limit`: 限制当前进程及其创建的任何进程使用的计算机资源。你可以对进程可以使用的 CPU 时间、进程可以创建的文件的大小等进行限制。
- `log`: 立即产生 watch shell 变量（第 365 页）通常每 10 分钟才会产生的报告。
- `login`: 登录用户。后面可以跟用户名。
- `logout`: 如果你在使用原始（登录）shell，则结束会话。
- `ls-F`: 与 `ls-F` 类似但速度更快。（此内置命令字符是不带任何空格的 `ls-F` 字符。）
- `nice`: 降低命令或 shell 的处理优先级。如果你想运行一个对系统有很大需求且不需要立即获得输出的命令，这个命令非常有用。如果你是超级用户（Superuser），可以使用 `nice` 提高命令的优先级。关于 `nice` 以及 bash 提供的 `nice` 程序的更多信息，请参阅第 734 页。
- `nohup`: 允许你在退出时不终止在后台运行的进程。某些系统被设置为自动执行此操作。关于 `nohup` 以及 bash 提供的 `nohup` 程序的信息，请参阅第 736 页。
- `notify`: 当你的作业状态发生变化时，让 shell 通知你（第 271 页）。
- `onintr`: 控制脚本内部发生中断何时，请参阅第 493 页的“trap: Catches a Signal”以获取 bash 中的等效命令。
- `popd`: 从目录栈中移除一个目录（第 274 页）。
- `printenv`: 显示所有的环境变量名称和值。
- `pushd`: 更改工作目录并将新目录放在目录栈的最顶（第 274 页）。
- `rehash`: 重新创建由哈希机制使用的内部表。每当调用 `tcsh` 的新实例时，哈希机制都会根据 `path` 的值创建一个所有可用命令的排序列表。当你向 `path` 中的某个目录添加命令后，使用 `rehash` 重新创建命令的排序列表。如果不这样做，`tcsh` 可能无法找到新命令。另请参阅 `hashstat`（第 379 页）和 `unhash`（第 381 页）。
- `repeat`: 接受两个参数——计数和简单命令（不带管道或命令列表）——按计数指定的次数重复命令。
- `sched`: 在指定时间执行命令。例如，以下命令会让 shell 在上午 10 点打印消息 `Dental appointment.`：
```
$ tsch s sched 10:00 echo "Dental appointment."
```
在没有任何参数的情况下，`sched` 会打印已计划命令的列表。当执行时间到达时，`tcsh` 会显示提示符之前执行命令。
- `set`: 声明、初始化并显示局部变量（第 355 页）。
- `setenv`: 声明、初始化并显示环境变量（第 355 页）。
- `shift`: 类似于 `bash shift` 内置命令（第 483 页）。在没有参数的情况下，`shift` 提升 `argv` 数组的索引。你可以配合数组名使用它对该数组执行操作。
- `source`: 执行作为参数提供的脚本：`source` 不派生另一个进程。它类似于 `bash .`（点）内置命令（第 259 页）。`source` 内置命令扩展了 TC shell，因此脚本中不需要开头的 `#!`。当前 shell 执行 `source`，以便脚本可以更改影响当前 shell 的命令（如 `set`）。在你对 `tcshrc` 或 `.login` 文件进行更改后，你可以使用 `source` 从 shell 执行它，从而将其应用。
- `stop`: 停止后台运行的作业。`stop` 内置命令接受多个参数。
- `suspend`: 停止当前 shell 并放入后台。`suspend` 类似于中断键，它会停止正在后台运行的作业。
- `time`: 执行你作为参数提供的命令。在没有参数的情况下，`time` 显示关于 shell 的信息。当你通过中断键中断它时，`tcsh` 在显示提示符之前执行它。
- `where`: 给定命令名称作为参数时，报告它是别名、内置命令还是路径中的可执行程序。
- `which`: 与 `where` 类似，它只报告命令的某处位置。

## 章节总结

`tcsh` 基于 C Shell，包含了历史、别名和作业控制等常用功能。你可能喜欢使用 `tcsh` 作为交互式 shell，特别是如果你熟悉 `bash`。Bourne Shell 既是命令解释器也是编程语言。C Shell 在加州大学伯克利分校开发，包含了历史功能。

## setenv

由于 `tcsh` 中没有 `export` 命令，你必须使用 `setenv` 创建环境变量（全局变量）。数值和非数值变量都使用 `set` 赋值。`unset` 命令移除局部变量，而 `unsetenv` 命令仅移除环境变量。

## Aliases

`tcsh alias` 的语法与 `bash` 中的 `alias` 略有不同。与不同，`tcsh alias` 允许使用历史替换命令行。大多数其他 `tcsh` 功能（如历史、单词补全和命令行编辑）与之对应。控制结构的语法略有不同，但提供了相应的功能。

## Globbing

Globbing 一词源自原始 Bourne Shell，是指指定字符（如 `*` 和 `?`）匹配文件名。如果 `tsch` 无法生成匹配模式的文件列表，它会显示错误消息。这与 `bash` 的行为形成对比，后者直接保留模式。标准输入和输出可以重定向到 `tcsh`，但没有简单的方法可以独立重定向它们。这需要创建一个子 shell 将标准输出重定向到文件，同时让标准错误对进程可用。

## 练习

1. 假设你正在处理以下历史列表：

```
37 mail alex
38 cd /home/jenny/correspondence/business/cheese_co
39 less letter.0321
40 vim letter.0321
41 cp letter.0321 letter.0325
42 grep hansen letter.0325
43 vim letter.0325
44 lpr letter*
45 cd ../milk_co
46 pwd
47 vim wilson.0321 wilson.0329
```

使用历史机制给出命令以：

a. 向 Alex 发送邮件。
b. 使用 `vim` 编辑名为 `wilson.0329` 的文件。
c. 将 `wilson.0329` 发送到打印机。
d. 将 `wilson.0321` 和 `wilson.0329` 发送到打印机。

2. 如何显示当前有效的别名？编写一个名为 `homedots` 的别名，列出你主目录下所有隐藏文件（仅名称）。

3. 当你在后台启动命令时，如何防止该命令将输出发送到终端？如果你在前台启动了一个命令，稍后决定让它在后台运行，你该怎么办？

4. 你可以在 `~/.tshrc` 中写入什么语句，以防止在重定向输出时不意外覆盖文件？你该如何覆盖这一功能？

5. 假设工作目录包含以下文件：

```
adams.ltr.03
adams.brief
adams.ltr.07
abelson.09
abelson.brief
anthony.073
anthony.brief
azevedo.99
```

在输入以下命令后按下 TAB 键，会发生什么？

- a. `less adams.l`
- b. `cat a`
- c. `ls ant`
- d. `file az`

在输入以下命令后按下 CONTROL-D，会发生什么？

- e. `ls ab`
- f. `less a`

6. 编写一个名为 `backup` 的别名（`alias`），它接受文件名作为参数，并创建一个与该文件名相同但扩展名为 `.bak` 的副本。

7. 编写一个名为 `qmake`（quiet make）的别名，它运行 `make`，并将标准输出和标准错误均重定向到名为 `make.log` 的文件中。`qmake` 命令应该接受与 `make` 相同的选项和参数。

8. 如何让 `tsch` 始终在提示符中显示工作目录的路径？

## 进阶练习

9. 要将 Bourne Again 脚本 `command_menu`（第 462 页）转换为 TC Shell 脚本，需要修改哪些行？进行修改并验证新脚本是否可以工作。

10. 用户通常认为 `rm`（甚至 `rm -i`）太不留情，因为会不可恢复地删除文件。创建一个名为 `delete` 的别名，将其参数的文件移动到 `~/.trash` 目录。创建第二个名为 `undelete` 的别名，将文件从 `~/.trash` 目录移动到工作目录。在你的 `~/.logout` 中创建以下行：

```
/bin/rm -f $HOME/.trash/* > /dev/null
```

解释如果将以下行放在你的 `~/.logout` 中，会有什么不同：

```
rm $HOME/.trash/*
```

11. 修改 `foreach_l` 脚本（第 374 页），使其接受要 `exec` 的命令作为参数。

12. 重写程序 `while_1`（第 375 页），使其运行得更快。使用内置命令 `time` 来验证执行时间上的改进。

13. 编写你自己的 `find` 版本命名为 `myfind`，它将输出写入文件 `findout`，但不要包含杂乱的错误信息（例如当你没有权限搜索某个目录时产生的错误）。`myfind` 命令应该接受与 `find` 相同的选项和参数。你能想到任何一种 `myfind` 无法按预期工作的情况吗？

14. 当给 `foreach_l` 脚本（第 374 页）提供的参数为 20 个或少一时，为什么接下来的命令没有执行？（为什么没有 `exit` 命令？）

![](img/bf98da8888128a6a4235ca4c80ee1f24_504_0.png)

## 第四部分：编程工具

- 第 10 章 编程工具
- 第 11 章 编程 Bourne Again Shell
- 第 12 章 gawk 模式处理语言
- 第 13 章 sed 编辑器

## 第 10 章 编程工具

本章内容

- 在 C388 中编程
- 使用共享库 396
- `make`: 保持程序集更新 399
- 调试 C 程序 407
- 线程 417
- 系统调用 417
- 源代码管理 420
- CVS: 并发版本系统 420

Linux 操作系统凭借其丰富的语言和开发工具，为编程提供了一个卓越的环境。C 语言是与 Linux 结合使用的最流行的系统编程语言之一，部分原因是因为操作系统本身大部分是用 C 语言编写的。本章将解释如何编译和链接。

### 使用 C 语言编程

在本章中，我们将探索 Linux 操作系统如何提供一个卓越的编程环境。C 语言是与 Linux 结合使用的最流行的系统编程语言之一，部分原因是因为操作系统本身大部分是用 C 语言编写的。本章将解释如何编译和链接。

### 检查你的编译器

要检查你是否有权限访问 `gcc`，请执行以下命令：

```bash
$ gcc --version
bash: gcc: not found
```
