
```
locate foo
/usr/lib/texmf/tex/latex/misc/footnpag.sty
/usr/share/automake/footer.am
/usr/share/games/fortunes/food
/usr/share/games/fortunes/food.dat
/usr/share/gimp/patterns/moonfoot.pat
```

locate 的输出包含绝对路径中关键字“foo”，或没有输出。

## ls
语法： ls [-laRl] file or directory

ls 命令允许你在目录中列出文件（和子目录）。它是 Linux 中最受欢迎的程序之一。下面的表 A-3 显示了 ls 的一些更受欢迎的选项。

### 表 A-3 ls 的常用选项

| 选项 | 显示内容 |
| -1 | 仅显示当前目录中的文件和目录名称 |
| -l | 长列表，包含文件和目录权限信息、大小、修改日期等 |
| -a | 当前目录中的所有文件和目录（包括名称以句点开头的文件） |
| -R | 递归显示子目录（如果有）的内容 |

## mkdir
语法： mkdir directory . . .

要创建目录，请使用 mkdir 命令。选择目录名时只有两个限制：（1）文件名最长可达 255 个字符，（2）目录名可以包含除 / 之外的任何字符。例如，以下示例在当前目录中创建三个子目录：

```
mkdir dir1 dir2 dir3
```

## mv
语法： mv [-if] sourcefile targetfile

使用 mv 命令移动或重命名目录和文件。该命令根据目标文件是否为现有目录来执行移动或重命名操作。为说明，假设你想将名为 foo 的目录改名为 foobar。

```
mv foo foobar
```

因为 foobar 不存在为目录，所以 foo 变为 foobar。如果你执行以下命令

```
mv doc.txt foobar
```

并且 foobar 是一个已存在的目录，你执行的是移动操作。文件 doc.txt 现在位于 foobar 目录中。

-f 选项会删除已存在的目标文件且从不提示用户。-i 选项会提示用户是否覆盖每个已存在的目标文件。如果响应不以“y”或“Y”开头，则文件将被跳过。

## pico
语法： pico [filename]

这个全屏文本编辑器非常用户友好，非常适合从 Windows 或 MS-DOS 环境迁移过来的用户。

## pwd
语法： pwd

此命令打印当前工作目录。显示的目录显示绝对路径。显示的目录中没有硬链接或软符号链接。

```
pwd
/home/usr/charmaine
```

## rm
**语法：** `rm [-rif] directory/file`

要删除文件或目录，请使用 rm 命令。以下是一些示例：

```
rm doc.txt
rm ~/doc.txt
rm /tmp/foobar.txt
```

使用 rm 删除多个文件时，可以使用通配符或逐个输入文件。例如，

```
rm doc1.txt doc2.txt doc3.txt
```

等价于：

```
rm doc[1-3].txt
```

rm 是一个功能强大的命令，如果使用不当会造成混乱。例如，假设你花了六个月时间完成的论文保存在当前工作目录中。你决定删除目录中的所有文档，以为自己在另一个目录中。在发现备份文件不存在（并且你不再否认）之后，你会想知道是否有什么办法可以防止这种情况发生。

rm 命令具有 -i 选项，可使 rm 交互式运行。这会告诉 rm 在删除每个文件之前征求你的许可。例如，如果你输入：

```
rm -i *.doc
rm: remove thesis.doc (yes/no)? n
```

-i 选项为你提供了一个降落伞。是否拉开绳索（回答 no）或承受后果（回答 yes）取决于你。-f 选项完全相反；-f（强制）选项告诉 rm 删除你指定的所有文件，而不管文件权限如何。只有在你 100% 确定要删除正确的文件（们）时才使用 -f 选项。

要删除目录及其内部的所有文件和目录，请使用 -r 选项。rm -r 将删除整个子树，如下所示：

```
rm -r documents
```

如果你不确定自己在做什么，请将 -r 选项与 -i 选项结合使用，如下所示：

```
rm -ri documents
```

上述示例在删除每个文件和目录之前会征求你的许可。

## sort
语法： sort [-rnd u] [-o outfile] [infile/sortedfile]

该命令执行的明显任务是对文件进行排序。然而，sort 还可以合并文件。sort 命令读取包含已排序数据的并将它们合并为一个大的已排序文件。使用 sort 的最简单方法是排序单个文件并在屏幕上显示结果。如果文件 a.txt 包含以下内容：

```
b
c
a
d
```

对 a.txt 进行排序并将结果显示到屏幕：

```
sort a.txt
a
b
c
d
```

要保存排序结果，请使用 -o 选项：sort -o sorted.txt a.txt 将排序后的 a.txt 文件保存到 sorted.txt 中。要使用 sort 合并已存在的已排序文件并将输出保存到 sorted.txt 中，请使用以下命令：

```
sort -o sorted.txt a.txt b.txt c.txt
```

该命令的 -r 选项会反转排序顺序。因此，如果使用 -r 选项，包含字母表字母的文件将按 z 到 a 的顺序排序。

-d 选项按字典顺序对文件进行排序。sort 命令仅考虑字母、数字和空格，忽略其他字符。

-u 选项查找相同的行并抑制除一行外的所有行。因此，sort 只产生唯一的行。

## stat
语法： stat file

此程序显示文件或目录的各种统计信息。例如：

```
stat foo.txt
```

此命令显示以下输出：

```
File: "foo.txt"
Size: 4447232      Filetype: Regular File
Mode: (0644/-rw-r--r--)  Uid: ( 0/root)  Gid: (0/root)
Device: 3,0  Inode: 16332      Links: 1
Access: Mon Mar  1 21:39:43 1999(00000.02:32:30)
Modify: Mon Mar  1 22:14:26 1999(00000.01:57:47)
Change: Mon Mar  1 22:14:26 1999(00000.01:57:47)
```

你可以看到以下内容被显示：文件访问时间；修改时间；更改日期；大小；所有者和组信息；权限模式；等等。

## strings
语法： strings filename

strings 命令打印至少四个字符长的字符序列。你主要使用此实用程序来描述非文本文件的内容。

## tail
**语法：** tail [-count | -fr] filename

tail 命令显示文件的末尾。默认情况下，tail 显示文件的最后 10 行。要显示文件 doc.txt 的最后 50 行，请执行以下命令：

```
tail -50 doc.txt
```

-r 选项以相反顺序显示输出。默认情况下，-r 显示文件中的所有行，而不仅仅是 10 行。例如，要以相反顺序显示文件 doc.txt 的全部内容，请使用以下命令：

```
tail -r doc.txt
```

要以相反顺序显示文件 doc.txt 的最后 10 行，请使用以下命令：

```
tail -10r doc.txt
```

![](img/9eb7e89292d2f85707b4d49102c865b7_568_0.png)

-f 选项在监视文件时很有用。有了此选项，tail 会等待其他程序将新数据写入文件。当其他程序向文件添加新数据时，tail 会在屏幕上显示数据。要停止 tail 监视文件，请按 Ctrl+C（中断键），因为 tail 命令不会自行停止。

## touch
**语法：** touch file or directory

此命令更新文件或目录的时间戳。如果指定的文件不存在，touch 会将其创建为空文件。

## umask
请参阅第 4 章中关于用户默认文件权限的部分。

## uniq
**语法：** `uniq [-c] filename`

uniq 命令比较相邻行并仅显示一个唯一行。当与 -c 选项一起使用时，uniq 会计算出现次数。例如，一个具有以下内容的文件

```
a
a
a
b
a
```

使用 uniq 时会产生以下结果：

```
uniq test.txt

a
b
a
```

注意相邻的 a 被删除了，但文件中并非所有的 a 都被删除。这是使用 uniq 时需要记住的一个重要细节。如果你想找到名为 test.txt 的文件中的所有唯一行，可以运行以下命令：

```
sort test.txt | uniq
```

此命令对 test.txt 文件进行排序并将所有相似的行放在彼此相邻的位置，使 uniq 只能显示唯一的行。例如，假设你想快速找到有多少唯一访客访问你的网站；你可以运行以下命令：

```
awk '{print $1}' access.log | sort | uniq
```

这会显示 CLF 日志文件中的唯一 IP 地址，而 Apache Web 服务器使用 CLF 日志文件来记录访客。

## vi
vi 程序是一个功能强大的全屏文本编辑器，你可以在几乎所有 Unix 系统上找到它。vi 编辑器不需要太多...
