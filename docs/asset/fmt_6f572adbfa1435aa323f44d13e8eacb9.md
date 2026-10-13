
最简单的选择是无所作为，但这并不友好。通过告知用户错误并再次要求输入目录名称，您的脚本可以更加友好。`while`循环非常适合执行此操作。事实上，`while`循环的常见用途是确定用户输入是否已正确收集。通常会采用类似以下策略：
- 1. 将变量的值设为空。
- 2. 启动一个在变量值不为空时退出的`while`循环。
- 3. 在`while`循环中，向用户提问并读取用户的响应。
- 4. 验证响应。
- 5. 如果响应无效，则将变量的值设为空。这使`while`循环能够重复。
- 6. 如果响应有效，变量的值不会改变。它继续保存用户的响应。由于变量的值不为空，`while`循环退出。

实现此功能的`while`循环如下

```
RESPONSE=
while [ -z "$RESPONSE" ] ;
do
```

```
echo 'Enter the name of a directory where your files are
located:'
read RESPONSE
if [ ! -d "$RESPONSE" ] ; then
  echo 'ERROR: Please enter a directory pathname.'
  RESPONSE=
fi
done
```

这里，您将用户的响应存储在变量`RESPONSE`中。最初此变量被设为空，使`while`循环开始执行。当`while`循环首次执行时，会提示用户如下：
Enter the name of a directory where your files are located:

用户可以在此提示下输入目录名称。当用户输入完毕并按下 Enter 后，`read`将输入存储到变量`RESPONSE`中。然后您检查以确保输入是目录。如果输入不是目录，您会发出错误消息并重复。会产生错误消息，以便用户知道输入有什么问题。如果用户未输入任何值，变量`RESPONSE`仍为空。在这种情况下，存储在变量`RESPONSE`中的值不是目录，因此会产生错误消息。

### 输入重定向和 while

`while`循环还可以与输入重定向和`read`结合使用，以便一次读取文件的一行。基本语法是

```
while read LINE
do
  :: # manipulate file here
done < file
```

在`while`循环体中，您可以操作指定文件的每一行。这方面的一个简单例子是

```
while read LINE
do
  case $LINE in
    '*root*') echo $LINE ;;
  esac
done < /etc/passwd
```

这里仅显示文件`/etc/passwd`中包含字符串`root`的行。

输出将类似于以下内容：

```
root:x:0:1:Super-User:/sbin/sh
```

### while 和子 Shell

前一个示例中使用的循环存在一个问题：在 Bourne shell 和旧版本的`ksh`中，它是在子 Shell 中执行的。这意味着对脚本环境的任何更改，例如导出变量和更改当前工作目录，在`while`循环完成后可能不会保留。作为示例，请考虑以下脚本：

```
#!/bin/sh
if [ -f "$1" ] ; then
i=0
while read LINE
do
i=`expr $i + 1`
done < "$1"
echo $i
fi
```

此脚本尝试统计作为参数传递给它的文件中的行数。

执行此脚本时使用文件

```
$ cat dirs.txt
/tmp
/usr/local
/opt/bin
/var
```

可能会产生以下不正确的输出：
0

虽然你在`while`循环中使用命令`i=`expr $i + 1``增加`$i`的值，但在`while`循环完成后，`$i`的值并未保留。在这种情况下，你需要在`while`循环内部更改变量的值，然后在循环外部使用该值。解决此问题的一种方法是先进入循环前重定向 STDIN，然后在循环完成后恢复 STDIN。基本语法是

```
exec n<&0 < file
while read LINE
do
: # manipulate file here
done
exec 0<&n
```

这里，`n`是一个大于 2 的整数，`file`是你想要读取的文件名。通常`n`选择为 3、4 或 5 这样的小数字。这样就可以构造一个 shell 版本的`cat`命令，如下所示：

```
#!/bin/sh
if [ $# -ge 1 ] ; then
  for FILE in "$@"
  do
    exec 4<&0 < "$FILE"
    while read LINE ; do echo $LINE ; done
    exec 0<&4 4<&-
  done
fi
```

### until 循环

`while`循环非常适合在某个条件为真时执行一组命令的情况，但有时你需要执行一组命令直到某个条件为真。`until`循环可在`ksh`、`bash`和`zsh`中使用，提供此功能。其语法是

```
until cmd
do
  list
done
```

这里`cmd`是一个单一命令，而`list`是一组一个或多个命令。虽然`cmd`可以是任何有效的 UNIX 命令，但它通常是第 11 章“流程控制”中介绍的类型测试表达式。

`until`循环的执行与`while`循环类似：
- 1. 执行`cmd`。
- 2. 如果`cmd`的退出状态为非零，则退出`until`循环。
- 3. 如果`cmd`的退出状态为零，则执行`list`。
- 4. 当`list`执行完毕后，返回步骤 1。

如果`cmd`和`list`都很短，`until`循环可以写成单行，如下所示：
```
until cmd ; do list ; done
```

在大多数情况下，`until`循环等同于使用 `!`运算符否定`cmd`的`while`循环。例如，以下`while`循环

```
x=1
while [ ! $x -ge 10 ]
do
  echo $x
  x=`expr $x + 1`
done
```

等同于以下`until`循环：

```
x=1;
until [ $x -ge 10 ]
do
  echo $x
  x=`expr $x + 1`
done
```

`until`循环与等价的`while`循环相比没有优势。由于它不被 Bourne shell 支持，大多数程序员不偏爱它。这里介绍它是为了完整性。

### for 和 select 循环

与`while`循环在某个条件为假时退出不同，`for`和`select`循环操作于项目列表。本节详细介绍这两种循环。

#### for 循环

`for`循环使你能够对列表中的每个项目重复执行一组命令。它最常见的用途之一是对大量文件执行相同的一组命令。基本语法是

```
for name in word1 word2 ... wordN
do
  list
done
```

这里`name`是变量的名称，`word1`到`wordN`是由空格分隔的字符序列（单词）。每次`for`循环执行时，变量`name`的值都会被设置为单词列表中的下一个单词，`word1`到`wordN`。第一次，`name`被设置为`word1`；第二次，它被设置为`word2`；以此类推。这意味着`for`循环执行的次数取决于指定的单词数量。例如，如果向`for`循环指定以下单词
there comes a time
the loop would execute four times. In each iteration of the for loop, the commands specified in list are executed.

循环将执行四次。在`for`循环的每次迭代中，`list`中指定的命令都会被执行。

`for`循环可以写成单行，如下所示：
`for name in word1 word2 ... wordN ; do list ; done`

如果`list`和单词数量都很短，通常会选择单行形式；否则，优先选择多行形式。

一个简单的`for`循环示例是

```
for i in 0 1 2 3 4 5 6 7 8 9
do
  echo $i
done
```

此循环按如下方式计数到九：
- 0
- 1
- 2
- 3
- 4
- 5
- 6
- 7
- 8
- 9

请注意，虽然输出与`while`循环相同，但`for`循环做的事情完全不同。在每次迭代中，`$i`被设置为列表中的下一个项目。当列表结束时，循环退出。在此示例中，你选择列表为 0 到 9 的数字。在`while`循环中，下一个要显示的数字是计算得出的，并不属于预先确定的列表。

如果你稍微更改列表，请注意输出如何变化：

```
for i in 0 1 2 4 3 5 8 7 9
do
  echo $i
done
```

- 0
- 1
- 2
- 4
- 3
- 5
- 8
- 7
- 9

### 操作一组文件
