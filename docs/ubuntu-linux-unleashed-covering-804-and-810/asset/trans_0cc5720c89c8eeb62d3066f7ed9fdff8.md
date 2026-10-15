

在文件中输入并保存为名为 trivial.pl 的文件。然后使用 chmod 命令（见以下侧边栏）使文件可执行，并在命令行中运行它。

## 命令行错误

如果收到消息 bash: trivial.pl: command not found 或 bash: ./trivial.pl: Permission denied，则说明你输入命令行有误或忘记使用 chmod 命令使 trivial.pl 可执行；

```
$ chmod +x trivial.pl
```

你可以通过以下方式强制在当前目录中执行该命令：

```
$ ./trivial.pl
```

或者你也可以使用 Perl 来运行程序，如下所示：

```
$ perl trivial.pl
```

列表中的示例程序是一个两行的 Perl 程序。输入该程序并运行它（使用 Perl 或使程序可执行）展示了如何创建你的第一个 Perl 程序，这一过程每天都在全球各地的 Linux 用户中重复！

## NOTE

#! 通常发音为 she-bang，即 sharp（音乐家对 # 字符的称呼）的缩写，以及 bang，即感叹号的另一个名称。这种记号也用于 shell 脚本。有关编写 shell 脚本的更多信息，请参阅第 11 章“Automating Tasks”。

#! 行在技术上根本不是 Perl 代码的一部分。# 字符表示屏幕行的其余部分是注释。注释是发给 shell 的消息，告诉它去哪里找到执行此程序的可执行文件。解释器会忽略注释行。

对此做法的例外包括 # 字符出现在引号字符串中以及用作正则表达式分隔符时。注释对于记录你的脚本很有用，如下所示：

```
#!/usr/bin/perl
# a simple example to print a greeting
print 'hello there\n';
```

代码块，例如可能出现在循环或条件语句分支中的代码块，用花括号 ({}) 表示。例如，这里有一个无限循环：

```
#!/usr/bin/perl
# a block of code to print a greeting forever
```
```perl
while (1) {
    print "hello there\n";
};
```

Perl 语句以分号结尾。Perl 语句可以跨越数行实际屏幕行，因为 Perl 不关心空白。

简单程序的第二行打印出引号中的文本。`\n` 是换行字符的转义序列。

## TIP

使用 perldoc 和 man 命令是获取有关系统上安装的 Perl 版本更多信息的简便方法。要了解如何使用 perldoc 命令，请输入以下内容：

```
```shell
$ perldoc perldoc
```
```

要获取有关 Perl 的入门信息，可以使用以下任一命令：

```
```shell
$ perldoc perl
$ man perl
```
```

要获取 Perl 文档的概述或目录表，可以这样使用 `perldoc` 命令：

```
```shell
$ perldoc perltoc
```
```

文档内容丰富且组织良好。Perl 包含一些标准的 Linux 手册页作为其功能简要指南，但也许了解更多关于 Perl 的最佳方式是阅读其 `perlfunc` 文档，其中列出了所有可用的 Perl 函数及其用法。你可以使用 `perldoc` 脚本查看此文档，并在命令行输入 `perldoc perlfunc`。你也可以在 http://www.cpan.org/doc/manual/html/pod/perlfunc.html 在线找到此文档。

## Perl Variables and Data Structures

Perl 是一种 *弱类型* 语言，这意味着它不需要你声明数据类型，例如要存储在特定变量中的值（数据）的类型。例如，C 要求你声明某个变量是整数、字符、结构或任何其他情况。Perl 变量是它们需要成为的任何类型，并且在需要时可以更改类型。

### Perl Variable Types

Perl 有三种变量类型：*scalars*、*arrays* 和 *hashes*。使用不同的字符来表示每种变量类型。

标量变量用 `$` 字符表示，如 `$penguin`。标量可以是数字或字符串，并且可以根据需要从一种类型更改为另一种类型。如果你像对待字符串一样对待数字，它就变成字符串。如果你像对待数字一样对待字符串，它将被转换

