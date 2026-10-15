
# 语法

```
if (expression) then
then-command-list
[else if (expression) then
then-command-list
...
else
else-command-list]
endif
```

用途：实现双向或多向分支。

这里，表达式是一个命令列表。表达式中命令的执行返回真（成功）或假（失败）状态。我们讨论 if 语句的三个版本，它们共同构成了该语句的完整语法和语义。if 语句最基本的用法是不带任何可选功能，其语法如下，通常用于双向分支。

# 语法

```
if (expression) then
then-commands
endif
```

用途：实现双向分支。

如果表达式为真，则执行 then-commands；否则，执行 endif 之后的命令。该语句的语义如图14.1所示。

![](img/02e070097d401d3bf7de4bf1c470b267_586_0.png)

你可以使用多种运算符来构成表达式，这些运算符用于测试文件、测试和比较整数及字符串，并通过逻辑连接两个或多个表达式来构成复杂表达式。表14.3描述了可用于构成表达式的运算符及其含义。与文件无关的运算符按优先级（从高到低）排列：括号、一元、算术、移位、关系、位运算和逻辑。

我们使用上述 if 命令的语法来修改 set_demo 文件中的脚本，使其只接受一个命令行参数，并检查该参数是文件还是目录。如果脚本运行时不带参数或带有多于一个参数，或者命令行参数不是

# 表14.3 用于构成表达式的 C Shell 运算符

| 运算符 | 功能 | 运算符 | 功能 |
|---|---|---|---|
| 括号 |  | 关系运算符 |  |
| () | 改变求值顺序 | > | 大于 |
|  |  | < | 小于 |
|  |  | >= | 大于或等于 |
|  |  | <= | 小于或等于 |
|  |  | != | 不等于（用于字符串比较） |
|  |  | == | 等于（用于字符串比较） |
| 一元运算符 |  | 位运算符 |  |
| - | 一元减 | & | 与 |
| ~ | 按位取反 | ^ | 异或 |
| ! | 逻辑非 | \| | 或 |
| 算术运算符 |  | 逻辑运算符 |  |
| % | 取余 | && | 与 |
| / | 除 | \|\| | 或 |
| * | 乘 |  |  |
| - | 减 |  |  |
| + | 加 |  |  |
| 移位运算符 |  |  |  |
| >> | 右移 |  |  |
| << | 左移 |  |  |
| 文件和字符串相关运算符 |  |  |  |
| 运算符 | 功能 | 运算符 | 功能 | 运算符 | 功能 |
| -d 文件 | 如果文件是目录则为真 | -e 文件 | 如果文件存在则为真 | -f 文件 | 如果文件是普通文件则为真 |
| -o 文件 | 如果用户拥有该文件则为真 | -r 文件 | 如果文件可读则为真 | -w 文件 | 如果文件可写则为真 |
| -x 文件 | 如果文件可执行则为真 | -z 文件 | 如果文件长度为零字节则为真 |  |  |

普通文件。脚本文件名为 if_demo1。该文件的内容及其示例运行如下。

```
% cat if_demo1
#!/bin/csh
if ( ( $#argv == 0 ) || ( $#argv > 1 ) ) then
    echo "Usage: $0 ordinary_file"
    exit 1
endif
if ( ! -e $1 ) then
    echo "$1 : non-existent file"
    exit 1
endif
if ( -d $1 ) then
    echo "$1 : directory"
    echo "Usage: $0 ordinary_file"
    exit 1
endif
if ( -f $1 ) then
    set filename = $argv[1]
    set fileinfo = `ls -il $filename`
    set inode = $fileinfo[1]
    set perms = $fileinfo[2]
    set size = $fileinfo[6]
    echo "File Name:      $filename"
    echo "Inode Number:   $inode"
    echo "Permissions:    $perms"
    echo "Size (bytes):   $size"
    exit 0
endif
echo "$0: argument must be an ordinary file"
exit 1
% ./if_demo1
Usage: if_demo1 ordinary_file
% ./if_demo1 lab1
lab1 : non-existent file
% ./if_demo1 dir1
dir1 : directory
Usage: if_demo1 ordinary_file
% ./if_demo1 lab3
File Name:      lab3
Inode Number:   4313
Permissions:    -rw-r--r--
Size (bytes):   221
%
```

在上述脚本中，如果你运行脚本，第一个包含复合表达式的 if 语句实例会显示错误消息并退出程序。
