
```
#!/bin/sh

# remindme - 在数据文件中搜索匹配行，或者在未指定参数的情况下
# 显示数据文件的全部内容

rememberfile="$HOME/.remember"

if [ $# -eq 0 ]; then
more $rememberfile
else
grep -i "$@" $rememberfile | $(PAGER:-more)
fi

exit 0
```

## 运行脚本

要使用 `remindme` 实用工具，首先使用 `remember` 脚本将笔记、电话号码或其他任何内容添加到 `rememberfile` 中。然后使用 `remindme` 搜索这个自由格式数据库，可以根据需要指定长或短的模式。

## 结果

```
$ remember
Enter note, with ^D:
The Boulder Community Network: http://bcn.boulder.co.us/
^D
```

然后，当我在几个月后想要记起那条笔记时：

```
$ remindme boulder
The Boulder Community Network: http://bcn.boulder.co.us/
```

或者如果我需要其中可能存在的任何其他数据：

```
$ remindme 800
Southwest Airlines: 800-IFLYSNA
```

## 破解脚本

虽然这绝对不是任何类型的 shell 脚本编程的杰作，但这些脚本几乎展示了 Unix 命令行难以惊的扩展性。如果你能想象出某种东西，那么很有可能有一种简单而直接的方法来实现它。

这些脚本可以从许多方面进行改进。例如，你可以创建一个记录的记录，每条记录都有时间戳，并且多行输入被保存为一个单一实体。

# 24 交互式计算器

## 代码

```
#!/bin/sh

# calc - 一个基于命令行的交互式计算器。

show_help() {
cat << EOF
Usage: calc [options] [expression]

Options:
  -h    显示帮助信息
  -s    设置精度（小数位数）

Examples:
  calc "150 / 3.5"
  calc -s 4 "sqrt(2)"
EOF
}

scale=2
while [ $# -gt 0 ]; do
  case $1 in
    -h) show_help; exit 0 ;;
    -s) scale=$2; shift ;;
    *) echo "未知选项: $1"; exit 1 ;;
  esac
done

if [ $# -gt 0 ]; then
  scale=$scale
  echo "$*" | bc
  exit 0
fi

while true
echo "calc> "
show_help
...
```

## 工作原理

这里并没有真正复杂的逻辑。代码中最有趣的部分可能是 `while` 语句，它创建了一个无限循环显示 `calc>` 提示符，直到用户通过文件结束序列 `^` 退出。而且，这个脚本的简单性正是它奇妙之处。

## 运行脚本

此脚本默认运行时是一个提示用户操作的交互式工具。如果带有参数调用，这些参数将传递给 `bc` 命令。

## 结果

```
$ calc 150 / 3.5
42.85
$ calc
Calc - 一个简单的计算器。输入 'help' 查看帮助，输入 'quit' 退出。
calc> help
Usage: calc [options] [expression]

Options:
  -h    显示帮助信息
  -s    设置精度（小数位数）

Examples:
  calc "150 / 3.5"
  calc -s 4 "sqrt(2)"
calc> 53534 ^3
160588137553864
calc> quit
$
```

# 25 单词拼检查

StarOffice、OpenOffice.org 和 Microsoft Word 等高级程序内置了拼写检查软件，但更基础的判断单词拼写是否正确的问题超出了这些应用程序的能力范围。

同样，大多数 Unix 使用效果良好的拼写检查包，尽管界面粗陋。给定一个输入文件或数据流，这些包会生成所有可能的拼写错误列表。某些拼写检查包包含交互式拼写检查应用程序。再次，它们都没有提供一种简单的检查单个单词拼写的方法。

## 没有安装拼写检查程序？

对于那些没有安装 `spell` 软件包的 Unix 发行版——尽管实际上，考虑到现在磁盘空间如此廉价，所有发行版现在都应该有——一个极的选择是安装 `ispell`，

http://fmg-www.cs.ucla.edu/geoff/ispell.html

## 代码

```
#!/bin/sh

# spellchecking - 检查单词的拼写情况。

spell="ispell -l"                # 如果你安装了 ispell
                                     # 如果没有，只需定义 spell=aspell
                                     # 等效即可

if [ $$ -lt 1 ]; then
  echo "Usage: $0 word or words" >&2; exit 1
fi

for word
do
  if [ -z "$(echo $word | $spell) ]; then
    echo "$word:          spelled correctly."
  else
    echo "$word:          misspelled."
  fi
done

exit 0
```

## 运行脚本

要使用此脚本，只需将一个或多个单词作为 `checkspelling` 命令的参数指定即可。

## 结果

很容易确定 "their" 的正确拼写方式：

```
$ checkspelling thier
thier:          misspelled.
thier:          spelled correctly.
```

## 编写脚本

使用拼写检查工具可以做很多事情，而且重要的是，`ispell` 已经可以完成相当多的工作。这只是谚喻中的冰山一角，正如你将在下一个脚本中看到的。

# 26 Spell: 一个交互式拼写检查工具

检查单个单词的拼写是有用的，但更常见的是，你可能想批量检查文件中所有的单词。如果你安装了 `ispell`，可以做到这一点，但 `ispell` 的界面让一些人感到困惑。如果你没有安装 `ispell`，许多基础的拼写检查包提供的功能并不比“这个单词写对了吗？”具有多少复杂性。因此，无论何种情况，一种检查并修复整个文件中所有拼写错误的替代方法可能正是你需要的，而这个 shell 脚本可以轻松实现。

## 代码

```
#!/bin/sh

# spell - 一个交互式拼写检查程序，允许你逐步
# 查看文档中所有已知的拼写错误，指定你想
# 修复哪些以及如何修复，并将更改应用到文件
# 文件的原始版本将以 .shp 后缀保存，
# 新版本将替换旧版本。

# 注意，你需要一个标准的 'spell' 命令才能使其工作，
# 这可能涉及在你的系统中安装 ispell、ispell 或 spell。

tempfile="tmp/$0.$$"
changerequests="tmp/$0.$$sed"
spell="-l1"      # 根据需要修改你自己的 spell

trap "rm -f $tempfile $changerequests" EXIT HUP INT QUIT TERM

#  ANSI 颜色序列定义

.script-library.sh
initializeANSI

getfix()
  # 询问用户指定更正。如果用户输入的替换单词
  # 也是拼错误的，该函数将调用自己，产生第 2 层嵌套。
  # 这可以根据用户的需要无限嵌套，但要跟踪嵌套
  # 以确保只有第 1 层输出“替换单词”的消息。

  word=$1
  filename=$2
  misspelled=1

  while [ $misspelled -eq 1 ];
    echo ""; echo "$(bold)Misspelled word $(word):$(boldoff)"
```
