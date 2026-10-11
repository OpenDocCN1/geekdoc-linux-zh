
```
$ cat test4
#!/bin/bash
# 使用变量保存列表

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

`$list` 变量包含用于迭代的标准文本值列表。注意，代码还使用另一个赋值语句将项目添加（或连接）到 `$list` 变量中包含的现有列表。这是一种常见的向存储在变量中的现有文本字符串末尾添加文本的方法。

## 从命令中读取值

生成列表中包含的值的另一种方法是使用命令的输出。你使用命令替换执行任何产生输出的命令，然后在 `for` 命令中使用该命令的输出：

```
$ cat test5
#!/bin/bash
# 从文件中读取值

file="states.txt"

for state in $(cat $file)
do
    echo "Visit beautiful $state"
done
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

此示例在命令替换中使用 `cat` 命令来显示 `states.txt` 文件的内容。注意，`states.txt` 文件将每个州放在单独的一行上，而不是用空格分隔。`for` 命令仍然一次遍历 `cat` 命令输出的每一行，假设每个州都在单独的一行上。然而，这并没有解决数据中包含空格的问题。如果你列出一个包含空格的州名，`for` 命令仍然将每个单词视为单独的值。这是有原因的，我们将在下一节中查看。

**注意**

`test5` 代码示例仅使用不含路径的文件名将文件名赋值给变量。这要求文件必须位于与脚本相同的目录中。如果情况并非如此，您需要使用完整的路径名（绝对路径或相对路径）来引用文件位置。

### 更改字段分隔符

此问题的根源在于特殊环境变量 `IFS`（内部字段分隔符）。`IFS` 环境变量定义了一组字符列表，`Bash` shell 使用这些字符作为字段分隔符。默认情况下，`Bash` shell 将以下字符视为字段分隔符：

- 空格
- 制表符
- 换行符

如果 `Bash` shell 在数据中看到这些字符中的任意一个，它会假设您正在列表中开始一个新的数据字段。在处理可能包含空格的数据（例如文件名）时，正如您在之前的脚本示例中看到的那样，这可能会让人烦恼。

为了解决这个问题，您可以暂时更改 shell 脚本中的 `IFS` 环境变量值，以限制 `Bash` shell 识别为字段分隔符的字符。例如，如果您希望将 `IFS` 值更改为仅识别换行符，您需要执行以下操作：

```bash
IFS=$'\n'
```

将此语句添加到您的脚本中，即可告知 `Bash` shell 忽略数据值中的空格和制表符。将这种技术应用到之前的脚本中，会得到以下结果：

```bash
$ cat test5b
#!/bin/bash
# reading values from a file

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
```

现在，shell 脚本可以使用列表中包含空格的值。

> **警告**
>
> 在处理长脚本时，您可能会在某个地方更改 `IFS` 值，然后忘记它，并假设脚本其他地方的值是默认值。养成一种安全的做法很有帮助：在更改 `IFS` 值之前保存其原始值，并在完成后恢复它。
>
> 这种技术可以这样编码：
>
> ```bash
> IFS.OLD=$IFS
> IFS=$'\n'
> <在代码中使用新的 IFS 值>
> IFS=$IFS.OLD
> ```
>
> 这确保了在脚本未来的操作中，`IFS` 值恢复为默认值。

`IFS` 环境变量还有其他出色的应用。假设您想要遍历由冒号分隔的文件中的值（例如 `/etc/passwd` 文件中的值）。您只需要将 `IFS` 值设置为冒号即可：

```bash
IFS=:
```

如果您想指定多个 `IFS` 字符，只需在赋值行将它们字符串化连接在一起：

```bash
IFS=$'\n':;"
```

该赋值使用换行符、冒号、分号和双引号字符作为字段分隔符。使用 `IFS` 字符解析数据的方式没有限制。

### 使用通配符读取目录

最后，您可以使用 `for` 命令自动遍历文件目录。为此，您必须在文件或路径名中使用通配符。这会强制 shell 使用*文件通配*。文件通配是指生成与指定通配符匹配的文件名或路径名的过程。

当您不知道所有文件名时，此功能在处理目录中的文件时非常有用：

```bash
$ cat test6
#!/bin/bash
# iterate through all the files in a directory
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
```

`for` 命令遍历 `/home/rich/test/*` 列表的结果。代码使用 `test` 命令（使用方括号方法）测试每个条目，查看它是目录（即使用 `-d` 参数）还是文件（即使用 `-f` 参数）。更多详情，请参见第 11 章“基本脚本构建”。

请注意，在此示例中，我在 `if` 语句测试中做了一些不同的操作：

```bash
if [ -d "$file" ]
```

在 Linux 中，目录和文件名中包含空格是完全合法的。为了适应这种情况，您应该用双引号将 `$file` 变量括起来。如果您不这样做，当您遇到包含空格的目录或文件名时，将会得到错误：

```bash
./test6: line 6: [: too many arguments
./test6: line 9: [: too many arguments
```

`Bash` shell 将额外的单词解释为 `test` 命令中的参数，从而导致错误。
