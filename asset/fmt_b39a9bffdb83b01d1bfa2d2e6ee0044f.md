
然而，`more`有一些局限性。例如，在上面的`ps`示例中，`more`无法向上滚动。`less`命令被作为一个比`more`更强大、更友好的工具而创建。`less`引入时有一句俗言：“Less is indeed more！”我们建议你不再使用`more`，而是使用`less`。

> 注意：`less`还有另一个值得注意的优点。与`vi`等文本编辑器不同，它在启动时不会读取整个文件。这导致在查看大文件时启动速度更快。

`less`命令可以使用与上面示例中相同的语法：

```
$ ps auxw | less      分页查看 ps 的输出

$ myfile.txt | less    分页查看文件内容

$ myfile.txt         分页查看文本文件
```

`less`允许你使用上下方向键、`PageUp`、`PageDown`和空格键进行导航。如果你在文件上使用`less`（而不是标准输入），按`p`键可以在`vi`中打开当前文件。`less`使用的编辑器来自`VISUAL`环境变量，或者在未设置`VISUAL`的`EDITOR`环境变量。如果都没有设置，`less`默认使用`vi`。与`vi`一样，`Shift+g`将你带到文件末尾。`Shift+f`将你带到文件末尾，然后在添加新输入时向下滚动，类似于`tail -f`。

按`Ctrl+c`中断该模式。与`vi`一样，使用`less`查看文件时，可以通过按`/`（斜杠）后跟字符串并回车来搜索字符串。要搜索后续出现的内容，重复按`/`和回车。

使用`less`向前和向后滚动，分别使用`f`和`b`键。例如，`10f`向前滚动10行，`15b`向后滚动15行。输入`d`向下滚动半屏幕，输入`u`向上滚动半屏幕。

## 使用 pr 分页文本文件

`pr`命令提供了一种快速将大量文本格式化为可以打印的形式。如果你想打印某些命令的结果，而无需打开文字处理器或文本编辑器，这会特别快。通过`pr`，你可以使用日期、时间、文件名和页码等头部信息格式化文本页。这里有一个示例：

```
$ rm -qa | sort | pr --column=2 | less  两列显示包列表
```

在这个示例中，`rpm -qa`命令列出系统中安装的所有软件包，并将该列表传递给`sort`命令进行字母排序。该列表随后被传递给`pr`命令，它将单列列表转换为两列（`--columns=2`）并分页。最后，通过`less`命令进行分页。

与其分页输出，你可以将输出发送到打印机。示例：

```
$ rpm -qa | sort | pr --column=2 > file
```

使用`pr`可以进行的其他文本处理包括取消分页（`-d`）、控制列数（`-c`）或偏移文本（`-t`）。

## 使用 grep 搜索文本

`grep`命令在需要搜索字符串时非常有用。事实上，它可以显示包含匹配项的行。示例：

```
$ grep "error" /var/log/syslog

$ grep -i "critical" /var/log/syslog
```

`grep`命令允许使用`-B`和`-A`标志显示匹配项之前之后的行。例如：

```
$ grep -B 2 "error" /var/log/syslog

$ grep -A 2 "error" /var/log/syslog
```

它还可以使用`-c`标志来统计匹配模式的行数。

```
$ grep -c "error" /var/log/syslog
```

## 使用 sort 输出

对文件内容或命令输出进行排序也很有用。这对于整理无序的输出非常有帮助。以下示例列出了当前已安装的所有 RPM 包的名称，提取任何包含`apparmor`名称的包，并按字母数字顺序对结果进行排序（正向和反向）：

```
$ rpm -qa | grep apparmor | sort

$ rpm -qa | grep apparmor | sort -r
```

以下命令根据内存使用（`ps`输出的第四字段）对进程进行排序。`-k`选项指定了用于排序的键字段。`4, 4`表示第四字段且仅限第四字段是键字段。

```
$ ps aux | sort -k 4,4
```

以下命令行按大小从小到大的顺序对已加载的内核模块进行排序。`n`告诉`sort`将第二个字段视为数字而不是字符串：

```
$ lsmod | sort -k 2,2n
```

## 使用 Strings 在二进制文件中查找文本

有时你需要读取二进制文件内部的 ASCII 文本。通过这种方式你可以了解到很多关于可执行文件的信息。在这种情况下，使用`strings`来提取所有人类可读的 ASCII 文本。`strings`命令是`binutils`包的一部分。这里是一些示例：

```
$ strings /bin/ls | grep -i libc 在 ls 中查找 libc 的出现情况

$ cat /bin/ls | strings 列出 ls 中所有的 ASCII 文本

$ strings /bin/ls 列出 ls 中的 ASCII 文本
```

## 使用 sed 替换文本

在文件中查找文本有时是替换文本的第一步。使用`sed`命令进行文本流编辑。`sed`命令实际上是一种完整的脚本语言。在本章的示例中，我们介绍了使用`sed`命令进行基础文本替换。

如果你熟悉`sed`中的文本替换命令，`sed`有一些相似之处。在下面的示例中，你仅会将每行中第一次出现的`francois`替换为`chris`。在这里，`sed`从管道获取输入，并将输出发送到`stdout`（你的屏幕）：

```
$ cat myfile.txt | sed s/francois/chris/
```

在替换行末尾添加`g`（如下面的命令所示），会导致`francois`的所有出现都被改为`chris`。此外，在下面的示例中，输入重定向自`myfile.txt`，输出重定向到`myfile.txt`：

```
$ cat myfile.txt | sed s/francois/chris/g > myfile.txt
```

## 第 5 章：处理文本

下一个示例替换了`/etc/apache2/http.conf`文件中每行第一次出现的`/var/www`。在这里，必须使用引号和反斜杠来转义正斜杠，以免它们被解释为分隔符：

```
$ sed 's\/var\/www/\/home\/www/' /etc/apache2/http.conf
```

正斜杠是`sed`的默认分隔符，你可以将分隔符更改为任何字符。当字符串包含斜杠时，更改分隔符可以让你的工作变得更容易。例如，之前的命令可以使用以下命令：

在第一行中，连字符（`-`）被用作分隔符。在第二种情况下，字母`D`是分隔符。

```
$ sed 's/var/www/-/home/www/-' /etc/apache2/http.conf
```

`sed`命令可以通过在每个替换前加上`-e`来同时运行多个替换。在这里，在`myfile.txt`文本流中，`francois`的所有出现处都被改为`FRANCOIS`，`chris`的出现处都被改为`CHRIS`：

```
$ sed -e s/francois/FRANCOIS/g -e s/chris/CHRIS/g < myfile.txt
```

你可以使用`sed`向文本流添加换行符。其中`<Enter>`出现在第二行是由`bash`生成的，而不是手动输入的。

```
$ echo aaabccc | sed 's/$/n'

aaa

ccc
```

当你需要替换换行符时，使用`tr`命令会更简单。

## 使用 tr 翻译或删除字符

`tr`命令是即时进行字符翻译的一种简单方法。在下面的示例中，换行符被替换为空格，因此所有文件输出在同一行：

```
$ ls | tr '\n' ' ' 将换行符替换为空格
```

`tr`命令可将一个字符替换为另一个，但它不像`sed`那样工作。下面的命令将文件中的所有小写`f`替换为大写`F`。

```
$ tr f F < myfile.txt 将文件中的每个 f 替换为 F
```

## 两个文件之间的差异

你也可以使用`tr`命令简单的删除字符。这里有两个示例：

```
$ ls | tr -d '\n' 删除换行符（结果为一行）

$ tr -d f myfile.txt 从文件中删除每个字母 f
```

`tr`命令在指定处理字符范围时可以进行一些巧妙的操作。这里有一个将小写`chris`转换为大写字母的示例：

```
$ echo chris | tr a-z A-Z 将 chris 转换为 CHRIS

CHRIS
```

可以通过以下语法获得相同的结果：

```
$ echo chris | tr '[:lower:]' '[:upper:]' 将 chris 转换为 CHRIS
