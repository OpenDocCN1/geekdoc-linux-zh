
```
#!/bin/bash

# longest-word : find longest string in a file

while [[ -n $1 ]]; do
    if [[ -r $1 ]]; then
        max_word=
        max_len=0
        for i in $(strings $1); do
            len=$(echo $i | wc -c)
            if (( len > max_len )); then
                max_len=$len
                max_word=$i
            fi
        done
        echo "$1: '$max_word' ($max_len characters)"
    fi
    shift
done
```

在此示例中，我们查找文件中找到的最长字符串。当在命令行中给出一个或多个文件名时，此程序使用 `strings` 程序（包含在 GNU `binutils` 包中）为每个文件生成可读文本“单词”列表。`for` 循环依次处理每个单词并判断当前单词是否迄今为止最长的。当循环结束时，最长的单词将被显示。

如果省略 `for` 命令的可选 `in words` 部分，`for` 默认处理位置参数。我们将修改 `longest-word` 脚本来使用此方法：

```
#!/bin/bash

# longest-word2 : find longest string in a file

for i; do
    if [[ -r $i ]]; then
        max_word=
        max_len=0
        for j in $(strings $i); do
            len=$(echo $j | wc -c)
            if (( len > max_len )); then
                max_len=$len
                max_word=$j
            fi
        done
        echo "$i: '$max_word' ($max_len characters)"
    fi
done
```

正如我们所见，我们已将最外层的循环改为使用 `for` 代替 `while`。通过省略 `for` 命令中的单词列表，将使用位置参数。在循环内部，先前实例中的变量 `i` 已更改为变量 `j`。`shift` 的使用也已被消除。

## Why i?

你可能已经注意到，在上面的每个 `for` 循环示例中都选择了变量 `i`。为什么？实际上没有特定原因，除了传统习惯。`for` 中使用的变量可以是任何有效变量，但 `i` 最常见，其次是 `j` 和 `k`。

> 这种传统的根源来自 `Fortran` 编程语言。在 `Fortran` 中，以字母 `I`、`J`、`K`、`L` 和 `M` 开头的未声明变量会自动被类型化为整数，而以其他字母开头的变量则被类型化为实数（带小数部分的数字）。这种行为导致程序员使用变量 `I`、`J` 和 `K` 作为循环变量，因为当需要临时变量（循环变量通常就是临时变量）时，使用它们的工作量更少。

> 这也导致了以下基于 `Fortran` 的俏皮话：

> “GOD is real, unless declared integer。”

## for: C Language Form

最近版本的 `bash` 添加了 `for` 命令语法的第二种形式，其类似于 C 编程语言中发现的形式。许多其他语言也支持这种形式：

```
for (( expression1; expression2; expression3 )); do
    commands
done
```

其中 `expression1`、`expression2` 和 `expression3` 是算术表达式，`commands` 是在循环的每次迭代期间执行的命令。

就行为而言，这种形式等同于以下结构：

```
(( expression1 ))
while (( expression2 )); do
    commands
    (( expression3 ))
done
```

`expression1` 用于初始化循环的条件，`expression2` 用于确定循环何时结束，而 `expression3` 在循环的每次迭代结束时执行。

这里有一个典型的应用：

```
#!/bin/bash

# simple_counter : demo of C style for command

for (( i=0; i<5; i=i+1 )); do
    echo $i
done
```

执行时，它会产生以下输出：

```
[me@linuxbox ~]$ simple_counter
0
1
2
3
4
```

在此示例中，`expression1` 将变量 `i` 初始化为零值，`expression2` 允许循环在 `i` 的值小于 5 时继续，而 `expression3` 每次循环重复时将 `i` 的值递增一。

C 语言形式的 `for` 在需要数字序列时非常有用。我们将在接下来的两章中看到它的几种应用。

## Summing Up

有了我们对 `for` 命令的了解，我们现在将对 `sys_info_page` 脚本进行最后的改进。目前，`report_home_space` 函数如下所示：

```
report_home_space () {
    if [[ $(id -u) -eq 0 ]]; then
        cat <<- _EOF_
<H2>Home Space Utilization (All Users)</H2>
<PRE>$(du -sh /home/*)</PRE>
_EOF_
    else
        cat <<- _EOF_
<H2>Home Space Utilization ($USER)</H2>
<PRE>$(du -sh $HOME)</PRE>
_EOF_
    fi
    return
}
```

接下来，我们将重写它，以为每个用户的 home 目录提供更多详细信息，并包含每个目录中的文件和子目录总数：

```
report_home_space () {
```

```
local format="%8s%10s%10s\n"
local i dir_list total_files total_dirs total_size user_name

if [[ $(id -u) -eq 0 ]]; then
    dir_list="/home/*"
    user_name="All Users"
else
    dir_list=$HOME
    user_name=$USER
fi

echo "<H2>Home Space Utilization ($user_name)</H2>"

for i in $dir_list; do
    total_files=$(find $i -type f | wc -l)
    total_dirs=$(find $i -type d | wc -l)
    total_size=$(du -sh $i | cut -f 1)
    
    echo "<H3>$i</H3>"
    echo "<PRE>"
    printf "$format" "Dirs" "Files" "Size"
    printf "$format" "----" "-----" "----"
    printf "$format" $total_dirs $total_files $total_size
    echo "</PRE>"
done
return
}
```

此重写应用了我们迄今为止学到的许多内容。我们仍然测试超级用户，但不是将完整的一组操作作为 `if` 的一部分执行，而是设置稍后在 `for` 循环中使用的一些变量。我们向函数添加了几个局部变量，并使用 `printf` 来格式化部分输出。

## Further Reading

- `Advanced Bash-Scripting Guide` 有一章关于循环，提供了多种使用 `for` 的示例：

  http://tldp.org/LDP/abs/html/loops1.html

- `Bash Reference Manual` 描述了循环复合命令，包括 `for`：

  http://www.gnu.org/software/bash/manual/bashref.html#Looping-Constructs

## 34 – Strings And Numbers

计算机程序都是关于处理数据。在过去的章节中，我们专注于文件级别的数据处理。然而，许多编程问题需要使用字符串和数字等较小的数据单元来解决。

在本章中，我们将介绍 shell 中用于操作字符串和数字的几个特性。shell 提供了多种参数扩展来执行字符串操作。除了算术扩展（我们在第 7 章中涉及过）之外，还有一个常见的命令行程序称为 `bc`，可执行更高级别的数学运算。
