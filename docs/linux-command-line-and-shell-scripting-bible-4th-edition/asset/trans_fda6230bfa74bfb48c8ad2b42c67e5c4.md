
现在 `for` 命令能够正确区分不同的值。此外，请注意，当你使用双引号将值括起来时，Shell 不会将引号作为值的一部分包含在内。

## 从变量中读取列表

在 Shell 脚本中，常见的情形是你先累积一个存储在变量中的值列表，然后需要遍历该列表。你也可以使用 `for` 命令来实现这一点：

```bash
$ cat test4
#!/bin/bash
# 使用变量来存储列表

list="Alabama Alaska Arizona Arkansas Colorado"
list=$list" Connecticut"

for state in $list
do
    echo "Have you ever visited $state?"
done
$ ./test4
Have you ever visited Alabama?
Have you ever visited Alaska?
Have you ever visited Arizona?
Have you ever visited Arkansas?
Have you ever visited Colorado?
Have you ever visited Connecticut?
$
```

`$list` 变量包含用于迭代的值的标准文本列表。请注意，代码还使用了另一个赋值语句将一项添加到（或拼接）现有在 `$list` 变量中包含的列表中。这是一种将文本添加到存储在变量中的现有字符串末尾的常见方法。

## 从命令中读取值

生成列表中值的另一种方法是使用命令的输出。你使用命令替换来执行任何产生输出的命令，然后在 `for` 命令中使用该命令的输出：

```bash
$ cat test5
#!/bin/bash
# 从文件中读取值

file="states.txt"

for state in $(cat $file)
do
    echo "Visit beautiful $state"
done
```

```text
$ cat states.txt
Alabama
Alaska
Arizona
Arkansas
Colorado
Connecticut
Delaware
Florida
Georgia
$ ./test5
Visit beautiful Alabama
Visit beautiful Alaska
Visit beautiful Arizona
Visit beautiful Arkansas
Visit beautiful Colorado
Visit beautiful Connecticut
Visit beautiful Delaware
Visit beautiful Florida
Visit beautiful Georgia
$
```

此示例使用命令替换中的 `cat` 命令来显示文件 `states.txt` 的内容。请注意，`states.txt` 文件中每个州都位于单独的一行上，而不是用空格分隔。假设每个州都在单独的一行上，`for` 命令仍然逐行遍历 `cat` 命令的输出。然而，这并未解决数据中包含空格的问题。如果你列出一个包含空格的州名，`for` 命令仍然将每个单词视为一个独立的值。其中原因将在下一节中讨论。

### 注意

`test5` 代码示例仅使用文件名而没有路径将文件名赋值给变量。这要求文件必须与脚本位于同一目录中。如果情况并非如此，你需要使用完整的路径名（绝对路径或相对路径）来引用文件位置。

## 更改字段分隔符

造成此问题的原因是特殊环境变量 `IFS`，即*内部字段分隔符*。`IFS` 环境变量定义了 Bash Shell 用作字段分隔符的字符列表。默认情况下，Bash Shell 将以下字符视为字段分隔符：

- 空格
- 制表符
- 换行符

如果 Bash Shell 在数据中检测到这些字符中的任何一个，它假设你正在列表中开始一个新的数据字段。在处理可能包含空格的数据（例如文件名）时，这可能会很麻烦，正如你在前面的脚本示例中所看到的那样。

为了解决这个问题，你可以暂时更改 Shell 脚本中 `IFS` 环境变量的值，以限制 Bash Shell 识别为字段分隔符的字符。例如，如果你想更改 `IFS` 值以仅识别换行符，你需要这样做：

```bash
IFS=$'\n'
```

在你的脚本中添加此语句会告诉 Bash Shell 忽略数据值中的空格和制表符。将此技术应用于前面的脚本会产生以下结果：

```bash
$ cat test5b
#!/bin/bash
# 从文件中读取值
file="states.txt"
IFS=$'\n'
for state in $(cat $file)
do
    echo "Visit beautiful $state"
done
$ ./test5b
Visit beautiful Alabama
Visit beautiful Alaska
Visit beautiful Arizona
Visit beautiful Arkansas
Visit beautiful Colorado
Visit beautiful Connecticut
Visit beautiful Delaware
Visit beautiful Florida
Visit beautiful Georgia
Visit beautiful New York
Visit beautiful New Hampshire
Visit beautiful North Carolina
$
```

现在，Shell 脚本可以使用列表中包含空格的值。

### 警告

在处理长脚本时，你可能在一个地方更改了 IFS 值，然后忘记了它，并在脚本的其他地方假设它是默认值。养成一种安全的做法是在更改之前保存原始的 IFS 值，并在完成后恢复它。

该技术可以这样编码：

```bash
IFS_OLD=$IFS
IFS=$'\n'
<在代码中使用新的 IFS 值>
IFS=$IFS_OLD
```

这确保了 IFS 值在脚本内的未来操作中恢复为默认值。

`IFS` 环境变量的其他出色应用也是可能的。假设你想要遍历文件中由冒号分隔的值（例如 `/etc/passwd` 文件中的值）。你只需将 `IFS` 值设置为冒号：

```bash
IFS=:
```

如果你想要指定多个 `IFS` 字符，只需在赋值行上将它们串联起来：

```bash
IFS=$'\n:;'
```

此赋值使用换行符、冒号、分号和双引号字符作为字段分隔符。使用 `IFS` 字符解析数据的方式没有限制。

## 使用通配符读取目录

最后，你可以使用 `for` 命令自动遍历目录中的文件。为此，你必须在文件或路径名中使用通配符字符。这会强制 Shell 使用*文件通配*（file globbing）。文件通配是生成匹配指定通配符字符的文件名或路径名的过程。

当你不知道所有文件名时，此功能非常适合处理目录中的文件：

```bash
$ cat test6
#!/bin/bash
# 遍历目录中的所有文件

for file in /home/rich/test/*
do

if [ -d "$file" ]
then
echo "$file is a directory"
elif [ -f "$file" ]
then
echo "$file is a file"
fi
done
$ ./test6
/home/rich/test/dir1 is a directory
/home/rich/test/myprog.c is a file
/home/rich/test/myprog is a file
/home/rich/test/myscript is a file
/home/rich/test/newdir is a directory
/home/rich/test/newfile is a file
/home/rich/test/newfile2 is a file
/home/rich/test/testdir is a directory
/home/rich/test/testing is a file
/home/rich/test/testprog is a file
/home/rich/test/testprog.c is a file
$
```

`for` 命令遍历 `/home/rich/test/*` 列表的结果。代码使用 `test` 命令（使用方括号方法）测试每个条目，查看它是目录（使用 `-d` 参数）还是文件（使用 `-f` 参数）（参见[第 11 章](#)，“基础脚本构建”）。

在这个示例中，请注意我们在 `if` 语句测试中做了一些不同的事情：

```bash
if [ -d "$file" ]
```

在 Linux 中，拥有包含空格的目录和文件名是完全合法的。为了适应这种情况，你应该用双引号将 `$file` 变量括起来。如果你不这样做，当你遇到包含空格的目录或文件名时，你将遇到错误：

```text
./test6: line 6: [: too many arguments
./test6: line 9: [: too many arguments
```

Bash Shell 将额外的单词解释为 `test` 命令中的参数，从而导致错误。

你还可以通过在 `for` 命令中列出一系列目录通配符，将目录搜索方法和列表方法组合在同一个 `for` 语句中：

```bash
$ cat test7
#!/bin/bash
# 遍历多个目录

for file in /home/rich/.b* /home/rich/badtest
do
    if [ -d "$file" ]
    then
    echo "$file is a directory"
elif [ -f "$file" ]
then
echo "$file is a file"
else
echo "$file doesn't exist"
fi
done
$ ./test7
/home/rich/.backup.timestamp is a file
/home/rich/.bash_history is a file
/home/rich/.bash_logout is a file
/home/rich/.bash_profile is a file
/home/rich/.bashrc is a file
/home/rich/badtest doesn't exist
$
```

`for` 语句首先使用文件通配符遍历由通配符字符产生的文件列表；然后遍历列表中的下一个文件。你可以在列表中组合任意数量的通配符条目进行遍历。

![](img/a5025f22e05b92f409563a958cac7312_476_0.png)

## 尝试 C 风格的 for 命令

如果你曾使用 C 编程语言进行过任何编程，你可能会惊讶于 Bash Shell 使用 `for` 命令的方式。在 C 语言中，`for` 循环通常定义一个变量，然后该循环在每次迭代中自动修改该变量。通常，
