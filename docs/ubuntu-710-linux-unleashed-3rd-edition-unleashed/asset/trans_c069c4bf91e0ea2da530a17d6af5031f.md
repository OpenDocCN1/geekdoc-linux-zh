
# 第24章

## 使用 Python

随着 PHP 在 Web 脚本领域占据主导地位，Python 正日益主导命令行脚本领域。Python 精确而简洁的语法使其成为最易于学习的语言之一，并且允许程序员更快地编码，花费更少的时间维护代码。虽然 PHP 在根本上与 Java 和 Perl 相似，但 Python 更接近 C 和 Modula-3，因此初看时可能会显得陌生。

大多数其他语言都有其核心的开发者群体，但 Python 有 Guido van Rossum——创造者、父亲和终身仁慈独裁者（BDFL）。尽管 Guido 现在花费在 Python 上的时间更少，但他仍然本质上拥有对语言变更的否决权，这使得它在漫长的开发岁月中保持一致。最终结果是，正如 Guido 自己所说，“即使你实际上对语言设计一无所知，你也能看出 Python 是一个非常简单的语言。”

以下页面构成了一个“快速入门”Python 教程，旨在为你提供组装基本脚本所需的所有信息，并指引你前往可以让你更进一步的资源。

### Linux 上的 Python

Ubuntu 默认安装了 Python，许多其他版本的 Linux 和 UNIX 也是如此——甚至 Mac OS X 也预装了 Python。这部分是出于便利，因为它是一种非常流行的脚本语言，如果用户想运行脚本，就无需稍后安装它。

Python 二进制文件安装在 /usr/bin/python；如果运行它，你将进入 Python 交互式解释器，在那里你可以输入命令并立即执行。虽然 PHP 也有交互模式（使用 php -a 激活它），但它既不如 Python 强大也不如 Python 灵活。

与 Perl、PHP 和其他脚本语言一样，你也可以通过在脚本开头添加 shebang 行（#!）指向 /usr/bin/python，然后将文件设为可执行，来执行 Python 脚本。

运行 Python 脚本的第三种也是最后一种方式是通过 mod_python，你可以通过 synaptic 安装它。

出于本次介绍的目的，我们使用交互式 Python 解释器，因为它在你输入命令时提供即时反馈。

### 本章内容

- Python on Linux
- The Basics of Python
- Functions
- Object Orientation
- The Standard Library and the Vaults of Parnassus
- Reference

immediately. Although PHP also has an interactive mode (use php -a to activate it), it is neither as powerful nor as flexible as Python's.

As with Perl, PHP, and other scripting languages, you can also execute Python scripts by adding a shebang line (#!) to the start of your scripts that point to /usr/bin/python and then setting the file to be executable.

The third and final way to run Python scripts is through mod_python, which you can install through synaptic.

For the purposes of this introduction, we use the interactive Python interpreter because it provides immediate feedback on commands as you type them.

### 开始交互

本章我们将使用交互式解释器，因此确保你能熟练使用它至关重要。开始时，打开一个终端并运行命令 python。你应该会看到以下内容：

```
[paul@caitlin ~]$ python
Python 2.4.3 (#2, Apr 27 2006, 14:43:58)
[GCC 4.0.3 (Ubuntu 4.0.3-1ubuntu5)] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

>>> 是你输入的地方，你可以像这样设置和获取变量：

```
>>> python = 'great'
>>> python
'great'
>>>
```

第一行将变量 python 设置为文本 great，第二行通过简单地输入你想要读取的变量名来从变量中读回该值。第三行显示 Python 打印变量；第四行你回到提示符以输入更多命令。Python 会记住你在交互式解释器中使用过的所有变量，这意味着你可以将一个变量设置为另一个变量的值。

完成后，按 Ctrl+D 退出。此时，解释器会忘记你所有的变量和命令，这就是为什么复杂的 Python 程序总是保存在脚本中！

## Python 的基础

Python 是一种与大多数其他语言完全不同的语言，但它如此合乎逻辑，大多数人都能迅速掌握。你已经看到如何轻松地分配字符串，但在 Python 中几乎所有事情都一样简单——只要你记住语法！

### 数字

Python 处理数字的方式比某些其他语言更精确。它拥有所有常规运算符——例如 + 用于加法，- 用于减法，/ 用于除法，* 用于乘法——但它增加了 % 用于取模（除法余数），** 用于幂运算，以及 // 用于向下取整除法。它也明确指定正在使用哪种类型的数字，如下例所示：

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

第一次除法返回 0，因为 a 和 b 都是整数（整数），所以 Python 将除法计算为整数，结果为 0。通过将 b 转换为 10.0，Python 将其视为浮点数，因此除法现在按浮点值计算，结果为 0.5。即使 b 是浮点数，使用 //——向下取整除法——也会将其向下舍入。

使用 **，你可以轻松看到 Python 如何处理整数：

```
>>> 2 ** 30
1073741824
>>> 2 ** 31
2147483648L
```

第一个语句将 2 的 30 次方（即 2 × 2 × 2 × 2 × 2 ...），第二个语句将 2 的 31 次方。注意第二个数字末尾有一个大写 L——这是 Python 告诉你它是一个长整数。长整数与普通整数之间的区别很小但很重要：普通整数可以使用 CPU 上的简单指令计算，而长整数——因为它们可以大到你需要的程度——需要在软件中计算，因此速度较慢。

指定大数字时，你无需在末尾加上 L——Python 会为你判断出来。此外，如果一个数字起初是普通数字然后超出其边界，Python 会自动将其转换为长整数。同样情况并不成立

