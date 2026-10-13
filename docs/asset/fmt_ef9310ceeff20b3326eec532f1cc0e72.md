
`command`

...

`fi`

```
`test expression`
```
一词指的是可以执行的多种不同类型的测试和比较之一。其中最常见的如表 9.1 所示；更多内容可以在 `test` 的手册页中找到。

# 第 9 小时

| 表达式 | 含义 |
| --- | --- |
| val1 = val2 | 如果单词或引用文本 `val1` 与单词或引用文本 `val2` 相同，则为真 |
| val1 != val2 | 如果单词或引用文本 `val1` 与单词或引用文本 `val2` 不相同，则为真 |
| val1 -gt val2 | 如果项目 `val1` 的数值大于 `val2` 的数值，则为真 |
| val1 -lt val2 | 如果项目 `val1` 的数值小于 `val2` 的数值，则为真 |
| val1 -eq val2 | 如果项目 `val1` 的数值与项目 `val2` 的数值相等，则为真 |
| -e file | 如果文件是某种类型的现有文件名称，则为真 |
| -f file | 如果文件是现有普通文件（不是设备或目录），则为真 |
| -d directory | 如果目录是现有目录名称，则为真 |
| -x command | 如果命令是标记为可执行的现有文件名称，则为真 |

为了说明条件执行，让我们用两种方式修改 `lxprint`。首先，添加几行，使得如果用户提供了经典的 `--help` 作为选项，`lxprint` 会打印帮助信息。然后，让 `lxprint` 在尝试调用 `latex` 或 `dvips` 之前验证文件是否存在。如果文件不存在，`lxprint` 应该显示错误信息。

改进后的 `lxprint` 如列表 9.2 所示。

## 列表 9.2 新旧改进型 lxprint

```
1 #!/bin/sh

2:

3 if [ "$1" = --help ]; then

4 echo lxprint to print files in one easy step.

5 echo Just supply the name of a .tex file as an argument!

6 exit 0

7 fi

8:

9 LATEXFILE="$1"

10:

11 if [ -f "$LATEXFILE" ]; then

12 DVFILE="${LATEXFILE} | sed 's/.tex$/dvi/'

13:

14 latex "$LATEXFILE"

15 dvips "$DVFILE"
```

## 运用 Shell 的力量

## 列表 9.2 续

```
16: else

17: echo 'There doesn't seem to be a file called $LATFILE.'

18: exit 1

19: fi
```

此列表包含两个条件语句。第一个从第 2 行开始到第 7 行结束，检查用户提供的参数是否确实是 `--help` 单词。如果是，则显示帮助信息。第二个条件语句从第 11 行开始并持续到第 19 行，检查用户请求格式化并打印的文件是否存在。如果文件存在，则开始格式化和打印。如果文件不存在，则打印错误信息。

### 为什么某些行被缩进了？

在脚本中，为每一层新嵌套缩进空格是传统做法。然而，在复杂的 `if...then` 条件语句中，缩进并不是强制的。如果是 `if...then` 语句，缩进可以使视觉上更容易理解脚本是如何运行的。

注意还引入了一个最后的命令。`exit` 命令可以退出脚本并返回命令提示符。它接受一个参数，状态，如果脚本正常退出，该状态应为零；如果脚本是因为遇到问题而退出，则状态为非零。

让我们尝试两个新的脚本块，首先通过参数 `--help` 调用 `lprint`，然后用一个不存在的文件名调用它：
```
[you@workstation20~$ lprint --help
Use lprint to print out a ~tex file in one extra step.
Just supply the name of a ~tex file as an argument!
[you@workstation20~$ lprint nosuchfile.tex
There doesn't seem to be a file called nosuchfile.tex.
[you@workstation20~$
```

改进后的 `lxprint` 已经具有功能，`lprint` 命令也得到了进一步改进。

## 反复测试

第 9 小时

测试（Testing Over and Again）在 shell 脚本中条件执行的类型，`if...then` 语句遵循这种格式：

```
while [ test expression ]; do

  command

  command

done
```

`if...then` 和 `while...do` 的区别在于，在前一种情况下条件为真时执行一次，而在后一种情况下只要条件为真，就会反复执行。在发布多个文档时，例如，一个大型项目 `@projections` 可以被拆分为以数字结尾的文件：

- `@projections1.tex`
- `@projections2.tex`
- `@projections3.tex`

这将允许 `lxprint` 接受像 `@projections` 这样的基础名称，并智能地按顺序打印文件。一个循环语句和更多的条件语句很容易实现。结果所示 9.3。

## 列表 9.3 整合序列的 lxprint 命令

```
#!/bin/sh

# 如果用户使用 --help 作为参数，

# 我们显示帮助信息。

if [ "$1" = --help ]; then

  echo lxprint to print files in one easy step.

  echo Just supply the name of a .tex file as an argument!

  exit 0

fi

LATEXFILE="$1"

# 作为参数的文件名，

# 查看它是否存在，

if [ -f "$LATEXFILE" ]; then

  DVFILE="${LATEXFILE} | sed 's/.tex$/dvi/'

  latex "$LATEXFILE"

  dvips "$DVFILE"

  # 如果文件不存在，

  # 我们显示错误信息。

else

  echo "There doesn't seem to be a file called $LATFILE."

  exit 1

fi

# 变量 COUNTER 将持有当前的

# 我们打印的序列。我们将从

# 1 开始每次使用 expr 将其加1

# 打印另一个文件。

COUNTER=1

while [ -f "$LATFILE$COUNTER.tex" ]; do

  echo "Printing $LATFILE$COUNTER.tex"

  latex "$LATFILE$COUNTER.tex"

  dvips "$LATFILE$COUNTER.dvi"

  COUNTER=$(expr $COUNTER + 1)

done
```

`lxprint` 的执行变得越来越复杂。现在当 `lxprint` 启动时，它会在第 6-12 行检查用户是否发送了 `--help` 作为参数。如果不是如此，它会检查第 18 行用户是否提供了有效文件名；如果是，则在第 19-22 行进行格式化和打印。如果参数无效，`lxprint` 会检查它是否是 `@projections` 这样的基础名称，然后智能地按顺序打印文件。一个循环语句和更多的条件语句很容易实现。结果所示 9.3。

花时间研究一下脚本、`expr` 的用法以及命令和变量替换。起初可能看起来很困难，但你最终将能够按照其编写的方式跟踪脚本流程。

### 重复执行预定义集合

虽然 `if..then` 和 `while..do` 语句通过执行测试并根据结果做出判断来工作，但另一个语句 `for..do` 语句会对列表中的每个元素执行一组命令。例如，`for..do` 循环为对长文件列表中的每个文件执行相同的操作提供了理想的功能。其语法如下：

```
for var in item1 item2 item3 ... do

command

command

...

done
```

`for..do` 语句将值 `item1` 赋值给 变量 `var` 并执行语句内部的命令。在到达 `done` 后，它将值 `item2` 赋值给该变量并再次执行语句内部的命令。此过程一直持续直到没有更多项目。

让我们通过增强 `lxprint` 命令的功能来演示 `for..do` 循环的使用——如果用户提供 `--all` 作为参数或选项，则打印用户工作目录下的每一个 .tex 文件。这可以通过一个位置良好的 `for..do` 语句轻松实现。更新后的最终 latex 代码如列表 9.4 所示。

## 列表 9.4 添加了 --all 功能的 lxprint 命令

```
1: #!/bin/sh

2:
```
