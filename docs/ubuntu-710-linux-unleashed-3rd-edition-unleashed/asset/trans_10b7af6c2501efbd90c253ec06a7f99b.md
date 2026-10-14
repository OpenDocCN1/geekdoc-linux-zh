

## 命令行错误

如果你收到消息 bash: trivial.pl: command not found 或 bash: ./trivial.pl: Permission denied，你要么输入了错误的命令行，要么忘记使 trivial.pl 可执行（使用 chmod 命令）：

```
$ chmod +x trivial.pl
```

你可以通过以下方式强制在当前目录中执行命令：

```
$ ./trivial.pl
```

或者你也可以使用 Perl 来运行程序，如下所示：

```
$ perl trivial.pl
```

列表中的示例程序是一个两行的 Perl 程序。输入该程序并运行它（使用 Perl 或使程序可执行）展示了如何创建你的第一个 Perl 程序，这一过程每天都在全球的 Linux 用户中重复！

## NOTE

#! 通常发音为 she-bang，即 sharp（音乐家对 # 字符的称呼）的缩写，以及 bang，即感叹号的另一个名称。这种记号也用于 shell 脚本。有关编写 shell 脚本的更多信息，请参阅第 11 章“Automating Tasks”。

#! 行在技术上根本不是 Perl 代码的一部分。# 字符表示屏幕行的其余部分是注释。注释是发送给 shell 的消息，告诉它去哪里找到可执行文件来运行此程序。解释器会忽略注释行。

对此做法的例外包括 # 字符位于引号字符串中时，以及它被用作正则表达式分隔符时。注释对于记录你的脚本很有用，如下所示：

```
#!/usr/bin/perl
# a simple example to print a greeting
print 'hello there\n';
```

代码块，例如可能出现在循环或条件语句分支中的代码块，用花括号 ({}) 表示。例如，这里有一个无限循环：

```
#!/usr/bin/perl
# a block of code to print a greeting forever
while (1) {
    print 'hello there\n';
};
```

Perl 语句以分号结尾。Perl 语句可以跨越几行实际屏幕行，因为 Perl 不关心空白。

简单程序的第二行打印出引号中包含的文本。\n 是换行字符的转义序列。

## TIP

使用 perldoc 和 man 命令是获取有关系统上安装的 Perl 版本更多信息的简便方法。要了解如何使用 perldoc 命令，请输入以下内容：

```
$ perldoc perldoc
```

要获取有关 Perl 的入门信息，你可以使用以下任一命令：

```
$ perldoc perl
```

```
$ man perl
```

要获取 Perl 文档的概述或目录，请按如下方式使用 perldoc 命令：

```
$ perldoc perltoc
```

文档内容广泛且组织良好。Perl 包含一些标准的 Linux 手册页作为其功能简要指南，但也许了解更多关于 Perl 的最好方法是阅读其 perlfun c 文档，其中列出了所有可用的 Perl 函数及其用法。你可以通过使用 perldoc 脚本并在命令行输入 perldoc perlfun c 来查看此文档。你也可以在 http://www.cpan.org/doc/manual/html/pod/perlfun c.html 在线找到此文档。

## Perl 变量和数据结构

Perl 是一种弱类型语言，这意味着它不需要你声明数据类型，例如要存储在特定变量中的值（数据）的类型。例如，C 要求你声明某个变量是整数、字符、结构或任何情况。Perl 变量是它们需要的任何类型，并且在需要时可以更改类型。

## Perl 变量类型

Perl 数组用 @ 字符表示，如 @fish。数组是按索引号引用的值列表，从第一个元素编号 0 开始，就像在 C 和 awk 中一样。数组中的每个元素都是标量值。因为标量值用 $ 字符表示，所以数组中的单个元素也用 $ 字符表示。

例如，$fish[2] 指的是 @fish 数组中的第三个元素。这往往会让一些人感到困惑，但与 C 中的数组类似，其中第一个数组元素是 0。

哈希用 % 字符表示，如 %employee。哈希是名称和值对的列表。哈希中的单个元素按名称引用而不是按索引引用（不像数组）。同样，因为值是标量，所以单个元素使用 $ 字符。

例如，$employee{name} 给你哈希中的一个值。处理哈希的两个相当有用的函数是 keys 和 values。keys 函数返回包含哈希所有键的数组，而 values 返回哈希值的数组。使用这种方法，清单 23.2 中的 Perl 程序显示了环境中的所有值，很像输入 bash shell 的 env 命令。

### LISTING 23.2 Displaying the Contents of the env Hash

```
#!/usr/bin/perl
foreach $key (keys %ENV) {
    print "$key = $ENV{$key}\n";
}
```

## 特殊变量

Perl 有各种各样的特殊变量，通常看起来像标点符号—— $_、$! 和 $]——并且都非常有用，可用于简写代码。$_ 是默认变量，$! 是操作系统返回的错误消息，而 $] 是 Perl 版本号。

$_ 也许是这些中最有用的，你将在本章中经常看到该变量的使用。$_ 是 Perl 默认变量，当未指定参数时使用。例如，以下两个语句是等价的：

```
chomp;
chomp($_);
```

以下循环是等价的：

```
for $cow (@cattle) {
    print "$cow says moo.\n";
}
for (@cattle) {
    print "$_ says moo.\n";
}
```

