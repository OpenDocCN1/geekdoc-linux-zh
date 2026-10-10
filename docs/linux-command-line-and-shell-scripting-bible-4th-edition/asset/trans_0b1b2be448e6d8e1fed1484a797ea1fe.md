

```bash
for (( a = 1; a < 4; a++ ))
do
    echo "Outer loop: $a"
    for (( b = 1; b < 100; b++ ))
    do
        if [ $b -eq 5 ]
        then
            break
        fi
        echo "  Inner loop: $b"
    done
done
$ ./test19
Outer loop: 1
  Inner loop: 1
  Inner loop: 2
  Inner loop: 3
  Inner loop: 4
Outer loop: 2
  Inner loop: 1
  Inner loop: 2
  Inner loop: 3
  Inner loop: 4
Outer loop: 3
  Inner loop: 1
  Inner loop: 2
  Inner loop: 3
  Inner loop: 4
$
```

内层循环中的 `for` 语句指定迭代直到 `b` 变量等于 100。然而，内层循环中的 `if-then` 语句指定当 `b` 变量的值等于 5 时，执行 `break` 命令。请注意，尽管内层循环被 `break` 命令终止，但外层循环仍按指定继续运行。

## 跳出外层循环

有时你可能处于内层循环中，但需要停止外层循环。`break` 命令包含一个命令行参数值：

```bash
break n
```

其中 `n` 指示要跳出的循环层级。默认情况下，`n` 为 1，表示跳出当前循环。如果你将 `n` 设置为 2，`break` 命令将停止下一层的外层循环：

```bash
$ cat test20
#!/bin/bash
# breaking out of an outer loop

for (( a = 1; a < 4; a++ ))
do
    echo "Outer loop: $a"
    for (( b = 1; b < 100; b++ ))
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

现在当 Shell 执行 `break` 命令时，外层循环停止。

## continue 命令

`continue` 命令是一种在循环内部提前停止处理命令但不完全终止循环的方式。这允许你在循环中设置条件，使 Shell 不执行某些命令。以下是使用 `continue` 命令的 `for` 循环的简单示例：

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
Iteration number: 1
Iteration number: 2
Iteration number: 3
Iteration number: 4
Iteration number: 5
Iteration number: 10
Iteration number: 11
Iteration number: 12
Iteration number: 13
Iteration number: 14
$
```

当 `if-then` 语句的条件满足时（值大于 5 且小于 10），Shell 执行 `continue` 命令，该命令跳过循环中其余的命令，但保持循环继续运行。当 `if-then` 条件不再满足时，一切恢复正常。

你可以在 `while` 和 `until` 循环中使用 `continue` 命令，但务必极其小心你所做的事情。请记住，当 Shell 执行 `continue` 命令时，它会跳过剩余的命令。如果你在这些条件中递增测试条件变量，就会发生不好的事情：

```bash
$ cat badtest3
#!/bin/bash
# improperly using the continue command in a while loop

var1=0

while echo "while iteration: $var1"
    [ $var1 -lt 15 ]
do
    if [ $var1 -gt 5 ] && [ $var1 -lt 10 ]
    then
        continue
    fi
    echo "    Inside iteration number: $var1"
    var1=$[ $var1 + 1 ]
done
$ ./badtest3 | more
while iteration: 0
Inside iteration number: 0
while iteration: 1
    Inside iteration number: 1
while iteration: 2
    Inside iteration number: 2
while iteration: 3
    Inside iteration number: 3
while iteration: 4
    Inside iteration number: 4
while iteration: 5
    Inside iteration number: 5
while iteration: 6
while iteration: 6
while iteration: 6
while iteration: 6
while iteration: 6
while iteration: 6
while iteration: 6
while iteration: 6
while iteration: 6
while iteration: 6
while iteration: 6
while iteration: 6
$
```

你需要确保将此脚本的输出重定向到 `more` 命令，以便你可以停止它。在 `if-then` 条件满足且 Shell 执行 `continue` 命令之前，一切都看起来正常。当 Shell 执行 `continue` 命令时，它会跳过 `while` 循环中的剩余命令。不幸的是，正是在 `while` 测试命令中测试的 `$var1` 计数变量在此处被递增。这意味着变量没有被递增，正如你从不断显示的输出处可以看到的。

与 `break` 命令一样，`continue` 命令允许你通过命令行参数指定继续哪个层级的循环：

```bash
continue n
```

其中 `n` 定义要继续的循环层级。以下是一个继续外层 `for` 循环的示例：

```bash
$ cat test22
#!/bin/bash
# continuing an outer loop

for (( a = 1; a <= 5; a++ ))
do
    echo "Iteration $a:"
    for (( b = 1; b < 3; b++ ))
    do
        if [ $a -gt 2 ] && [ $a -lt 4 ]
        then
            continue 2
        fi
        var3=$[ $a * $b ]
        echo "   The result of $a * $b is $var3"
    done
done
$ ./test22
Iteration 1:
   The result of 1 * 1 is 1
   The result of 1 * 2 is 2
Iteration 2:
   The result of 2 * 1 is 2
   The result of 2 * 2 is 4
Iteration 3:
Iteration 4:
   The result of 4 * 1 is 4
   The result of 4 * 2 is 8
Iteration 5:
   The result of 5 * 1 is 5
   The result of 5 * 2 is 10
$
```

`if-then` 语句：

```bash
if [ $a -gt 2 ] && [ $a -lt 4 ]
then
    continue 2
fi
```

使用 `continue` 命令来停止处理循环内部的命令，但继续外层循环。请注意，在脚本输出中，值 3 的迭代没有处理任何内层循环语句，因为 `continue` 命令停止了处理，但它继续外层循环的处理。

## 处理循环的输出

最后，你可以将 Shell 脚本中循环的输出进行管道传输或重定向。你通过在 `done` 命令的末尾添加处理命令来实现这一点：

```bash
for file in /home/rich/*
do
    if [ -d "$file" ]
    then
        echo "$file is a directory"
    elif
        echo "$file is a file"
    fi
done > output.txt
```

Shell 不会在监视器上显示结果，而是将 `for` 命令的结果重定向到文件 `output.txt`。

考虑以下将 `for` 命令输出重定向到文件的示例：

```bash
$ cat test23
#!/bin/bash
# redirecting the for output to a file

for (( a = 1; a < 10; a++ ))
do
    echo "The number is $a"
done > test23.txt
echo "The command is finished."
$ ./test23
The command is finished.
$ cat test23.txt
The number is 1
The number is 2
The number is 3
The number is 4
The number is 5
The number is 6
The number is 7
The number is 8
The number is 9
$
```

Shell 创建文件 `test23.txt` 并将 `for` 命令的输出仅重定向到该文件。Shell 像往常一样在 `for` 命令之后显示 `echo` 语句。

同样的技术也适用于将循环的输出管道传输到另一个命令：

```bash
$ cat test24
#!/bin/bash
# piping a loop to another command

for state in "North Dakota" Connecticut Illinois Alabama Tennessee
do
    echo "$state is the next place to go"
done | sort
echo "This completes our travels"
$ ./test24
Alabama is the next place to go
Connecticut is the next place to go
Illinois is the next place to go
North Dakota is the next place to go
Tennessee is the next place to go
This completes our travels
$
```

`for` 命令列表中的州值并未按任何特定顺序列出。`for` 命令的输出被管道传输到 `sort` 命令，该命令改变了 `for` 命令输出的顺序。运行脚本确实表明输出在脚本内部被正确排序。

## 通过几个实际示例进行操作

既然你已经看到了如何使用不同的方式在 Shell 脚本中创建循环，让我们看看一些实际使用它们的示例。循环是遍历系统上数据的一种常见方式，无论是文件夹中的文件还是文件中包含的数据。这里有一些示例，展示了如何使用简单的循环来处理数据。

### 查找可执行文件

当你从命令行运行程序时，Linux 系统会搜索一系列文件夹以查找该文件。这些文件夹在 `PATH` 环境变量中定义。如果你想找出什么

