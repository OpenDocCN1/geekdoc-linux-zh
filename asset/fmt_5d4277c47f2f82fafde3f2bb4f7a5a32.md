
真正的缩进可以使用 `-i` 配合 `-pe` 来对文件进行原地编辑；`Perl` 读取文件，呈现行供编辑，并将结果保存到原始文件中。你可以为 `-i` 提供一个模式，告诉 `Perl` 如何备份每个文件的原始版本。例如，`-i bak` 将 `passwd` 备份为 `passwd.bak`——如果你不提供备份模式，则完全没有备份。注意 `-i` 和后缀名之间没有空格。

#### Perl 扩展模块

`CPAN`（位于 `cpan.org` 的全面 Perl 存档网络）是用户贡献 Perl 库的仓库。`cpan` 命令极大方便了新模块的安装，它类似于专门用于 Perl 模块的 `yum` 或 `APT` 包管理器。如果你使用的是 Linux 系统，请检查你的发行版是否将你需要的模块作为标准功能打包——安装系统级包要简单得多，然后让系统随时间推移自行更新。

![](img/9b33263d3e7e36cd43da7756018c8735_113_0.png)

## 第 2 章 脚本与 Shell

在没有 `cpan` 命令的系统中，尝试运行 `perl -MCPAN -e shell` 作为实现相同功能的替代方案：

```
$ sudo perl -MCPAN -e shell
```

```
cpan shell -- CPAN exploration and modules installation (v1.9205)

Readline input (maybe install Bundle::CPAN or Bundle::CPANxx!)

cpan[1]> install Class:Date

CPAN: Storable loaded ok (v2.18)

CPAN: LWP::Agent loaded ok (v5.819)

CPAN: Time::HiRes loaded ok (v1.9711)

several pages of status updates ...
```

用户可以在其家目录下安装 Perl 模块供个人使用，但该过程并不一定简单。我们建议对于从 CPAN 安装系统级第三方模块采取宽松政策；社区提供了一个中心的分发点，代码公开检查，且模块贡献者可以通过姓名标识。Perl 模块并不比其他开源软件更危险。

许多 Perl 模块使用 C 语言编写的组件以获得更好的性能。安装涉及编译这些段，因此你需要包含 C 编译器和全套库的完整开发环境。

对于大多数语言来说，Perl 程序中最常见的错误是重新实现社区编写模块已经提供的功能。养成在处理任何 Perl 问题时第一步访问 CPAN 的习惯。这可以节省开发和调试时间。

### 2.5 Python 脚本

随着项目变得越来越大和复杂，面向对象设计和实现的益处变得愈发明显。Perl 在五年前就错过了 OO 的班车，并一直在拼命追赶。Perl 的面向对象编程版本仍然感觉有些不稳。

本节介绍的是 Python 2。Python 3 正在开发中，可能会在本书出版期间发布。与 Perl 6 不同，它似乎是一个相对增进的更新。

具有强大 OO 背景的工程师通常喜欢 Python 和 Ruby 等具有明显 OO 影响的脚本语言。 Perl 目前似乎已经处于采用曲线的下降阶段，因此对于管理层来说相对容易说。包括 OpenSolaris 在内的多个操作系统，

> Thomas Christensen 评论：“Python 的哲学是代码应该是易读的。这就是为什么它使用缩进来定义块而不是大括号或关键字。这迫使程序员思考代码的结构，并通常会导致更整洁、更易维护的项目。”

#### 对象、字符串、数字、列表、字典、元组和文件

Python 中的所有数据类型都是对象，这使得它们比在 Perl 中更有功能和灵活性。

在 Python 中，列表包含在方括号中。数组从零开始计数，这是本章涵盖的三种脚本语言中少数不改变的概念之一。

Python 新引入了“元组”`tuples`，它们本质上是不可变的列表。元组比数组快，并且有助于表示实际上是可修改的数据（注意：元组是不可变的，而列表是可变的）。元组的语法与列表相同，区别在于分隔符是圆括号而不是方括号。由于 `(thing)` 像一个简单的表达式，因此包含单个元素的元组需要一个额外的逗号来消除歧义：`(thing,)`。

这里是 Python 中一些基本的变量和数据类型操作：

此示例产生以下输出：

```
$ python objects

name: Gwen

rating: 10

characters: ['SpongeBob', 'Patrick', 'Squidward']

elements: ['lithium', 'carbon', 'boron']
```

Python 中的变量没有在语法上通过类型标记或声明，但它们所引用的对象具有底层类型。在大多数情况下，Python 不会自动为你转换类型，但单独的函数或运算符会。例如，你不能在不显式将数字转换为其字符串表示的情况下（使用 `+` 运算符）将字符串和数字数字。然而，格式化运算符和语句会将所有内容强制转换为字符串。每个对象都有字符串表示。

字符串格式化运算符 `%` 与 C 或 Perl 中的 `sprintf` 函数非常相似，但它可以出现在任何字符串出现的地方。它是一个二元运算符，获取左侧的字符串和右侧要插入的值。如果有多个值要插入，这些值必须以元组的形式呈现。

![](img/9b33263d3e7e36cd43da7756018c8735_117_0.png)

### 第 2 章 脚本与 Shell

Python 字典与 Perl `hash` 是同一个东西；即一个键值对的列表。字典字面量包含在花括号中，每个键值对之间用冒号分隔。

```python
#!/usr/bin/python

ordinal = { 1 : 'first', 2 : 'second', 3 : 'third' }

print("The ordinal array contains", ordinal)

print("The ordinal of 1 is", ordinal[1])
```

在实际使用中，Python 字典非常像数组，但下标（键）可以是整数以外的对象。

```
$ python dictionary

The ordinal array contains [1: 'first', 2: 'second', 3: 'third']

The ordinal of 1 is first
```

Python 将打开的文件视为带有关联方法的对象。顾名其名，`readline` 方法读取单行，因此下面的示例从 `/etc/passwd` 文件中读取并打印两行。

```python
#!/usr/bin/python

f = open('/etc/passwd', 'r')

print(f.readline())

print(f.readline())

f.close()
```

```
$ python fileio

at:x:25:Batch daemon:/var/spool/atjobs:/bin/true

bin:x:1:1:bin/bin/true
```

`print` 语句末尾的逗号是为了抑制换行，因为从原始文件读取时每一行已经包含了一个换行符。

#### 输入验证示例

下面的脚本片段是我们目前输入验证器的 Python 版本。它演示了子程序和命令行参数的使用，以及其他一些 Python 特性。

```python
#!/usr/bin/python

import sys

import os

def show_usage(message, code=1):

    print(message)

    print("%s: source_dir dest_dir" % sys.argv[0])

    sys.exit(code)
```

#### 循环

```python
if len(sys.argv) != 3:
    show_usage("2 arguments required; you supplied %d" % (len(sys.argv) - 1))
elif not os.path.isdir(sys.argv[1]):
    show_usage("Invalid source directory")
elif not os.path.isdir(sys.argv[2]):
    show_usage("Invalid destination directory")

dest = sys.argv[1:3]

print("Source Directory is", dest[0])

print("Destination Directory is", dest[1])
```
