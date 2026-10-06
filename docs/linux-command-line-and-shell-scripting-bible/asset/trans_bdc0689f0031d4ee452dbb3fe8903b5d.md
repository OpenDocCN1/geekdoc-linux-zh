

# tcsh 壳

# 表 21-5
tcsh 文件测试运算符

| 算符 | 描述 |
|---|---|
| r | 读取权限 |
| w | 写入权限 |
| x | 可执行 |
| X | 位于路径中或内置命令 |
| e | 文件存在 |
| o | 文件所有者 |
| z | 大小为零 |
| s | 大小非零 |
| f | 普通文件 |
| d | 目录 |
| l | 符号链接 |

这为你的脚本脚本提供了一种测试文件状态简单方法：

```
$ cat test6
!/bin/tcsh
# testing for the $HOME directory and a file

if ( -d $HOME ) then
    echo "The HOME directory exists"
endif
if ( -f $HOME/test ) then
    echo "The test file exists"
else
    echo "The test file doesn't exist"
endif
$ ./test6
The HOME directory exists
The test file doesn't exist
$ touch $HOME/test
$ ./test6
The HOME directory exists
The test file exists
$
```

使用文件测试运算符，你可以在脚本使用文件之前轻松地确定其文件的状态。

# foreach 语句

tcsh 壳不使用 for 语句，但它包含一个 `foreach` 语句，用于遍历数组变量或列表中的值。`foreach` 语句的格式为：

```
foreach varl (wordlist)
  statements
end
```

参数 `wordlist` 可以是一个数组变量，也可以是由空格分隔的值列表：

```
$ cat test7
#!/bin/tcsh
# testing the foreach statement

echo "The directories in your PATH are:"
foreach dir ($path)
  echo $dir
end
$ ./test7
The directories in your PATH are:
/usr/local/bin
/bin
/usr/bin
/usr/X11R6/bin
$
```

这是遍历数组变量的一种极方法，特别是当你不知道数组中有多少元素时。

# while 语句

tcsh 中的 `while` 语句允许你一直循环，直到指定的表达式评估为 FALSE 条件。`while` 命令的格式为：

```
while (expression)
  statements
end
```

在 `while` 语句中使用的表达式与 `if` 语句的格式相同，同时也适用于特殊的 `=` 和 `!~` 字符串比较符号：

```
$ cat test8
#!/bin/tcsh
# determining the factorial of a value
```

```
set value=$1
set factorial = 1
```

```
set counter = 1
while ($counter <= $value )
  @ factorial = ($factorial * $counter)
  @ counter += 1
end
echo "The factorial of $value is $factorial"
$ ./test8
The factorial of 5 is 120
$
```

`while` 语句会持续循环语句，直到表达式评估为 FALSE 条件。

# switch 命令

tcsh 壳中的 `switch` 命令允许你根据字符串匹配的值执行多个语句。`switch` 语句的格式为：

```
switch (string)
case val1:
  statements
case val2:
  statements
default:
  statements
endsw
```

壳程序会将字符串值与每个 `case` 语句中列出的值进行比较。如果某个 `case` 语句的值与字符串匹配，壳程序将执行该 `case` 语句包含的所有语句，以及之后所有的 `case` 语句。

如果你只想让 `switch` 执行单个 `case` 部分中的语句，可以在 `case` 部分的末尾使用 `break` 命令。这会导致壳程序跳转到结束语句。如果没有一个 `case` 值匹配，则将执行 `default` 部分的语句。

这里是在壳脚本中使用 `switch` 语句的一个示例：

```
$ cat test9
!/bin/tcsh
# reading input and using the switch statement

echo -n "Please enter a word: "
set input = $<
switch ($input)
case test:
  echo "This is a test"
  breaksw
case hello:

```
echo "Hello world!"
breaksw
case exit:
  echo "Thank you for playing"
  breaksw
default:
  echo "Sorry, I don't understand that command"
endsw
$ ./test9
Please enter a word: test
This is a test
$ ./test9
Please enter a word: testing
Sorry, I don't understand that command
$ ./test9
Please enter a word: exit
Thank you for playing
$
```

由于 tcsh 壳没有包含 bash 壳那样的 `read` 语句，你必须直接从 STDIN 读取输入值。你使用 `<` 符号来实现：

```
set input = $<$
```

获取输入后，`switch` 语句会将文本与每个 `case` 语句进行比较。如果没有匹配，则使用 `default` 语句（如果提供了）。

> 如果你好奇的话，tcsh 壳在壳脚本中不支持函数。在将 bash 脚本转换为 tcsh 环境时，这是一个巨大的障碍。

# 总结

本章讨论了 C 壳中包含的功能。虽然 C 壳在 Linux 世界中并不流行，但你可能仍然遇到它，因此了解它与 bash 壳的区别是一个好主意。

## 第四部分 替代性 Linux 壳

