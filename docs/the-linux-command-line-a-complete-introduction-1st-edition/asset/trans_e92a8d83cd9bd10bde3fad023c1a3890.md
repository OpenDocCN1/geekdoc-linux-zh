
`for` 的 C 语言形式在需要数值序列时非常有用。在接下来的两章中，我们将会看到它的几种应用。

## 最后说明

借助我们对 `for` 命令的了解，现在我们将对 `sys_info_page` 脚本进行最后的改进。目前，`report_home_space` 函数如下所示：

```sh
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

接下来，我们将重写该函数，为每个用户的主目录提供更多详细信息，并包含每个目录中的文件和子目录总数：

```sh
report_home_space () {
    local format="%8s%10s%10s\n"
    local i dir_list total_files total_dirs total_size user_name

    if [[ $(id -u) -eq 0 ]]; then
        dir_list=/home/*
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

这次重写应用了我们目前学到的很多知识。我们仍然测试超级用户，但不再将整套操作作为 if 的一部分来执行，而是设置一些稍后在 for 循环中使用的变量。我们向函数添加了几个局部变量，并使用 printf 格式化部分输出。

## 34

## 字符串和数字

计算机程序讲的都是处理数据。在过去的章节中，我们专注于在文件层面处理数据。然而，许多编程问题需要使用更小的数据单元（如字符串和数字）来解决。

在本章中，我们将了解几个用于处理字符串和数字的 shell 特性。shell 提供了多种参数扩展来执行字符串操作。除了算术扩展（我们在第 7 章中提到过），还有一个常见的命令行程序 bc，它可以执行更高级的数学运算。

## 参数扩展

虽然参数扩展在第 7 章中出现过，但我们没有详细讨论，因为大多数参数扩展用于脚本中，而不是命令行中。我们已经接触过某些形式的参数扩展，例如 shell 变量。shell 还提供了更多其他形式。

## 基本参数

参数扩展最简单的形式体现在变量的常规使用中。例如，$a 展开后变为变量 a 所包含的内容。简单参数也可以用花括号括起来，如 ${a}。这不会影响展开，但如果变量与其他文本相邻，可能会使 shell 产生混淆，此时就需要使用花括号。在这个例子中，我们尝试通过将字符串 _file 附加到变量 a 的内容后面来创建一个文件名。

```sh
[me@linuxbox ~]$ a="foo"
[me@linuxbox ~]$ echo "$a_file"
```

如果我们执行这一序列，结果将为空，因为 shell 会尝试展开名为 a_file 的变量，而不是 a。这个问题可以通过添加花括号来解决：

```sh
[me@linuxbox ~]$ echo "${a}_file"
foo_file
```

我们还了解到，大于 9 的位置参数可以通过将数字放在花括号中来访问。例如，要访问第 11 个位置参数，可以这样写：${11}。

## 处理空变量的扩展

有几个参数扩展用于处理不存在或为空的变量。这些扩展对于处理缺失的位置参数和为参数赋予默认值非常方便。下面就是这样一个扩展：

${parameter:-word}

如果 parameter 未设置（即不存在）或为空，则该扩展的结果是 word 的值。如果 parameter 不为空，则扩展结果是 parameter 的值。

```sh
[me@linuxbox ~]$ foo=
[me@linuxbox ~]$ echo ${foo:-"substitute value if unset"}
substitute value if unset
[me@linuxbox ~]$ echo $foo

[me@linuxbox ~]$ foo=bar
[me@linuxbox ~]$ echo ${foo:-"substitute value if unset"}
[me@linuxbox ~]$ echo $foo
bar
```

下面是另一个扩展，它使用等号而不是短横线：

${parameter:=word}
