
`-n` 切换表示我希望针对输出的每一行运行 Perl 代码。`-a` 切换将输出分割到 `@F` 数组中。`-e` 切换表示 Perl 代码将跟在命令行之后。

## 相关的 Ubuntu 和 Linux 命令

在 Linux 上使用 Perl 时，你将使用这些命令和工具：

- `a2p`—一个用于将 awk 脚本翻译为 Perl 的过滤器
- `find2perl`—一个使用 find 从命令行创建 Perl 代码的工具
- `pgrep`—一个使用与 Perl 兼容的正表达式搜索数据的工具
- `perlcc`—一个用于 Perl 程序的编译程序
- `perdoc`—一个用于阅读 Perl 文档的工具
- `s2p`—一个用于在 Perl 中翻译 sed 脚本的过滤器
- `vi`—`vi`（实际上是 `vim`）文本编辑器

# 引用参考

首要要查找的地方是 Perl 文档和 Linux 手页（`man` pages）。
Perl 及其所有文档以及数百万行 Perl 程序在互联网上都是可用的。许多 Usenet 新闻组也致力于 Perl，书架和一本季度期刊也是如此。

# 书籍

尽管你当地的书店店可能有几十本关于 Perl 的书，但以下是其中非常推荐的。你也可以查看 Camel Critiques（Tom Christiansen; http://language.perl.com/critiques/index.html）来获取其他可用 Perl 书的评论。

- *Advanced Perl Programming*, Sriram Srinivasan, O'Reilly & Associates
- *Sams Teach Yourself Perl in 21 Days, Second Edition*, Laura Mays, Sam Publishing
- *Sams Teach Yourself in 24 Hours, Second Edition*, Clinton Pierce, Sam Publishing
- *Learning Perl, Third Edition*, Rand L. Schwartz, Tom Phoenix, O'Reilly & Associates
- *Programming Perl, Third Edition*, Larry Wall, Tom Christiansen, and Jon Orwant, O'Reilly & Associates

*Effective Perl Programming: Writing Better Programs with Perl*, Joseph Hall, Addison-Wesley Company
*CGI Programming with Perl, Second Edition*, Gunther Birnie, Scott Shishir Gundavaram, O'Reilly & Associates
*Mastering Regular Expressions*, Jeffrey Fried, O'Reilly & Associates

# Usenet

在 Usenet 上查看以下内容：

- `comp.lang.perl.misc`—讨论 Perl 语言的各个方面。确保你的问题是针对 Perl 特定的，而不是通用的。常客倾向于抨击那些不懂区别的人。
- `comp.infosystems.www.authoring.cgi`—讨论 CGI 程序的编写，因为大部分讨论是针对 Perl 的。确保你的问题与 CGI 编程相关，而不仅仅是 Perl。常客对保持主题非常挑。

# WWW

在万维网上查看这些站点：

- http://www.perl.com—Perl 官方主页。这里可以找到关于 Perl 的各种信息，从它的历史和文化到实用的技巧。这里也是为你的系统下载 Perl 解释器的地方。
- http://www.perl.com/CPAN—这里之前提到过，但值得单独提及。CPAN（全面 Perl 存档网络）是寻找模块和程序的地方。如果你用 Perl 写了你认为特别用的代码，可以将其提供给 Perl 社区。
- http://www.perl.com/pub/q/FAQs—常见 Perl 查询的常见问题解答；该网站提供了一种快速搜索 Perl 答案的方法。
- http://www.perl.org—HTML 作者公会是在线学习的最好起点之一。如果你精通 Perl，请去 http://jobs.perl.org。
- http://www.perl.org/pm—致力于协助 Web 开发者的非营利组织。其服务之一是大量的邮件列表。
- http://www.perl.org/tpj—Perl Journal 是一份“读者支持的每月电子杂志”，致力于 Perl 语言。TPJ 总是充满优秀且信息丰富的文章，对于初学者和经验程序员来说都是无价的资源。
- http://www.ibm.com/developerworks/linux/library/perl—关于单行 Perl 脚本和代码的短教程。

# 其他

不属于上述任何类别的价值资源是与 Perl 相关的互联网聊天（IRC）频道。你通常可以在 IRC 上找到几个可用频道。然而，名称相似的频道的问题、讨论和重点因服务器而异。例如，`#perlhelp` 频道通常用于有关安装和学习 Perl 的通用问题。`#perl` 频道通常用于高级问题，但在某些服务器上可能欢迎初学者的问题。你可能在 `#cgi` 和 `#html` 频道中找到一些有用的答案。访问 http://perl.de/irc 获取服务器列表。

# 第 24 章

## 本章内容

# 使用 Python

- Linux 上的 Python
- Python 基础
- 函数
- 面对象
- 标准库与 Parnassus 宝库
- 引用参考

随着 PHP 开始主导 Web 脚本世界，Python 正在日益缩小命令行脚本的领域。Python 精确且简洁的语法使其成为最容易学习的语言之一，它允许程序员更快地编写代码并花费更少的时间维护代码。尽管 PHP 在根本上与 Java 和 Perl 相似，但 Python 更接近 C 和模块，因此起初看起来可能很陌生。

大多数其他语言在其核心处有一组开发者，而 Python 有 Guido van Rossum——创建者、父亲和终身仁慈独裁者（BDFL）。虽然 Guido 现在在 Python 上花费的时间更少了，但他本质上仍然拥有否决权。正如 Guido 自己的话所：“即使你对语言设计一无所知，也能看出 Python 是一门简单的语言。”

后续页面构成了关于 Python 的“快速入门”教程。

# Linux 上的 Python

Ubuntu 默认安装了 Python，许多其他 Linux 和 Unix 版本也是如此。部分原因是因为它是如此流行的脚本语言，节省了以后安装的时间。

Python 二进制文件安装在 `/usr/bin/python`；如果你运行它，就会进入解释器，可以在其中输入命令并立即执行。PHP 也有交互模式（使用 `-a` 激活），它既不强大也不灵活。

与 Perl、PHP 以及其他语言一样，你也可以通过在脚本开头添加 shebang 行 (`#!`) 指 `/usr/bin/python` 并设置文件为可执行来运行 Python 脚本。

运行 Python 脚本的第三也是最后的方法是通过 `mod_python`，你可以通过 `synaptic` 安装。

# 获取交互

为了介绍介绍，我们使用交互式解释器，因为它会在你输入时提供即时反馈。开始之前，打开终端并运行命令 `python`。你会看到：

```
[paul@caitlin ~$ python

Python 2.4.3 (#2, Apr 27 2006, 14:43:58)

[GCC 4.0.3 (Ubuntu 4.0.3-1ubuntu)] on linux

Type "help", "copyright", "credits" or "license" for more information.

>>>
```

`>>>` 是你输入内容的地方，你可以像这样设置和获取变量：

```
>>> python = 'great'
>>> python
'great'
>>>
```

在第一行，变量被设置为文本 `great`，在第二行，通过简单输入想要读取的变量名称从变量中读取该值。第三行显示 Python 打印变量；第四行你回到了提示符处可以输入更多命令。

完成后，按 `Ctrl+D` 退出。此时，解释器会忘记你所有的变量和命令，这就是为什么复杂的 Python 程序总是保存在脚本中！

# Python 基础

Python 是一种与其他大多数语言完全不同的语言，它非常有逻辑性，使得大多数人都能快速学会。你已经见过如何轻松地赋值字符串，但在 Python 中，几乎一切都是轻而举见的——只要你记住语法！

## 数字

Python 处理数字的方式比其他某些语言更精确。它拥有所有的常规运算符——例如用于加法的 `+`、`-` 减法、`/` 除法和 `*` 乘法——但它增加了 `%` 取模（除余数）、`**` 幂以及 `//` 整除。它对使用的哪种类型的数字也十分明确，如下例所示：

```python
>>> a = 5
```
