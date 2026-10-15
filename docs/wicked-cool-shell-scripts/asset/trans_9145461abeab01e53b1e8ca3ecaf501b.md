
## 调整 UNIX

![](img/4ffb1cc24a1b24b49254839643abedb2_128_0.png)

局外人可能把 UNIX 想象成一种在众多不同系统上统一、漂亮的命令行体验，这些系统都符合 POSIX 标准。但任何用过不止一种 UNIX 系统的人都知道，在这些宽泛的参数范围内，各系统之间的差异有多大。例如，你会发现几乎每个 UNIX 或 Linux 系统都保留 `ls` 作为标准命令，但你的版本支持 `--color` 选项吗？你的 Bourne shell 版本支持变量切片（比如 `${var:0:2}`）吗？

shell 脚本最有价值的用途之一，或许就是调整你所用特定风味的 UNIX，使其更像其他系统。虽然大多数现代 GNU 工具都能在非 Linux 的 UNIX 系统上正常运行（例如，你可以用新版 GNU tar 替换笨重的旧版 tar），但通常调整 UNIX 所涉及的系统更新并不需要如此剧烈，而且也可以避免为受支持系统添加新二进制文件时可能带来的隐患。相反，shell 脚本可以用来将常用选项映射为当前系统中的等价选项，利用核心 UNIX 能力为现有命令创建更智能的版本，甚至解决某些功能长期缺失的问题。

### #27 显示带行号的文件

有几种方法可以为显示的文件添加行号，其中许多方法都非常简短。例如，下面是一种使用 `awk` 的解决方案：

```
awk '{ print NR": "$0 }' < inputfile
```

在某些 UNIX 实现中，`cat` 命令有一个 `-n` 选项，而在另一些实现中，`more`（或 `less`、`pg`）分页器有一个选项用于指定输出每一行时都带上行号。但在某些 UNIX 变体中，这些方法都不管用，此时清单 4-1 中的简单脚本就能完成这项工作。

### 代码

```
#!/bin/bash

# numberlines--A simple alternative to cat -n, etc.

for filename in "$@"
do
    linecount="1"
    while IFS="" read line
do
        echo "${linecount}: $line"
        linecount="$(( $linecount + 1 ))"
    done < $filename
done
exit 0
```

清单 4-1：numberlines 脚本

### 工作原理

这个程序的主循环有一个巧妙之处：它看起来像是一个普通的 `while` 循环，但关键部分其实是 `done < $filename`。事实证明，每个主要的块结构都充当它自己的虚拟子 shell，因此这种文件重定向不仅有效，而且是一种让循环逐行迭代 `$filename` 内容的简便方法。再配合 `read` 语句（①）——这个内层循环每次迭代都会将一行内容读入 `line` 变量——然后很容易就能在输出该行时以行号作为前缀，并递增 `linecount` 变量（②）。

清单 4-3 中的脚本将这一任务自动化，利用了 shell 的 `${#varname}` 结构，该结构返回变量 *varname* 中存储数据的长度。

### 代码

```bash
#!/bin/bash
# toolong—Feeds the fmt command only those lines in the input stream
#   that are longer than the specified length

width=72

if [ ! -r "$1" ] ; then
    echo "Cannot read file $1" >&2
    echo "Usage: $0 filename" >&2
    exit 1
fi

❶ while read input
do
    if [ ${#input} -gt $width ] ; then
        echo "$input" | fmt
    else
        echo "$input"
    fi
❷ done < $1

exit 0
```

*清单 4-3：toolong 脚本*

### 工作原理

注意，文件通过循环末尾的 `< $1`（❷）被送入 `while` 循环，然后通过 `read input`（❶）逐行读取，将文件的每一行依次赋值给 `input` 变量，从而可以分析每一行。

如果你的 shell 没有 `${#var}` 这种写法，你可以用超级有用的“字数统计”命令 `wc` 来模拟这一行为：

```bash
varlength="$(echo "$var" | wc -c)"
```

然而，`wc` 有个令人讨厌的习惯，它会在输出前面加上空格，以便在输出列表中让数值整齐对齐。为了避免这个烦人的问题，需要稍作修改，让最终管道步骤中只保留数字，如下所示：

```bash
varlength="$(echo "$var" | wc -c | sed 's/[^[:digit:]]//g')"
```

