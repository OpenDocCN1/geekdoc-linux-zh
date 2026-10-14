

执行时，它会产生以下输出：

```
[me@linuxbox ~]$ simple_counter
0
1
2
3
4
```

在此示例中，*expression1* 将变量 *i* 初始化为零值，*expression2* 允许循环在 *i* 的值小于 5 时继续，而 *expression3* 每次循环重复时将 *i* 的值递增一。

C 语言形式的 *for* 在需要数字序列时非常有用。我们将在接下来的两章中看到它的几种应用。

## Summing Up

有了我们对 *for* 命令的了解，我们现在将对 *sys_info_page* 脚本进行最后的改进。目前，*report_home_space* 函数如下所示：

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

此重写应用了我们迄今为止学到的许多内容。我们仍然测试超级用户，但不是将完整的一组操作作为 if 的一部分执行，而是设置稍后在 for 循环中使用的一些变量。我们向函数添加了几个局部变量，并使用 printf 来格式化部分输出。

## Further Reading

- *Advanced Bash-Scripting Guide* 有一章关于循环，提供了多种使用 for 的示例：
  http://tldp.org/LDP/abs/html/loops1.html
- *Bash Reference Manual* 描述了循环复合命令，包括 for：
  http://www.gnu.org/software/bash/manual/bashref.html#Looping-Constructs

## 34 – Strings And Numbers

计算机程序都是关于处理数据。在过去的章节中，我们专注于文件级别的数据处理。然而，许多编程问题需要使用字符串和数字等较小的数据单元来解决。

在本章中，我们将介绍 shell 中用于操作字符串和数字的几个特性。shell 提供了多种参数扩展来执行字符串操作。除了算术扩展（我们在第 7 章中涉及过）之外，还有一个常见的命令行程序称为 bc，可执行更高级别的数学运算。

## Parameter Expansion

尽管参数扩展在第 7 章中出现过，但我们没有详细介绍它，因为大多数参数扩展是在脚本中而不是在命令行中使用。我们已经使用了一些参数扩展形式；例如，shell 变量。shell 提供了更多。

### Basic Parameters

参数扩展的最简单形式反映在变量的普通使用中。例如：

```
$a
```

展开后，成为变量 a 的内容。简单参数也可以用大括号括起来：

```
${a}
```

这对扩展没有影响，但在变量与可能使 shell 混淆的其他文本相邻时是必需的。在此示例中，我们尝试通过将字符串 "_file" 附加到变量 a 的内容来创建文件名。

```
[me@linuxbox ~]$ a="foo"
[me@linuxbox ~]$ echo "$a_file"
```

如果我们执行此序列，结果将为空，因为 shell 将尝试扩展名为 a_file 的变量而不是 a。可以通过添加大括号来解决此问题：

```
[me@linuxbox ~]$ echo "${a}_file"
foo_file
```

我们还看到，位置参数大于 9 可以通过将数字用大括号括起来来访问。例如，要访问第十一个位置参数，我们可以这样做：

```
${11}
```

### Expansions To Manage Empty Variables

几个参数扩展处理不存在和空变量。这些扩展对于处理缺失的位置参数和为参数分配默认值非常方便。

```
${parameter:-word}
```

如果 parameter 未设置（即不存在）或为空，此扩展的结果为 word 的值。如果 parameter 不为空，扩展的结果为 parameter 的值。

```
[me@linuxbox ~]$ foo=
[me@linuxbox ~]$ echo ${foo:-"substitute value if unset"}
substitute value if unset
[me@linuxbox ~]$ echo $foo

[me@linuxbox ~]$ foo=bar
[me@linuxbox ~]$ echo ${foo:-"substitute value if unset"}
bar
[me@linuxbox ~]$ echo $foo
bar
```

```
${parameter:=word}
```

如果 parameter 未设置或为空，此扩展的结果为 word 的值。此外，word 的值将被赋给 parameter。如果 parameter 不为空，扩展的结果为 parameter 的值。

```
[me@linuxbox ~]$ foo=
[me@linuxbox ~]$ echo ${foo:="default value if unset"}
```
