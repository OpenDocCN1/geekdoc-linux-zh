
```bash
$ cat test20
#!/bin/bash
# breaking out of an outer loop
for (( a = 1; a < 4; a++ ))
do
    echo "Outer loop: $a"
    for (( b = 1; b < 10; b++ ))
    do
        if [ $b -gt 4 ]
        then
            break 2
        fi
        echo "  Inner loop: $b"
    done
done
$ ./test20
Outer loop: 1
  Inner loop: 1
  Inner loop: 2
  Inner loop: 3
  Inner loop: 4
$
```

现在，当 shell 执行 `break` 命令时，外层循环停止。

### `continue` 命令

`continue` 命令是一种在循环内提前停止处理命令但不完全终止循环的方法。这允许你在循环中设置条件，使 shell 不执行命令。以下是在 `for` 循环中使用 `continue` 命令的一个简单示例：

```bash
$ cat test21
#!/bin/bash
# using the continue command
for (( var1 = 1; var1 < 15; var1++ ))
do
    if [ $var1 -gt 5 ] && [ $var1 -lt 10 ]
    then
        continue
    fi
    echo "Iteration number: $var1"
done
$ ./test21
```

# 第二部分：Shell 脚本基础

```text
迭代次数: 1
迭代次数: 2
迭代次数: 3
迭代次数: 4
迭代次数: 5
迭代次数: 10
迭代次数: 11
迭代次数: 12
迭代次数: 13
迭代次数: 14
$
```

当 `if-then` 语句的条件满足时（值大于 5 且小于 10），shell 会执行 `continue` 命令，该命令会跳过循环中剩余的命令，但保持循环继续运行。当 `if-then` 条件不再满足时，程序恢复正常运行。

你可以在 `while` 和 `until` 循环中使用 `continue` 命令，但请务必极其谨慎。请记住，当 shell 执行 `continue` 命令时，它会跳过剩余的命令。如果你在那些被跳过的条件中递增测试条件变量，就会发生糟糕的事情：

```bash
$ cat badtest3
#!/bin/bash
# 在 while 循环中错误地使用 continue 命令

var1=0

while echo "while 迭代: $var1"
do
    if [ $var1 -gt 5 ] && [ $var1 -lt 10 ]
    then
        continue
    fi
    echo " 迭代次数内部: $var1"
    var1=$[ $var1 + 1 ]
done
$
```

```text
$ ./badtest3 | more
while 迭代: 0
迭代次数内部: 0
while 迭代: 1
迭代次数内部: 1
while 迭代: 2
迭代次数内部: 2
while 迭代: 3
迭代次数内部: 3
while 迭代: 4
迭代次数内部: 4
while 迭代: 5
迭代次数内部: 5
while 迭代: 6
while 迭代: 6
while 迭代: 6
while 迭代: 6
while 迭代: 6
while 迭代: 6
while 迭代: 6
while 迭代: 6
while 迭代: 6
$
```

你最好确保将此脚本的输出重定向到 `more` 命令，以便你能够停止程序。在 `if-then` 条件满足并且 shell 执行 `continue` 命令之前，一切看起来都正常。当 shell 执行 `continue` 命令时，它会跳过 `while` 循环中剩余的命令。不幸的是，正是在那里，在 `while` 测试命令中测试的 `$var1` 计数器变量被递增。这意味着该变量没有被递增，从不断显示的输出中可以看出。

与 `break` 命令一样，`continue` 命令允许你通过命令行参数指定要继续的循环级别：

`continue n`

其中 `n` 定义要继续的循环级别。以下是一个继续外层 `for` 循环的示例：

```bash
$ cat test22
#!/bin/bash
# 继续外层循环

for (( a = 1; a <= 5; a++ ))
do
    echo "迭代 $a:"
    for (( b = 1; b < 3; b++ ))
    do
        if [ $a -gt 2 ] && [ $a -lt 4 ]
        then
            continue 2
        fi
        var3=$[ $a * $b ]
        echo " $a * $b 的结果是 $var3"
    done
done

$ ./test22
迭代 1:
    1 * 1 的结果是 1
    1 * 2 的结果是 2
迭代 2:
    2 * 1 的结果是 2
    2 * 2 的结果是 4
迭代 3:
迭代 4:
    4 * 1 的结果是 4
    4 * 2 的结果是 8
迭代 5:
    5 * 1 的结果是 5
    5 * 2 的结果是 10
$
```

`if`-`then` 语句使用 `continue` 命令停止处理循环内部的命令，但继续外层循环：

```bash
if [ $a -gt 2 ] && [ $a -lt 4 ]
then
    continue 2
fi
```

请注意脚本输出，对于值 `3` 的迭代没有处理任何内层循环语句，因为 `continue` 命令停止了处理，但它继续外层循环的处理。

#### 处理循环的输出

最后，你可以在 shell 脚本中对循环的输出进行管道传输或重定向。你通过在 `done` 命令的末尾添加处理命令来实现这一点：

```bash
for file in /home/rich/*
do
    if [ -d "${file}" ]
    then
        echo "${file} 是一个目录"
    elif [ -f "${file}" ]
    then
        echo "${file} 是一个文件"
    fi
done > output.txt
```

shell 不会在监视器上显示结果，而是将 `for` 命令的结果重定向到 `output.txt` 文件。

请考虑将 `for` 命令的输出重定向到文件的以下示例：

```bash
$ cat test23
#!/bin/bash
# 将 `for` 输出重定向到文件

for (( a = 1; a < 10; a++ ))
do
    echo "该数字是 $a"
done > test23.txt

echo "命令已完成。"
$ ./test23
命令已完成。
$ cat test23.txt
该数字是 1
该数字是 2
该数字是 3
该数字是 4
该数字是 5
该数字是 6
该数字是 7
该数字是 8
该数字是 9
$
```

shell 创建 `test23.txt` 文件，并将 `for` 命令的输出仅重定向到该文件。shell 像往常一样显示 `for` 命令之后的 `echo` 语句。

同样的技术也适用于将循环的输出管道传输到另一个命令：

```bash
$ cat test24
#!/bin/bash
# 将循环管道传输到另一个命令

for state in "North Dakota" Connecticut Illinois Alabama Tennessee
do
    echo "$state 是下一个要去的地方"
done | sort
echo "我们的旅行到此结束"
$ ./test24
Alabama 是下一个要去的地方
Connecticut 是下一个要去的地方
Illinois 是下一个要去的地方
North Dakota 是下一个要去的地方
Tennessee 是下一个要去的地方
我们的旅行到此结束
$
```

州名值在 `for` 命令列表中并没有按特定顺序列出。`for` 命令的输出被管道传输到 `sort` 命令，该命令改变了 `for` 命令输出的顺序。运行脚本确实表明输出在脚本内被正确排序。

##### 总结

循环是编程的固有部分。Bash shell 提供三种循环命令，你可以在脚本中使用它们。

- `for` 命令允许你遍历值列表——这些值可以包含在命令行中、存储在变量中，或通过文件通配符获取——以从通配符中提取文件和目录名称。

- `while` 命令提供了一种基于命令条件进行循环的方法，使用普通命令或 `test` 命令，后者允许你测试变量条件。只要命令（或条件）产生 0 退出状态，`while` 循环就会继续遍历指定的命令集。
