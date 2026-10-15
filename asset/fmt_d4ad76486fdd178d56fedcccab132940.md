
其中 `first.py` 是当前工作目录中包含大量语法正确的Python命令的文件，并且Python程序位于你UNIX环境中的程序执行路径中。

这种执行Python代码的方法有时被称为将其作为用户编写的库模块来运行。

如果 `first.py` 中的命令不包含任何定向到屏幕的输出（例如使用 `print` 语句），那么 `shell` 提示符会立即重新出现，并且当脚本文件终止时，你将不在Python解释器中！

### 16.1.6.3 方式3 (导入脚本模式)

与方式2类似，你使用自己选择的文本编辑器创建并保存包含多条Python命令的脚本文件，可能命名为 `first.py`，保存在你执行Python的当前工作目录中。

然后，你运行Python，并在Python命令提示符下使用 `import` 命令将脚本文件导入Python。使用此模式的一个好理由是，如果你的脚本文件包含函数定义。下面是一个简单的例子：

### 示例 16.0.c

```
>>> import first
>>>
```

其中 `first` 是不带 `.py` 扩展名的文件。它应包含Python命令并位于当前工作目录中。现在，`first.py` 中的对象、语句、表达式和模块（如Python函数）在Python解释器中对你可用。使用此模式的一个好理由是，将这些结构和函数引入当前的交互式Python会话。

注意：一旦你通过按住键盘上的 `<Ctrl>` 和 `D` 键退出 Python，当前的交互式会话即告结束，你在 Python 中创建的环境也会丢失。

## 16.1.7 Python 的用途

Python 可以完成多种编程任务，大致可分为以下几类示例：

- Shell 脚本
- 系统编程
- 网络和互联网脚本
- 数据库编程
- 系统管理脚本
- 图形用户界面（GUI）脚本
- 科学与数学编程
- 数据挖掘

在本章中，我们使用了所示的所有三种 Python 运行模式，并给出 Python 语言的初学者入门介绍。我们还遵循所示的层级模式，大致从该模式的最底层到最顶层。本章其余部分可分为三部分：

- 第 16.2 节介绍如何安装 Python。
- 第 16.3 节在该模型框架内给出 Python 的基本语法。
- 第 16.4 节给出一些简单的、已实际演练的示例，展示在 UNIX 中可以使用 Python 完成的某些实际编程任务类别。

我们使用 Python 2.7.9，这是本书编写时更为成熟和通用的 Python 版本，它随我们的基础 UNIX 系统 PC-BSD 捆绑并提供，且会自动安装。运行 Python 2.X 的一个优势是，已有大量现成的 Python 2.X 程序和模块库，你可以将它们整合到自己的程序中。在必要之处，我们会指出 Python 2.X 和 Python 3.X 之间的差异，这些差异对于初学者程序员来说并不难克服。

## 16.2 如何在 PC-BSD 和 Solaris 系统上安装 Python

PC-BSD 和 Solaris 都预装了某个版本的 Python，普通用户即可使用。但是，如果你在安装其他 UNIX 操作系统时，该系统并未包含 Python，或者你想要在系统现有版本之外再安装一个更新版本，或者想要替换现有版本，那么你可能需要在系统上安装 Python。本节内容有四种可能的途径。请注意，由于系统管理员安装你的系统的方式存在差异，并且你安装的 UNIX 版本也各不相同，下一节中的四步安装过程可能需要由系统管理员替你完成！一个类似情况的典型例子是：你的 `/usr/bin` 中没有 C 编译器，或者你想要升级到最新的 `gcc` 编译器，却不知道在有无包管理器的情况下该如何操作。

### 16.2.1 在 PC-BSD 上安装 Python

要了解你正在使用的计算机上是否已安装 Python 2.7.X，最简单的方法是在控制台或终端窗口的 `shell` 提示符下输入 `python` 并按 `<Enter>` 键。我们在 PC-BSD 系统上执行此操作时，会得到以下结果：

```
[bob@pcbsd-6064] % python

Python 2.7.9 (default, Feb 12 2014, 19:30:28)

[GCC 4.2.1 Compatible FreeBSD Clang 3.3 (tags/RELEASE_33/final 183502)] on freebsd10

Type "help", "copyright", "credits" or "license" for more information.

>>>
```

三个大于符号 (`>>>`) 是 Python 解释器提示符，表示你已经进入 Python 环境！

要退出到终端窗口的命令行提示符，请在 `>>>` 之后按 `<Ctrl-D>`。

系统响应的第一行显示此系统上运行的是 Python 2.7.9。

如果在终端窗口的命令行上收到错误消息，例如 `command not found`，则可能是你的系统尚未安装 Python，或者你没有权限访问它。这时你需要联系系统管理员安装该程序，或授予你执行它的权限。

本章中的每个程序都可以在 Python 2.7.9 中完成，但如果你想运行第 16.4.4 节中的示例，则必须获取 Python 2.7.9（或你阅读本书时 2.7 版本的最新发行版）并将其安装到你的系统上。

在 PC-BSD 系统上安装 Python 最简单的方法是，以超级用户身份使用命令 `pkg install python`，然后按照 `pkg` 程序提供的提示进行操作。例如，如果你想要安装 Python 2.7.X 或 Python 3.X，可以输入 `pkg install python27` 或 `pkg install python3`。如果你确实安装了 Python 3.X，则在命令行上输入 `python3.4` 来运行它。

### 16.2.2 在 Solaris 上安装 Python

对于 Solaris，你可以使用 IPS 包管理器升级随系统预装的 Python 版本。如果你在 Solaris 下运行默认的 GNOME 桌面，我们建议你使用图形版本的 IPS 包管理器来下载并安装最新版本的 Python 2.7.X。有关图形化 IPS 包管理器在 Solaris 中的外观，请参见本章末尾的图 16.22。我们不提供在本书中图形化使用 IPS 包管理器的安装说明。

chapter，但在本章第 23 章“UNIX 系统管理基础”中，我们确实会详细介绍如何在 Solaris 上使用命令行、基于文本的 IPS 包管理器来安装软件包。

## 16.3 基本设置和语法，以及获取帮助

要在本章后面的部分中以实际示例使用 Python，首先有必要熟悉该语言的语法；例如，如何将其用作计算器来执行单行 Python 代码以完成简短、有意义的任务。

如果您需要了解 Python 中某个特定模块、关键字或主题的帮助，您始终可以按如下方式输入 `help` 函数调用以进入帮助系统：

```
>>>help()
Welcome to Python 2.7! This is the online help utility.

If this is your first time using Python, you should definitely

check out

the tutorial on the Internet at http://docs.python.org/tutorial/.

Enter the name of any module, keyword, or topic to get help on

writing

Python programs and using Python modules. To quit this help

utility and

return to the interpreter, just type "quit".

To get a list of available modules, keywords, or topics, type

"modules",

"keywords", or "topics". Each module also comes with a one-line

summary

of what it does; to list the modules whose summaries contain a

given word

such as "spam", type "modules spam".

help>
```
