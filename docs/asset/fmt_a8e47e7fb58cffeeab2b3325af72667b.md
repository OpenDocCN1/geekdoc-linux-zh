
## 站点配置文件

典型的 Python 安装可能包含许多第三方模块和包。为了配置这些包，解释器首先导入 `site` 模块。`site` 模块的作用是搜索包文件并将额外的目录添加到模块路径 `sys.path`。此外，`site` 设置了 Unicode 字符串转换的默认编码。

`site` 模块通过根据 `sys.prefix` 和 `sys.exec_prefix` 的值构建目录列表来工作：

```python
sys.prefix               # 仅限 Windows
sys.exec_prefix         # 仅限 Windows
sys.path += '/lib/python/site-packages',
sys.exec_prefix += '/lib/python/site-packages',
sys.exec_prefix += '/lib/python/site-python'
```

此外，可能会向此列表添加用户 site 包目录（在下一节中描述）。

对于列表中的每个目录，都会检查该目录是否存在。如果存在，则将其添加到 `sys.path` 变量中。接下来，检查是否存在任何路径配置文件（以 `.pth` 后缀结尾）。路径配置文件包含一个相对于路径文件位置的目录、zip 文件或 `.egg` 文件列表，这些文件应该被添加到 `sys.path`。

```text
# foo 配置文件 'foo.pth'
foo
bar
```

路径配置文件中的每个目录都必须逐行列出。注释和空行会被忽略。当 `site` 模块加载该文件时，它会检查每个目录是否存在。如果存在，则将该目录添加到 `sys.path`。重复项只会添加到路径一次。

在将所有路径都添加到 `sys.path` 后，将尝试导入一个名为 `sitecustomize` 的模块。该模块的目的是执行任何额外的（任意的）站点自定义。如果导入 `sitecustomize` 时因 `ImportError` 失败，则该错误会被静默忽略。`sitecustomize` 的导入发生在将任何用户目录添加到 `sys.path` 之前，因此将其放在你的目录中没有影响。

`site` 模块负责设置默认的 Unicode 编码。默认情况下，编码设置为 `'ascii'`。但是，可以通过在 `sitecustomize.py` 中放置代码，调用 `sys.setdefaultencoding()` 并指定新编码 `'utf-8'` 来更改编码。如果你愿意尝试，也可以修改 `site` 的源代码，以根据机器的区域设置自动设置编码。

## 用户站点包

通常情况下，第三方包的安装方式使得所有用户都可以访问。然而，单个用户可以在用户目录中安装模块和包。在 UNIX 和 MacOS 系统上，该目录位于 `~/.local` 下，并命名为 `~/.local/lib/python2.6/site-packages`。在 Windows 系统上，该目录由 `%APPDATA%` 环境变量决定，它通常类似于 `C:\Documents\ and\ Settings\David Beazley\Data`。在该文件夹中，你会找到一个 `"Python\Python26\site-packages"` 目录。

如果你正在编写想在库使用的自定义 Python 模块和包，可以将它们放在用户-site 目录。如果你正在安装第三方模块，可以通过提供 `--user` 选项手动将它们安装到此目录。

## 启用未来特性

可以通过以下方式启用影响旧版本兼容性的新特性：

```python
from __future__ import division
```

需要注意的是，没有任何功能是可以关闭的。目前已定义了以下内容：

| 特性名称 |or |
| :--- | :--- |
| nested_scopes | 支持嵌套作用域。在 2.1 中引入。 |
| generators | 支持生成器。在 2.2 中引入。 |
| division | 修改后的语义，整数除法返回浮点数。在 2.3 中引入。 |
| absolute_import | 修改导入行为。在 2.4 中引入。 |
| with_statement | 支持上下文管理器。在 2.5 中引入。 |
| print_function | 使用 `print()` 代替 print 语句。在 2.6 中引入。 |

## 程序终止

当没有语句执行、当出意之外的 `SystemExit` 异常时（由 `sys.exit()` 生成）或解释器接收到 SIGTERM 或 SUP 信号（在 UNIX 上）时，程序终止。退出时，解释器减少当前命名空间中所有对象的引用计数。如果对象的引用计数达到零，则对象被销毁并调用其 `__del__()` 方法。

重要的是，在某些情况下 `__del__()` 方法可能不会被调用。这发生在对象之间存在循环引用时（在这种情况下对象已分配但从空间访问）。尽管 Python 的垃圾回收在执行期间可以回收循环引用，但在终止时并不一定调用。

由于无法保证 `__del__()` 在终止时会被调用，显式清理对象（如文件和网络连接）可能是一个好主意。为了实现这一点，为用户定义的对象添加清理方法（例如 `close()`）。另一种可能性是编写一个终止函数并用 `atexit` 模块注册它，如下：

```python
import atexit
connection = open_connection("dead.com")
```

```python
def cleanup():
    print("Going away...")
    close_connection(connection)
atexit.register(cleanup)
```

垃圾回收也可以以此方式调用：

```python
import atexit
atexit.register(gc)
```

关于程序终止的最后一个特性是，某些对象的 `__del__()` 方法可能会尝试访问其他模块定义的全局数据或方法。这些对象可能已经被销毁，`__del__()` 中发生 `NameError` 异常，你可能会得到如下错误：

```
Exceptions.NameError: 'c' in method Bar.__del__ of Bar instance at <0310> ignored
```

如果发生这种情况，意味着 `__del__()` 提前终止了。它还意味着它在尝试执行重要操作（例如安全地关闭服务器连接）时失败了。如果这是一个问题，那么在你的代码中执行显式的关闭步骤可能是一个好主意，而不是依赖解释器在程序终止时销毁对象。

通过在 `__del__` 方法定义中声明默认参数来消除：

```python
import foo
class Bar(object):
    def __del__(self, foo=foo):
        foo.bar()  # 在模块执行中使用某些内容
```

在某些情况下，在不执行任何清理操作的情况下终止执行是有用的。这可以通过调用 `os.exit(status)` 实现。该函数提供了指向底层 `exit()` 系统调用的接口，后者负责杀死 Python 解释器进程。当它被调用时，程序会立即终止，不会进行任何进一步的处理或清理。

## 测试、调试、性能分析与调优

与 C 或 Java 等语言中的程序不同，Python 程序不会由产生可执行程序的编译器进行处理。在这些语言中，编译器是防止编程错误的第一道防线——它可以捕获错误，例如调用函数时参数数量错误或为变量赋值不当的值（即类型检查）。然而，在 Python 中，这些检查在程序运行时才会发生。正因如此，在运行和测试程序之前，你永远无法确定你的程序是否正确。不仅如此，除非你能够以执行其内部控制流中每个可能分支的方式运行程序，否则总会有某些隐藏错误在等待出现（幸运的是，这通常在发布几天后才会发生）。

为了解决这些问题，本章涵盖了用于测试、调试和性能分析 Python 代码的技术和库模块。最后，还讨论了优化 Python 代码的一些策略。

## 文档字符串（Docstring Strings）与 doctest 模块

如果函数、类或模块的第一行是一个字符串，则该字符串被称为文档字符串（documentation string）。包含文档字符串被认为是一种良好的风格，因为这些字符串用于向 Python 软件开发工具提供信息。例如，`help()` 命令会检查文档字符串，Python IDE 也会查看这些字符串。由于程序员在交互式 Shell 中进行实验时会查看文档字符串，因此字符串通常会包含简短的交互元素。例如：

```python
# splitter.py
def split(line, types=None, delimiter=None):
    """分割文本行并可选地执行类型转换。
    """
    # 例如：
    >>> split('GOOG 100 490.50')
    ['GOOG', '100', '490.50']
```
