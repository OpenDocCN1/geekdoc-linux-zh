

```
{ ls -l; echo "Listing of foo.txt"; cat foo.txt; } > output.txt
```

使用子 shell 类似：

```
(ls -l; echo "Listing of foo.txt"; cat foo.txt) > output.txt
```

使用这种技术我们节省了一些输入，但组命令或子 shell 真正发挥作用的地方在于管道。在构建命令管道时，通常很有用将多个命令的结果合并为单一流。组命令和子 shell 使此操作变得简单：

```
{ ls -l; echo "Listing of foo.txt"; cat foo.txt; } | lpr
```

在这里，我们将三个命令的输出合并并将其通过管道传输到 lpr 的输入，以生成打印报告。

在下面的脚本中，我们将使用组命令并查看可与关联数组结合使用的几种编程技术。该脚本名为 array-2，在给定目录名时，会打印该目录中文件的列表以及文件所有者和组所有者的名称。在列表末尾，脚本会打印每个所有者和组拥有的文件数量的统计。这里我们看到当脚本给定目录 /usr/bin 时的结果（为简洁起见已压缩）：

```
[me@linuxbox ~]$ array-2 /usr/bin
/usr/bin/2to3-2.6              root      root
/usr/bin/2to3                 root      root
/usr/bin/a2p                  root      root
/usr/bin/abrowser             root      root
/usr/bin/aconnnect            root      root
/usr/bin/acpi_fakekey         root      root
/usr/bin/acpi_listen          root      root
/usr/bin/add-apt-repository   root      root
.
.
/usr/bin/zipgrep              root      root
/usr/bin/zipinfo              root      root
/usr/bin/zipnote              root      root
/usr/bin/zip                  root      root
```

```
27  echo
28
29  # List owners
30  echo "File owners:"
31  { for i in "${!owners[@]}"; do
32    printf "%-10s %d file(s)\n" "$i" ${owners["$i"]}
33  done } | sort
34  echo
35
36  # List groups
37  echo "File group owners:"
38  { for i in "${!groups[@]}"; do
39    printf "%-10s %d file(s)\n" "$i" ${groups["$i"]}
40  done } | sort
```

让我们看看这个脚本的运行机制：

第 5 行：关联数组必须使用 declare 命令并带 -A 选项创建。在此脚本中我们按如下方式创建了五个数组：

files 包含目录中的文件名，以文件名作为索引

file_group 包含每个文件的组所有者，以文件名作为索引

file_owner 包含每个文件的所有者，以文件名作为索引

groups 包含属于索引组的 文件数量

owners 包含属于索引所有者的文件数量

第 7-10 行：检查是否传递了有效的目录名作为位置参数。如果没有，则显示用法消息并以退出状态 1 退出脚本。

第 12-20 行：遍历目录中的文件。使用 stat 命令，第 13 行和第 14 行提取文件所有者和组所有者的名称，并将值分配给各自的数组（第 16、17 行），以文件名作为数组索引。同样，文件名本身被分配给 files 数组（第 15 行）。

第 18-19 行：属于文件所有者和组所有者的文件总数各递增一。

第 22-27 行：输出文件列表。这是通过使用 "${array[@]}" 参数扩展实现的，该扩展会展开整个数组元素列表，每个元素作为单独的词处理。这允许文件名中可能包含嵌入的空格。另请注意，整个循环用大括号括起来，从而形成一个组命令。这允许将循环的整个输出通过管道传输到 sort 命令。这是因为数组元素的展开不是排序的。

第 29-40 行：这两个循环与文件列表循环类似，只是它们使用 "${!
array[@]" 扩展，该扩展会展开数组索引列表而不是数组元素列表。

## 进程替换

虽然它们看起来相似并且都可用于合并流以进行重定向，但组命令和子 shell 之间存在重要区别。组命令在其当前 shell 中执行所有命令，而子 shell（顾名思义）则在其当前 shell 的子副本中执行命令。这意味着环境会被复制并提供给 shell 的新实例。当子 shell 退出时，环境的副本会丢失，因此对子 shell 环境所做的任何更改（包括变量赋值）也会丢失。因此，在大多数情况下，除非脚本需要子 shell，否则组命令优于子 shell。组命令速度更快且占用内存更少。

我们在第 28 章中看到了子 shell 环境问题的示例，当时我们发现管道中的 read 命令并不像我们直觉上期望的那样工作。回顾一下，如果我们构建如下管道：

```
echo "foo" | read
echo $REPLY
```

REPLY 变量的内容始终为空，因为 read 命令在子 shell 中执行，而其 REPLY 的副本在子 shell 终止时被销毁。

由于管道中的命令始终在子 shell 中执行，任何分配变量的命令都会遇到此问题。幸运的是，shell 提供了一种称为进程替换的奇特扩展形式，可用于解决此问题。

进程替换有两种表达方式：

对于产生标准输出的进程：

<(list)

或，对于接收标准输入的进程：

>(list)

其中 list 是命令列表。

要解决 read 的问题，我们可以像这样使用进程替换：

```
read < <(echo "foo")
echo $REPLY
```

