
`-n` 选项表示我想对输出的每一行运行 Perl 代码。`-a` 选项自动将输出分割到 `@F` 数组中。`-e` 选项表示 Perl 代码将跟随在命令行。

## 相关的 FEDORA 和 LINUX 命令

当你配合 Perl 使用时，将使用这些命令和工具：

- `a2p`—一个将 `awk` 脚本翻译成 Perl 的过滤器
- `find2perl`—一个用于使用 `find` 命令从命令行创建 Perl 代码的工具
- `pcregrep`—一个使用与 Perl 兼容的正则表达式搜索数据的实用程序
- `perlc`—Perl 程序的编译器
- `perdoc`—一个用于读取 Perl 文档的工具
- `s2p`—一个将 `sed` 脚本翻译成 Perl 的过滤器
- `vi`—vi（实际上是 vim）文本编辑器

## 参考资料

首先要查找的地方是 Perl 文档和 Linux 的 `man` 页面（帮助手册）。

Perl 及其所有文档以及数百万行 Perl 程序在互联网上免费提供。许多 Usenet 新闻组也致力于 Perl，此外还有满架的书籍和一本每季度出版一次的期刊。

## 书籍

虽然你当地的书书店可能有几十种关于 Perl 的书，但以下是其中比较受推荐的几本。你也可以查看 Camel Critiques（Tom Christiansen; http://language.perl.com/critiques/index.html）来获取其他可用 Perl 书的评论。

- *Advanced Perl Programming*, Sriram Srinivasan 著，O'Reilly & Associates
- *Sams Teach Yourself Perl in 21 Days, Second Edition*, Laura Lemay 著，Sams Publishing
- *Sams Teach Yourself Perl in 24 Hours, Second Edition*, Clinton Pierce 著，Sams Publishing
- *Learning Perl, Third Edition*, Randal L. Schwartz, Tom Phoenix 著，O'Reilly & Associates
- *Programming Perl, Third Edition*, Larry Wall, Tom Christiansen 和 Jon Orwant 著，O'Reilly & Associates
- *Effective Perl Programming: Writing Better Programs with Perl*, Joseph Hall 著，Addison-Wesley Publishing
- *CGI Programming with Perl, Second Edition*, Gunther Birznecks, Shishir Gundaram 著，O'Reilly & Associates
- *Mastering Regular Expressions*, Jeffrey Friedl 著

## Usenet

查看 Usenet ：

- `comp.lang.perl`—讨论 Perl 语言的各个方面。确保你的问题是关于 Perl 特定的，而不是通用的。这里的活跃用户倾向于喷那些不懂的人。
- `comp.infosystems.www.authoring`—讨论 CGI 编写，大部分讨论是关于 Perl 的。这里的活跃用户对保持主题非常严格。

## WWW

查看万网上的这些网站：

- http://www.perl.com/—Tom 维护的 Perl 语言首页。在这里可以找到关于 Perl 的各种信息，从历史文化到实用技巧。这也是你下载 Perl 解释器的地方。
- http://www.perl.com/CPAN—这是上述网站的一部分，但值得单独提及。CPAN（综合 Perl 存档）是你寻找 Perl 模块和程序的地方。如果你编写了认为非常有用的 Perl 代码，可以提供给 Perl 社区。
- http://www.perl.com/pub/FAQs—常见问题索引。
- http://learn.perl.org/—学习最好的地方之一。
- http://www.hwg.org/—HTML Writers 是一个致力于 Web 开发者的非盈利组织。它的服务之一是大量的邮件列表。
- http://www.tpj.com/—The Perl Journal是一本致力于 Perl 语言的读者支持每月杂志。TPJ 总是充满了精彩、有趣且启发性的文章，对于新手和资深程序员来说，都是无价的资源。
- http://www-106.com/developerworks/linux/library/p101—关于单行脚本的简短教程。
- http://www.pm.org/—Perl Mongers 是本地用户组。在你所在的地区可能有一个。

## 第 31 章 使用 Python

Python 二进制文件安装在 `/usr/bin/python`；如果你运行该文件，将进入 Python 交互式解释器，在其中你可以输入命令并立即获得执行。尽管 PHP 也有交互模式（使用 `php -a` 激活），但它的功能并不像 Python 强大。

与 Perl、PHP 和其他脚本语言一样，你也可以通过在脚本开头添加指向 `/usr/bin/python` 的 shebang 行，然后将文件设置为可执行，来运行 Python 脚本。

运行 Python 脚本的第三种也是最后的方法是通过 `mod_python`，当你从“添加/删除软件”对话框中选择 Web 服务器应用程序组时，它会被默认安装。

出于对本介绍的考虑，我们将使用交互式 Python 解释器，因为它会在你输入命令时提供即时反馈。

## 交互式操作

本章我们将使用交互式解释器，因此你熟练使用它至关重要。要开始操作，请打开终端并运行命令 `python`。你应该看到以下内容：

```
[paul@caitlin ~]$ python

Python 2.3.4 (#1, Oct 26 2004, 16:42:40)

[GCC 3.4.2 20041017 (Red Hat 3.4.2-6.fc3)] on linux2

Type "help", "copyright", "credits" or "license" for more information.

>
```

`>>>` 是你输入内容的地方，你可以这样设置和获取变量：

```
>>> python = 'great'
>>> python
'great'
>>>
```

在第一行中，变量 `python` 被设置为文本 `great`；在第二行，通过只需输入想要读取的变量名称即可从变量中读取该值。第三行显示 Python 打印该变量；第四行，你回到了提示符处，可以输入更多命令。Python 在交互式解释器运行期间记住你使用的所有变量，这意味着你可以将一个变量设置为另一个变量的值。

完成后，按下 `Ctrl+D` 退出。此时，解释器会忘记你所有的变量和命令，这就是为什么复杂的 Python 程序总是保存在脚本中的原因！

## Python 基础

Python 是一门与其他大多数语言完全不同的语言，但它非常有逻辑性，以至于大多数人都能很快学会。你已经看到如何轻松地赋值字符串，但在 Python 中，几乎所有操作都那么简单——只要你记住语法！

## 数字

Python 处理数字的方式比其他语言更精确。它拥有所有常规运算符——例如用于加法的 `+`、减法的 `-`、除法的 `/` 和乘法的 `*`——但它还增加了 `%` 用于取模（除法余数）、`**` 用于幂运算以及 `//` 用于地板除法。它对所使用的数字类型也非常具体，如下例所示：

```
>>> a = 5
>>> b = 10
>>> a * b
50
>>> a / b
0
>>> b = 10.0
>>> a / b
0.5
>>> a // b
0.0
```
