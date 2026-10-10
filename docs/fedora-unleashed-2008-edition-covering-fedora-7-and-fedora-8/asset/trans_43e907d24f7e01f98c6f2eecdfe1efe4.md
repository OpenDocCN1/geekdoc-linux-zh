

命令执行结果被存储到一个变量中。例如，如果你想统计当前目录中名为 test.txt 的文件行数，并将结果存储在一个名为 var 的变量中，你可以使用以下命令：

| 命令 | 环境 |
|---|---|
| var=`wc -l test.txt` | bash |
| set var = `wc -l test.txt` | tcsh |

## bash 中的表达式比较

比较数值或评估相似数据之间的差异——例如文件信息、字符串或数字——这一任务被称为*表达式比较*。表达式比较是 shell 程序中使用逻辑完成任务的组成部分。两个操作数（数值或字符串）的逻辑比较方式在不同 shell 中略有不同。在 bash 中，可以使用名为 `test` 的命令来实现表达式的比较。在 tcsh 中，你可以编写表达式来实现相同的功能。

bash shell 语法提供了一个名为 `test` 的命令来比较字符串、数字和文件。`test` 命令的语法如下：

```
test expression
```

或者

```
[ expression ]
```

bash 以相同的方式处理这两种形式的 `test` 命令。`test` 命令支持以下几种类型的比较：

- 字符串比较
- 数值比较
- 文件操作符
- 逻辑操作符

### 字符串比较

以下操作符可用于比较两个字符串表达式：

- `==`——比较两个字符串是否相等
- `!=`——比较两个字符串是否不相等
- `-n`——评估字符串长度是否大于零
- `-z`——评估字符串长度是否等于零

以下是使用这些操作符在名为 `compare1` 的 shell 程序中对两个字符串 `string1` 和 `string2` 进行比较的一些示例：

```bash
#!/bin/sh
string1="abc"
string2="abd"
if [ $string1 = $string2 ]; then
    echo "string1 equal to string2"
else
    echo "string1 not equal to string2"
fi
if [ $string2 != $string1 ]; then
    echo "string2 not equal to string1"
else
    echo "string2 equal to string1"
fi
if [ $string1 ]; then
    echo "string1 is not empty"
else
    echo "string1 is empty"
fi
if [ -n $string2 ]; then
    echo "string2 has a length greater than zero"
else
    echo "string2 has length equal to zero"
fi
if [ -z $string1 ]; then
    echo "string1 has a length equal to zero"
else
    echo "string1 has a length greater than zero"
fi
```

如果你执行 `compare1`，将得到以下结果：

```text
string1 not equal to string2
string2 not equal to string1
string1 is not empty
string2 has a length greater than zero
string1 has a length greater than zero
```

如果两个字符串的长度不相等，系统会用尾随空格填充较短的字符串以进行比较。也就是说，如果 `string1` 的值为 ab，而 `string2` 的值为 abc，为了进行比较，`string2` 会被填充一个尾随空格——其值将变为 abc（后跟空格）。

## 数值比较

以下操作符可用于比较两个数字：

- `-eq`——比较两个数字是否相等
- `-ge`——比较一个数字是否大于或等于另一个数字
- `-le`——比较一个数字是否小于或等于另一个数字
- `-ne`——比较两个数字是否不相等
- `-gt`——比较一个数字是否大于另一个数字
- `-lt`——比较一个数字是否小于另一个数字

以下 shell 程序比较了三个数字 `number1`、`number2` 和 `number3`：

```sh
#!/bin/sh
number1=5
number2=10
number3=5

if [ $number1 -eq $number3 ]; then
    echo "number1 is equal to number3"
else
    echo "number1 is not equal to number3"
fi

if [ $number1 -ne $number2 ]; then
    echo "number1 is not equal to number2"
else
    echo "number1 is equal to number2"
fi

if [ $number1 -gt $number2 ]; then
    echo "number1 is greater than number2"
else
    echo "number1 is not greater than number2"
fi

if [ $number1 -ge $number3 ]; then
    echo "number1 is greater than or equal to number3"
else
    echo "number1 is not greater than or equal to number3"
fi

if [ $number1 -lt $number2 ]; then
    echo "number1 is less than number2"
else
    echo "number1 is not less than number2"
fi

if [ $number1 -le $number3 ]; then
    echo "number1 is less than or equal to number3"
else
    echo "number1 is not less than or equal to number3"
fi
```

当你执行该 shell 程序时，你将得到以下结果：

```
number1 is equal to number3
number1 is not equal to number2
number1 is not greater than number2
number1 is greater than or equal to number3
number1 is less than number2
number1 is less than or equal to number3
```

## 文件操作符

以下操作符可用作文件比较操作符：

- `-d`——判断文件是否为目录
- `-f`——判断文件是否为常规文件
- `-r`——判断是否设置了文件的读权限
- `-s`——判断文件是否存在且长度大于零
- `-w`——判断是否设置了文件的写权限
- `-x`——判断是否设置了文件的执行权限

假设在一个目录中有一个名为 compare3 的 shell 程序，该目录下有一个名为 file1 的文件，以及当前目录下的一个子目录 dir1。假设 file1 的权限为 r-x（读和执行权限），dir1 的权限为 rwx（读、写和执行权限）。该 shell 程序的代码将如下所示：

```sh
#!/bin/sh
if [ -d $dir1 ]; then
    echo "dir1 is a directory"
else
    echo "dir1 is not a directory"
fi
if [ -f $dir1 ]; then
    echo "dir1 is a regular file"
else
    echo "dir1 is not a regular file"
fi
if [ -r $file1 ]; then
    echo "file1 has read permission"
else
    echo "file1 does not have read permission"
fi
if [ -w $file1 ]; then
    echo "file1 has write permission"
else
    echo "file1 does not have write permission"
fi
if [ -x $dir1 ]; then
    echo "dir1 has execute permission"
else
    echo "dir1 does not have execute permission"
fi
```

如果你执行该 shell 程序，你将得到以下结果：

```
dir1 is a directory
file1 is a regular file
file1 has read permission
file1 does not have write permission
dir1 has execute permission
```

### 逻辑操作符

逻辑操作符使用布尔逻辑来比较表达式，通过使用代表 NOT（非）、AND（与）和 OR（或）的字符来比较值。

- `!`——否定一个逻辑表达式
- `-a`——对两个逻辑表达式进行逻辑与运算
- `-o`——对两个逻辑表达式进行逻辑或运算

这个名为 logic 的示例使用了前述 compare3 示例中提到的文件和目录：

```sh
#!/bin/sh
if [ -x file1 -a -x dir1 ]; then
    echo file1 and dir1 are executable
else
    echo at least one of file1 or dir1 are not executable
fi

if [ -w file1 -o -w dir1 ]; then
    echo file1 or dir1 are writable
else
    echo neither file1 or dir1 are writable
fi

if [ ! -w file1 ]; then
    echo file1 is not writable
else
    echo file1 is writable
fi
```

如果你执行 logic，它将产生以下结果：

```
file1 and dir1 are executable
file1 or dir1 are writable
file1 is not writable
```

## 特殊语句：for、while 及其他

Bash 自带各种内置语句，用于处理更复杂的条件检查，例如循环和 switch 块。就像许多其他方面一样，bash 共享相同的语法，因此以下部分适用于两种 shell。

### for 语句

for 语句用于在指定条件为真时执行一组命令，每次执行一次。for 语句有几种格式。bash 使用的第一种格式如下：

```
for curvar in list
do
    statements
done
```

如果你想对 `list` 中的每个值执行一次 `statements`，应使用此形式。在每次迭代中，列表的当前值被分配给 `curvar`。`list` 可以是包含多个项的变量，或者是由空格分隔的值列表。第二种格式如下：

```bash
for curvar
do
   statements
done
```

在此形式中，对于传递给 shell 程序的每个位置参数，`statements` 会执行一次。在每次迭代中，位置参数的当前值被分配给变量 `curvar`。

这种形式也可以写成如下样子：

```bash
for curvar in $@
do
   statements
done
```

请记住，`$@` 提供传递给 shell 程序的位置参数列表，并且以与用户最初调用命令的方式一致的引用形式呈现。

假设你想为目录中的每个文件创建备份版本，并将其存储在一个名为 `backup` 的子目录中。你可以这样在 bash 中操作：

```bash
#!/bin/sh
for filename in *
do

   cp $filename backup/$filename
   if [ $? -ne 0 ]; then
      echo "copy for $filename failed"
   fi
done
```

在上面的示例中，每个文件的备份副本会被创建。如果复制失败，则会生成一条消息。

### while 语句

`while` 语句可用于在指定条件为真时执行一系列命令。一旦指定条件评估为 `False`，循环就会终止。如果指定条件最初评估为 `False`，循环可能根本不会执行。你应该小心使用 `while` 命令，因为如果指定条件从未评估为 `False`，循环将永远不会终止。

