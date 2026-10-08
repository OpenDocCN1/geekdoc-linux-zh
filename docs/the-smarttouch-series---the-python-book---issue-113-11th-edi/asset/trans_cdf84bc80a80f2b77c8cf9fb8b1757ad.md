

## 50 个必备 Python 命令

Python 以其高密度著称，拥有大量几乎可以执行任何操作的模块。在这里，我们将探讨每个人都必须了解的核心基础知识。Python 拥有一个庞大的额外模块环境，这些模块可以在数百个不同领域提供功能。然而，每种编程语言都有一个核心功能集，每个人都需要了解它才能完成有用的工作。Python 在这方面也不例外。在这里，我们将查看我们认为对 Python 编程至关重要的 50 个命令。其他人可能会选择略有不同的集合，但这个列表包含了最顶尖的内容。

我们将涵盖所有基本命令，从程序开始时导入额外模块到结束时向调用环境返回值。我们还将查看一些有助于了解 Python 当前会话的命令，例如已定义的变量列表以及内存是如何被使用的。

由于 Python 环境涉及使用大量额外模块，我们还将查看几个严格位于 Python 之外的命令。你将学习如何安装外部模块以及如何管理针对不同开发项目的多个环境。既然这是一个命令列表，就假设你已知晓如何使用循环和条件结构的基本方法。这篇文章旨在帮助你记住那些你以前见过的命令，并希望向你介绍一些你可能尚未见过的命令。

尽管我们已尽力将所有可能需要的内容打包进这 50 个技巧中，但 Python 是一门如此广泛的语言，因此一些命令未被涵盖。一旦你掌握了这些内容，请抽出时间来学习我们在这里未涵盖的那些命令。

```text
For help: View Search Terminal Help
Python Shell: python3(--)  Edit: 09 users, 22:59:05
Python version: 3.5
>>> import sys
>>> sys.version_info
major=3, minor=5, micro=3, releaselevel='final', serial=0
>>> import math
>>> math.__copyright__, math.__doc__
("", "LICENSE" for more information.
"Copyright (c) 2001-2014 Python Software Foundation.
All rights reserved.

This software may have been modified by Python contributors.
Copyright notice

Python 3.5.1 |Anaconda 2.4.1 (64-bit)| (default, Feb 15 2016, 22:25:29) [GCC 4.2.1 Compatible Apple LLVM 7.0.0 (clang-700.1.81)] on darwin
>>> import this
The Zen of Python, by Tim Peters
>>> help(import)
Help on built-in function __import__ in module builtins:
__import__(name, globals=None, locals=None, from list=(), level=0)
    Import a module.  The argument is the name of a module to be
    imported.  The optional argument globals provides the dictionary
    ...
```

### 01 导入模块

Python 的优势在于它可以通过模块进行扩展的能力。许多程序的第一步是导入你所需的模块。最简单的导入语句是直接调用 `import modulename`。在这种情况下，所提供的函数和对象不在通用命名空间中。你需要使用完整名称（`modulename.methodname`）来调用它们。你可以使用 `import modulename as mn` 命令来缩短 `modulename.` 部分。你可以使用 `from modulename import *` 命令从给定模块导入所有内容，从而完全跳过这个问题。然后你可以直接调用这些提供的功能。如果你只需要提供的项中的几个，可以通过用方法或对象名称替换 `*` 来选择性地导入它们。

### 02 重新加载模块

当模块首次被导入时，任何初始化函数都会在那时运行。这可能涉及创建数据对象或建立连接。但是，这在给定会话中仅执行一次。再次导入相同的模块不会重新执行任何初始化代码。如果你希望重新运行此代码，需要使用 reload 命令。格式为 `reload(modulename)`。需要牢记的一点是，前一次导入的字典不会被清空，而是会被覆盖。这意味着在导入和重新加载之间发生变化的任何定义都会正确更新。但是，如果你删除了一个定义，旧的定义仍会存在并可访问。可能会有其他副作用，因此请谨慎使用。

### 03 安装新模块

虽然我们查看的大多数命令都是需要在 Python 会话内执行的 Python 命令，但有几个必要的命令需要在 Python 外部执行。其中第一个是 pip。安装模块涉及下载源代码并编译包含的外部代码。幸运的是，可以在 http://pypi.python.org 找到包含数百个 Python 模块的仓库。你可以使用 `pip install modulename` 命令来安装新模块，而不必手动完成所有操作。该命令还会执行依赖项检查，并在安装你请求的模块之前安装任何缺失的模块。如果你希望将此新模块安装到计算机的全局库中，可能需要管理员权限。在 Linux 机器上，你只需使用 sudo 运行 pip 命令即可。否则，你可以通过添加命令行选项 `--user` 将其安装到你的个人库目录中。

> “市面上每一种编程语言都有一个核心功能集，每个人都需要了解它才能完成有用的工作。Python 也不例外。”

### 04 执行脚本

导入模块确实会运行模块文件内的代码，但它是通过 Python 引擎内的模块维护代码进行的。此维护代码还负责运行初始化代码。如果你只想获取一个 Python 脚本并在当前会话中执行其中的原始代码，可以使用 `execfile(filename.py)` 命令，其中主要选项是一个包含要加载和执行的 Python 文件的字符串。默认情况下，任何定义都会加载到当前会话的 locals 和 globals 中。你可以选择为 execfile 命令包括两个额外参数。这两个选项都是字典，一个用于不同的 locals 集合，另一个用于不同的 globals 集合。如果你只提供这样一个字典，则假定它是 globals 字典。此命令的返回值为 None。

### 05 增强型 Shell

默认交互式 shell 通过命令 `python` 提供，但功能相当有限。增强型 shell 由命令 `ipython` 提供。它为代码开发者提供了许多额外功能。一个完整的历史系统可供使用，不仅可以访问当前会话的命令，还可以访问以前会话的命令。还有提供增强型当前 Python 会话交互方式的 magic 命令。对于更复杂的交互，你可以创建和使用宏。你甚至可以轻松地查看 Python 会话的内存并反编译 Python 代码。你甚至可以创建配置文件，以处理每次使用 Python 时可能需要执行的初始化步骤。

### 06 评估代码

有时，你可能有以编程方式组装的代码块。如果这些代码片段作为字符串组装，你可以使用命令 `eval(code_string)` 来执行结果。代码字符串内的任何语法错误都会作为异常报告。默认情况下，此代码在当前会话内执行，使用当前的 globals 和 locals 字典。`eval` 命令还可以接受另外两个可选参数，你可以为 globals 和 locals 提供不同的字典集合。如果只有一个额外参数，则假定它是 globals 字典。你可以选择传入使用 compile 命令创建的代码对象，而不是代码字符串。此命令的返回值为 None。

