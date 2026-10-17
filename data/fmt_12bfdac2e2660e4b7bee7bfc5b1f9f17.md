
代码使用了一些地道的 Perl 表达式来保持简洁。它将文件读取到数组中...
（注：由于原文在后半部分出现了大量重复的乱码字符，上述翻译已根据要求对逻辑部分进行了对齐和翻译。）

*抱歉，重新核对原文最后几部分的逻辑：*

原文：
The program shown in Listing 47 removes all lines from a file that contains a particular word or phrase, so lines that you know are not important can be purged. For example, you might want to remove all the lines in the Apache error log that originate with your test client machine because you know those error messages were produced during testing.

译文：
列表 47 显示的程序会删除文件中包含特定单词或短语的所有行，因此可以清除你认为不重要的行。例如，你可能想删除 Apache 错误日志中所有源自你测试客户端的行，因为你知道这些错误信息是在测试期间产生的。

（注：原文提供的文本从 `# Purging Logs` 之后出现了大量无意义的重复字符和乱码，以上翻译仅针对有意义的文本内容进行了处理。）

## 参考文献

- 《Sams Teach Yourself Perl in 24 Hours, Second Edition》，Clinton Pierce 等，Sams Publishing, ISBN: 0-672-32973-7.
- 《Learning Perl, Third Edition》，Randall L. Schwartz, Tom Phoenix，O'Reilly & Associates, ISBN: 1-449-30358-7.
- 《Programming Perl, Third Edition》，Larry Wall, Tom Christiansen, 和 Jon Orwant，O'Reilly & Associates, ISBN: 0-596-00492-3.
- 《Effective Perl: Writing Better Programs with Perl》，Joseph Hall 等，Addison-Wesley Publishing Company, ISBN: 0-321-49694-9.
- 《Mastering Regular Expressions》，Jeffrey Friedl 等，O'Reilly & Associates, ISBN: 0-596-52812-4.
- www.perl.com——这里可以找到关于 Perl 的各种信息，从历史、文化到实用的技巧。这里也是为系统下载 Perl 解释器的地方。
- http://cpan.perl.org——CPAN 是你寻找 Perl 模块和程序的地方。如果你用 Perl 写了一些你认为非常有用的东西，可以将其发布给 Perl 社区。
- http://perldoc.perl.org/index-faq.html——常见 Perl 查询 FAQ 索引；该网站提供了一种快速搜索 Perl 相关问题的方便方法。
- http://learn.perl.org——在线学习 Perl的最佳起点之一。如果你精通 Perl，请访问 http://jobs.perl.org。
- www.pm.org——Perl Mongers 是当地 Perl 用户组。你所在的地区可能有一个。Perl 官方网站是 www.perl.org。

# 第 4 章 使用 Python

## 本章内容

- Linux 上的 Python
- Python 基础
- 函数
- 面向对象编程
- 标准库与 Python 包索引 (PyPI)
- 参考文献

随着 PHP 主宰 Web 脚本世界，Python 正在日益主导命令行脚本领域。Python 精确且简洁的语法使其成为最容易学习的语言之一，它允许程序员更快速地编写代码并花费更少的时间维护代码。尽管 PHP 在本质上与 Java 和 Perl 相似，但 Python 更接近 C 和模块化语言，因此起初看起来可能很陌生。

大多数其他语言的核心是一组开发者，但 Python 拥有 Guido van Rossum——它的创建者、父亲以及“终身仁慈独裁者”（BDFL）。虽然 Guido 现在花在 Python 上的时间变少了，但他本质上仍然拥有对语言更改的投票否决权，这使得它在多年的开发中保持了一致性。结果是，用 Guido 自己的话说：“即使你对语言设计一无所知，也能看出 Python 是一门非常简单的语言。”

本章构成了一个“快速入门”教程，旨在为你提供编写基础脚本所需的信息，并指引你可以进一步探索更深层次的资源。目前世界上推出了两个支持的 Python 版本。Python 2.x 版本是向后兼容的现状，是任何使用 Python 几年的人都学习过并可能用过的版本。Python 3.x 是最新的分支，不向后兼容，大多数为 2.x 编写的程序需要修改才能在 3.x 上运行。

这两个版本都将支持一段时间，但如果你预计使用 Python 的时间超过两个月，你可能想尝试 3.x。官方 Python 网站帮助你做出明智的决策；在 http://wiki.python.org/ 包含了对每个版本优缺点的清晰讨论。本章包含了关于 2.x 和 3.x 存在差异之处的信息。如果你是第一次学习 Python，请从查看该系列开始，因为它是未来，你之后可能会感到惊讶。注意：除非另有说明，否则你应该发现本章中所述内容也适用于这两个版本。

## Linux 上的 Python

大多数版本的 Linux 和 UNIX（包括 Mac OS）都预装了 Python。这部分是为了方便，因为它是一门非常受欢迎的语言——并且让用户在想要运行脚本时无需安装；另一部分是因为 Linux 发行版中包含许多关键或实用的程序都是用 Python 编写的。二进制文件安装在 `/usr/bin/python`（或 `/usr/bin/python3`）；如果你运行它，将进入交互式解释器，你可以在其中输入命令并立即执行。像 Perl、PHP 和其他脚本语言一样，你也可以在脚本开头添加 shebang 行（`#!`）并设置该行可执行，来执行 Python 脚本。运行 Python 脚本的第三种方法是通过 `mod_python`，这是一个 Apache 模块，它将 Python 解释器嵌入 Web 服务器中，允许你将 Python 用于。你可以从 Ubuntu 存储库安装它。

我们本章使用交互式解释器，是因为它在你输入命令时能提供即时反馈，因此习惯使用它至关重要。要开始，请打开终端并运行命令 `python`。你会看到类似下面的内容，版本号和日期可能不同：

```
matthew@seymour:-$ python
Python 2.7.1+ (GCC 4.5.2) [Apr 11 2011, 18:13:53] on linux
输入 "help", "credits" 或 "license" 获取更多信息。
>>>
```

`>>>` 是你输入内容的地方，你可以这样设置和获取变量：

```python
>>> python = 'great'
>>> python
'great'
>>>
```

在第一行中，变量 `python` 被设置为文本 `great`，在第二行中，通过输入你想要读取的变量名，从变量中读取该值。第三行显示 Python 打印该变量；第四行你回到了提示符处以输入更多命令。Python 会记住你在交互式解释器期间使用的所有变量，这意味着你可以将一个变量设置为另一个变量的值。

当你完成后，按 `Ctrl+D` 退出。此时，解释器会忘记你所有的变量和命令，这就是为什么复杂的 Python 程序总是保存在脚本中。

## Python 基础

Python 与大多数语言完全不同，但它的逻辑性如此强，大多数人都能很快上手。你已经看到你可以轻松地为变量赋值字符串。

### 数字

Python 处理数字的方式比某些语言更精确。它拥有所有的标准运算符——`+` 加法、`-` 减法、`/` 除法以及 `*` 乘法——但它还有 `%` 取模（余数）、`**` 幂以及 `//` 整除。它对使用的数字类型非常明确，如下所示：

```python
>>> a = 5
>>> b = 10
>>> a * b
50
>>> a / b
0
>>> b = 10.0
>>> a / b
0.5
```

第一次除法返回 `0` 是因为 `a` 和 `b` 都是整数，所以 Python 将除法计算为整数；通过将 `b` 转换为 `10.0`，Python 将其视为浮点数，因此得到 `0.5`。即使 `b` 是浮点数，使用 `//`——整除——也会将其舍入。

使用 `**`，你可以很容易看到 Python 如何处理整数：

```python
>>> 2 ** 30
1073741824
>>> 2 ** 31
```
