
# 打印所有未被 getline 读取的行

```awk
# print all lines except read with getline
{
  print "line #", NR, $0
}

# if line begins with "b" process it specially
/^b/
{
  # use getline to read the next line into variable named hold
  getline hold

  # print value of hold
  print "skip this line:", hold

  # $0 is not affected when getline reads into a variable
  # $1 holds previous value
  print "previous line began with:", $1
}

{
  print ">>>> finished processing line #", NR
  print ""
}
```

```bash
$ awk -f g5 < alpha
line # 1 aaaaaaaa
>>>> finished processing line # 1

line # 2 bbbbbbbbb
skip this line: cccccccc
previous line began with: bbbbbbbbbbb
>>>> finished processing line # 3
```

```
line # 4 dddddddd
>>>> finished processing line # 4
```

`NR`，当前的记录行数。尽管 `getline` 在读取到变量时不会改变 `$0`，但 `gawk` 会递增 `NR`。

## $cat g5

```awk
# 打印所有未被 getline 读取的行
{
  print "line #", NR, $0
}

# 如果行以 "b" 开头，则对其进行特殊处理
/^b/
{
  # 使用 getline 将下一行读入名为 hold 的变量
  getline hold

  # 打印 hold 的值
  print "skip this line:", hold

  # 当 getline 读取到变量时，$0 不受影响
  # $1 保持上一个一次的值
  print "previous line began with:", $1
}

{
  print ">>>> finished processing line #", NR
  print ""
}
```

```bash
$ awk -f g5 < alpha
line # 1 aaaaaaaa
>>>> finished processing line # 1

line # 2 bbbbbbbbb
skip this line: cccccccc
previous line began with: bbbbbbbbbbb
>>>> finished processing line # 3
```

```
line # 4 dddddddd
>>>> finished processing line # 4
```

## COPROCESS: TWO-WAY I/O

协进程（Coprocess）是一个与另一个进程并行运行的进程。从 `3.1` 版本开始，`gawk` 可以调用协进程来与后台进程直接交换信息。当你工作在客户端/服务器环境、设置 `SQL (page902)` 前端/后端，或与系统网络交换数据时，协进程会非常有用。`gawk` 语法通过在启动后台进程的进程名称前加上 `|&` 来识别协进程。

协进程命令必须是一个过滤器（即它从标准输入读取并向标准输出写入），并且可以刷新其缓冲区。

# 练习

- 1. 编写一个 `gawk` 程序，为文件中的每一行编号，并将输出发送到标准输出。
- 2. 编写一个 `gawk` 程序，显示第一个字段的字符数，随后显示第一个字段的内容，并将输出发送到标准输出。
- 3. 编写一个 `gawk` 程序，使用 `cars` 文件（第 537 页），显示所有价格超过 5000 美元的汽车，并将输出发送到标准输出。
- 4. 使用 `gawk` 确定 `/etc/termcap` 中包含多少行包含 `vt100` 字符串。使用 `grep` 验证你的答案。

# 高级练习

- 5. 实验使用 `pgawk`。它是做什么的？它有什么用处？
- 6. 编写一个名为 `net_list` 的 `gawk` 程序，从 `www.sobell.com` 上的 `cars` 文件（参见第 558 页的“从网络获取输入”）读取并显示每辆汽车的品牌、型号和价格列表。用 `TAB` 分隔输出字段。
- 7. 扩展练习 6 中开发的 `net_list` 程序，使用 `to_upper`（第 557 页）作为协处理器，仅以大写字母显示汽车品牌列表。每行的型号及后续字段应与其在 `cars` 文件中的显示一致。
- 8. 如何让 `gawk` 能够齐地格式化（即“漂亮打印”）一个 `gawk` 程序文件？（提示：参见 `gawk` man 手页。）

# 第 13 章 sed 编辑器

本章

- 语法 564
- 参数 564
- 选项 564
- 编辑器基础 564
- 地址 565
- 指令 566
- 控制结构 567
- 模式空间和暂存空间 568
- 示例 568

`sed`（流编辑器）工具是一个批处理（非交互式）编辑器。它转换可能来自文件或标准输入的输入流。它经常被用作管道中的过滤器。由于它只对输入进行一次扫描，因此 `sed` 比 `ed` 这样的交互式编辑器更高效。本章描述了 GNU `sed`。

# 语法

`sed` 命令行具有以下语法：

```
sed [-n] program [ file-list ]
sed [-n] -f program-file [ file-list ]
```

`sed` 工具从你在命令行指定的文件或标准输入中获取输入。除非你将 `sed` 的输出重定向到其他地方，否则它将输出到标准输出。

# 参数

`program` 是命令行中的 `sed` 程序。这种格式允许你编写简单、简短的 `sed` 程序，而无需创建单独的程序文件。`program-file` 是包含 `sed` 程序的文件的路径（参见“编辑器基础”）。`file-list` 包含 `sed` 处理的普通文件的路径。这些就是输入文件。当你没有指定文件时，`sed` 从标准输入获取输入。

# 选项

`--file program-file` / `-f program-file`

使 `sed` 从名为 `program-file` 的文件中读取程序，而不是从命令行。你可以在命令行上多次使用此选项。

`--in-place[=suffix]` / `-i [suffix]`

在原地编辑文件。如果没有此选项，`sed` 将其输出发送到标准输出。使用此选项时，`sed` 会用其输出替换它正在处理的文件。当你指定了后缀时，`sed` 会创建一个带有后缀的原始文件的备份。如果你想在原始文件名和后缀之间显示一个点，必须在文件名中包含一个点。

`--help`

总结 `sed` 的用法。

`--quiet` or `--n` / `-n -silent`

使 `sed` 不按照打印 (`p`) 指令或标记指定的例外，不将行复制到标准输出。

# 编辑器基础

一个程序由一个或多行组成，语法如下：

```
[ address , address ] instruction [ argument-list ]
```

地址是可选的。如果你省略了地址，`sed` 处理所有行。指令是修改文本的编辑指令。地址选择命令操作的行。`argument-list` 中的数字和参数取决于指令。如果你想在一行中放置多个 `sed` 命令，可以使用分号 (`;`) 分隔它们。

`sed` 工具处理输入的方式：

1. 从 `file-list` 读取一行输入。
2. 从程序或程序文件读取第一条指令。如果地址选择了输入行，则按照指令对该行进行操作。
3. 从程序或程序文件读取下一条指令。如果地址选择了输入行，则对该行（可能已被之前的指令修改）进行操作。
4. 重复步骤 3，直到执行程序或程序文件中所有的指令。
5. 如果还有另一行输入，则重新从步骤 1 开始；否则，结束。

# 地址

行号是选择某行的地址。作为一个特殊情况，行号 `$` 代表输入的最后一行。

正则表达式（参见附录 A）是选择包含匹配字符串行的地址。虽然使用斜杠来分隔正则表达式，但 `sed` 允许使用除反斜杠或换行符以外的任何字符来实现目的。

除另外，指令前可以跟零、一个或两个地址（行号或正则表达式）。如果不使用地址，`sed` 处理所有行。如果你指定了一个范围，`sed` 选择该范围的行。范围通过逗号 (`,`) 指定。

# 指令

- `delete` (`d`): 删除选定的行。
- `next` (`n`): 跳过当前指令并继续执行下一条。
- `append` (`a`): 在选定的之后追加指定的文本。
- `insert` (`i`): 在选定的之前插入指定的文本。
- `change` (`c`): 将选定的更改更改指定的文本。
- `print` (`p`): 将选定的行打印到标准输出。
- `write` (`w`): 将选定的行写入 `file` 指定的文件。
- `branch` (`b`): 如果满足条件，跳转到指定的地址。
- `execute` (`x`): 在每条选定的行上执行脚本文件。
- `substitute` (`s`): 将指定的模式替换为替换字符串。

# 控制结构

`(NOT)` 导致 `sed` 将位于同一行的后续指令应用到所有未被指令地址部分选中的行行。例如，`3!d` 删除第 3 行以外的所有行，`S2p` 显示除最后一行以外的所有行。

`(分组指令)` 当你将一组指令封装在一对大括号 `{}` 内部时，单个地址（或地址对）将选择该组指令操作的行。使用分号（`;`）分隔出现在同一行中的多个命令。

# 分支指令

`sed` 帮助信息将分支指令列为“`sed` 高级大师的命令”，并建议如果你需要这些指令，使用 `awk` 或 `Perl` 编写程序会更好。

- `+:label` 识别 `sed` 程序中的一个位置。该标签可以用作 `b` 和 `t` 分支指令的目标。
- `b [label]` 无条件地将控制转移（分支）到标签。如果不带标签，则跳过当前输入行的后续指令，并读取下一行输入（第 565 页）。
- `t [label]` 仅当自上次读取输入行以来，替换（`Substitute`）指令执行成功时，才将控制转移（分支）到标签（条件分支）。如果不带标签，则跳过当前输入行的后续指令，并读取下一行输入（第 565 页）。

# 模式空间 (Pattern Space) 和持有空间 (Hold Space)

`sed` 实用有两个缓冲区。到目前为止回顾的命令作用于模式空间，模式空间最初持有 `sed` 刚刚读取的输入行。持有空间可以在你在模式空间中操作数据时存储数据；它是一个临时缓冲区。在将数据放入持有空间之前，它是空的。本节将讨论在模式空间和持有空间之间移动数据的命令。

- `g` | 将持有空间的内容复制到模式空间。模式空间的原始内容将丢失。
- `G` | 在模式空间的末尾追加一个换行符（`NEWLINE`）和持有空间的内容。
- `h` | 将模式空间的内容复制到持有空间。持有空间的原始内容将丢失。
- `H` | 在持有空间的末尾追加一个换行符（`NEWLINE`）和模式空间的内容。
- `x` | 交换模式空间和持有空间的内容。

# 示例

新数据文件。以下示例使用输入文件 `new`：

```
$cat new
Line one.
The second line.
The third.
This is line four.
Five.
This is the sixth sentence.
This is line seven.
Eighth and last.
```

除非你指示它不要这样做，否则 `sed` 会将所有行（无论是否选中）发送到标准输出。当你从命令行使用 `-n` 选项时，`sed` 仅会将某些行（例如由打印 `p` 指令选中的行）发送到标准输出。

以下命令显示 `new` 文件中包含单词 `line`（小写）的所有行。此外，由于没有 `-n` 选项，`sed` 会显示所有输入行。结果是包含单词 `line` 的行被了两次。

```
$sed '/line/ p' new
Line one.
The second line.
The second line.
The third.
This is line four.
This is line four.
Five.
This is the sixth sentence.
This is line seven.
This is line seven.
Eighth and last.
```

该命令使用了地址 `/line/`，这是一个简单字符串的正则表达式。`sed` 实用工具会选择每个包含该模式匹配项的行。打印 `p` 指令显示每个被选中的行。
以下命令使用了 `-n` 选项，以便 `sed` 显示被选中的行：

```
$sed -n '/line/ p'
The second line.
This is line four.
This is line seven.
```

接下来 `sed` 根据行号显示文件的一部分。打印指令选中并显示了第 3 行到第 6 行。

```
$sed -n '3,6 p'
The third.
This is line four.
Five.
This is the sixth sentence.
```

下一条命令行使用退出 `q` 指令，使 `sed` 仅显示文件的开头。在这种情况下，`sed` 显示了 `new` 的前五行，就像执行 `head -5 new` 命令一样。

```
$sed '5 q'
Line one.
The second line.
The third.
This is line four.
Five.
```

# 程序文件 (program-file)

当你需要给 `sed` 提供更复杂或更冗的指令时，可以使用程序文件。`print3_6` 程序的功能与之前示例中的命令行命令相同。`-f` 选项告诉 `sed` 它应该从命令行指定的命名读取程序。

```
$cat print3_6
3,6 p
```

```
$sed -n -f print3_6 new
The third.
This is line four.
Five.
This is the sixth sentence.
```

# 追加 (Append)

下一个程序选择第 2 行并使用追加 `a` 指令在选定之后之后一个换行符和文本 `AFTER.`。由于命令行没有包含 `-n` 选项，`sed` 会复制输入文件 `new` 的所有行。

```
$cat append_demo
2 a\
AFTER.
```

```
$sed -f append_demo new
Line one.
The second line.
AFTER.
The third.
This is line four.
Five.
This is the sixth sentence.
This is line seven.
Eighth and last.
```

# 插入 (Insert)

`insert_demo` 程序选择所有包含字符串 `This/` 的行，并在选定行之前插入一个换行符和文本 `BEFORE.`。

```
$cat insert_demo
/This/ i
BEFORE.
```

```
$sed -f insert_demo new
Line one.
The second line.
The third.
This is line four.
Five.
This is the sixth sentence.
BEFORE.
This is line seven.
Eighth and last.
```

# 更改 (Change)

下一个示例演示了带有地址范围的更改 `c` 指令。当你指定行范围时，它不是更改每一行，而是将该块行更改为单次。

```
$cat change_demo
2,4 c
NEW TEXT
HERE.
```

```
$sed -f change_demo new
Line one.
SED WILL INSERT
THREE LINES IN PLACE
OF THE SELECTED LINES.
Five.
This is the sixth sentence.
This is line seven.
Eighth and last.
```
