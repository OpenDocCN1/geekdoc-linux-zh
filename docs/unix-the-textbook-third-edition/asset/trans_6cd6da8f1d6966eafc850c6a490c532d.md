

它们构成了测试语句。此外，在运算符、括号、方括号或操作数之前和之后至少需要一个空格。如果需要将测试表达式继续到下一行，你必须在按 <Enter> 之前使用反斜杠 (\ )，以免 shell 将下一行视为单独的命令。回想一下 \ 是一个 shell 元字符。我们在第一个会话中演示了 test 命令的使用，但随后使用 [] 的更简单语法。

test 命令支持许多用于测试文件和整数、测试和比较字符串，以及逻辑连接两个或多个表达式以形成复杂表达式的运算符。表 12.4 描述了在大多数 UNIX 系统上 test 命令支持的运算符的含义。

我们使用 if 语句修改 set_demo 文件中的脚本，使其仅接受一个命令行参数，并检查该参数是否为文件或目录。如果脚本未带参数或带多于一个命令行参数运行，或命令行参数不是普通文件，则脚本返回错误消息。脚本文件的名称为 if_demo1。

## 表 12.4 test 命令的运算符

| 文件测试 |  | 整数测试 |  | 字符串测试 |  |
|---|---|---|---|---|---|
| 表达式 | 返回值 | 表达式 | 返回值 | 表达式 | 返回值 |
| -d file | True if file is a directory | int1 -eq int2 | True if int1 and int2 are equal | str | True if str is not an empty string |
| -f file | True if file is an ordinary file | int1 -ge int2 | True if int1 is greater than or equal to int2 | str1 = str2 | True if str1 and str2 are the same |
| -r file | True if file is readable | int1 -gt int2 | True if int1 is greater than int2 | str1 != str2 | True if str1 and str2 are not the same |
| -s file | True if length of file is nonzero | int1 -le int2 | True if int1 is less than or equal to int2 | -n str | True if the length of str is greater than zero |
| -t [filedes] | True if file descriptor filedes is associated with the terminal | int1 -lt int2 | True if int1 is less than int2 | -z str | True if the length of str is zero |
| -w file | True if file is writable | int1 -ne int2 | True if int1 is not equal to int2 |  |  |
| -x file | True if file is executable |  |  |  |  |

## 形成复杂表达式的运算符

|  |  |  |  |
|---|---|---|---|
| ! | Logical NOT operator: true if the following expression is false | (expression) | Parentheses for grouping expressions; at least one space before and one after each parenthesis |
| -a | Logical AND operator: true if the previous (left) and next (right) expressions are true | -o | Logical OR operator: true if the previous (left) or next (right) expression is true |

```
$ cat if_demo1
#!/bin/sh
if test $# -eq 0
then
    echo "Usage: $0 ordinary_file"
    exit 1
fi
if test $# -gt 1
then
    echo "Usage: $0 ordinary_file"
    exit 1
fi
if test -f "$1"
then
    filename=$1
    set -- `ls -l $filename`
    perms="$1"
    size="$5"
    set `ls -i $filename`
    inode="$1"
    echo "File Name:        $filename"
    echo "Inode Number:     $inode"
    echo "Permissions:      $perms"
    echo "Size (bytes):     $size"
    exit 0
fi
echo "$0: argument must be an ordinary file"
exit 1
$ ./if_demo1
Usage: if_demo1 ordinary_file
$ ./if_demo1 lab1 lab4
Usage: if_demo1 ordinary_file
$ ./if_demo1 dir1
if_demo1: argument must be an ordinary file
$ ./if_demo1 lab1
File Name:      lab1
Inode Number:   679
Permissions:    -rwxr--r--
Size (bytes):   243
$
```

在前面的脚本中，第一个 if 语句在你不带任何命令行参数运行脚本时显示错误消息并退出程序。第二个 if 语句在你带多于一个参数运行脚本时显示错误消息并退出程序。第三个 if 语句在前两个条件为假时执行——也就是说，如果你仅带一个参数运行脚本。此 if 语句在命令行参数是普通文件时产生所需的结果。如果传递的参数是

