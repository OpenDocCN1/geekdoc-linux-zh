
$ cat temp
第二句。
这是第四句。
这是第七句。

以下是一个 Bourne Shell 脚本子程序 sub，它可以将一组文件中所有的 REPORT 替换为 report，将 FILE 替换为 file，将 PROCESS 替换为 process。For 结构遍历命令行提供的文件列表。（有关 For 结构的更多信息，请参阅第 640 页。）在处理每个文件时，sub 会在文件上运行 sed 之前显示文件名。该脚本使用了多行嵌入式 sed 指令；只要指令中的 NEW 被引起来（即放在单引号之间），sed 就会接受该多行指令，就就像它出现在单行上一样。每个 Substitute（替换）指令都包含一个 g（全局）标志，以处理一个字符串在某行中出现多次的情况：

```
$ cat sub
for file
echo $file
mv $file $$.subhld
sed 's/REPORT/report/g
s/FILE/file/g
s/PROCESS/process/g' $$.subhld > $file
done
rm $$.subhld
```

```
$ sub file1 file2 file3
file1
file2
file3
```

随后，sed 使用 Write（写入）指令将文件的一部分复制到另一个文件（temp2）。行号 2 和 4 用逗号隔开，选择了 sed 要复制的行范围。此脚本不会修改这些行：

```
$ cat write_demo2
2,4 temp2
```

```
$ sed -n -f write_demo2 new
```

```
$ cat temp2
第二行。
第三行。
这是第四行。
```

脚本 write_demo3 与 write_demo2 非常相似，但在 Write 指令之前使用了 NOT 运算符 (!)，这导致 sed 将内容写入未被地址选中的文件行：

# 1318 sed

```
$ cat write_demo3
2,4 !temp3
```

```
$ sed -n -f write_demo3 new
```

```
$ cat temp3
第一行。
五。
这是第六句。
这是第七行。
第八也是最后。
```

随后，next_demo1 演示了 Next（下一行）指令。当它处理选定的行（第 3 行）时，sed 会立即开始处理下一行，而不打印第 3 行，也不显示第 3 行：

```
$ cat next_demo
3 n
p
```

```
$ sed -n -f next_demo new
第一行。
第二行。
这是第四行。
五。
这是第六句。
这是第七行。
第八也是最后。
```

下一个示例使用了文本地址。第六行包含该字符串，因此 Next 指令导致 sed 不显示该行：

```
$ cat next_demo2
/the/ n
p
```

```
$ sed -n -f next_demo2 new
第一行。
第二行。
第三行。
这是第四行。
五。
这是第七行。
第八也是最后。
```

下组示例使用文件 compound.in 来演示了 sed 指令是如何协同工作的：

```
$ cat compound.in
1. 这一页上的单词...
2. 这一页上的单词...
3. 这一页上的单词...
4. 这一页上的单词...
```

第一个使用 compound.in 的示例指示 sed 在第 1、2、3 行将字符串 words 替换为 text，并在第 2、3、4 行将字符串 text 替换为 TEXT。该示例还选择并删除了第 3 行。结果是第 1 行为 text，第 2 行为 TEXT，没有第 3 行，第 4 行为 words。sed 在第 2 和 3 行进行了两次替换：针对 words 和针对 text。然后 sed 删除了第 3 行：

```
$ cat compound
1,3 s/words/text/
2,4 s/text/TEXT/
3 d
```

```
$ sed -f compound.in
1. 这一页上的文本...
2. 这一页上的 TEXT...
4. 这一页上的单词...
```

下一个示例显示了 sed 脚本中指令的顺序至关重要。两个 Substitute 指令都应用于第二行（如前一个示例所示），但替换发生的顺序改变了结果：

```
$ cat compound2
2,4 s/text/TEXT/
1,3 s/words/text/
3 d
```

```
$ sed -f compound2.in
1. 这一页上的文本...
2. 这一页上的文本...
4. 这一页上的单词...
```

接下来，compound3 在第 2 行后追加了两行。sed 工具显示了文件的所有行，因为命令行上没有出现 -n 选项。脚本末尾的 Print（打印）指令额外显示了 3 行：

```
$ cat compound3
2 a\nThis is line 2a.\nThis is line 2b.
3 p
```

```
$ sed -f compound3 compound.in
1. 这一页上的单词...
2. 这一页上的单词...
This is line 2a.
This is line 2b.
3. 这一页上的单词...
3. 这一页上的单词...
4. 这一页上的单词...
```

下一个示例显示 sed 总是显示追加的内容。在这里第 2 行被删除了，但 Append（追加）指令仍然显示了追加到它的两行。如果你在命令行上使用 -n 选项，则会显示追加行：

```
$ cat compound4
2 a\
This is line 2a.\
This is line 2b.
2 d
```

```
$ sed -f compound4 compound.in
1. 这一页上的单词...
This is line 2a.
This is line 2b.
3. 这一页上的单词...
4. 这一页上的单词...
```

最后的示例在地址中使用了正则表达式。以下指令中的正则表达式（"^"）匹配行开头的一个字符（即匹配每一个非空行）。第二个和第三个斜杠之间的替换字符串包含一个 TAB 字符，后跟一个取符号 (&)。取取符号的值取决于正则表达式匹配到的任何内容：

```
$ sed 's/^/ /&' new
第一行。
第二行。
第三行。
```

这种类型的替换对于缩进文件以创建左边距很有用。有关正则表达式的更多信息请参阅附录 A。

你可能希望将前面的 sed 指令放入 shell 脚本，这样你每次想缩进文件时就不需要记住（并重新输入）它：

```
$ cat indent
sed 's/^/ /&' $*
$ chmod u+x indent
$ indent new
第一行。
第二行。
第三行。
```

当你创建一个认为可能以后再次使用的 sed 指令时，通常将其放入 shell 脚本或脚本文件中是一个好主意，可以节省你重构它的精力。

在下面的 shell 脚本中，正则表达式（两个空格后跟一个 *）匹配行末尾的一个或多个空格。此脚本移除行末尾的空格，这对于清理你使用 vi 创建的文件有用：

```
$ cat cleanup
sed 's/ *//' $*
```

# ssh

在远程计算机上安全地执行命令

ssh [option]|[user@host] [command line]

ssh 工具通过在远程系统上启动一个 shell 来在主机上运行命令行。如果没有命令行，ssh 将将你登录到远程计算机。

ssh 实用程序可以 rsh 和 login，在不安全网络上的两台机器之间提供安全的加密通信。更多信息，请参阅第 374 页的“ssh: Logs in or Runs a Command on a Remote Computer”。

![](img/aa8214d49e1cf50152c4328451293b_1370_0.png)

Arguments host是要登录或在其上运行命令的机器。除非你建立了几种身份验证类型之一，否则 ssh 会提示远程系统的用户名和密码。当 ssh 能够自动登录时，它将以运行 ssh 命令的用户登录，或者就像 ssh 命令行上有 user@ 一样。

命令行在远程系统上运行。如果没有命令行，ssh 将你登录到远程系统。如果不希望本地 shell 在传递给 ssh 之前扩展特殊字符，必须对命令行加引号。

# Options

-l login-name 如果你在远程计算机上的用户名与本地登录名不同，可以使用此选项指定远程登录名。这是在命令行上使用 user@ 的替代方案。

-l login-name -t 为远程机器上的 ssh 进程分配一个伪 tt。如果没有此选项，当你使用 ssh 在远程系统上运行命令时，ssh 不会为进程分配 tt（终端）。相反，ssh 将远程进程的输入和标准输出连接到 ssh 会话：通常但并不总是你所想要的。此选项强制 ssh 在远程机器上分配一个 tty，以便需要 tty 的程序可以工作。

# Notes

参阅第 374 页的“ssh: Logs in or Runs a Command on a Remote Computer”获取有关 ssh 的更多信息。另请参阅第 375 页的可选章节，了解如何使用 ssh 通过隧道创建 VPN 的示例。

