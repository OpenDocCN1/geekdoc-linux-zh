
列表 3-16：存储日程项目的 `.agenda` 原始内容

# 破解脚本

这个脚本仅仅触及了这一复杂而有趣话题的表面。如果能让它向前看几天就好了，例如；这可以在 `agenda` 脚本中通过一些日期计算来实现。如果你有 GNU `date` 命令，日期计算是很容易的。如果没有，那么，仅在 shell 中启用日期计算需要一个复杂的脚本。我们将在书的后面详细查看日期，特别是第 330 页的第 99 号脚本、第 332 页的第 100 号脚本以及第 335 页的第 101 号脚本。

另一个（更简单的）技巧是在当当前日期没有匹配项时让 `agenda` 输出为空，而不是“On the agenda for today:” 后面什么都没有的这种比较粗略的方式。

此脚本还可以用于 Unix，以发送更广泛的事件提醒，例如备份计划、公司假期和员工生日。首先，每个用户机器上的 `agenda` 脚本将额外检查一个共享的只读 `.agenda` 文件。然后在每个用户的 `.login` 或类似的在登录时调用的文件中添加对 `agenda` 脚本的调用。

> 注意
> 惊讶的是，不同 Unix 和 Linux 系统上的 `date` 实现各不相同。如果你尝试用自己的 `date` 命令进行更复杂的操作并失败了，请务必检查帮助页面（man page）以查看你的系统能做什么和不能做什么。

# 调整 UNIX

![](img/954a28cc04c09826495e330f44c0085b_128_0.png)

外人可能认为 Unix 是一种跨越许多不同系统的良好的、统一的命令行体验，这得益于它们对 POSIX 标准的遵守。但任何用过超过一个 Unix 系统的人都知道，在这些宽泛的参数范围内，它们的差异巨大。你很难找到一个不留标准命令的 Unix 或 Linux 机器，例如，你的版本支持 `--color` 标志吗？你的 Bourne shell 支持变量切片（如 `${var:0}`）吗？

也许 shell 脚本最有价值的用途就是调整你特定的 Unix 版本，使其与其他系统保持相似。大多数现代 GNU 工具在非 Linux 的 Unix 上运行运行良好（例如，……）。

## 显示带有行号的文件

有几种方法可以添加行号，例如，使用 `awk`：

```bash
awk '{ print NR ": $0 }' infile
```

### 代码

```bash
#!/bin/bash

# numberlines - 一个简单的示例

for filename in "$@"
do
  linecount=1
  while IFS= read -r line; do
    echo "${linecount}: $line"
    linecount=$((linecount + 1))
  done < "$filename"
done

exit 0
```

列表 4-1：`numberlines` 脚本

### 工作原理

程序的主要部分是 `while` 循环：它将每行加载到 `line` 变量中，然后很容易输出行号并增加 `linecount` 变量。

### 运行脚本

你可以向此脚本传递多个文件名。虽然不能通过管道输入，但通过 `cat` 修复并不困难。

### 结果

列表 4-2 显示了使用 `numberlines` 脚本带有行号的文件。

```bash
$ numberlines alice.txt
```
+1: Alice was beginning to get tired of sitting by her sister on the
2: bank, of having nothing to do: once or twice she peeked into the
3: book her sister was reading, but it had no pictures or conversations
4: 'and what is the use of a book,' thought Alice 'without pictures or
5: conversations?
6: So she was considering in her mind (as well as she could, for the
7: hot day made her sleepy and stupid), whether the pleasure
8: making a daisy-chain would be worth the trouble of getting up and
9: picking the daisies, when suddenly a white Rabbit with pink eyes ran
10: close by her. |

列表 4-2：对《爱丽丝仙游》片段测试 `numberlines` 脚本

# 破解脚本

一旦你有了带有行号的文件，你可以这样反转文件中所有行的顺序：

```bash
cat -n filename | sort -rn | cut -c8
```

## 仅对长行换行

如果你有一个文档想要对长行换行但保持其他内容不变？……：在编辑器中手动遍历每一行，将长行单独传递给 `fmt`。（你可以在 vi 中将光标移动到目标行并使用 `!fmt` 来实现这一点）

Listing 4-3 中的脚本自动完成了该任务，它利用了 shell 构造 `${#varname}`，该构造返回存储在变量 `varname` 中的数据内容的长度。

### 代码

```bash
#!/bin/bash

# toolong--Feeds the fmt command only those lines in the input stream
# that are longer than the specified length

width=72

if [ ! -r "$1" ]; then
    echo "Cannot read file "$1" >&2"
    echo "Usage: $0 filename" >&2
    exit 1
fi

while read input
do
    if [ ${#input} -gt $width ]; then
        echo "$input" | fmt
    else
        echo "$input"
    fi
done < $1

exit 0
```

Listing 4-3: `toolong` 脚本

### 工作原理

注意，文件通过循环末尾简单的 `< $1` 传递给 `while` 循环，并且每一行都可以通过 `read input` 读取并进行分析，这会将文件的每一行逐行赋值变量 `input`。

如果你的 shell 没有支持 `${#var}` 符号，你可以使用非常有用的“单词计数”命令 `wc` 来模拟它：

```
varlen="$(echo "$var" | wc -c)"
```

然而，`wc` 有一个烦人的习惯，会在输出结果前面加空格，以便让数值在输出列表中对齐。为了避免这个棘手的问题，需要进行轻微修改，通过最后的管道只保留数字，如下所示：

```
varlen="$(echo "$var" | wc -c | sed s/[^[:digit:]]//g"
```
