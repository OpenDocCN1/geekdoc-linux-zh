
chown false mknod sed ypdomainname
cp fgrep more setserial zcat
cpio gawk mount sh
csh grep mt sleep
date gunzip mv sort

**新术语** 正则表达式是一种特殊字符串指定模式的语言。ls 命令支持使用通配符和正则表达式，这意味着你可以使用与 find 和 locate 命令中看到的示例类似且更复杂的选项。例如，如果你只想在当前目录中搜索文本文件，可以使用以下命令：

```
# ls *.txt
```

最后，如果你想查看系统上的所有文件，可以使用 ls -R 选项，它会递归遍历目录以显示其内容。虽然你可以使用这种方法搜索文件并建立系统文件的目录，但请注意，列出文件可能需要几分钟时间。列表中还可能包含你不想列出的文件，或其他操作系统文件系统上的文件，例如 DOS 或 Windows，特别是如果你使用以下命令：

```
# ls -R /
```

更好的方法可能是使用 -d 选项与 -R 配合使用，只列出一定数量的目录层级。例如，以下命令搜索根（/）目录沿线的三个目录层级：

```
# ls -Rd /*/*/*
```

然而，有一个更好的工具可以让你了解系统的目录结构——tree——将在下一节中讨论。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_103_0.png)

> 你喜欢 ls -AF 显示目录的方式吗？你希望 ls 始终使用颜色吗？如果你希望 ls 命令始终显示这种详细程度，请参阅第 6 小时。

## 使用 dir 和 vdir 命令列出目录

如果你实在无法掌握使用 ls 列出目录，可以使用 dir 或 vdir 命令。与 ls 相比，这些命令只有大约 45 个命令行选项，但功能同样强大。它们的工作方式与 ls 类似，但具有某些默认值。

dir 命令的工作方式与默认的 ls 命令类似，以排序的列形式列出文件，如以下示例所示：

```
# dir
01_hyph.dat    49_thes.dat    bin            help           store
01_spell.dat   Desktop        config         install.ini    template
01_thes.dat    LICENSE        database       instdb.ins     wordbook
44_hyph.dat    README         download       kino           xp3
44_spell.dat   addin          explorer       l_soffice.xpm
44_thes.dat    autotext       filter         lib
49_hyph.dat    backup         fonts          s_soffice.xpm
49_spell.dat   basic          gallery        sofficecrc
```

vdir 命令的工作方式与 ls -l 选项类似，默认以长格式列出，如下所示：

```
# vdir
total 3659
-rw-rw-rw- 1 bball users 65605 Oct 27 10:00 01_hyph.dat
-rw-rw-rw- 1 bball users 313015 Oct 27 10:00 01_spell.dat
-rw-rw-rw- 1 bball users 375808 Oct 27 10:00 01_thes.dat
-rw-r--r-- 1 bball users 65605 Oct 27 10:00 44_hyph.dat
-rw-r--r-- 1 bball users 313015 Oct 27 10:00 44_spell.dat
-rw-r--r-- 1 bball users 380928 Oct 27 10:00 44_thes.dat
-rw-rw-rw- 1 bball users 51765 Oct 27 10:00 49_hyph.dat
-rw-rw-rw- 1 bball users 602497 Oct 27 10:00 49_spell.dat
-rw-rw-rw- 1 bball users 1191936 Oct 27 10:00 49_thes.dat
drwxr-xr-x 2 bball users 1024 Dec 2 11:21 Desktop
-rw-r--r-- 1 bball users 11631 Oct 27 10:00 LICENSE
-rw-r--r-- 1 bball users 8435 Oct 27 10:00 README
drwxr-xr-x 3 bball users 1024 Dec 2 11:21 addin
drwxr-xr-x 2 bball users 1024 Dec 2 11:21 autotext
drwxr-xr-x 2 bball users 1024 Dec 30 15:41 backup
drwxr-xr-x 2 bball users 1024 Dec 17 11:43 basic
drwxr-xr-x 2 bball users 2048 Dec 2 11:22 bin
drwxr-xr-x 11 bball users 3072 Jan 4 09:52 config
drwxr-xr-x 2 bball users 1024 Dec 2 11:30 database
drwxr-xr-x 2 bball users 1024 Dec 2 11:20 download
drwxr-xr-x 2 bball users 1024 Dec 2 11:20 explorer
drwxr-xr-x 2 bball users 1024 Dec 2 11:22 filter
drwxr-xr-x 4 bball users 1024 Dec 2 11:20 fonts
drwxr-xr-x 14 bball users 2048 Dec 2 11:22 gallery
drwxr-xr-x 4 bball users 1024 Dec 2 11:21 help
-rw-r--r-- 1 bball users 15569 Dec 2 11:22 install.ini
-rw-r--r-- 1 bball users 274209 Dec 17 11:20 instdb.ins
drwxr-xr-x 2 bball users 1024 Dec 2 11:21 kino
-rw-r--r-- 1 bball users 5199 Oct 27 10:00 l_soffice.xpm
drwxr-xr-x 2 bball users 3072 Dec 2 11:21 lib
-rw-r--r-- 1 bball users 812 Oct 27 10:00 s_soffice.xpm
-rw-r--r-- 1 bball users 8406 Jan 4 09:52 sofficecrc
drwxr-xr-x 3 bball users 1024 Dec 2 11:38 store
drwxr-xr-x 13 bball users 1024 Dec 17 11:43 _template
drwxr-xr-x 2 bball users 1024 Dec 2 12:08 wordbook
drwxr-xr-x 5 bball users 1024 Dec 2 11:20 xp3
```

虽然 dir 或 vdir 没有单独的手册页（它们在 ls 手册页中提到），但你可以使用 --help 选项获取每个命令的帮助。

## 使用 cat 命令列出和合并文件

cat（连接文件）命令用于将文件内容发送到屏幕。你也可以使用此命令将文件内容发送到其他文件，使用一种称为输出重定向的过程。本节向你展示此命令的一些基本用法。有关标准输入、标准输出和重定向的更多信息，请参阅第 6 小时。虽然 cat 可用于读取短文件，但通常用于合并、创建、覆盖或追加文件。要使用 cat 查看短文件，可以输入以下命令：

```
# cat test.txt
This text file was created by the cat command.
Cat could be the world's simplest text editor.
If you read this book, you'll learn how to use cat.
This is the last line of text in this file.
```

cat 命令还有许多选项。如果你想查看带行号的文件，以便标记特定短语，可以使用 -n 选项：

```
# cat -n test.txt
1 This text file was created by the cat command.
2 Cat could be the world's simplest text editor.
3 If you read this book, you'll learn how to use cat.
4 This is the last line of text in this file.
```

你也可以使用 cat 同时查看多个文件，因为 cat 接受通配符：

```
# cat -n test*
1 This text file was created by the cat command.
2 Cat could be the world's simplest text editor.
3 If you read this book, you'll learn how to use cat.
4 This is the last line of text in this file.
5 This is the first line of test2.txt.
6 This file was also created by cat.
7 This is the last line of test2.txt.
```

正如你所见，cat 也会在输出中包含第二个文件，并对输出的每一行编号，而不是对每个文件编号。请注意，你也可以使用以下命令同时查看两个文件：

```
# cat test.txt test2.txt
```

输出与使用通配符时完全相同。

但查看多个文件只是使用 cat 的一种方式。你也可以使用 cat 命令与重定向运算符（>）来合并文件。例如，如果你想将 test.txt 和 test2.txt 合并到名为 test3.txt 的第三个文件中，可以使用以下命令：

```
# cat test* > test3.txt
```

你可以按如下方式检查结果：

```
# ls -l test*
-rw-r--r-- 1 bball users 190 Jan  4 16:06 test.txt
-rw-r--r-- 1 bball users 108 Jan  4 16:07 test2.txt
-rw-r--r-- 1 bball users 298 Jan  4 16:07 test3.txt
```

但如果想在不创建更大的第三个文件的情况下合并 test.txt 和 test2.txt 呢？在这种情况下，你首先决定是想将 test.txt 的内容放入 test2.txt，还是将 test2.txt 的内容放入 test.txt。然后，使用 cat 与 >> 重定向运算符，输入以下命令：

```
# cat test.txt >> test2.txt
```

这会将 test.txt 的内容追加到 test2.txt 的末尾。要检查结果，再次使用 cat：

```
# cat test2.txt
This is the first line of test2.txt.
This file was also created by cat.
This is the last line of test2.txt.
This text file was created by the cat command.
Cat could be the world's simplest text editor.
If you read this book, you'll learn how to use cat.
This is the last line of text in this file.
```

请注意，你也可以按如下方式输入命令：

```
# cat -n test.txt >> test2.txt
```

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_106_0.png)
