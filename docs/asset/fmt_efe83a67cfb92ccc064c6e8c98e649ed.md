
上一个示例中 `echorepeat` 脚本里的 `seq` 命令通过反引号（命令替换）执行，其作用仅仅是生成供 `for` 结构处理的字符串列表。另外注意，在上一个示例中，`NUM` 变量并没有在循环体内进行处理。

# while 结构

`while` 结构是 shell 脚本中另一种常用的循环结构。与 `for` 结构不同，`while` 结构以测试语句开始。只要（或当）测试返回真，循环内的命令就会执行。当测试语句返回假时，`while` 循环内的命令停止执行。`while` 结构通常会设置一个变量（计数器变量），其值在每次循环时都会变化。为了让 `while` 结构正常工作，必须设置好：当计数器达到特定值时，测试语句返回假。这防止了循环无限执行。

`while` 结构的语法如下：

```
while this returns true
do
  these commands
done
```

下面的示例说明了 `while` 结构的一用法。

```
[root@server1 ~]# cat echorepeat
!/bin/bash
COUNTER=0
while [ $COUNTER -lt 7 ];
do
  echo "All work and no play makes Jack a dull boy" >> /tmp/redrum
  COUNTER=`expr $COUNTER + 1`
done
```

```
[root@server1 ~]#
[root@server1 ~]# ./echorepeat
[root@server1 ~]# cat /tmp/redrum
All work and no play makes Jack a dull boy
All work and no play makes Jack a dull boy
All work and no play makes Jack a dull boy
All work and no play makes Jack a dull boy
All work and no play makes Jack a dull boy
All work and no play makes Jack a dull boy
All work and no play makes Jack a dull boy
[root@server1 ~]#_
```

上面的脚本创建了一个名为 `COUNTER` 的计数器变量并将其设置为 0。接下来，`while` 结构使用测试语句在执行循环内命令之前确定 `COUNTER` 的值是否小于 7。`COUNTER` 变量的初始值为 0，它将文本 "All work and no play makes Jack a dull boy" 追加到 `/tmp/redrum` 文件中并将 `COUNTER` 变量的值加 1。注意包裹 `expr` 命令的反引号，这是对 `COUNTER` 变量进行数值加 1（0 = 1）所必需的。在阶段 (i) ，`COUNTER` 变量的值仍小于 7，`while` 结构再次执行命令。该过程重复直到 `COUNTER` 变量的值等于 7。

> 你可以使用 `true` 或 `:` 来代替测试语句，以创建一个无限执行的 `while` 结构。

# until 结构

`until` 结构仅仅是 `while` 结构的相反；它以测试语句开始，循环内的命令一直执行直到测试语句返回真。因此，`until` 通常包含一个计数器变量，并且语法与 `while` 结构几乎相同：

```
until this returns true
do
this commands
done
```

例如，下面的 `until` 结构等同于上一个示例中的 `while` 结构：

```
[root@server1 ~]# cat echorepeat
!/bin/bash
COUNTER=0
until [ $COUNTER -eq 7 ];
do
  echo "All work and no play makes Jack a dull boy" >> /tmp/redrum
  COUNTER=`expr $COUNTER + 1`
done
```

```
[root@server1 ~]#
[root@server1 ~]# ./echorepeat
[root@server1 ~]# cat /tmp/redrum
All work and no play makes Jack a dull boy
All work and no play makes Jack a dull boy
All work and no play makes Jack a dull boy
All work and no play makes Jack a dull boy
All work and no play makes Jack a dull boy
All work and no play makes Jack a dull boy
All work and no play makes Jack a dull boy
[root@server1 ~]#
```

# 第 7 节 使用 BASH

## 特殊变量

shell 脚本在执行时可以接收参数；这些参数被称为位置参数，可以在 shell 内部使用特殊变量进行引用。`$1` 代表第一个参数的内容，`$2` 代表第二个参数的内容，`$3` 代表第三个参数的内容，以此类推。如果参数超过九 个，可以使用大括号来指示相应的位置参数；例如，`${10}` 代表第十个参数的内容。特殊变量 `$0` 代表本身。

下面的示例说明了位置参数的使用：

```
[root@server1 ~]# cat pptest
#!/bin/bash
echo The command you typed was: $0
echo The first argument you typed was: $1
echo The second argument you typed was: $2
echo The third argument you typed was: $3
[root@server1 ~]# chmod a+x pptest
[root@server1 ~]# ./pptest
The command you typed was: ./pptest
The first argument you typed was:
The second argument you typed was:
The third argument you typed was:
[root@server1 ~]# ./pptest one two three
The command you typed was: ./pptest
The first argument you typed was: one
The second argument you typed was: two
The third argument you typed was: three
[root@server1 ~]# _
```

## Shell 扩展

通常使用 `$` 字符来扩展变量。但是，可以使用大括号来指定变量名。例如，要返回以 `HOST` 开头的变量名，可以使用 `${HOST*}` 语法。

```
[root@server1 ~]# echo ${HOST*}
HOSTNAME HOSTTYPE
[root@server1 ~]#
```

或者，你可以使用 `${VAR:=value}` 语法在创建变量的同时返回其值，如下面的示例所示：

```
[root@server1 ~]# echo ${MYVAR:="This is a sample variable"}
This is a sample variable
[root@server1 ~]# _
```

# 第 7 章 使用 Bash 壳 387

使用位置参数是提示用户输入的一种高效的替代方案。例如，你可以修改本章之前描述的 `testmkdir` 脚本，使用两个位置参数来指定源文件和目标目录。每次运行脚本时，都可以指定不同的参数来执行不同的操作，如下所示：

```bash
[root@server1 ~]# cat testmkdir
#!/bin/bash
#此脚本需要两个参数：file> 和 <target directory>
if mkdir $2
then
cp $1 $2
echo "The $1 file was successfully copied to $2"
else
echo "The $2 directory could not be created."
fi
```
