
The `r` command tells vi to read in the contents of the named file to the current position of the cursor. Listing 6.14 shows the result.

##### LISTING 6.14 Contents of the File after Execution of `:r`

```
My bag of Tricks

This command returns the current time in seconds since the epoch:

perl -e 'print time'
```

This function is not restricted to text files only. To read in the output of a command, you could use the following approach shown in Listing 6.15.

##### LISTING 6.15 Reading the Output of Commands (stdout)

```
My bag of Tricks

This command returns the current time in seconds since the epoch:

perl -e 'print time'

Output of commands can be read in with "r !command":

-

-

-

-

:r !ls -l
```

After pressing Enter, the screen looks as shown in Listing 6.16.

##### LISTING 6.16 Result of r !

```
My bag of Tricks

This command returns the current time in seconds since the epoch:

perl -e 'print time'

Output of commands can be read in with "r !command":

total 8

-rw-r--r-- 1 ekeller users 22 2004-06-04 11:09

epoch_time.txt
```

```text
-rw-r--r--    1 ekeller  users        108 2004-06-04 11:11
my_bag_of_tricks.txt
~
~
3 more lines                                      10,1
All
```

此序列适用于所有向标准输出输出文本的命令。

#### 6.2.2.2 fold 命令

当你用 `vi` 等工具编写文档时，行往往会变得很长。工作时行的长度通常不是问题，但一旦文档完成，那些长行有时会妨碍阅读，难以理解。幸运的是，过去有很多人不得不处理这个问题，其成果就是 `fold` 命令。`fold` 只做一件事：它将较长的行折叠成更易于管理的 80 个字符（默认值），或通过 `-w` 参数指定其他长度。为了确保 `fold` 不会拆开单词，使用 `-s` 选项使其仅在最近的空白字符处断行。清单 6.17 演示了该命令。

**清单 6.17** 使用 `fold` 重新格式化文本文件

```text
root@unixhost:~> cat file_with_long_lines.txt
This file contains really long lines, lines that wrap while d
isplayed in a Terminal window. Paragraphs of a documentation
about how long lines can be really annoying and unreadable if
  the cat command is used.
Fortunately there is help, the command fold. Available on alm
ost every *NIX system.
root@unixhost:~> fold -s file_with_long_lines.txt
This file contains really long lines, lines that wrap while displayed
in a Terminal window. Paragraphs of a documentation about how long
lines can be really annoying and unreadable if the cat command is
used.
Fortunately there is help, the command fold. Available on almost every
*NIX system.
root@unixhost:~>
```

#### 6.2.2.3 bc 计算器

`bc` 不是像 `xcalc` 那样的计算器，而是一种计算语言。这种语言本身强大到足以写一本小书，因此作者在此只集中介绍一个方便的功能：在十进制、八进制和十六进制之间进行转换。

例如，要将数字 7 转换为二进制，可以使用清单 6.18 中所示的命令。

**清单 6.18** 使用 `bc` 进行十进制/二进制转换

```text
root@unixhost:~> bc
bc 1.06
Copyright 1991-1994, 1997, 1998, 2000 Free Software Foundation, Inc.
This is free software with ABSOLUTELY NO WARRANTY.
For details type `warranty'.
ibase=10
obase=2
7
111
quit
root@unixhost:~>
```

解释器启动后，命令 `ibase=10` 告诉它，如果输入是数字，则按十进制处理；这是默认设置。第二行 `obase=2` 表示将输出转换为二进制。第三行是数字 7，按下回车后，它被转换为二进制，即 111。最后一个命令 `quit` 退出解释器。如果只需要这个简单的转换，你有一种更快的方法来达到同样的结果，如清单 6.19 所示。

**清单 6.19** 使用管道配合 `bc`

```text
root@unixhost:~> echo "obase=2;7" | bc
111
```

`echo` 输出字符串 `obase=2;7`，并通过管道传给 `bc`。分号充当行分隔符，就像在 `Perl` 或 `C` 中一样。

`bc` 有两个版本，即“原始”版本和扩展的 GNU 版本。后者包含 `print` 命令等，其行为与 `Perl` 中的同名命令有些相似。例如，`Solaris` 默认提供的版本不认识 `print` 命令，但如果需要额外功能，你总是可以安装 GNU 版本。

甚至可以编写用 `bc` 语言编写的程序。清单 6.20 展示了如何利用这一能力。

**清单 6.20** `bc` 程序 `conv_tab.bc`

```text
x=0;
print "\n"
print "dec\tbin\thex\n"
while(x < 21){
    obase=10
    print x, "\t"
    obase=2
    print x, "\t"
    obase=16
    print x, "\n"
    x=x+1
}
quit
```
