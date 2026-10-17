
```bash
if [ condition ]
then
    commands
fi
```

如果你指定的 `condition` 评估为真逻辑值，shell 将运行 `then` 代码段中的命令。如果 `condition` 评估为假逻辑值，shell 脚本将跳过 `then` 代码段中的命令。

在 bash shell 编程中，条件表达式有相当多种不同的格式。内置了用于数值、字符串值，甚至是文件和目录的测试。表 19-1 列出了可用的不同内置测试。

### 表 19-1 条件测试

| 测试 | 类型 | 描述 |
| :----------------- | :----- | :------------------------------------------------- |
| `n1 -eq n2` | 数值 | 检查 `n1` 是否等于 `n2`。 |
| `n1 -ge n2` | 数值 | 检查 `n1` 是否大于或等于 `n2`。 |
| `n1 -gt n2` | 数值 | 检查 `n1` 是否大于 `n2`。 |
| `n1 -le n2` | 数值 | 检查 `n1` 是否小于或等于 `n2`。 |
| `n1 -lt n2` | 数值 | 检查 `n1` 是否小于 `n2`。 |
| `n1 -ne n2` | 数值 | 检查 `n1` 是否不等于 `n2`。 |
| `str1 = str2` | 字符串 | 检查 `str1` 是否与 `str2` 相同。 |
| `str1 != str2` | 字符串 | 检查 `str1` 是否与 `str2` 不同。 |
| `str1 < str2` | 字符串 | 检查 `str1` 是否小于 `str2`。 |
| `str1 > str2` | 字符串 | 检查 `str1` 是否大于 `str2`。 |
| `-n str1` | 字符串 | 检查 `str1` 的长度是否大于零。 |
| `-z str1` | 字符串 | 检查 `str1` 的长度是否为零。 |
| `-d file` | 文件 | 检查 `file` 是否存在且是一个目录。 |
| `-e file` | 文件 | 检查 `file` 是否存在。 |
| `-f file` | 文件 | 检查 `file` 是否存在且是一个普通文件。 |
| `-r file` | 文件 | 检查 `file` 是否存在且可读。 |
| `-s file` | 文件 | 检查 `file` 是否存在且非空。 |
| `-w file` | 文件 | 检查 `file` 是否存在且可写。 |
| `-x file` | 文件 | 检查 `file` 是否存在且可执行。 |
| `-O file` | 文件 | 检查 `file` 是否存在且由当前用户拥有。 |
| `-G file` | 文件 | 检查 `file` 是否存在且其默认组与当前用户相同。 |
| `file1 -nt file2` | 文件 | 检查 `file1` 是否比 `file2` 更新。 |
| `file1 -ot file2` | 文件 | 检查 `file1` 是否比 `file2` 更旧。 |

按照以下步骤使用条件进行测试：

- 打开你最喜欢的文本编辑器并创建文件 `test5.sh`。

- 在编辑器中输入以下代码：

```bash
#!/bin/bash
# testing the if condition
if [ $1 -eq $2 ]
then
	echo "Both values are equal!"
	exit
fi

if [ $1 -gt $2 ]
then
	echo "The first value is greater than the second"
	exit
fi

if [ $1 -lt $2 ]
then
	echo "The first value is less than the second"
	exit
fi
```

- 保存该文件，然后使用以下命令为其分配执行权限：

```bash
chmod u+x test5.sh
```

- 运行该文件并提供两个数值参数：

```bash
$ ./test5.sh 10 5
The first value is greater than the second
$
```

`test5.sh` 脚本评估在命令行中作为参数输入的两个值。只有评估为真逻辑值的 if-then 语句中的命令会被 shell 脚本处理。

### case 语句

你经常会发现自己试图评估变量的值，在一系列可能的值中寻找特定值，类似于我在上一个示例中演示的那样。与其编写多个 if-then 语句来测试所有可能的条件，不如使用 case 语句。

case 语句允许你以面向列表的形式检查单个变量的多个值：

```bash
case variable in
    pattern1) commands1;;
    pattern2 | pattern3) commands2;;
    *) default_commands;;
esac
```

case 语句将指定的变量与不同的模式进行比较。如果变量与模式匹配，shell 将执行该模式指定的命令。你可以在一行中列出多个模式，使用竖线运算符分隔每个模式。星号符号是捕获所有不匹配任何列出模式的值的通配符。

按照以下步骤编写一个使用 case 语句的脚本：

- 打开你最喜欢的文本编辑器并创建文件 `test6.sh`。

- 在编辑器中输入以下代码：

```bash
#!/bin/bash
# using the case statement

case $USER in
    rich | barbara)
        echo "Welcome, $USER"
        echo "Please enjoy your visit";;
    testing)
        echo "Special testing account";;
    jessica)
        echo "Don't forget to log off when you're done";;
    *)
        echo "Sorry, you're not allowed here";;
esac
```

- 保存该文件并使用以下命令更改执行权限：

```bash
chmod u+x test6.sh
```

- 运行该文件：

```bash
$ ./test6.sh
Welcome, rich
Please enjoy your visit
$
```

case 语句为指定每个可能变量值的各种选项提供了一种更简洁的方式。

## 循环

在编写脚本时，你经常会发现自己处于一种希望多次重复相同命令的情境中，例如对目录中的所有文件应用某个命令。bash shell 提供了一些基本的循环命令来满足这一需求。

### for 循环

for 语句遍历系列中的每个元素，例如目录中的文件或文本文档中的行。for 命令的格式是：

```bash
for variable in series ; do
  commands
done
```

变量变成一个占位符，在每次迭代中取系列中每个元素值。命令可以像你在脚本中定义的其他任何变量一样使用该变量。以下是一个示例，展示了如何使用 for 循环遍历目录中的所有文件。

```bash
$ cat test7.sh
#!/bin/bash
# iterate through the files in the Home folder
for file in $(ls | sort) ; do
 if [ -d $file ]
 then
  echo "${file} is a directory"
 fi
 if [ -f $file ]
 then
  echo "${file} is a file"
 fi
```

完成

如果你运行 `test7.sh` 这个 shell 脚本，你会看到主目录中文件和目录的列表：

```
$ chmod u+x test7.sh
$ ./test7.sh
Desktop is a directory
Documents is a directory
Downloads is a directory
Music is a directory
Pictures is a directory
Public is a directory
Templates is a directory
test1.sh is a file
test2.sh is a file
test3.sh is a file
test4.sh is a file
test5.sh is a file
test6.sh is a file
test7.sh is a file
today.txt is a file
Videos is a directory
$
```

这大大节省了编写代码的工作量，因为你不需要在一堆 `if-then` 或 `case` 语句中手动检查每个文件！

## while 循环
