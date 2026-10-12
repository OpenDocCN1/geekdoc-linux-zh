
```bash
for f in ./*.aac; do
  cp "$f"
  cp "$f" "$f.bak"
done
```

# 使用 Awk 和 Sed 更快地处理文本

通过终端处理文本让你的生活更简单

教程

![](img/bab7f65683e8ebca10d1e8aa808ba7ff_38_0.png)

SRE - mnsouk@linux:~/docs/article/working/sedAWK.linux/var/files - ssh - 90x45

```bash
$ sed 's|usr/local/bin/perl|/usr/bin/perl|g' .*
#!/usr/bin/perl
```

```
print "This is script 1";
```

```bash
exit 0;
!//usr/bin/perl
```

```
print "This is script 2";
```

```bash
exit 0;
!//usr/bin/perl
```

```
print "This is script 3";
```

```bash
exit 0;
cat pscript1.pl
#!/usr/local/bin/perl
```

```
print "This is script 4";
```

```bash
exit 0;
cat pscript2.pl
#!/usr/local/bin/perl
```

![](img/bab7f65683e8ebca10d1e8aa808ba7ff_38_1.png)

## 01 安装 Awk 和 Sed

好消息是，每种 Linux 发行版都预装了 `Sed` 和至少一个版本的 `Awk`，因此你不需要手动安装它们，不过你可能想通过你 Linux 版本的包管理器使用不同的变体。

![](img/bab7f65683e8ebca10d1e8aa808ba7ff_38_2.png)

## 02 使用 Sed

`Sed` 命令可以在文件中全局将一个字符串替换为另一个：

```bash
$ sed 's/string/two/g' file
```

如果你想将原始文件内容保存到新文件中并保留过的字符，请使用以下选项：

上一个命令将单词 "three" 替换为 "3"， 输出到文件 `text` 并保留原始文件 `text`。

如果你想执行不区分大小的搜索和替换，请使用以下命令：

```bash
$ sed -i.bak 's/three/3/g' file
```

![](img/bab7f65683e8ebca10d1e8aa808ba7ff_38_3.png)

## 03 使用 Awk

"Hello World" 程序可以用两种方式编写。第一种是通过命令行，第二种是通过存储脚本。如果你是新手，最好在单独的文件中使用 `Awk`。

默认情况下，`Awk` 根据空格和制表符将输入行分割为字段。你可以使用 `-F` 命令选项和其他字符来更改字段分隔符。

## 04 一个 Sed 示例

`Awk` 允许你创建多个文件。以下示例显示了多个文件中来自 `"/usr/local/bin/perl"` 的二进制文件路径：

```bash
$ sed 's|/usr/local/bin/perl|/usr/bin/perl|g'
```

注意，为了将 `/` 作为普通字符使用，必须对该字符进行转义。

永远记住，使用 `Sed` 时，之前的文件将永久消失。

![](img/bab7f65683e8ebca10d1e8aa808ba7ff_38_4.png)

## 05 一个 Awk 示例

如果你想打印文件的第一和第三列，你应该遵循以下命令：

```bash
awk '{print $1, $3}'
```

如果你想反向打印第二列和第三列，请执行以下命令：

```bash
awk '{print $3, $2}'
```

要打印输入的最后两列，使用：

```bash
awk '{print $(NF-1), $NF}'
```

在这里，`NF` 是一个保存当前行字段数量的变量，`$NF` 是当前行的最后一个字段。`$0` 变量代表当前行。

![](img/bab7f65683e8ebca10d1e8aa808ba7ff_38_5.png)

39 www.linux.co.uk

## 教程

SRE — mtsouk@mail:~/docs/article/working/sedAWK.linux/var/files - 90x45

## Awk 内置函数

```bash
cat numbers
1
2
3
4
5
6
7
8
9
10
```

```bash
files |awk '{print "Square root of " $1 ":" sqrt($1)}'
```

Square root of 1: 1.4142

Square root of 2: 1.7321

Square root of 4: 2

Square root of 5: 2.2361

Square root of 7: 2.6457

Square root of 8: 2.8284

Square root of 9: 3.1622

```bash
files |head
0 6 times
1 6 times
2 6 times
3 6 times
4 6 times
5 6 times
6 6 times
7 6 times
8 6 times
9 6 times
0 6 times
```

## 08 Awk 内置函数

`Awk` 拥有用于字符串、数字和操作的内置函数。你可以通过它可以生成随机数，但请注意，`rand()` 函数可以生成随机数。

![](img/bab7f65683e8ebca10d1e8aa808ba7ff_39_0)

## 09 模式匹配

`Awk` 使用模式块来匹配模式。`FILENAME` 变量持有当前文件名，`BEGIN` 块可以定义它。`Awk` 脚本可以匹配到：

## 07 使用 Awk 处理事情

通过终端 (`cat`) 来处理文本。`cut` (`-d' ' -f1`) 做了某些操作。它删除了从每行的第一个字符到行尾的内容。

所以，到为止输出看起来像这样：

27/Jul/2014 06:34:03

`Awk` `-F":"print $2"` 命令定义 `":"` 为字段分隔符并打印第二个字段。然后 `"sort -n"` 命令按数字而不是字母顺序排序。`"uniq"` 命令在需要统计出现次数时配合使用重复行。最后，`awk "print $2;1"` 交换列中的数据。输出，然后 `> file.txt` 将输出保存到文件中。

如果你按第二列排序输出，你可以找到一天中最忙碌的时段。

![](img/bab7f65683e8ebca10d1e8aa808ba7ff_40_1.png)

```bash
SR - mseekoul@mail.com/docs/working/sedawk.LUD/var-files --90x45
```

## 14. Gaw 和 Awk

在 Linux 系统上，`Awk` 通常是 `Gaw` 或 `Awk` 的符号链接，各种变体与 `Awk` 原始版本的区别在于它们支持更多如函数和变量。

## 单词计数

这是一个非常有挑战性的示例，展示了 `Awk` 的高级功能。该 `Awk` 脚本 (`wordfreq.awk`) 读取文本文件并利用关联数组统计每个单词在文中出现的次数。

## 13 更多 Apache 日志处理

查找当天唯一 IP 地址总数的另一种技巧，你可以执行以下命令：

## 14. 无法完全替代 Perl 或 Python，但正如你所看到的，它工作良好且你用它编写文本。另一方面，Awk 不适合数据库，但 Python 会是一个更明智的选择，因为它们可以连接到我的 MySQL 数据库。主要点是，学习和使用 Awk 对每个 Linux 用户或管理员都有益。

## 教程

将您的软件和文件保留在系统之间，因为它们存储在服务器而非本地存储中

![](img/bab7f65683e8ebca10d1e8aa808ba7ff_41_0.png)

从任何连接了网络的计算机远程连接到功能完的 Ubuntu 发行版

# 从 NFS 服务器启动 Linux

该发行版安装在始终处于开启状态的服务器上。如果设置得当，它可以在多个系统上使用。

无盘启动允许您从网络上的多个位置访问同一个发行版，而无需反复处理文件传输。

## 资源

一个 `Ubuntu` 服务器

虽然您可能认为它们很常见，但大型机配合哑终端终端（`dumb terminals`）的概念在现在已经是一个过时的考虑了。高性能机器的普及让每个人都拥有一自己的系统变得更加容易，这真的改变了现状。
