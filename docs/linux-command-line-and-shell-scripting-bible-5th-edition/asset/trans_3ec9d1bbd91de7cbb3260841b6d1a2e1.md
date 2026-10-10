

该组合键会在 Bash 中生成一个 EOF 字符。使用这个键组合会终止 gawk 程序并返回到命令行接口提示符。

## 使用数据字段变量

gawk 的主要功能之一是其操纵文本文件中数据的能力。它通过为每一行中的每个数据元素自动分配一个变量来实现这一点。默认情况下，gawk 会为检测到的每行文本中的每个数据字段分配以下变量：

- $0 代表整行文本。
- $1 代表该行文本中的第一个数据字段。
- $2 代表该行文本中的第二个数据字段。
- $n 代表该行文本中的第 n 个数据字段。

每行文本中的每个数据字段由*字段分隔符*确定。当 gawk 读取一行文本时，它会使用定义的字段分隔符来界定每个数据字段。gawk 中的默认字段分隔符是任意空白字符（例如制表符或空格字符）。

以下是一个 gawk 程序的示例，它读取文本文件并仅显示第一个数据字段的值：

```bash
$ cat data2.txt
One line of test text.
Two lines of test text.
Three lines of test text.
$
$ gawk '{print $1}' data2.txt
One
Two
Three
$
```

这个程序使用 $1 字段变量来显示每行文本的第一个数据字段。对于读取使用不同字段分隔符的文件，请使用 `-F` 选项指定该字符：

```bash
$ gawk -F: '{print $1}' /etc/passwd
root
daemon
bin
[. . .]
christine
sshd
$
```

这个短程序显示了系统中 passwd 文件里的第一个数据字段。由于 /etc/passwd 文件使用冒号（`:`）来分隔数据字段，为了分隔每个数据元素，我在 gawk 选项中使用了字段分隔符（`-F:`）。

![](img/0798d50a0e5dbf1265fbda3832b3e015_490_0.png)

## 在程序脚本中使用多个命令

如果只能执行一条命令，编程语言将没什么用处。gawk 编程语言允许将命令组合成正常的程序。要在命令行上指定的程序脚本中使用多个命令，只需在每条命令之间放置一个分号：

```bash
$ echo 'My name is Rich' | gawk '{ $4="Christine"; print $0}'
My name is Christine
$ 
```

第一条命令将值赋给 $4 字段变量。第二条命令随后打印整个数据字段。注意从输出可以看出，gawk 程序用新值替换了原始文本中的第四个数据字段。

你还可以使用次级提示符逐行输入你的程序脚本命令：

```bash
$ gawk '{
> $4="Christine";
> print $0}'
My name is Rich
My name is Christine
$ 
```

一旦用单引号打开，Bash shell 会提供次级提示符，提示我们输入更多数据。我逐行添加这些命令，直到输入结束的单引号为止。由于命令行中未定义文件名，gawk 程序从 STDIN 检索数据。当我运行程序时，它等待通过 STDIN 传入的文本。要退出程序，请按 Ctrl+D 键组合以表示数据结束并返回 shell 提示符。

## 从文件读取程序

与 sed 编辑器一样，gawk 编辑器允许你将程序存储在文件中，并在命令行中引用它们：

```bash
$ cat script2.gawk
{print $1 "'s home directory is " $6}
$ 
$ gawk -F: -f script2.gawk /etc/passwd
root's home directory is /root
daemon's home directory is /usr/sbin
bin's home directory is /bin
[...]
christine's home directory is /home/christine
sshd's home directory is /run/sshd
$ 
```

script2.gawk 程序脚本再次使用 print 命令来打印 /etc/passwd 文件的主目录数据字段（字段变量 $6）和用户名数据字段（字段变量 $1）。

## 第 19 章：介绍 **sed** 和 **gawk**

你可以在程序文件中指定多个命令。为此，只需将每个命令放在单独的行上。你不需要使用分号：

```bash
$ cat script3.gawk
{
text = "'s home directory is "
print $1 text $6
}
$
```

```bash
$ gawk -F: -f script3.gawk /etc/passwd
root's home directory is /root
daemon's home directory is /usr/sbin
bin's home directory is /bin
[...]
christine's home directory is /home/christine
sshd's home directory is /run/sshd
$
```

**script3.gawk** 程序脚本定义了一个变量 `text`，用于保存**print** 命令中使用的文本字符串。注意，gawk 程序在引用变量的值时不使用美元符号，这与 shell 脚本不同。

## 在处理数据前运行脚本

**gawk** 程序还允许你指定程序脚本何时运行。默认情况下，**gawk** 从输入中读取一行文本，然后在该行数据上执行程序脚本。有时，你可能需要在处理数据之前运行脚本，例如为报告创建标题部分。**BEGIN** 关键字用于实现这一点。它强制 **gawk** 在执行 **BEGIN** 关键字指定的程序脚本时，先于 **gawk** 读取数据：

```bash
$ gawk 'BEGIN {print "Hello World!"}'
Hello World!
$
```

这次 **print** 命令在读取任何数据之前显示文本。但是，显示文本后，它立即退出，不等待任何数据。

原因是 **BEGIN** 关键字仅在处理任何数据之前应用指定的脚本。如果你想用正常的程序脚本处理数据，必须使用另一个脚本部分定义程序：

```bash
$ cat data3.txt
Line 1
Line 2
Line 3
$
```

```bash
$ gawk 'BEGIN {print "The data3 File Contents:"}
> {print $0}' data3.txt
The data3 File Contents:
Line 1
Line 2
Line 3
$
```

## 第三部分：高级 Shell 脚本编程

现在，在 gawk 执行 BEGIN 脚本后，它使用第二个脚本处理任何文件数据。这样做时要小心——这两个脚本在 gawk 命令行上仍被视为一个文本字符串。你需要相应地放置单引号。

## 在处理数据后运行脚本

与 BEGIN 关键字类似，END 关键字允许你指定一个程序脚本，gawk 在读取数据后执行该脚本：

```bash
$ gawk 'BEGIN {print "The data3 File Contents:"}
> {print $0}
> END {print "End of File"}' data3.txt
The data3 File Contents:
Line 1
Line 2
Line 3
End of File
$
```

当 gawk 程序完成打印文件内容时，它会执行 END 脚本中的命令。这是在所有正常数据处理完成后，为报告添加页脚数据的一个绝佳技术。

你可以将所有这些元素组合到一个小型的程序脚本文件中，以便从简单的数据文件创建完整的报告：

```bash
$ cat script4.gawk
BEGIN {
  print "The latest list of users and shells"
  print "UserID \t Shell"
  print "-------- \t ------"
  FS=":"
}

{
  print $1 "    \t " $7
}

END {
  print "This concludes the listing"
}
$
```

该文件使用 BEGIN 脚本为报告创建标题部分。它还定义了一个名为 FS 的特殊变量。这是定义字段分隔符的另一种方式。这样，你就无需依赖脚本用户在命令行选项中定义字段分隔符。

以下是运行此 gawk 程序脚本的部分截断输出：

```bash
$ gawk -f script4.gawk /etc/passwd
The latest list of users and shells
UserID      Shell
------      ----
root        /bin/bash
daemon      /usr/sbin/nologin
[...]  
christine   /bin/bash
sshd        /usr/sbin/nologin
This concludes the listing
$ 
```

正如预期，BEGIN 脚本创建了标题文本，程序脚本处理了指定数据文件（/etc/passwd 文件）中的信息，END 脚本生成了页脚文本。print 命令中的 \t 产生了一些格式良好的制表符输出。

这让你稍微领略了使用简单 gawk 脚本所能提供的强大功能。第 22 章“高级 gawk”描述了一些可用于 gawk 脚本的基本编程原理，以及你甚至可以在 gawk 程序脚本中使用的更高级的编程概念，从而从最晦涩的数据文件中创建专业外观的报告。

## 查看 sed 编辑器基本命令

成功使用 sed 编辑器的关键在于了解其众多的命令和格式，这些命令和格式有助于你自定义文本编辑。本节描述了一些你可以纳入脚本中开始使用 sed 编辑器的基本命令和功能。

## 介绍更多替换选项

我已经介绍了如何使用 s 命令将一行中的文本替换为新文本。然而，s 命令还有几个附加选项，可以帮助简化你的生活。

### 替换标志

s 命令替换文本字符串中匹配模式的方式有一个注意事项。观察以下示例中发生了什么：

```bash
$ cat data4.txt
This is a test of the test script.
This is the second test of the test script.
$
$ sed 's/test/trial/' data4.txt
This is a trial of the test script.
This is the second trial of the test script.
$ 
```

s 命令在替换多行中的文本时工作正常，但默认情况下，它只替换每行中第一次出现的实例。要让 s 命令作用于不同的出现位置

