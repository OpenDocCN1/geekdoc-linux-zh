
```bash
#!/bin/bash

# longest-word2: find longest string in a file

for i; do
    if [[ -r "$i" ]]; then
        max_word=
        max_len=0
        for j in $(strings "$i"); do
            len=$(echo -n "$j" | wc -c)
            if (( len > max_len )); then
                max_len="$len"
                max_word="$j"
            fi
        done
        echo "$i: '$max_word' ($max_len characters)"
    fi
done
```

正如我们所见，我们已将最外层的循环改为使用 `for` 代替 `while`。通过省略 `for` 命令中的单词列表，位置参数将被使用。循环内部，变量 `i` 的先前实例已被更改为变量 `j`。`shift` 的使用也被消除了。

### 为什么是 `I`？

你可能已经注意到，在之前的每个 `for` 循环示例中都选择了变量 `i`。为什么？实际上没有特定原因，除了传统。`for` 中使用的变量可以是任何有效变量，但 `i` 最常见，其次是 `j` 和 `k`。

这一传统的根源来自 Fortran 编程语言。在 Fortran 中，以字母 `I`、`J`、`K`、`L` 和 `M` 开头的未声明变量会自动被类型化为整数，而以其他字母开头的变量则被类型化为实数（带小数部分的数字）。这种行为导致程序员使用变量 `I`、`J` 和 `K` 作为循环变量，因为当需要临时变量（循环变量通常如此）时，使用它们的工作量更少。

它还导致了以下基于 Fortran 的俏皮话：“GOD 是真实的，除非声明为 integer。”

### `for`：C 语言形式

`bash` 的最新版本添加了 `for` 命令语法的第二种形式，其形式类似于 C 编程语言中的形式。许多其他语言也支持这种形式。

```
for (( expression1; expression2; expression3 )); do
    commands
done
```

这里，`expression1`、`expression2` 和 `expression3` 是算术表达式，而 `commands` 是在循环的每次迭代期间要执行的命令。

就行为而言，这种形式等同于以下结构。

```
(( expression1 ))
while (( expression2 )); do
    commands
    (( expression3 ))
done
```

`expression1` 用于初始化循环的条件，`expression2` 用于确定循环何时结束，而 `expression3` 在循环的每次迭代结束时执行。

**这是一个典型的应用：**

```bash
#!/bin/bash

# simple_counter: demo of C style for command
for (( i=0; i<5; i=i+1 )); do
    echo $i
done
```

**执行时，它会产生以下输出：**

```text
[me@linuxbox ~]$ simple_counter
0
1
2
3
4
```

在此示例中，`expression1` 将变量 `i` 初始化为零值，`expression2` 允许循环在 `i` 的值小于 5 时继续执行，而 `expression3` 每次循环重复时将 `i` 的值递增 1。

C 语言形式的 `for` 在需要数字序列时非常有用。我们将在接下来的两章中看到它的几个应用。

### 总结

有了对 `for` 命令的了解，我们现在将对 `sys_info_page` 脚本进行最后的改进。目前，`report_home_space()` 函数如下所示：

```bash
report_home_space () {
    if [[ "$(id -u)" -eq 0 ]]; then
        cat <<- _EOF_
            <h2>Home Space Utilization (All Users)</h2>
            <pre>$(du -sh /home/*)</pre>
        _EOF_
    else
        cat <<- _EOF_
            <h2>Home Space Utilization ($USER)</h2>
            <pre>$(du -sh "$HOME")</pre>
        _EOF_
    fi
    return
}
```

接下来，我们将重写它，以为每个用户的 home 目录提供更多详细信息，并包含每个目录中的文件和子目录总数。

```bash
report_home_space () {

    local format="%8s%10s%10s\n"
    local i dir_list total_files total_dirs total_size user_name

    if [[ "$(id -u)" -eq 0 ]]; then
        dir_list=/home/*
        user_name="All Users"
    else
        dir_list="$HOME"
        user_name="$USER"
    fi

    echo "<h2>Home Space Utilization ($user_name)</h2>"

    for i in $dir_list; do
        total_files="$(find "$i" -type f | wc -l)"
        total_dirs="$(find "$i" -type d | wc -l)"
        total_size="$(du -sh "$i" | cut -f 1)"

        echo "<h3>$i</h3>"
        echo "<pre>"
        printf "$format" "Dirs" "Files" "Size"
        printf "$format" "----" "-----" "----"
        printf "$format" "$total_dirs" "$total_files" "$total_size"
        echo "</pre>"
    done
    return
}
```

此重写应用了我们迄今为止学到的许多内容。我们仍然测试超级用户，但不是将完整的一组操作作为 `if` 的一部分执行，而是设置稍后在 `for` 循环中使用的一些变量。我们向函数添加了几个局部变量，并使用 `printf` 来格式化部分输出。

# 34 字符串和数字

![](img/314a0280bc10c5c0d45be132de172677_547_0.png)

计算机程序都是关于处理数据的。在过去的章节中，我们专注于文件级别的数据处理。然而，许多编程问题需要使用字符串和数字等较小的数据单元来解决。

在本章中，我们将介绍 shell 中用于操作字符串和数字的几个特性。shell 提供了多种参数扩展来执行字符串操作。除了算术扩展之外，我们在第 7 章中已经涉及过，还有一个众所周知的命令行程序 `bc`，它执行更高级别的数学运算。

## 参数扩展

尽管参数扩展在第 7 章中出现过，但我们没有详细介绍它，因为大多数参数扩展用于脚本而不是命令行。我们已经使用了一些参数扩展形式，例如 shell 变量。shell 还提供了更多。

**NOTE**

### 管理空变量的扩展

有几个参数扩展旨在处理不存在和空的变量。这些扩展对于处理缺失的位置参数和为参数分配默认值非常有用。这里有一个这样的扩展：

```bash
${parameter:-word}
```

如果 `parameter` 未设置，即不存在或为空，则此扩展的结果为 `word` 的值。如果 `parameter` 不为空，则扩展结果为 `parameter` 的值。

```text
[me@linuxbox ~]$ foo=
[me@linuxbox ~]$ echo ${foo:-'substitute value if unset'}
substitute value if unset
[me@linuxbox ~]$ echo $foo

[me@linuxbox ~]$ foo=bar
[me@linuxbox ~]$ echo ${foo:-'substitute value if unset'}
bar
[me@linuxbox ~]$ echo $foo
bar
```

这里是另一个扩展，我们使用等号代替连字符：

```bash
${parameter:=word}
```
