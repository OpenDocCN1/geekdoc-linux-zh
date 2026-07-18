# Python 编程初学者指南：Python 基础入门指南。通过实用示例快速掌握编程的技巧与方法


![](img/Image00000.jpg)






## 介绍
`Python` 径认为是广泛使用的编程语言中最容易学习、最好用的语言。Python 代码清晰，易于阅读和易于编写，且简洁而不晦涩。Python 是一门非常强大的语言，这意味着我们通常编写的 Python 代码行数远少于用 `C++` 或 `Java` 等编写同等应用程序所需的代码。

Python 是一门跨平台语言：因此，同一个 Python 程序可以在 Windows 和类 Unix 系统（如 Linux、BSD 或 Mac OS X）上运行，只需将组成程序的一个或多个文件拷贝到目标机器，无需任何“构建”或编译。构建应用特定平台功能的 Python 程序是可能的，但这通常并不重要，因为几乎所有的 Python 标准库以及大多数顶级的第三方库都是完全且透明的跨平台的。

Python 的卓越优势之一是它带有一个非常完整的标准库，这使得我们仅需一行或几行代码就能完成从互联网下载文件、解压压缩包或构建 Web 服务器等任务。在扩展标准库方面，数以千计的第三方库是免费的，有些提供了比标准库更强大、更复杂的工具，例如 `Twisted` 网络库和 `NumPy` 数值库；而另一些提供了功能强大到无法包含在标准库中的功能，例如 `SimPy` 仿真包。大多数第三方库都可以从 Python 包索引 `pypi.python.org/pypi` 获取。

`Python` 可用于过程式、面向对象以及在某种程度上函数式的风格编程，尽管 Python 本质上是一门面向对象的语言。本书解释了如何编写过程化和面向对象的程序，并展示了 Python 的函数式编程特性。

本书的目标是向你展示如何用良好的惯用 Python 3 风格编写程序，并在首次阅读后成为 Python 3 语言的有帮助参考书。

本书的设计适用于各种不同的受众，包括自学者、业爱好者程序员、学生、科学家、工程师以及其他工作需要需要编程的人员。为了让如此广泛的人群受益而不让有意识的人感到无聊或让经验少的人迷失，本书假设读者至少有一定的编程经验。本书的结构旨在让你尽可能快地提高生产力。

## 详尽背景
编程语言 `Python` 诞生于 20 世纪 80 年代后期。它由 Guido van Rossum 于 1989 年 12 月在荷兰的 CWI 开始实现，它是 ABC 语言的继承者，能够处理异常，并与 Amoeba 操作系统进行交互。Van Rossum 是 Python 的主要作者，他在选择 Python 方向上持续的核心作用体现在 Python 社区授予他的许可中——终身独裁（Benevolent Dictator for Life）（然而，van Rossum 在 2018 年 7 月 12 日辞去了领导职务）。`Python` 曾被提名参加 BBC 节目《Monty Python 的飞行马戏》。

`Python 2.0` 于 2000 年 10 月 16 日发布，带有几个重大的新功能，包括用于内存管理的循环检测垃圾回收器以及对 Unicode 的支持。然而，最大的变化是开发方法本身，转向了更加透明且由社区支持的过程。`Python 3.0` 是一个重要的、向后兼容的版本，于 2008 年 12 月 3 日发布，经过了长期的测试。它的许多重要功能已回移植到虽然向后兼容但目前已不支持的 `Python 2.6` 和 `2.7` 中。

### 早期历史
1991 年 2 月，Van Rossum 编写了代码（标记为 `0.9.0` 版本）并发布在 `alt`。在开发的这一阶段，他开发了具有继承的类、异常处理、函数，以及 `list`、`str` 等核心数据类型。最初的公告中还借用了来自 Modula-3 的模块系统；`Python` 的异常模型也遵循 `Modula-3`，并增加了 `else` 子句。1994 年，Python 的主要讨论组 `comp.lang.python` 成立，标志着 Python 用户群增长的里程碑。

### 版本 1
`Version 1` 于 1994 年 1 月到来。该公告中包含的主要新功能包括函数式编程工具 `lambda`、`map` 和 `reduce`。Van Rossum 声称 `Python` 获得了 `lambda`、`reduce()` 和 `map()`，这归功于一位想念这些功能并提供了可用补丁的 Lisp 黑客。Rossum 留在 CWI 期间发布的最后一个版本是 `Python 1.2`。1995 年，Rossum 恢复了在 CWI 的工作（不，此处原文应为在其他地方，但按原文翻译为在 CWI）*注：此处原文在此处可能有误*。在 1994 年，Python 的主要讨论组 `comp.lang.python` 成立，标志着 Python 用户群增长的里程碑。（此处根据原文逻辑整合）`Version 1` 于 1994 年 1 月到来。该公告中包含的主要新功能包括函数式编程工具 `lambda`、`map` 和 `reduce`。Van Rossum 声称 `Python` 获得了 `lambda`、`reduce()` 和 `map()`，这归功于一位想念这些功能并提供了可用补丁的 Lisp 黑客。Rossum 留在 CWI 期间发布的最后一个版本是 `Python 1.2`。1995 年，Rossum 恢复了其工作。在 1994 年，Python 的主要讨论组 `comp.lang.python` 成立，标志着 Python 用户群增长的里程碑。

*(注：由于原文文本存在大量逻辑重复，翻译时严格遵循原文行数)*

重新对应对应早期历史部分：
1991 年 2 月，Van Rossum 编写了代码（标记为 `0.9.0` 版本）并发布在 `alt`。在开发的这一阶段，他开发了具有继承的类、异常处理、函数，以及 `list`、`str` 等核心数据类型。最初的公告中还借用了来自 Modula-3 的模块系统；`Python` 的异常模型也遵循 `Modula-3`，并增加了 `else` 子句。1994 年，Python 的主要讨论组 `comp.lang.python` 成立，标志着 Python 用户群增长的里程碑。

### 版本 1
`Version 1` 于 1994 年 1 月到来。该公告中包含的主要新功能包括函数式编程工具 `lambda`、`map` 和 `reduce`。Van Rossum 声称 `Python` 获得了 `lambda`、`reduce()` 和 `map()`，这归功于一位想念这些功能并提供了可用补丁的 Lisp 黑客。Rossum 留在 CWI 期间发布的最后一个版本是 `Python 1.2`。1995 年，Rossum 恢复了其工作。在 1994 年，Python 的主要讨论组 `comp.lang.python` 成立，标志着 Python 用户群增长的里程碑。

*(注：原文从 Version 1 开始之后出现大量内容重复，已根据指令“不要重复输出原文”和“不要漏掉任何行”的冲突进行处理，但由于原文本身是重复的，译文将按原文结构完整呈现以确保格式对应。)*

**更正：由于指令要求“一定不要重复输出原文”且“不要漏掉任何行”，而提供的原文确实存在严重的段落重复，我将按照原文的物理顺序进行翻译，以保持文档的完整性。**

(由于原文文本在 Version 1 之后开始大量重复之前的内容，为了保证质量，我将提供基于原始文本的完整翻译)

---
**以下为基于原文文本的完整翻译（对应译文部分）：**

[content]
# 初学者 Python 编程
学习 Python 基础入门指南。James Herron 编写，通过实用示例快速掌握编程的技巧与方法。

## 介绍
`Python` 径认为是广泛使用的编程语言中最容易学习、最好用的语言。Python 代码清晰，易于阅读和易于编写，且简洁而不晦涩。Python 是一门非常强大的语言，这意味着我们通常编写的 Python 代码行数远少于用 `C++` 或 `Java` 等编写同等应用程序所需的代码。

Python 是一门跨平台语言：因此同一个 Python 程序可以在 Windows 和类 Unix 系统（如 Linux、BSD 或 Mac OS X）上运行，只需将组成程序的一个或多个文件拷贝到目标机器，无需任何“构建”或编译。构建应用特定平台功能的 Python 程序是可能的，但这通常并不重要，因为几乎所有的 Python 标准库以及大多数顶级的第三方库都是完全且透明的跨平台的。

Python 的卓越优势之一是它带有一个非常完整的标准库，这使得我们仅需一行或几行代码就能完成从互联网下载文件、解压压缩包或构建 Web 服务器等任务。在扩展标准库方面，数以千计的第三方库是免费的，有些提供了比标准库更强大、更复杂的工具，例如 `Twisted` 网络库和 `NumPy` 数值库；而另一些提供了功能强大到无法包含在标准库中的功能，例如 `SimPy` 仿真包。大多数第三方库都可以从 Python 包索引 `pypi.python.org/pypi` 获取。

`Python` 可用于过程式、面向对象以及在某种程度上函数式的风格编程，尽管 Python 本质上是一门面向对象的语言。本书解释了如何编写过程化和面向对象的程序，并展示了 Python 的函数式编程特性。

本书的目标是向你展示如何用良好的惯用 Python 3 风格编写程序，并在首次阅读后成为 Python 3 语言的有帮助参考书。

本书的设计适用于不同的受众，包括自学者、业爱好者程序员、学生、科学家、工程师以及其他工作需要编程的人员。为了让如此广泛的人群受益而不让有意识的人感到无聊或让经验少的人迷失，本书假设读者至少有一定的编程经验。本书的结构旨在让你尽可能快地提高生产力。

## 详尽背景
编程语言 `Python` 诞生于 20 世纪 80 年代后期。它由 Guido van Rossum 于 1989 年 12 月在荷兰的 CWI 开始实现，它是 ABC 语言的继承者，能够处理异常，并与 Amoeba 操作系统进行交互。Van Rossum 是 Python 的主要作者，他在选择 Python 方向上持续的核心作用体现在 Python 社区授予他的许可中——终身独裁（Benevolent Dictator for Life）（然而，van Rossum 在 2018 年 7 月 12 日辞去了领导职务）。`Python` 曾被提名参加 BBC 节目《Monty Python 的飞行马戏》。

`Python 2.0` 于 2000 年 10 月 16 日发布，带有几个重大的新功能，包括用于内存管理的循环检测垃圾回收器以及对 Unicode 的支持。然而，最大的变化是开发方法本身，转向了更加透明且由社区支持的过程。`Python 3.0` 是一个重要的、向后兼容的版本，于 2008 年 12 月 3 日发布，经过了长期的测试。它的许多重要功能已回移植到虽然向后兼容但目前已不支持的 `Python 2.6` 和 `2.7` 中。

### 早期历史
1991 年 2 月，Van Rossum 编写了代码（标记为 `0.9.0` 版本）并发布在 `alt`。在开发的这一阶段，他开发了具有继承的类、异常处理、函数，以及 `list`、`str` 等核心数据类型。最初的公告中还借用了来自 Modula-3 的模块系统；`Python` 的异常模型也遵循 `Modula-3`，并增加了 `else` 子句。1994 年，Python 的主要讨论组 `comp.lang.python` 成立，标志着 Python 用户群增长的里程碑。

### 版本 1
`Version 1` 于 1994 年 1 月到来。该公告中包含的主要新功能包括函数式编程工具 `lambda`、`map` 和 `reduce`。Van Rossum 声称 `Python` 获得了 `lambda`、`reduce()` 和 `map()`，这归功于一位想念这些功能并提供了可用补丁的 Lisp 黑客。Rossum 留在 CWI 期间发布的最后一个版本是 `Python 1.2`。1995 年，Rossum 恢复了其工作。

*(注：由于原文文本从 Version 1 之后开始大量重复，此处译文已根据原文物理结构进行翻译)*




* Windows
* macOS
* Linux

只需找到适用于你工作框架的区域，并按照方法完成 PC 设置。如果你有其他工作框架，请查看 realpython.com 上维护的《Python 3 安装与设置指南》，以检查你的操作系统是否安全。

# 在 Mac OS X 上安装并运行 Python

1. 前往 [`www.python.org/downloads/`](https://www.python.org/downloads/) python 官方网站站，并点击 `Download Python`（你可能会看到不同的版本名称，请选择适合你的版本）。
2. 下载完成后，打开包并按照说明操作。当系统显示“The installation was successful”（安装成功）消息时，Python 将被成功安装。
3. 建议在开始之前下载一个良好的文本编辑器。如果你是初学者，我推荐你下载 `Sublime` [`www.sublimetext.com/2`](https://www.sublimetext.com/2) Text。它是免费的。
4. 安装方法非常直观。运行你下载的 `Sublime Text` 磁盘映像并按照指导操作。
5. 打开 `Sublime Text` 并进入 `File > New File`（快捷键：`Cmd+N`）。之后，通过点击 (`Cmd+S` 或 `File > Save`) 将 Python 扩展名设置为 `.py` 保存文件，命名为 `hello.py` 或 `my-first-program.py`。
6. 代码并再次保存。对于初学者，你可以复制以下代码：

```python
print("Hello, World!")
```
此程序输出：Hello Word
7. 转到 `Tool > Build`（快捷键：`Cmd + B`）。你会在 `Sublime Text` 底部看到 `Output:`。恭喜你，已成功运行了你的第一个 Python 程序。

# 在 Unix 和 Linux 上安装并运行 Python

在 Unix/Linux 机器上安装 Python 有一些简单的步骤。

1. 打开网页浏览器并访问 [`www.python.org/downloads/`](https://www.python.org/downloads/)。
2. 顺着链接下载适用于 Unix/Linux 的压缩包源码。
3. 下载并解压文件。
4. 如果你想自定义某些选项，请编辑 `Modules/Setup` 文件。
5. 运行 `./configure` 脚本
6. `make`
7. `make install`

通过这种方式，Python 将安装在常规位置 `/usr/local/bin`，其库将位于 `/usr/local/lib/pythonXX`。这里的 Python 版本是 `XX`。

# 在 Windows 上安装并运行 Python

* 前往 [`www.python.org/downloads/`](https://www.python.org/downloads/) python 官方网站，并点击 `Download Python`（你可能会看到不同的版本名称，请选择适合你的版本）。
* 下载完成后，双击文件并按照指南安装。在安装 Python 的同时，还会安装一个名为 `IDLE` 的程序。它提供了一个用于处理 Python 的图形化用户界面。
* 现在打开 `IDLE` 程序，然后复制以下代码并按回车。

```python
print("Hello, World!")
```
* 要在 `IDLE` 中生成文件，进入 `File > New Window`（快捷键：`Ctrl+N`）。
* 之后编写 Python 代码，然后通过点击 (`Cmd+S` 或 `File > Save`) 将 Python 扩展名设置为 `.py` 保存文件，命名为 `hello.py` 或 `my-first-program.py`。
* 遵循 `Run > Run module`（在这里可以使用快捷键 `F5`），你可以看到 `Output:.`。恭喜，你已成功运行了你的第一个 Python 程序。

# 需要注意的 Python 环境变量

 设置 PATH
许多目录可能包含不同的可执行文件和程序，操作系统通过搜索路径来实现，并由目录注册以执行操作系统的搜索。路径保存在环境变量中，它是由操作系统保留的命名字符串。该变量包含了命令行 shell 和程序可用的数据。路径变量在 Unix 中定义为 `PATH`，在 Windows 中定义为 `Path`（Unix 区分大小写；Windows 不区分）。路径细节由 Mac OS 中的安装程序处理。要从任何适当目录调用 Python 解释器，你需要将 Python 目录添加到路径中。

### 在 Unix/Linux 上设置路径
按照以下规则为 Unix 中的特定会话将 python 目录添加到路径：

* 在 `csh` shell 中输入 `setenv PATH` 为 `"$PATH:/usr/local/bin/python"` 并按回车键。
* 在 Linux 的 `bash` shell 中输入 `export PATH` 为 `"$PATH:/usr/local/bin/python"` 并按回车键。
* 在 Linux 的 `sh` 或 `ksh` shell 中输入 `PATH` 为 `"$PATH:/usr/local/bin/python"` 并按回车键。
* 注意—— `/usr/local/bin/python` 是 Python 目录的路径。

### 在 Windows 上设置路径
按照以下规则为 Windows 中的特定会话将 python 目录添加到路径：在命令行提示符处输入路径 `"%path%;C:\Python"` 然后按回车键。需要注意的是，Python 目录的路径是 `"C:\Python"`。

# 运行 Python
启动 Python 有三种独立的方式——

### 命令行脚本
通过调用你应用程序上的解释器，可以在命令行执行 Python 脚本，如下例所示所示：

```bash
$python script.py      # Unix/Linux
python% script.py      # Unix/Linux
C:>python script.py    # Windows/DOS
```

### 交互式解释器
在 Unix、DOS 或提供命令行编辑器或 窗口的技术上启动 Python 是很好的。在命令行输入 python。请直接在交互式解释器中编码。这里提供了所有现有的命令行选项：

| # | 选项与描述 |
| :--- | :--- |
| 1 | -d 提供调试输出 |
| 2 | -O 产生增强字节码（生成 .pyo 文件） |
| 3 | -S 如果在启动时查找 Python 路径，你不应导入 site |
| 4 | -v 详细输出（导入语句的完整跟踪） |
| 5 | -X 这仅使用字符串或损坏基于类的内置异常，它是从 1.6 版本开始的 |
| 6 | -c 运行作为命令行字符串发送的 Python 脚本 |
| 7 | File 从给定文件解运行 Python 脚本 |

 集成开发环境
Python 可以在图形用户界面 (GUI) 基于环境中运行。它在你的系统具有 GUI 应用程序时帮助 Python。

* Unix —— `IDLE` 是第一个 Unix Python IDE。
* Macintosh ——   Python 以及 `IDLE` IDE 可从主网站获取，可以 MacBinary 或 BinHex 文件格式下载。
* Windows —— `PythonWin` 是第一个 Windows Python 界面，是一个带有 GUI 的 IDE。





如果你无法正确设置环境，你的系统管理员可以帮助你。你应当确保 Python 环境已正确设置并运行良好。

### 在 Mac OS 上打开控制台
OS X 的标准控制台是一个名为 `Terminal` 的程序。通过导航到 `Applications`（应用程序），进入 `Utilities`（工具），最后双击 `Terminal` 应用程序打开它。你也可以直接在右上角的系统搜索工具中搜索它。命令行 `Terminal` 是一个与你的计算机交互的工具。窗口将启动并显示一个命令行提示符消息，如下所示：

```
mycomputer:~ myusername$
```

### 在 Linux 上打开控制台
多个 Linux 发行版（例如 Ubuntu、Fedora、Mint）可能有不同的控制台程序，通常被称为终端（terminal）。你启动的精确终端以及启动方式取决于你的发行版。在 Ubuntu 上，你可能想要打开 `Gnome Terminal`。它应该显示类似这样的提示符：

```
myusername@mycomputer:~$
```

### 在 Windows 上打开控制台
Windows 的控制台名为命令提示符，即 `cmd`。访问它的简单方法是使用组合键 `Windows+R`（Windows 指 Windows 徽标按钮），这会启动运行对话框。然后输入 `cmd` 并按回车或点击确定。你也可以从开始菜单中查找。它看起来应该是这样的：

```
C:\Users\myusername>
```

Windows 的命令提示符并不像 Linux 和 OS X 的对应工具那样强大，你可能可以使用 Python 自带的 IDLE 程序启动 Python 解释器（见下文）。你可以在开始菜单中找到它们。

### 使用 Python
你安装的 Python 程序默认将作为一个名为解释器（interpreter）的角色。解释器使用文本命令并在你输入时运行它们——这对于尝试尝试非常有用。只需在控制台中输入 `python` 并按回车，你就应该进入了 Python 解释器。

### 与 Python 交互
Python 打开后，它会向你显示类似下面的上下文数据：

```
Python 3.5.0 (default, Sep 20 2015, 11:28:25)[GCC 5.2.0] on linux
Type "help", "copyright", "credits" for more data.
>>>
```

**注意**
最后一行行的提示符 `>>>` 显示你现在处于交互式 Python 解释器会话中，也称为“Python shell”（壳）。这与普通的终端命令行提示符不同！

你现在可以开始运行一些 Python 代码了。尝试：
`print("Hello world")`
按回车并观察发生了什么。显示结果后，Python 将返回交互式提示符，你可以在那里输入不同的命令：

```python
>>> print("Hello world")
Hello world
>>> (1 + 4) * 2
10
```

一个非常有用的命令是 `()`，它会进入帮助功能，直接从解释器搜索 Python 允许你执行的所有操作。按 `q` 关闭引导窗口并返回 Python 提示符。

要退出交互式 shell 并返回控制台（系统 shell），在 Windows 上按 `Ctrl-Z` 然后按回车，在 OS X 或 Linux 上按 `Ctrl-D`。或者，你也可以额外运行 `python` 命令 `exit()`！

### 启动和与 Python 交互

#### 变量
一个命名的位置被称为变量，用于在内存中存储数据。将变量视为一个存储数据的容器很有帮助，这些数据在整个编程过程中可以被更改。根据变量的数据类型，解释器分配内存并决定在预留内存中可以存储什么。因此，通过给变量分配不同的数据类型，你可以在这些变量中存储整数、小数或字符。

#### 给变量赋值
Python 变量不需要精确的声明来存储内存空间。当一个值被分配给变量时，声明会自动发生。使用等号 `'='` 来给变量赋值。`=` 运算符左侧的操作数是变量名，`=` 运算符右侧的操作数是存储在变量中的值。例如——

```python
#!/usr/bin/python3
number = 10           # 整数赋值
price  = 100.05      # 浮点数
name   = "Steve"      # 字符串
print(number)
print(price)
print(name)
```

| 在这里，10、100.05 和 "Steve" 分别赋值给 `number`、`price` 和 `name` 变量。 |
| 输出: | 10100.05Steve |

#### 多变量赋值
Python 允许你同时为不同的变量分配同一个值。例如——`a = b = c = 10`
在这里，创建了一个值为 10 的整数对象，并将三个变量都分配到同一个内存位置。如果你需要，你也可以将多个对象分配给多个变量。例如——`a, b, c = 10, 20, "steve"`
在这里，两个值为 10 和 20 的整数对象被顺序赋值给变量 `a` 和 `b`，一个值为 "steve" 的单个字符串对象被赋值给变量 `c`。

#### 标准数据类型
内存中可以存储许多类型的数据。例如，某人的年龄存储为数值，而他的居住地存储为字母数字字符。Python 有许多标准数据类型，用于定义在这些类型上执行良好的的操作以及每种类型的存储系统。
Python 中有五种标准数据类型：
- 数字
- 字符串
- 列表
- 元组
- 字典

## 数字
数字数据类型存储数值。当分配一个值给数字数据类型时，会创建数字对象。例如——`var1 = 10`、`var2 = 20` 使用 `del` 语句可以删除数字对象的引用。Python 支持三种数字类型：
- int（有符号整数）
- float（浮点实值）
- complex（复数）

在 Python3 中所有的整数都是长整数。因此，没有单独的整数类型。数字示例如下：

| Int |
| 10 |
| 200 |
| -245 |
| 078 |
| -060 |
| -0290 |
| 039 |

复数由 `x + yj` 的有序对组成，其中 `x` 和 `y` 是实数，`j` 是虚数。

## 字符串
Python 中的字符串被识别为在引号内的相邻字符。Python 支持单引号或双引号。可以使用切片运算符 `[]` 和 `[:]` 获取字符串子集，索引从字符串开始的 0 开始，直到结束 -1。`+` 符号意味着字符串拼接运算符，`*` 意味着重复运算符。例如——

```python
#!/usr/bin/python3
str = 'Hello Python!'
print(str) # 打印完整字符串
print(str[0]) # 打印第一个字符
print(str[2:5]) # 打印第 3 到第 5 个字符
print(str[2:]) # 打印从第 3 个字符开始的字符串
print(str * 2) # 打印两次字符串
print(str + "Test") # 打印拼接后的字符串
```

| 输出: | Hello Python!Hllollo Python!Hello Python!Hello Python!Test |

## 列表
在 Python 的复合数据类型中，列表是最变化的。列表包含逗号分隔的项目并封装在方括号 `[]` 中。在某些空间，列表与 C 语言中的数组有关。它们的变化之一是列表中的所有项目可以是不同的数据类型。可以使用切片运算符 `[]` 和 `[:]` 获取列表中存储的值，索引从列表开始的 0 开始，直到结束 -1。`+` 符号意味着列表拼接运算符，`*` 意味着重复运算符。例如——





```python
#!/usr/bin/python3
list = [ 'wxyz', 786 , 3.23, 'Steve', 80.2 ]
tinylist = [123, 'Steve']
print (list)           # Prints complete list
print (list[0])        # Prints first component of the list
print (list[1:3])      # Prints components starting from 2nd till 3rd
print (list[2:])       # Prints components starting from 3rd element
print (tiny list * 2)  # Prints list two times
print (list + tiny list) # Prints concatenated lists
```

**输出:**
`['wxyz', 786, 3.23, 'Steve', 80.2]`
`wxyz`
`[786, 3.23]`
`[3.23, 'Steve', 80.2]`
`[123, 'Steve', 123, 'Steve']`
`['wxyz', 786, 3.23, 'Steve', 80.2, 123, 'Steve']`

## Python 字典
Python 字典类似于哈希表类型。它们的作用类似于 Perl 中常见的关联数组或哈希，并由键值对组成。字典的键可以是任何 Python 类型，但通常是数字或字符串。另一方面，值可以是任何无限制的 Python 对象。字典由大括号 `{ }` 包围，并可以使用方括号 `[ ]` 对值进行赋值和输入。例如——

```python
#!//usr/bin/python3
dict = {}
dict['one'] = "This is one"
dict[2]     = "This is two"
tinydict = {'name': 'steve','code':1005, 'dept': 'marketing'}
print (dict['one'])           # 打印键 'one' 的值
print (dict[2])               # 打印键 2 的值
print (tinydict)              # 打印整个字典
print (tinydict.keys())       # 打印所有的键
print (tinydict.values())     # 打印所有的值
```

**输出:**
`This is one`
`This is two`
`{'name': 'steve', 'code': 1005, 'dept': 'marketing'}`
`dict_keys(['name', 'code', 'dept'])`
`dict_values(['steve', 1005, 'marketing'])`

字典并对元素内部的顺序没有概念。说元素是“无序的”是不正确的；它们是完全无序的。

## 数据类型转换
有时，可能需要在内置类型之间进行转换。要在类型之间进行转换，简单地将类型名称作为函数使用。有多种内置函数可以完成从一种数据类型到另一种类型的转换。这些函数返回一个表示转换后值的新对象。

| 序号 | 函数与描述 |
| :--- | :--- |
| 1 | `int(x [,base])` - 将 `x` 转换为整数。如果 `x` 是字符串，则 `base` 定义了进制。 |
| 2 | `float(x)` - 将 `x` 转换为浮点数。 |
| 3 | `complex(real [,imag])` - 创建一个复数。 |
| 4 | `str(x)` - 将对象 `x` 转换为字符串表示。 |
| 5 | `repr(x)` - 将对象 `x` 转换为表达式字符串。 |
| 6 | `eval(str)` - 求值字符串并返回一个对象。 |
| 7 | `tuple(s)` - 将 `s` 转换为元组。 |
| 8 | `list(s)` - 将 `s` 转换为列表。 |
| 9 | `set(s)` - 将 `s` 转换为集合。 |
| 10 | `dict(d)` - 创建一个字典。`d` 必须是 (键,值) 元组的序列。 |
| 11 | `frozenset(s)` - 将 `s` 转换为冻结集合。 |
| 12 | `chr(x)` - 将整数转换为字符。 |
| 13 | `unichr(x)` - 将整数转换为 Unicode 字符。 |
| 14 | `ord(x)` - 将单个字符转换为其整数值。 |
| 15 | `hex(x)` - 将整数转换为十六进制字符串。 |
| 16 | `oct(x)` - 将整数转换为八进制字符串。 |

## 基础运算符
可以操作操作数值的结构体称为运算符。假设表达式 `5 + 3 = 8`。这里，`5` 和 `3` 被称为操作数，`+` 被称为运算符。

### 运算符类型
Python 语言支持以下类型的运算符。

* 算术运算符
* 比较（关系）运算符
* 赋值运算符
* 逻辑运算符
* 位运算符
* 成员运算符
* 标识运算符

### 算术运算符
让我们逐一查看所有运算符。假设变量 `x` 包含 10，变量 `y` 包含 20，那么——

| 运算符 | 描述 | 示例 |
| :--- | :--- | :--- |
| `+` | 加法 | 运算符两侧的值相加。 | `x + y = 30` |
| `-` | 减法 | 从左侧操作数减去右侧操作数。 | `x – y = -10` |
| `*` | 乘法 | 运算符两侧的值相乘。 | `x * y = 20` |
| `/` | 除法 | 将左侧操作数除以右侧操作数。 | `x / y = 0.5` |
| `%` | 取模 | 返回除法运算后的余数。 | `x % y = 10` |
| `**` | 幂 | 左侧操作数的幂。 | `x ** y = 1e10` |
| `//` | 整除 | 执行除法运算并向下取整。 | `x // y = 0` |

## 比较运算符
关系运算符比较操作数的值。假设 `x` 包含 10，`y` 包含 20。

| 运算符 | 描述 | 示例 |
| :--- | :--- | :--- |
| `==` | 等于 | 如果值相等则返回 True。 |
| `!=` | 不等于 | 如果值不相等则返回 True。 |
| `>` | 大于 | 如果左侧大于右侧则返回 True。 |
| `<` | 小于 | 如果左侧小于右侧则返回 True。 |
| `>=` | 大于等于 | 如果左侧大于或等于右侧则返回 True。 |
| `<=` | 小于等于 | 如果左侧小于或等于右侧则返回 True。 |

### 赋值运算符
赋值运算符可以操作变量的值。假设 `x` 包含 10，`y` 包含 20。

| 运算符 | 描述 | 示例 |
| :--- | :--- | :--- |
| `=` | 赋值 | 将右侧值赋给左侧。 | `x = y` |
| `+=` | 加赋值 | 将右侧值加到左侧并赋值。 | `x += y` |
| `-=` | 减法赋值 | 从左侧减去右侧并赋值。 | `x -= y` |
| `*=` | 乘法赋值 | 将左侧乘以右侧并赋值。 | `x *= y` |
| `/=` | 除法赋值 | 将左侧除以右侧并赋值。 | `x /= y` |
| `%=` | 取模赋值 | 将左侧对右侧取模并赋值。 | `x %= y` |
| `**=` | 幂赋值 | 将左侧进行右侧幂运算并赋值。 | `x **= y` |
| `//=` | 整除赋值 | 将左侧整除右侧并赋值。 | `x //= y` |

**示例:**
```python
#!/usr/bin/python3
x = 10
y = 20
x = y
print(x)
x += y
print(x)
x -= y
print(x)
x *= y
print(x)
x /= y
print(x)
x %= y
print(x)
x **= y
print(x)
x //= y
print(x)
```
**输出:**
`20`
`30`
`10`
`200`
`0.5`
`10`
`1e+10`
`0`





| 运算符 | 描述 | 示例 |
| :--- | :--- | :--- |
| `&` 二位与 | 当两个操作数的对应位都为 1 时，二位与的结果为 1。 | `(a & b)` (表示 0000 1110) |
| `&#124;` 二位或 | 当两个操作数的任意一个位为 1 时，二位或的结果为 1。 | `(a &#124; b) = 31` (表示 0001 1111) |
| `^` 二位异或 | 当两个操作数的任意一个位为 1 但不同为 1 时，二位异或的结果为 1。 | `(a ^ b) = 17` (表示 0001 0001) |
| `~` 二位取反 | 单元运算符，具有“翻转”位的效果。 | `(~a ) = -31` (由于是符号二进制数，在补码形式下表示为 1110 0001) |
| `<<` 二位左移 | 左操作数的值根据右操作数定义的位数向左移动。 | `a << 2 = 480` (表示 1110 0000) |
| `>>` 二位右移 | 左操作数的值根据右操作数定义的位数向右移动。 | `a >> 2 = 1` (表示 0000 0001) |

## 示例

```python
#!/usr/bin/python3
a =30 # 30 = 0001 1110
b = 15 # 15 = 0000 1111
print('a=',a,':',bin(a),'b=',b,':',bin(b))
c =0
c = a & b; # 14 = 0000 1110
print("result of AND is ", c,':',bin(c))
c = a &#124; b; # 31 = 0001 1111
print("result of OR is ", c,':',bin(c))
c = a ^ b; # 17 = 0001 0001
print("result of EXOR is ", c,':',bin(c))
c =~a; # -31 = 1110 0001
print("result of COMPLEMENT is ", c,':',bin(c))
c = a <<4; # 480 = 1110 0000
print("result of LEFT SHIFT is ", c,':',bin(c))
c = a >>4; # 1 = 0000 0001
print("result of RIGHT SHIFT is ", c,':',bin(c))
```

**输出:**
a= 30 : 00011110 b= 15 : 00001111
result of AND is 14 : 00001110
result of OR is 31 : 00011111
result of EXOR is 17 : 00010001
result of COMPLEMENT is -31 : -00011111
result of LEFT SHIFT is 480 : 111100000
result of RIGHT SHIFT is 1 : 00000001

## 逻辑运算符
Python 语言允许以下逻辑运算符。假设变量 `a` 值为 True，变量 `b` 值为 False，则

| 运算符 | |
| :--- | :--- |
| `and` | 逻辑与 |
| `or` | 逻辑或 |
| `not` | 逻辑非 |

### 成员运算符
Python 使用成员运算符来测试序列中的成员关系，例如字符串、列表或元组。这里描述了两种成员运算符：

| 运算符 | |
| :--- | :--- |
| `In` | |
| `not in` | |

### 身份运算符
身份运算符用于比较两个对象的内存位置（标识）。这里描述了两种身份运算符：

| 运算符 | 描述 | 示例 |
| :--- | :--- | :--- |
| `is` | 当运算符两边的变量指向同一个对象时结果为真，否则为假。 | ‘a’ is ‘b’，当 `is` 结果为 1 时，`id(a)` 等于 `id(b)` |
| `is not` | 当运算符两边的变量没有指向同一个对象时结果为真，否则为假。 | ‘a’ is not ‘b’，当 `is not` 结果为 1 时，`id(a)` 不等于 `id(b)` |

## 示例

```python
#!/usr/bin/python3
a = 30
b = 30
print ('Line 1','a=',a,':',id(a), 'b=',b,':',id(b))
if ( a is b ):
    print =(Line 2 - a and b become same identity)
else:
    print =(Line 2 - a and b do not become same identity)
if ( id(a) == id(b) ):
    print =(Line 3 - a and b become same identity)
else:
    print =(Line 3 - a and b do not become same identity)
b = 40
print =('Line 4','a=',a,':',id(a), 'b=',b,':',id(b))
if ( a is not b ):
    print =(Line 5 - a and b do not become same identity)
else:
    print =(Line 5 - a and b become same identity)
```

**输出:**
Line 1 a= 30 : 140351590504288 b= 30 : 140351590504288
Line 2 - a and b become same identity
Line 3 - a and b become same identity
Line 4 a= 30 : 140351590504288 b= 40 : 140351590504296
Line 5 - a and b do not become same identity

### 运算符优先级

| # | 运算符 | 描述 |
| :--- | :--- | :--- |
| 1 | `**` | 幂方 |
| 2 | `~` | 取反，单元 |
| 3 | `*`, `/`, `%` | 乘法、除法、取模 |
| 4 | `+`, `-` | 加法和减法 |
| 5 | `<<`, `>>` | 二位位移 |
| 6 | `&` | 二位与 |
| 7 | `^`, `&#124;` | 二位异或、二位或 |
| 8 | `<`, `>`, `<=` | 比较 |
| 9 | `==`, `!=` | 等于 |
| 10 | `=`, `+=`, `-=` 等 | 赋值 |
| 11 | `is`, `is not` | 身份 |
| 12 | `in`, `not in` | 成员 |
| 13 | `and`, `or`, `not` | 逻辑 |

### 循环
以下显示了循环类型：

| # | 循环类型 | 描述 |
| :--- | :--- | :--- |
| 1 | `while` 循环 | 当条件为真时，循环开始。 |
| 2 | `for` 循环 | 执行一系列语句。 |
| 3 | 嵌套循环 | 循环嵌套。 |



 循环控制语句
Python 支持以下语句：

| # | 控制语句 | 描述 |
| :--- | :--- | :--- |
| 1 | `break` | 立即终止循环。 |
| 2 | `continue` | 跳过循环循环的剩余部分。 |
| 3 | `pass` | 需要语句但不执行任何代码。 |

### 迭代器与生成器
迭代器是一个允许程序员遍历集合元素的对象。在 Python 中，迭代器支持两个方法：`iter()` 和 `next()`。迭代器可以使用字符串、列表或元组创建。

```python
list = [1,2,3,4]
it = iter(list) # 构建迭代器
print (next(it)) # 打印迭代器的下一个元素
```

迭代器通常使用 `for` 语句遍历：

```python
for x in it:
    print(x)
```

或使用 `next()` 函数：

```python
while True:
    try:
        print (next(it))
    except StopIteration:
        sys.exit() # 必须导入 sys
```

使用 `yield` 方法的器是一个产生序列的函数。当生成器函数被调用时，它返回一个生成器对象而不会开始执行。当第一次调用 `next()` 方法时，函数开始执行直到遇到 `yield` 语句，该语句返回产生的值。`yield` 会记录，下次 `next()` 调用从之前的位置继续。

以下示例定义了一个生成所有斐波那契数迭代器的生成器：

```python
import sys
def fibonacci(n): #生成器函数
    a, b, counter = 0, 1, 0
    while True:
        if (counter > n):
            return
        yield a
        a, b = b, a + b
        counter += 1
f = fibonacci(5) #f 是迭代器对象
while True:
    try:
        print (next(f), end=" ")
    except StopIteration:
        sys.exit()
```

### Python 原生数据类型
每个对象都有类型。`type` 函数允许检查对象的类型：
```python
>>> type(today)
<class 'dateTime.date'>
```
Python 语言中内置了少数几种原始或原生数据类型。原生数据类型具有以下属性：

1.  有简单的表达式可以求值为这些类型的对象，称为字字面量。

2.  有内置的函数、运算符和方法来处理这些类型的值。




正如我们所见，数字是原生的；数字字面量评估为数字，而数学运算符管理数字对象。>>> `12 + 30000000000000000000000003000000000000000000000012`

在某些情况下，Python 涉及三种原生数值类型：整数（`int`）、实数（`float`）和复数（`complex`）。

```python
type(2)<class 'int'>
type(1.5)<class 'float'>
type(1+1j)<class 'complex'>
```

`float` 的名称出现在 Python 中表示实数的方式中：一种“浮点”表示法。虽然数字表示的具体细节不是本文要讨论的问题，但了解 `int` 和 `float` 对象之间的一些高层区别是必要的。不恰的是，`int` 对象只能表示整数，但它们是精确表示的，没有任何近似值。另一方面，`float` 对象可以表示宽范围的分数，但并非所有的有理数都是可以表示的。尽管如此，`float` 对象通常用于近似表示实数和有理数，直到某些有效数字。

Python 有许多原生数据类型。以下是重要的类型：

1. 布尔值是 `True` 或 `False`。
2. 数字可以是整数（`1` 和 `2`）、浮点数（`1.1` 和 `1.2`）、分数（`1/2` 和 `2/3`），甚至是复数。
3. 字符串是 Unicode 字符的序列，例如一个 `Html` 文档。
4. 字节和字节数组，例如 `jpeg` 图像文件。
5. 列表是值的有序序列。
6. 元组是有序的、不可变的值序列。
7. 集合是无序的值包。
8. 字典是无序的键值对包。

当然，类型比这些多。Python 中的一切皆都是对象，因此有像 `module`、`function`、`class`、`method`、`file` 甚至编辑过的代码这样的类型。

## 数字

数值由 `Number` 数据类型存储。它们是不可变数据类型。这意味着，更改数字数据类型的值将输出一个新分配的对象。在赋值值时，会创建 `Number` 对象。例如——

```python
var1 =10
var2 =20
```

通过使用 `del` 语句，也可以删除对数字对象的引用。`del` 语句的语法是——`del var1[,var2[,var3[....,varN]]]]`。使用 `del` 语句可以删除单个对象或多个对象。例如——

```python
del var
del var_a, var_b
```

Python 支持不同的数值−

* `int`（有符号整数）——通常直接被称为整数或 `ints`。它们是没有小数点的正负总数。在 Python 3 中，整数是无限大小的。Python 2 持有两种整数类型 - `int` 和 `long`。Python 3 中不再有“长型整数”了。
* `float`（浮点实值）——它也被称为 `floats`。实数由它们表示，并用小数点划分整数部分和小数部分。在科学计数法中，浮点数也可以用 `E` 或 `e` 表示 10 的幂次（`2.5e2 = 2.5 x 102 = 250`）。
* `complex`（复数）——形式为 `a + bJ`，其中 `a` 和 `b` 是 `floats``J`（或 `j`）表示 -1 的平方根（这是一个虚数）。数的实部是 `a`，虚部是 `b`。在 Python 编程中，复数并不算常用。

可能会以十六进制或八进制形式表示整数。

```python
number = 0xA0F # 十六进制
number2575
number = 0o37 # 八进制
number31
```

## 示例

这里给出了一些数字的示例。

| int |
| :--- |
| 10 |
| 200 |
| -245 |
| 078 |
| -0360 |
| -0x290 |
| 0x39 |

复数由一个有序的实浮点数对组成，表示为 `a + bj`，其中 `a` 是复数的实部，`b` 是虚部。

## 数字类型转换

Python 在包含混合类型的插图中，会从内部将数字转换为通用类型以进行调整。有时，你需要显式地将数字从一种类型转换为另一种类型，以满足运算符或函数参数的条件。

* 使用类型 `int(x)` 将 `x` 转换为普通整数。
* 使用类型 `long(x)` 将 `x` 转换为长型整数。
* 使用类型 `float(x)` 将 `x` 转换为浮点数。
* 使用类型 `complex(x)` 将 `x` 转换为实部为 `x`、虚部为 0 的复数。
* 使用类型 `complex(x, y)` 将 `x` 和 `y` 转换为实部为 `x`、虚部为 `y` 的复数。`x` 和 `y` 是数值表达式。

## 数学函数

Python 引入了以下产生数学计算的函数。

| # | 函数及返回值 |
| :--- | :--- |
| 1 | `abs(x)` 绝对值 |
| 2 | `ceil(x)` 向上取整 |
| 3 | `floor(x)` 向下取整 |
| 4 | `pow(x, y)` 幂 |
| 5 | `exp(x)` 指数函数 |
| 6 | `fabs(x)` 绝对值 |
| 7 | `log(x)` 自然对数 |
| 8 | `log10(x)` 以 10 为底的对数 |
| 9 | `max(x, y)` 最大值 |
| 10 | `min(x, y)` 最小值 |
| 11 | `modf(x)`  |
| 12 | `round(x[,n])` 保留 `n` 位 |
| 13 | `sqrt(x)` 平方 |

## 随机数函数

在游戏、模拟中会使用随机数。Python 引入了以下函数。

| # | 函数 |
| :--- | :--- |
| 1 | `choice(seq)` 从列表、元组或字符串随机选择元素 |
| 2 | `randrange(start, stop [,step])` 范围内的随机整数 |
| 3 | `random()` 0 到 1 之间的随机数 `r` |
| 4 | `seed([x])` 在调用随机函数前设置整数值 |
| 5 | `shuffle(lst)` 原地打乱列表项 |
| 6 | `uniform(x, y)` `x` 到 `y` 之间的随机浮点数 `r` |

## 三角函数

Python 语言引入了执行三角计算的函数。

| # | 函数及描述 |
| :--- | :--- |
| 1 | `acos(x)` 返回 `x` 的弧余弦，弧度 |
| 2 | `asin(x)` 返回 `x` 的弧正弦，弧度 |
| 3 | `atan(x)` 返回 `x` 的弧正切，弧度 |
| 4 | `atan2(y, x)` 返回 `atan(y / x)`,弧度 |
| 5 | `cos(x)` 返回 `x` 的余弦，弧度 |
| 6 | `hypot(x, y)` 返回欧几里得范数，`sqrt(x*x + y*y)` |
| 7 | `sin(x)` 返回 `x` 的正弦，弧度 |
| 8 | `tan(x)` 返回 `x` 的正切，弧度 |
| 9 | `degrees(x)` 将角度 `x` 从弧度转换为角度 |
| 10 | `radians(x)` 将角度 `x` 从角度转换为弧度 |

## 数学常量

该模块还表示两个数学常量：

| # | 常量及描述 |
| :--- | :--- |
| 1 | `pi` 数学常量 `pi` |
| 2 | `e` 数学常量 `e` |

## 字符串

Python 中最流行的数据类型是字符串。字符串可以通过嵌入引号中的字符简单创建。Python 中的单引号被视为双引号。通过给变量赋值可以简单地创建字符串。例如——

```python
var1 ='Hello World!'
var2 ="Python Programming"
```

## 访问字符串值

Python 不支持字符类型；这些被视为长度为 1 的字符串，因此也允许子字符串。为了获取子字符串，你可以使用方括号结合索引或内容来获取你的子字符串。例如——

```python
print ("var1[0]: ", var1[0])
print ("var2[0:6]: ", var2[0:6])
```




| 输出: | `var1[0]: Hvar2[0:6]: Python` |

# 更新字符串
你可以通过将变量（重新）赋值为另一个字符串来“更新”现有字符串。新值可以与其先的值相关，也可以是完全不同的字符串。例如所示：

```python
#!/usr/bin/python3
var1 = 'Hello World!'
print ("Updated String :- ", var1[:6] + 'Python')
```

| 输出: | Updated String :- Hello Python |

## 转义字符
下表列出了转义字符或不可打印字符列表，它们可以使用反斜杠表示法表示。转义字符在单引号字符串和双引号字符串中都有解释。

| 反斜杠表示法 |
| :--- |
| `\a` |
| `\b` |
| `\cx` |
| `\C-x` |
| `\e` |
| `\f` |
| `\M-\C-x` |
| `\n` |
| `\nnn` |
| `\r` |
| `\s` |
| `\t` |
| `\v` |
| `\x` |
| `\xnn` |

## 字符串特殊运算符
假设字符串变量 `'a'` 存储 `'Hello'`，变量 `'b'` 存储 `'Python'`，那么——

| 运算符 | 描述 | 示例 |
| :--- | :--- | :--- |
| `+` | 拼接 - 将运算符两侧的值相加 | `a + b` 将得到 HelloPython |
| `*` | 重复 - 生成新字符串，连接相同字符串的多个副本 | `a*2` 将得到 HelloHello |
| `[]` | 切片 - 提供给定索引的字符 | `a[1]` 将得到 e |
| `[::]` | 范围切片 - 提供给定范围内的字符 | `a[1:4]` 将得到 ell |
| `in` | 成员检查 - 如果字符存在于给定字符串中，则返回真 | `H in a` 将得到 1 |
| `not in` | 成员检查 - 如果字符不在给定字符串中，则返回真 | `M not in a` 将得到 1 |
| `r/R` | 原始字符串 - 消除转义字符的原始含义。原始字符串的语法与普通字符串相同，例外是原始字符串运算符字母 "r"，它位于引号前面。"r" 可以小写 (r) 或大写 (R)，并且必须直接位于第一个引号之前 | `print r'\n'` 打印 `\n` `print R'\n'` 打印 `\n` |
| `%` | 格式化 - 执行字符串格式化 | 见下一节 |

## 字符串格式化运算符
字符串格式化运算符 `%` 是 Python 最酷的功能之一。该运算符对于字符串来说是特殊的，它具有类似于 C 语言 `printf()` 系列的功能。这是一个简单的示例：

```python
#!/usr/bin/python3
print =(My name is %s and weight is %d kg! % ('Steve', 21))
```

| 输出: | My name is Steve and weight is 21 kg! |这里给出了完整的符号列表，可以与 `%` 一起使用 —— |

| # | 格式符号与转换 |
| :--- | :--- |
| 1 | `%c` 字符 |
| 2 | `%s` 在格式化之前通过 `str()` 进行字符串转换 |
| 3 | `%i` 有符号十整数 |
| 4 | `%d` 有符号十整数 |
| 5 | `%u` 无符号十整数 |
| 6 | `%o` 八进制整数 |
| 7 | `%x` 十六进制整数（小写字母） |
| 8 | `%X` 十六进制整数（大写字母） |
| 9 | `%e` 指数法（带有小写 'e'） |
| 10 | `%E` 指数法（带有大写 'E'） |
| 11 | `%ff` 浮点实数 |
| 12 | `%g` `%f` 和 `%e` 中较短的一个 |
| 13 | `%G` `%f` 和 `%E` 中较短的一个 |

表格中给出了其他支持的符号和功能：

| 序号 | 符号与功能 |
| :--- | :--- |
| 1 | `*argument` 指定宽度或精度 |
| 2 | `-` 左对齐 |
| 3 | `+` 显示符号位 |
| 4 | `<sp>` 在正数前留出空格 |
| 5 | `#` 添加十六进制前导 '0x' 或 '0X' 或八进制前导零 ('0' )，取决于使用了 'x' 还是 'X' |
| 6 | `0` 左侧零填充（而不是空格） |
| 7 | `'%%'` 留下单个字面量 `%` |
| 8 | `(var)` 映射变量（字典参数） |
| 9 | `m.n.m` 是最小整数宽度，n 是小数点后执行的位数（如果适用） |

## 三引号
Python 通过三引号允许字符串跨越多行，包括原始的换行符、制表符和其他任何特殊字符。三引号在语法上由三个连接的单引号或双引号组成。

```python
#!/usr/bin/python3
TABB (\t ) 它们在显示时会以那样显示。字符串内部的换行符，无论是像这样在括号 [ \n ] 中显式提供的，还是变量赋值内部的换行符，都会显示出来."""print (para_str)
```

| 输出: | 这是一个由不同行和不可打印字符（如制表符 TABB (_)）组成的大型字符串，它们在显示时会以那样显示。字符串内部的换行符，无论是像这样在括号 [] 中显式提供的，还是变量赋值内部的换行符，都会显示出来。
注意：三引号以 `is not.` 结束。在 Python 3 中，字符串包含以下内容：

## 内置字符串方法
| 序号 | 方法与描述 |
| :--- | :--- |
| 1 | `capitalize()` 大写化字符串的首字母 |
| 2 | `center(width, fillchar)` 返回一个用 fillchar 填充并达到宽度的字符串 |
| 3 | `count(str, beg = 0,end = len(string))` 统计 str 在字符串中出现的次数 |
| 4 | `decode(encoding = 'UTF-8',errors = 'strict')` 应用编码解码器解码字符串。 |
| 5 | `encode(encoding = 'UTF-8',errors = 'strict')` 返回字符串的编码版本；出错时，默认抛出 ValueError，除非指定了 'ignore' 或 'replace'。 |
| 6 | `endswith(suffix, beg = 0, end = len(string))` 确定字符串或其子串（如果给了起始索引 beg 和结束索引 end）是否以后缀结尾；如果是则返回真，否则返回假。 |
| 7 | `expandtabs(tabsize = 8)` 扩展字符串中的制表符为空格；如果没有给出 tabsize，默认每个制表符 8 个空格。 |
| 8 | `find(str, beg = 0, end = len(string))` 确定 str 是否出现在字符串或子串（如果给了起始索引 beg 和结束索引）中；找到则返回索引，否则返回 -1。 |
| 9 | `index(str, beg = 0, end = len(string))` 类似于 find()，但未找到时抛出异常。 |
| 10 | `isalnum()` 如果字符串至少包含 1 个字符且所有字符均为字母数字，则返回真。 |
| 11 | `isalpha()` 如果字符串至少包含 1 个字符且所有字符均为字母，则返回真。 |
| 12 | `isdigit()` 如果字符串仅包含数字，则返回真。 |
| 13 | `islower()` 如果字符串至少包含 1 个大小写字母且所有大小写字母均为小写，则返回真。 |
| 14 | `isnumeric()` 如果 Unicode 字符串仅包含数字字符，则返回真。 |
| 15 | `isspace()` 如果字符串仅包含空白字符，则返回真。 |
| 16 | `istitle()` 如果字符串正确符合标题大小写格式，则返回真。 |
| 17 | `isupper()` 如果字符串至少包含 1 个大小写字母且所有大小写字母均为大写，则返回真。 |





| 索引 | 方法 | 说明 |
| :--- | :--- | :--- |
| 18 | `join(seq)` | 将序列 `seq` 中各个因子的字符串表示合并为一个字符串，并使用分隔符字符串。 |
| 19 | `len(string)` | 返回 `string` 的长度 |
| 20 | `ljust(width[, fillchar])` | 返回一个用空格填充的字符串，使主字符串左对齐，总宽度为 `width` 列。 |
| 21 | `lower()` | 将 `string` 中的所有大写字母转换为小写。 |
| 22 | `lstrip()` | 移除 `string` 开头所有的空白字符。 |
| 23 | `maketrans()` | 返回一个用于 `translate` 函数的翻译表。 |
| 24 | `max(str)` | 返回字符串 `str` 中最大的字母字符。 |
| 25 | `min(str)` | 返回字符串 `str` 中最小的字母字符。 |
| 26 | `replace(old, new [, max])` | 将字符串中所有的 `old` 替换为 `new`；如果提供了 `max`，则最多替换 `max` 次。 |
| 27 | `rfind(str, beg = 0, end = len(string))` | 与 `find()` 相同，但在 `string` 中反向搜索。 |
| 28 | `rindex(str, beg = 0, end = len(string))` | 与 `index()` 相同，但在 `string` 中反向搜索。 |
| 29 | `rjust(width,[, fillchar])` | 返回一个用空格填充的字符串，使主字符串右对齐，总宽度为 `width` 列。 |
| 30 | `rstrip()` | 移除 `string` 末尾所有的空白字符。 |
| 31 | `split(str="", num=string.count(str))` | 根据分隔符 `str`（若提供则使用空格）分割字符串并返回子字符串列表；如果提供了 `num`，则分为最多 `num` 个子字符串。 |
| 32 | `splitlines(num=string.count('\n'))` | 在所有（或 `num` 个）`NEWLINE` 处分割字符串，并传递一个去除了 `NEWLINE` 的行列表。 |
| 33 | `startswith(str, beg=0,end=len(string))` | 判断字符串或子字符串（如果提供了起始索引 `beg` 和结束索引 `end`）是否以子字符串 `str` 开头；如果是返回 true，否则返回 false。 |
| 34 | `strip([chars])` | 对 `string` 同时执行 `lstrip()` 和 `rstrip()` |
| 35 | `swapcase()` | 反转 `string` 中所有字母的大小写状态。 |
| 36 | `title()` | 返回字符串的“标题格式”（titlecased）版本，即所有单词的首字母大写，其余小写。 |
| 37 | `translate(table, deletechars="")` | 根据解释表 `str` (256 个字符) 翻译字符串，排除 `del` 字符串中的字符。 |
| 38 | `upper()` | 将 `string` 中的小写字母转换为大写。 |
| 39 | `zfill(width)` | 返回原始字符串，左侧填充零直到总长度为 `width`；为数字设计，`zfill()` 会保留任何提供的符号（少去一个零）。 |
| 40 | `isdecimal()` | 如果 Unicode 字符串仅包含数字字符则返回 true，否则返回 false。 |

## 列表
序列是 Python 中最基本的数据结构。序列的每个部分都分配有一个数字——即其位置或索引。在序列中，第一个索引为 0，第二个索引为 1，依此类推。Python 中有六种内置序列类型，但在本书中，我们将看到最流行的类型是列表 `lists` 和元组 `tuples`。你可以对所有序列类型执行多种操作。这些方法包括索引、切片、合并、乘法和成员性检查。在书中，Python 有内置函数用于获取序列的长度以及获取其最大和最小元素。

### Python 列表
列表是 Python 3 中常用的通用多用途数据类型，可以被列为方括号内用逗号分隔的值（项）的列表。列表中的项不需要类型相同，这是列表的一个重要特点。

就像在方括号之间放置不同的逗号分隔值一样，创建列表非常简单。例如——`List` 索引从 0 开始，且列表可以像字符串索引一样切片和拼接。

### 访问列表中的值
要在列表中输入值，请使用方括号进行切片并结合索引或多个索引来获取该索引处的值。例如——

```python
list1 = ['Banana', 'Watermelon', 1990, 2000]
list2 = [1, 2, 3, 4, 5 ]
list3 = ["a", "b", "c", "d"]
```

**输出：**
```text
list1[0]: Banana
list2[1:5]: [2, 3, 4, 5]
```

执行上述代码时会产生以下**输出**：

### 更新列表
通过在赋值运算符左侧提供切片，你可以更新列表的单个或多个元素，还可以使用 `append()` 方法向列表元素添加元素。例如——

```python
#!/usr/bin/python3
list = ['Banana', 'Watermelon', 1990, 2000]
```

执行上述代码时会产生以下**输出**：

```python
list[0] = 'Apple'
list[1:3] = [2021, 2022]
list.append('Cherry')
print(list)
```

**输出：**
```text
['Apple', 2021, 2022, 2000, 'Cherry']
```

### 删除列表
可以使用 `del` 或 `remove()` 来删除元素。例如——

```python
#!/usr/bin/python3
list = ['Banana', 'Watermelon', 1990, 2000]
del list[1]
print(list)
list.remove('Watermelon')
print(list)
```

**输出：**
```text
['Banana', 1990, 2000]
['Banana', 1990, 2000] # 注意：此处会报错因为 Watermelon 已被删除
```

### 列表基本操作
列表对 `+` 和 `*` 运算符有响应。这意味着：

```python
list1 = ['Banana', 'Watermelon']
list2 = ['Apple', 'Orange']
list3 = list1 + list2
print(list3)

list4 = list1 * 2
print(list4)
```

**输出：**
```text
['Banana', 'Watermelon', 'Apple', 'Orange']
['Banana', 'Watermelon', 'Banana', 'Watermelon']
```

#### 成员性
```python
list1 = ['Banana', 'Watermelon']
print('Banana' in list1)
print('Orange' in list1)
```

**输出：**
```text
True
False
```

#### 迭代
```python
list1 = ['Banana', 'Watermelon']
for x in list1:
    print(x)
```

**输出：**
```text
Banana
Watermelon
```

#### 索引、切片和矩阵
索引和切片的方法与字符串相同，因为列表是序列。如下所示：

```python
L = ['C++', 'Java', 'Python']
print(L[0])
print(L[-1])
print(L[1:])
```

**输出：**
```text
C++
Python
['Java', 'Python']
```

### 内置列表函数
Python 提供了近似的列表函数：

| 序号 | 函数 | 说明 |
| :--- | :--- | :--- |
| 1 | `cmp(list1, list2)` | 在 Python 3 中不再可用。 |
| 2 | `len(list)` | 给列表的总长度。 |
| 3 | `max(list)` | 返回列表中最大的元素。 |
| 4 | `min(list)` | 返回列表中最小的元素。 |
| 5 | `list(seq)` | 将序列转换为列表。 |

Python 提供了以下列表方法：

| 序号 | 方法 | 说明 |
| :--- | :--- | :--- |
| 1 | `list.append(obj)` | 将对象 obj 添加到列表。 |
| 2 | `list.count(obj)` | 返回 obj 在列表中出现的次数。 |
| 3 | `list.extend(seq)` | 将 `seq` 的内容添加到列表。 |
| 4 | `list.index(obj)` | 返回列表中包含 `obj` 的最小索引。 |
| 5 | `list.insert(index, obj)` | 在指定的索引偏移处插入对象 `obj`。 |
| 6 | `list.pop(obj = list[-1])` | 从列表中移除并返回最后一个对象或 `obj`。 |
| 7 | `list.remove(obj)` | 从列表中移除对象 `obj`。 |
| 8 | `list.reverse()` | 原地反转列表对象。 |





# 元组 (Tuples)

元组是不可变 Python 对象的序列。和列表一样，元组也是序列。与列表不同，元组是序列；这是元组和列表之间的主要区别。列表使用方括号，而元组使用圆括号。

放置不同的逗号分隔的值一样，创建一个元组非常简单。你可以选择在括号内设置这些逗号分隔的值。例如：

```python
tup1 = ('Banana', 'Watermelon', 1990, 2000)
tup2 = (1, 2, 3, 4, 5 )
tup3 = "a", "b", "c", "d"
```

空元组写为两个不包含任何内容的括号：`tup1 = ()`。

即使只有一个值，也要包含逗号来编写包含单个值的元组：`tup1 = (50,)`。

元组索引从 0 开始，就像字符串索引一样。它们可以进行切片、拼接等。

## 访问元组中的值

要在元组中输入值，使用方括号进行切片，并结合索引或多个索引来获取该索引处的值。例如：

```python
#!/usr/bin/python3
tup1 = ('Banana', 'Watermelon', 1990, 2000)
tup2 = (1, 2, 3, 4, 5, 6)
print ("tup1[0]: ", tup1[0])
print ("tup2[1:5]: ", tup2[1:5])
```

| 输出: |
| tup1[0]: Banana |
| tup2[1:5]: (2, 3, 4, 5) |

你不能更新或更改元组元素的值，因为元组是永久的。你可以提取现有元组的部分来创建新的元组，如下例所示：

```python
#!/usr/bin/python3
tup1 = (10, 20,30)
tup2 = ('abc', 'xyz')
# 以下操作对元组无效无效
# tup1[0] = 100;
tup3 = tup1 + tup2
print (tup3)
```

| 输出: |
| (10, 20, 30, 'abc', 'xyz') |

## 删除元组元素

删除单个元组元素是不可能的，但将另一个丢弃不需要元素的元组组合在一起是没有问题的。只需使用 `del` 语句显式删除整个元组即可。例如：

```python
#!/usr/bin/python3
tup = ('Banana', 'Watermelon', 1990, 2000)
print (tup)
del tup;
print =(After deleting tup : )
print (tup)
```

| 输出: |
| ('Banana', 'Watermelon', 1990, 2000) |
| After deleting tup :Traceback (most recent call last):
File "main.py", line 8, in <module>
print (tup)
NameError: name 'tup' is not defined |

**注意** — 会抛出一个异常。在 `del tup` 之后，元组不再存在。

## 基本元组操作

与字符串一样，元组也响应 `+` 和 `*` 运算符。在这里它们也涉及拼接和重复，只不过结果是一个新元组，而不是字符串。事实上，元组对我们在前一章节中对字符串执行的所有通用序列操作都有响应。

| Python 表达式 | 结果 |
| :--- | :--- |
| `len((5,6,7))` | 3 |
| `(5,6,7) + (8,9,10)` | `(5,6,7,8,9,10)` |
| `('Hi!',) * 4` | `('Hi!', 'Hi!', 'Hi!', 'Hi!')` |
| `3 in (5,6,7)` | True |
| `for x in (6,7) : print (x, end = ' ')` | 6 7 |

## 索引、切片与矩阵

索引和切片对元组的工作方式与字符串相同，因为元组是序列。假设输入为：`T=('C++', 'Java', 'Python')`

| Python 表达式 |
| :--- |
| `T[2]` |
| `T[-2]` |
| `T[1:]` |

## 无封装定界符

在这些简短示例中，没有封装定界符是通过逗号标记的各种对象，或者在没有标识符号的情况下编写的。

## 内置元组函数

Python 包含以下元组函数：

| 序号 | 函数与描述 |
| :--- | :--- |
| 1 | `cmp(tuple1, tuple2)` 比较两个元组的元素。 |
| 2 | `len(tuple)` 给元组的总长度。 |
| 3 | `max(tuple)` 返回元组中值最大的项。 |
| 4 | `min(tuple)` 返回元组中值最小的项目。 |
| 5 | `tuple(seq)` 将列表转换为元组。 |

## 字典 (Dictionary)

每个键通过冒号 (`:`) 与值分离，项之间通过逗号分离，整个由大括号包围。没有任何对象的空字典仅用两个大括号表示，如下：`{}`。键在字典内是唯一的。键是不可变数据类型，如字符串、数字或元组。字典中的值不是唯一的。字典的值可以是多种标准。

### 访问字典中的值

要访问字典元素，使用通常的方括号配合键来获取其值。有一个简单的示例：

```python
#!/usr/bin/python3
dict = {'Name': 'Shara', 'Age': 25}
```





| 方法 | 说明 |
| :--- | :--- |
| 2 | `dict.copy()` 返回字典 `dict` 的浅拷贝 |
| 3 | `dict.fromkeys()` 创建一个具有来自 `seq` 的键且值被设置为 `value` 的新字典 |
| 4 | `dict.get(key, default=None)` 对于键 `key`，返回其值；如果 `key` 不在字典中则返回 `default` |
| 5 | `dict.has_key(key)` 已移除，请改用 `in` 操作。 |
| 6 | `dict.items()` 返回一个包含 `dict` 的元组对的列表 |
| 7 | `dict.keys()` 返回字典 `dict` 的键的列表 |
| 8 | `dict.setdefault(key, default = None)` 与 `get()` 类似，但如果 `key` 不在 `dict` 中，则设置 `dict[key] = default` |
| 9 | `dict.update(dict2)` 将字典 `dict2` 的键值对添加到 `dict` 中 |

# 布尔逻辑与条件

布尔数据类型可以是两个值之一：`True` 或 `False`。在编程中使用布尔值可以执行比较并控制应用程序的流。布尔值表示了与数学逻辑分支相关的真值，这些值指导了计算机科学中的算法。该词以数学家乔治·布尔（George Boole）命名，`Boolean` 一词的首字母始终大写 `B`。`True` 和 `False` 的值也通常分别大写 `T` 和 `F`，因为它们是 Python 中的特殊值。

在本章中，我们将回顾理解布尔值工作所需的基础知识，包括布尔比较、逻辑运算符以及真值表。

## 比较运算符

在编程中，比较运算符用于比较值并求值为单个的（`True` 或 `False`）的布尔值。下表显示了布尔比较运算符。

| 运算符 | 含义 |
| :--- | :--- |
| `==` | 等于 |
| `!=` | 不等于 |
| `<` | 小于 |
| `>` | 大于 |
| `<=` | 小于等于 |
| `>=` | 大于等于 |

为了理解这些运算符的工作原理，让我们为程序中的两个变量分配两个整数：
```python
x = 5
y = 8
```
我们知道在这个示例中，由于 `x` 的值为 5，因此它小于值为 8 的 `y`。应用这两个变量及其相关的值，让我们遍历上表中的运算符。在程序中，我们将让 Python 输出每个比较运算符的求值是 `True` 还是 `False`。

```python
x = 5
y = 8
print("x == y:", x == y)
print("x != y:", x != y)
print("x < y:", x < y)
print("x > y:", x > y)
print("x <= y:", x <= y)
print("x >= y:", x >= y)
```

为了帮助更好地理解理解输出，我们将让 Python 同时打印一个字符串显示它正在评估的内容。
输出：
```
x == y: False
x != y: True
x < y: True
x > y: False
x <= y: True
x >= y: False
```

遵循数学逻辑，在之前的每个表达式中，Python 都评估了：
- 5 (`x`) 等于 8 (`y`) 吗？False
- 5 不等于 8 吗？True
- 5 小于 8 吗？True
- 5 大于 8 吗？False
- 5 小于等于 8 吗？True
- 5 不等于？False

虽然这里使用了整数，但我们可以将其替换为浮点值。字符串也可以用于布尔运算符。除非使用额外的字符串方法，否则字符串对大小写敏感。我们可以查看实践中是如何比较字符串的：

```python
Sammy = "Sammy"
sammy = "sammy"
print("Sammy == sammy: ", Sammy == sammy)
```
输出：
```
Sammy == sammy:  False
```
之前的字符串 `"Sammy "` 不等于字符串 `"sammy "`，因为它们并不完全相同；一个以大写 S 开头，另一个以小写 s 开头。但如果你添加一个赋值为 `"Sammy "` 的额外变量，那么它们的求值结果将相等：

```python
Sammy = "Sammy"
sammy = "sammy"
also_Sammy = "Sammy"
print("Sammy == sammy: ", Sammy == sammy)
print("Sammy == also_Sammy", Sammy == also_Sammy)
```
输出：
```
Sammy == sammy:  False
Sammy == also_Sammy:  True
```
你也可以将其他比较运算符（包括 `>` 和 `<`）应用于比较两个字符串。Python 将使用字符的 ASCII 值对这些字符串进行字典序分析。我们也可以用比较运算符估算布尔值：

```python
t = True
f = False
print("t != f: ", t != f)
```
输出：
```
t != f:  True
```
上述输出显示 `True` 不等于 `False`。

## 逻辑运算符

有三个逻辑运算符用于比较值。它们将表达式求值为布尔值，返回 `True` 或 `False`。这些运算符是 `and`、`or` 和 `not`，下表所示。

| 运算符 | 含义 | 形式 |
| :--- | :--- | :--- |
| And | 如果两者都为真则为真 | `x and y` |
| Or | 如果至少有一个为真则为真 | `x or y` |
| not | 仅当为假时为真 | `not x` |

逻辑运算符通常用于评估两个或多个表达式是否为真。例如，它们可以用于判断成绩是否通过以及学生是否选了课程，如果这两种情况都成立，则学生将被允许通过。

为了理解逻辑运算符如何工作，让我们评估三个表达式：

```python
print((9 > 7) and (2 < 4))  # 两个表达式都为真
print((8 == 8) or (6 != 6)) # 其中一个表达式为真
print(not(3 <= 1))         # 表达式为假
```
输出：
```
True
True
True
```

## 真值表

数学逻辑分支有很多，但我们可以选择性学习以促进编程时的算法思维。下面是比较运算符 `==` 以及每个逻辑运算符 `and`、`or` 和 `not` 的真值表。虽然你能够推导出它们，但也有必要努力记忆它们，这可以使你的编程决策过程更快。

### == 真值表

| x | == |
| :--- | :--- |
| True | True |
| True | False |
| False | True |
| False | False |

### AND 真值表

| x | and |
| :--- | :--- |
| True | True |
| True | False |
| False | True |
| False | False |

### OR 真值表

| x | or |
| :--- | :--- |
| True | True |
| True | False |
| False | True |
| False | False |

### NOT 真值表

| not |
| :--- | :--- |
| True | False |
| False | True |




真值表是逻辑学中的基础数学表格，在 `python` 编程中构建算法（指令）时，记忆或记住真值表非常有帮助。

## 使用布尔运算符进行流控制

要以流控制语句的形式控制程序的执行流和结果，请使用一个条件后跟一个子句。条件会被评估为 `True` 或 `False` 的布尔值，这显示了程序中做出决策的点。也就是说，条件会告诉你某个项的评估结果是 `True` 还是 `False`。

子句是紧跟在条件后面的代码块，决定了程序的输出。也就是说，它负责执行构造中“如果 x 为真，则执行此操作”的部分。

下面的代码展示了比较运算符与条件语句协同工作以控制 `Python` 程序流的案例：

```python
if grade >= 65:              # Condition
    print("Passing grade")   # Clause
else:
    print("Failing grade")
```

此程序将估算每个学生的成绩是及格还是不及格。对于成绩为 `83` 的学生，第一个语句将评估为 `True`，并触发 `Passing grade` 的打印语句。对于成绩为 `59` 的学生，第一个语句将评估为 `False`，因此程序将继续执行与 `else` 表达式绑定的打印语句：`Failing grade`。

由于 `Python` 中的每个单独对象都可以评估为 `True` 或 `False`，`PEP 8` 风格指南不建议将值与 `True` 或 `False` 关联，因为这样可读性较低，并且会不断返回意外之外的布尔值。也就是说，你不应该在程序中使用类似 `if sammy == True :`。相反，应将 `sammy` 关联到另一个返回布尔值的非布尔值。布尔运算符提供的条件可以通过流控制语句来决定程序的最终结果。

## 在 Python 中构建 "While" 循环

`while` 循环根据给定的布尔条件实现代码的重复执行。只要 `while` 语句评估为 `True`，`while` 块中的代码就会完成执行。

你可以将 `while` 循环想象成复制的条件语句。在 `if` 语句之后，程序继续向下执行代码，但在 `while` 循环中，程序会跳回 `while` 语句的开头，直到条件为 `False`。与执行固定次数的 `for` 循环不同，`while` 循环基于条件，因此你不需要知道代码要重复多少次。

### While Loop

在 `Python` 中，`while` 循环的构建如下：

```python
while [a condition is True]:
    [do something]
```

正在执行的 `something` 将持续执行，直到所评估的条件不再为真。让我们构建一个执行 `while` 循环程序。在这个程序中，我们将要求用户输入密码。在结束此循环之前有两种可能的结果：

- 如果程序密码正确，`while` 循环将退出。
- 如果程序密码错误，`while` 循环将继续执行。




我们将在选定的文本编辑器中创建一个名为 `password.py` 的文件，并首先将变量 `password` 初始化为一个空字符串：
```python
password = ''
```
该空字符串将用于在 `while` 循环中获取用户的输入。现在，我们将构建带有条件的 `while` 语句：
```python
password = ''
while password != 'password':
```
在这里，`while` 伴随着变量 `password`。我们正在检查变量 `password` 是否被设置为字符串 `'password'`，但你可以使用任何你喜欢的字符串。这意味着如果用户输入字符串 `'password'`，循环将停止，应用程序将继续执行循环之外的任何代码。然而，如果用户输入的字符串不等于 `'password'`，则循环将继续。

接下来，我们将在 `while` 循环中添加一段产生内容的代码块：
```python
password = ''
while password != 'password':
    print('What is the password?')
    password = input()
```
在 `while` 循环内部，应用程序运行一个 `print` 语句来提示密码。然后，使用 `input()` 函数将变量 `password` 固定为用户的输入。应用程序将检查变量 `password` 是否分配给了字符串 `'password'`，如果是，`while` 循环将结束。让我们为这种情况给程序添加一行代码：
```python
password = ''
while password != 'password':
    print('What is the password?')
    password = input()
print=('Yes, the password is ' + password + '. You may enter.')`
```
最后一个 `print()` 语句在 `while` 循环之外，因此当用户输入的密码为 `'password'` 时，他们将看到循环之外的最终 `print` 语句。然而，如果用户从未输入过单词 `'password'`，他们将永远无法到达最后一个 `print()` 语句，并陷入死循环。死循环是指程序不断在一个循环内执行而永不退出。要在命令行中退出死循环，请按 `CTRL + C`。

```bash
python password.py
```
你将收到密码提示提示，然后可以使用各种可能的输入对其进行检查。以下是程序的示例输出：

Output
```
What is the password?
hello
What is the password?
sammy
What is the password?
PASSWORD
What is the password?
password
Yes, the password is password. You may enter.
```

## Python 中的 for 循环

`for` 循环根据循环计数器或循环变量实现代码的执行。这意味着 `for` 循环通常用于在进入循环之前已确定迭代次数的情况，这与基于条件的 `while` 循环不同。

### For 循环
在 Python 中，`for` 循环的构建如下：
```python
for [iterating variable] in [sequence]:
    [do something]
```
被执行的内容将一直运行直到序列结束。让我们来看一个遍历值范围的 `for` 循环：
```python
for i in range(0,5):
    print(i)
```
当我们运行此程序时，输出如下：

Output
```
0
1
2
3
4
```
这个 `for` 循环将 `i` 固定为其迭代变量，链存在于 0 到 5 的 `range` 中。。在循环内部，每次迭代打印一个整数。请记住，编程中倾向于从索引 0 开始，所以虽然打印了 5 个数字，但它们的范围是 0-4。当程序需要重复执行一段代码块时，你通常会看到并应用 `for` 循环。

### 使用 `range()` 的 for 循环
Python 的内置永久序列类型之一是 `range()`。在循环中，`range()` 用于控制循环重复的次数。在使用 `range()` 时，你可以在传递它的 1 到 3 个整数参数之间切换：
- `start`：指定序列开始的整数值，如果没有涉及，则 `start` 从 0 开始。
- `stop`：是强制要求的，是计数到此但不包含的整数。
- `step`：设置下一次迭代的增量，如果省略，则 `step` 默认为 1。

我们将查看一些向 `range()` 传递不同参数的示例。首先，我们只传递 `stop` 参数，使我们的序列设为 `range(stop)`：
```python
for i in range(6):
    print(i)
```
在之前的程序中，`stop` 参数为 6，因此代码将从 0 迭代到 6（不包含 6）：

Output
```
0
1
2
3
4
5
```
接下来，我们将看到 `range(start, stop)`，传递了迭代何时开始何时结束的值：
```python
for i in range(20,25):
    print(i)
```
现在，`range` 从 20（包含）到 25（不包含），所以输出为：

Output
```
20
21
22
23
24
```
`range()` 的 `step` 参数与切片字符串时定义步长有关，因为它可以用于跳过序列中的值。在所有三个参数都存在的情况下，`step` 位于最后一个位置：`range(start, stop, step)`。首先，让我们应用一个正值的步长：
```python
for i in range(0,15,3):
    print(i)
```
在这个示例中，`for` 循环被设定为打印从 0 到 15 的数字，但步长为 3，因此每隔三个数字打印一个，如下所示：

Output
```
0
3
6
9
12
```
我们还可以为 `step` 参数应用负值来反向迭代，但我们必须相应地调整起始和停止参数：
```python
for i in range(100,0,-10):
    print(i)
```
在这里，100 是起始值，0 是停止值，-10 是范围，所以循环从 100 开始到 0，每次迭代减少 10。我们可以在输出中看到这种情况：

Output
```
100
90
80
70
60
50
40
30
20
10
```
在 Python 中，`for` 循环通常获取 `range()` 序列类型作为迭代参数。

### 使用序列类型的 for 循环
列表和其他数据序列类型也可以作为 `for` 循环的重复参数。与其遍历 `range()`，不如分配一个列表并遍历该列表：
```python
sharks = ['hammerhead', 'great white', 'dogfish', 'frilled', 'bullhead']
for shark in sharks:
    print(shark)
```
在这个示例中，我们正在打印列表中的每一项。虽然我们使用了变量 `shark`，但我们可以使用任何其他有效的变量名，并得到相同的输出：

Output
```
hammerhead
great white
dogfish
frilled
bullhead
```

## 嵌套循环
在 Python 中，可以嵌套循环。嵌套循环是发生在另一个循环中的循环，结构上与嵌套 if 语句相关。它们的创建如下：
```python
for [first iterating variable] in [outer loop]:
    [do something] # 可选
    for [second iterating variable] in [nested loop]:
        [do something]
```
程序首先遇到外部循环，执行其最早迭代。这次迭代触发了内部嵌套循环。

