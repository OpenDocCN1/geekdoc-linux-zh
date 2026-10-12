

## grep

**语法：** `grep [options] pattern [file...]`

grep 命令允许你在一个或多个文件中搜索特定的字符模式。包含该模式的每一行都将显示在终端上。当你有大量文件并想找出哪些文件包含特定单词或短语时，grep 命令非常有用。

使用 `-v` 选项，你可以显示不匹配模式的行。也许你想选取 `data.txt` 中*不*包含单词 `the` 的行：

```
grep -vw 'the' data.txt
```

如果未指定 `-w` 选项，则包含 the 的任何单词都会匹配，例如 toge[the]r。`-w` 选项指定模式必须是完整单词。`-i` 选项在搜索模式时忽略大小写差异。

## head

**语法：** `head [-count | -n number] filename`

head 命令显示文件的前几行。默认情况下，显示文件的前十行。不过，你可以使用上述选项指定不同的行数。以下示例说明如何查看文本文件 doc.txt 的前两行：

```
head -2 doc.txt
# Outline of future projects
# Last modified:  02/02/01
```

## ln

**语法：** `ln [-s] sourcefile target`

ln 命令创建两种类型的链接：硬链接和软链接。链接可以被视为文件的另一个名称。创建链接后，它与原始文件无法区分。具有硬链接的文件，直到所有链接都被移除，才会从硬盘上删除。不使用 `-s` 选项创建硬链接：

```
ln ./www ./public_html
```

然而，硬链接确实有局限性：它既不能链接到另一个目录，也不能链接到另一个文件系统上的文件。但是，通过使用 `-s` 选项，你可以创建软链接，从而消除这些限制：

```
ln -s /dev/fs02/jack/www /dev/fs01/foo/public_html
```

前面的命令在文件系统 2 上的目录 www 和文件系统 1 上新创建的文件 public_html 之间创建了一个软链接。

## locate

**语法：** `locate keyword`

locate 命令查找特定文件或命令的路径。locate 会查找精确匹配或子串匹配。例如：

```
locate foo
/usr/lib/texmf/tex/latex/misc/footnpag.sty
/usr/share/automake/footer.am
/usr/share/games/fortunes/food
/usr/share/games/fortunes/food.dat
/usr/share/gimp/patterns/moonfoot.pat
```

locate 产生的输出将在绝对路径中包含关键字 foo，或者根本没有任何输出。

## ls

**语法：** `ls [-laRl] file or directory`

ls 命令允许你列出目录中的文件（和子目录）。它是最常用的程序之一。配合 `-1` 选项使用时，ls 命令仅显示当前目录中的文件和目录名称。使用 `-l` 选项时，将显示包含文件/目录权限信息、大小、修改日期等的长列表格式。使用 `-a` 选项可查看当前目录中的所有文件和目录（包括名称以句点开头的）。`-R` 选项允许命令递归显示子目录的内容（如果有）。

## mkdir

**语法：** `mkdir directory ...`

要创建目录，请使用 `mkdir` 命令。选择目录名时仅有两个限制：文件名最长可达 255 个字符，目录名称可以包含除 `\` 以外的任何字符。

以下示例在当前目录中创建三个目录，前提是当前目录具有写权限：

```
mkdir dir1 dir2 dir3
```

## mv

**语法：** `mv [-i-f] sourcefile targetfile`

使用 `mv` 命令移动或重命名目录和文件。该命令将执行移动或重命名，具体取决于 `targetfile` 是否为现有目录。举例来说，假设你想将一个名为 `foo` 的现有目录重命名为 `foobar`：

```
mv foo foobar
```

因为 `foobar` 不存在作为目录，所以 `foo` 将被重命名为 `foobar`。如果发出以下命令

```
mv doc.txt foobar
```

且 `foobar` 是现有目录，则将执行移动操作。文件 `doc.txt` 现在将位于目录 `foobar` 中。

`-f` 选项删除现有目标文件且从不提示用户。`-i` 选项提示用户是否覆盖每个已存在的目标文件。如果响应不以 `y` 或 `Y` 开头，则跳过该文件。

## pico

**语法：** `pico [filename]`

`pico` 是一个全屏文本编辑器，非常用户友好，高度适合从 MS Windows 或 DOS 环境迁移到 Linux 的用户。

## pwd

**语法：** `pwd`

pwd 命令打印当前工作目录。显示的目录将是绝对路径。显示的目录均不会是硬链接或软符号链接。

## rm

**语法：** `rm [-rif] directory/file`

要删除文件或目录，请使用 `rm` 命令。以下是一些示例：

```
rm doc.txt
rm ./doc.txt
rm /tmp/foo.txt
```

要使用 `rm` 删除多个文件，请使用通配符或单独键入每个文件。例如，

```
rm doc1.txt doc2.txt doc3.txt
```

等同于

```
rm doc[1-3].txt
```

如果使用不当，`rm` 是一个可能造成混乱的强力命令。例如，假设你在电脑上存放了一篇论文，你为此辛苦工作了过去六个月。你决定 `rm` 所有文档，错误地以为你在另一个目录中，而不是存放论文的那个目录。在发现不存在备份文件（且你不再否认现实）后，你会想知道是否本可以以某种方式防止这个错误。

`rm` 命令的 `-i` 选项使 `rm` 具有交互性。它告诉 `rm` 在删除每个文件前询问你的许可。例如，如果你输入

```
rm -i *.doc
rm: remove thesis.doc (yes/no)? n
```

`-i` 选项给了你一把“降落伞”，询问你是否拉绳（回答 no，默认）还是承担后果（回答 yes）。`-f` 选项则完全相反。`-f`（强制）选项告诉 rm 删除你指定的所有文件，而不管文件权限如何。仅当你 100% 确定要删除正确的文件时才使用 `-f` 选项。

要删除目录及其内部的所有文件和目录，请使用 `-r` 选项。`rm -r` 将删除整个子树：

```
rm -r documents
```

如果你不确定自己在做什么，请将 `-r` 选项与 `-i` 选项结合使用：

```
rm -ri documents
```

前面的示例在删除每个文件和目录前都会请求你的许可。

## sort

**语法：** `sort [-rndu] [-o outfile] [infile/sortedfile]`

该命令执行的显而易见的任务是排序。然而，sort 还可以合并文件。sort 读取包含预先排序数据的文件，并将它们合并为一个大的已排序文件。

要保存排序结果，请使用 `-o` 选项：`sort -o sorted.txt a.txt` 将把排序后的 a.txt 文件保存在 sorted.txt 中。要使用 sort 将现有的已排序文件合并为一个文件并将输出保存在 sorted.txt 中，请使用以下命令：

```
sort -o sorted.txt a.txt b.txt c.txt
```

该命令的 `-r` 选项反转排序顺序。因此，如果一行包含字母表中的字母，使用 `-r` 选项将按 z 到 a 的顺序排序。

`-d` 选项按字典顺序排序文件。sort 仅考虑字母、数字和空格，忽略其他字符。

`-u` 选项查找相同的行并仅保留一行，抑制其他行。因此，sort 仅产生唯一的行。

## stat

**语法：** `stat file`

该程序显示文件或目录的各种统计信息。例如，

```
stat foo.txt
```

显示以下输出：

```
File: "foo.txt"
  Size: 4447232      Filetype: Regular File
  Mode: (0644/-rw-r----)  Uid: (  0/root)   Gid: (  0/root)

Device: 3,0   Inode: 16332     Links: 1

Access: Mon Mar  1 21:39:43 2000 (00000.02:32:30)
Modify: Mon Mar  1 22:14:26 2000 (00000.01:57:47)
Change: Mon Mar  1 22:14:26 2000 (00000.01:57:47)
```

正如你所见，此输出显示了文件访问、修改、状态改变日期、大小、所有者和组信息、权限模式等。

## strings

**语法：** `strings filename`

strings 命令打印至少四个字符长的字符序列。此实用程序主要用于描述非文本文件的内容。

## tail

**语法：** `tail [-count | -n number] filename`

tail 命令显示文件的末尾。默认情况下，tail 显示文件的最后 10 行。要显示文件 doc.txt 的最后 50 行，请发出此命令：

```
tail -50 doc.txt
```

