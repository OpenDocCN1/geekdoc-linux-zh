

## 替换空行和制表符

另一个有选项是 -s，它将任意数量的空行替换为单个空行（删除文件中多余的空白，同时保留结构）。

例如：

```
userbible-> cat gapfruits
apple
```

orange
peach

pear

```
userbible-> cat -s gapfruits
apple
```

orange
peach

pear

```

-T 将制表符（tabs）替换为可见字符 (^)：

```
userbible-> cat morefruits
kiwi	mango
pear	quince
```

```
userbible-> cat -T morefruits
kiwi^Imango
pear^quince
```

第一行有一个制表符，第二行是空格。有时制表符和空格之间的区别非常重要：例如在 Makefile 和制表符分隔的文件中。-T 选项让你能够轻松辨别它们。

## 理解二进制文件

如果你对包含不可打印字符的二进制文件执行 cat（例如，可执行文件或由 Microsoft Word 等应用程序创建的文件），你仍然会在屏幕上看到很多“垃圾”内容，在某些情况下，你的终端会混乱，导致提示符之前的字符显示错误。cat -v 选项通过更智能地显示不可打印字符来避免垃圾内容。因此，使用 cat -v wordfile.doc 是比纯文本查看此类文件的更好方法。另请参见本章中关于 strings 和 anti- 命令的章节。

## 第三部分 ◆ 在 SUSE Linux 中使用命令行

如果你的终端设置混乱，导致提示符由奇怪的字符组成，通常可以通过输入命令 `reset` 来补救局面。在你输入时，你可能会看到屏幕上出现错误的字符，但只要你按下回车键，终端应该恢复正常。这无论你使用的是文本控制台、xterm 还是 KDE konsole 窗口都适用。

## tac

tac 命令的作用几乎与 cat 相同，但它是反序显示文件的行：

```
user:-> cat fruits
apple
banana
cherry
```

```
user:-> tac fruits
cherry
banana
apple
```

注意，tac 并不提供 cat 的所有选项。

## zcat

zcat 命令解压 gzipped 文件并执行与 cat 相同的操作。例如，SUSE 安装磁盘上的 INDEX.gz 文件是一个 gzipped 文本文件，包含磁盘上软件包的索引。使用 zcat INDEX.gz 可以查看其内容。

## head

head 命令从文件顶部输出部分内容。默认情况下，它输出前十行，但通过选项 -n 后跟一个数字，它可以输出任意数量的行。例如，head -n5 file 输出文件的前五行。

## tail

tail 命令输出包括末尾在内的文件部分。同样，默认情况下输出最后几行，但如果与数字选项一起使用，它可以像之前描述 head 命令那样输出任意数量的行。

一个非常有用的选项是 -f（用于持续跟随），它会随着文件的增长输出追加的数据。这允许你在对其他地方进行更改的同时监控日志文件，例如：

```
# tail -f /var/log/messages
```

## 第 10 章 ♦ 文本处理 273

结合 head 和 tail 显然可以为你提供从文件中获取某些特定行的简单方法：

```
user@bible:-> cat file1
line 1
line 2
line 3
line 4
line 5
line 6
```

```
user@bible:-> head -n file| tail -n2
line 4
line 5
```

所以你提取了文件前五行中的最后两行。

## expand

expand 命令将制表符转换为空格。让我们使用在“替换空行和制表符”节中使用的同一个示例：

```
user@bible:-> cat morefruits
kiwi
mango
pear
quince
```

```
user@bible:-> cat -T morefruits
kiwi"Imango"
pear
quince
```

```
cat morefruits | expand | cat -T
kiwi
mango
pear
quince
```

通过管道将文件内容通过 expand 命令，你将制表符转换成了空格。cat -T 的输出显示制表符已经消失。这是整理包含混合制表符和空格空白文件的方便方法。

## nl

nl 命令输出带有行号的文件，类似于 cat -n。但它有各种选项来调节行的格式以及它们的应用方式。例如：

```
user@bible:/media/cdrom/ > zcat INDEX.gz | nl -n ri | head -n1000 tail -3
00998 /CD1/user/1586/ethtool-1.8-123.1586.rpm
00999 /CD1/user/1586/evlog-1.6.0-31.1586.rpm
001000 *
```

在这个示例中，你得到了未解的 INDEX.gz 文件（来自 SUSE 安装媒体的索引文件）前 1,000 行中的最后 3 行，并带有前零一直编号到 i。-n 选项允许你指定编号格式。我们选择了 rz 作为编号格式，它表示右对齐并带有前零。

## uniq

uniq 命令输出删除除了相邻相同行的文件。它不会删除不相邻的重复行。例如：

```
user@bible:-> cat fish
angfish
bream
bream
cod
dfish
cod
```

```
user@bible:-> uniq fish
angfish
bream
cod
dfish
cod
```

uniq 命令在检查唯一性之前可以跳过特定数量的字段或字符。例如：

```
user@bible:-> cat numberedfish
1 angfish
2 bream
3 bream
4 cod
5 dogfish
6 cod
```

```
user@bible:-> uniq -f1 numberedfish
1 angfish
2 bream
4 cod
5 dogfish
6 cod
```

-f1 选项告诉 uniq 命令在判断行是否匹配时跳过文件的第一个字段。因为第 2 行和第 3 行相同，所以第 3 行被删除了。

## sort

sort 命令如其名——对文件的行进行排序。默认按字母排序，如第二个代码块所示。在第三个代码块中，你可以看到 -r 选项将字母排序变为了反向排序，将文件从 z 到 a 进行排序。

```
usable:-> cat animals
cobra
aardark
zebra
duck
elephant
```

```
usable:-> sort animals
aardark
cobra
duck
elephant
zebra
```

```
usable:-> sort -r animals
zebra
elephant
duck
cobra
aardark
```

有很多选项：最重要的是 -n（数字排序）和 -u（用于唯一：跳过重复行）。

## 从文件中提取行

在这一节中，我们将考虑更具挑战性的任务：根据某些标准从文本文件中提取你需要的精确行或行部分。

## grep

grep 命令是全局正则表达式打印器（global regular expression printer）。这意味着它不仅可以在文件中搜索特定字符串并输出出现该字符串的行，还可以搜索遵循特定模式的文本并输出匹配的行。例如，模式可以是单个大写字母后跟两个或多个数字、英国邮编、有效的美国社会安全号码、以若干空格后跟小写字母开头的行，或任何可以用类似术语描述的内容。

在最简单的情况下，你可以使用 grep 输出文件中包含某个特定字符串的行：

```

@bible:-> cat file2
albatross
bat
hit
Batman
bathroom
debit
ding
doubt
dingbat
```

```
user@bible:-> grep bat file2
albatross
bat
bathroom
dingbat
```

包含精确字符串 bat 的行被选中了。注意你没有在输出中看到 Batman，因为 grep 默认是区分大小写的。若要进行不区分大小写的搜索，你需使用 grep -i：

```
user@bible:-> grep -i bat file2
albatross
bat
Batman
bathroom
dingbat
```

## grep 选项

在正则表达式表示中，点（.）代表单个字符，因此像 b.t 的表达式表示字母 b 后面跟任何其他字符，最后是字母。搜索包含此类序列的任意行的命令：

```
user@bible:-> grep b.t file2
albatross
bat
bathroom
debit
dingbat
```

搜索以字母 d 开头的行：

```
user@bible:-> grep ^d file2
debit
doubt
```

在这里，符号 ^ 代表行的开头。同样，符号 $ 代表行的结尾，所以 bat$ 搜索行尾的字符串 bat：

```
user@bible:-> grep bat$ file2
bat
dingbat
```

要搜索包含字母 d 后跟任意字符再跟字母的行，请使用：

```
user@bible:-> grep d.*t file2
debit
doubt
dingbat
```

* 符号表示前面字符的零或多次重复。

这些示例仅触冰一角。

grep -v 意味着输出不包含表达式的行。例如在这里你找到了不包含 bat 字符串且不以 d 开头的行：

```
user@bible:-> grep -v bat file2| grep -v ^d
bit
```

下面是一个更实用的示例：

```
# grep [0-9]* /var/log/2/access.log | grep -i googlebot
```

（可能）列出了 Apache 日志文件 9 日中所有来自 Google 搜索引擎机器人的访问。当然，这略显原始；你没有指定日志字符串的字段。

## 正则表达式与 grep

在日志中查找正则表达式是你最想要经常使用的内容。在这种情况下，你也可能构建形式为 grep [grep]|grep-v . . . 的长命令。

例如涉及英国（UK）邮编的 grep。英国邮编看起来像这样：OX5 2AX、N1 5JD 和 AL13 4RG。为了在文件中搜索此类类型的字符串，你使用以下命令：

```
# grep -E `[a-zA-Z]{1,2} *[0-9]{1,2} [a-zA-Z]{1,2}` file
```

grep -E 意味着你正在使用扩展正则表达式。在这里，你正在寻找一个或两个字母，后跟任意数量的空格、一个或两个数字、一个或两个字母。

