
# 扁平土地

在清单 4.20 中，最后一条命令将 *ed* 脚本 `switch.sh` 显示到标准输出。该脚本将修改 `n.txt` 文件，如清单 4.21 所示。

## 清单 4.21：通过 *ed* 脚本修改文件

```
$ diff -q n.txt random.txt
Files n.txt and random.txt differ
$
$ ed n.txt < switch.sh
21
52
$
$ diff -q n.txt random.txt
$
```

在清单 4.21 中，`diff` 命令对两个文件进行简单比较。请注意，它向 STDOUT 发送了一条消息，指出这两个文件不同。然后使用了 *ed* 实用程序。为了执行清单 4.21 中由 `diff` 命令创建的脚本，使用了 STDIN 重定向运算符。清单 4.21 中的最后一条命令表明这两个文件之间现在没有任何差异。

# 管道命令

如果你真想在 Linux 命令行上实现强大且快速的结果，你需要探索管道（pipes）。管道是一个简单的重定向运算符，由 ASCII 字符 124（`|`）表示，称为竖线、垂直斜杠或垂直线。

**提示**：请注意，某些键盘和文本显示器不将竖线显示为单条垂直线。相反，它看起来像垂直的双短横线。

使用管道，你可以在同一个命令行上将多个命令之间的 STDOUT、STDIN 和 STDERR 进行重定向。这才是强大的重定向。

使用管道符号进行重定向的基本语法如下：

```
`command 1 | command 2 [ | command n], . . .`
```

管道重定向的语法表明，第一个命令 **command1** 被执行。其 STDOUT 被重定向为第二个命令 **command2** 的 STDIN。此外，你可以管道连接的命令数量可以超过两个。请记住，管道中的任何命令的 STDOUT 都会被重定向为管道中下一个命令的 STDIN。清单 4.22 展示了管道重定向的简单用法。

## 清单 4.22：使用管道重定向

```
$ grep /bin/bash /etc/passwd | wc -l
3
$
```

在清单 4.22 中，管道中的第一个命令在密码文件中搜索任何以 /bin/bash 结尾的记录。这基本上就是找到所有使用 Bash shell 作为默认账户 shell 的用户账户。管道中第一个命令的输出作为输入传递给管道中的第二个命令。`wc -l` 命令将计算由 `grep` 命令生成的行数。结果表明，在这个 Linux 系统上，只有三个账户将 Bash shell 设置为默认 shell。

你可以富有创意地使用管道重定向。清单 4.23 展示了一个命令，该命令在一个管道中使用了超过四种不同的实用程序来审计使用 /sbin/nologin 默认 shell 的账户。

## 清单 4.23：对多个命令使用管道重定向

```
$ grep /sbin/nologin /etc/passwd | cut -d ":" -f 1 | sort | less
abrt
adm
avahi
bin
chrony
[...]
:
```

在清单 4.23 中，`grep` 命令的输出作为输入传递给 `cut` 命令。`cut` 实用程序仅从每个密码记录中删除第一个字段，即账户用户名。`cut` 命令的输出用作输入传递给 `sort` 命令，该命令按字母顺序对用户名进行排序。最后，`sort` 实用程序的输出作为输入管道传递给 `less` 命令，以便悠闲地浏览账户用户名。

在你希望保留命令管道输出的副本同时查看其内容的情况下，`tee` 命令会有所帮助。类似于水管中的 T 型接头，水流被发送到多个方向，`tee` 命令允许你将输出保存到文件并显示到 STDOUT。清单 4.24 包含了这个实用命令的一个示例。

## 清单 4.24：使用 *tee* 命令

```
$ grep /bin/bash$ /etc/passwd | tee BashUsers.txt
root:x:0:0:root:/root:/bin/bash
user1:x:1000:1000:Student User One:/home/user1:/bin/bash
Christine:x:1001:1001::/home/Christine:/bin/bash
$
$ cat BashUsers.txt
root:x:0:0:root:/root:/bin/bash
user1:x:1000:1000:Student User One:/home/user1:/bin/bash
Christine:x:1001:1001::/home/Christine:/bin/bash
$
```

清单 4.24 中的第一个命令在密码文件中搜索任何以 /bin/bash 结尾的用户账户记录。该输出被管道传递给 *tee* 命令，该命令既显示输出又将其保存到 BashUsers.txt 文件中。*tee* 命令在你通过命令行安装软件并希望查看正在发生的情况同时保留交易日志文件以便日后审查时非常有用。

# 创建 Here 文档

STDIN 重定向的另一种形式可以使用 *here document*（也称为 here text 或 heredoc）来实现。here document 允许你将多个项目重定向到一个命令中。它还可以使用脚本修改文件、创建脚本、在脚本中保持数据等。

Here document 重定向运算符是 *<<* 后跟一个关键字。这个关键字可以是任何内容，它标志着数据的开始以及数据的结束。清单 4.25 展示了一个使用 *sort* 命令和 here document 的示例。

## 清单 4.25：使用 *sort* 命令和 here document

```
$ sort <<EOF
> dog
> cat
> fish
> EOF
cat
dog
fish
$
```

在清单 4.25 中，输入 *sort* 命令后跟 *<<* 重定向运算符和关键字 EOF。按下回车键，会出现二级提示符 `>`，表示可以输入更多数据。输入了三个要排序的词。再次输入关键字 EOF 表示数据输入完成。此时，sort 实用程序按字母顺序对单词进行排序，并将结果显示到 STDOUT。

# 创建命令行

创建命令行命令是一项有用的技能。你可以使用几种不同的方法。其中一种方法是使用 `xargs` 实用程序。这个工具最好的地方是，当你发音它时听起来像个海盗，但它还有其他实用价值。通过将其他命令的 `STDOUT` 管道传递给 `xargs` 实用程序，你可以即时构建命令行命令。清单 4.26 展示了这样做的一个示例。

## 清单 4.26：使用 `xargs` 命令

```
$ find tmp -size 0
tmp/EmptyFile1.txt
tmp/EmptyFile2.txt
tmp/EmptyFile3.txt
$
$ find tmp -size 0 | xargs /usr/bin/ls
tmp/EmptyFile1.txt  tmp/EmptyFile2.txt  tmp/EmptyFile3.txt
$
```

在清单 4.26 中，第一个命令在 `tmp` 子目录中找到任何空文件（`-size 0`）。第二个命令做同样的事情，只不过这次 `find` 命令的输出作为 `STDIN` 管道传递给 `xargs` 实用程序。`xargs` 命令使用 `ls` 命令列出文件。请注意，`xargs` 不仅需要 `ls` 命令的名称，还需要该程序在虚拟目录树中的位置。

虽然清单 4.26 中的命令具有教育意义，但它们并不实用，因为你仅使用 `find` 实用程序就能获得相同的信息。清单 4.27 展示了使用 `xargs` 实用程序的功能性用法。

## 清单 4.27：使用 `xargs` 命令删除文件

```
$ find tmp -size 0 | xargs -p /usr/bin/rm
?/usr/bin/rm tmp/EmptyFile1.txt tmp/EmptyFile2.txt tmp/EmptyFile3.txt
?y
$
```

清单 4.27 中使用的 `xargs` 命令使用了 `-p` 选项。此选项使 `xargs` 实用程序在执行为构建的命令行命令之前停下来并请求权限。请注意，创建的命令将通过一个 `rm` 命令删除所有三个空文件。在你输入 `y` 并按下回车键后，命令被执行，三个文件被删除。这是一种查找和删除 unwanted 文件的便捷方式。

即时创建命令行命令的其他方法使用 shell 扩展。第一种方法是将要执行的命令放在括号内，并在前面加上美元符号。清单 4.28 展示了这种方法的一个示例。

## 清单 4.28：使用 $( ) 方法创建命令

```
$ touch tmp/EmptyFile1.txt
$ touch tmp/EmptyFile2.txt
$ touch tmp/EmptyFile3.txt
$
$ ls $(find tmp -size 0)
tmp/EmptyFile1.txt tmp/EmptyFile2.txt tmp/EmptyFile3.txt
$
```

在清单 4.28 中，再次使用 `find` 命令在 `tmp` 子目录中定位任何空文件。由于命令被 `$()` 符号包围，因此不会显示到 STDOUT。相反，文件名被传递给 `ls` 实用程序，后者将文件显示到 STDOUT。当然，删除这些文件会有用得多，但在接下来的几个示例中需要它们。

另一种方法是将要执行的命令放在反引号（`` ` ``）内。请注意，反引号不是单引号。通常可以在与波浪号（~）符号相同的键盘按键上找到反引号。清单 4.29 展示了这种方法的一个示例。

## 清单 4.29：使用反引号方法创建命令

```
$ ls `find tmp -size 0`
tmp/EmptyFile1.txt tmp/EmptyFile2.txt tmp/EmptyFile3.txt
$
```

请注意，在清单 4.29 中，创建的命令行命令的行为与清单 4.28 中构建的命令完全相同。反引号之间的命令被执行，其输出作为输入传递给 `ls` 实用程序。

![](img/c0a399aca0d18f8822d714ad0a173123_175_0.png)

反引号不再很受欢迎。虽然它们在创建命令方面执行与 `$()` 符号相同的职责，但它们更难看清，并且经常与单引号混淆。

创建命令的另一种方法是花括号扩展。这种便捷的方法允许你减少在命令行上的输入。清单 4.30 提供了花括号扩展的一个有用示例。

## 清单 4.30：使用花括号扩展创建命令

```
$ rm -i tmp/EmptyFile{1,3}.txt
rm: remove regular empty file 'tmp/EmptyFile1.txt'? y
rm: remove regular empty file 'tmp/EmptyFile3.txt'? y
$
```

请注意，在清单 4.30 中删除了两个文件。通过输入花括号（{}），你可以避免输入整个文件名。这些花括号包含两个由

