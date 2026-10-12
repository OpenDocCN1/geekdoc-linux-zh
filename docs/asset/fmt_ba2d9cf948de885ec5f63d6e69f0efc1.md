
与 `extract_stack(frame, limit)` 相同。

```
tb_lineno(traceback)
```

返回 `traceback` 中的行号。

## types

`types` 模块定义了对应于函数、模块、生成器和其他元素的内置类型名称。该模块的内容通常与 `isinstance()` 函数和其他类型操作结合使用。

| 变量 | 说明 |
| --- | --- |
| `BuiltinFunctionType` | 内置函数类型 |
| `CodeType` | 代码对象类型 |
| `FrameType` | 执行帧类型 |
| `FunctionType` | 用户定义函数和 lambda 的类型 |
| `GeneratorType` | 生成器迭代器类型 |
| `GetSetType` | 描述符类型 |
| `LambdaType` | `FunctionType` 的别名 |
| `MemberType` | 成员描述符类型 |
| `MethodType` | 用户定义类方法的类型 |
| `ModuleType` | 模块类型 |
| `TracebackType` | `traceback` 对象的类型 |

大多数定义类型对象作为构造函数，用于创建该类型的对象。以下描述提供了创建函数、模块、代码对象和方法的参数。

```
FunctionType(code, globals [, name [, defargs [, closure]]])
```

创建一个新的函数对象。

```
CodeType(argcount, nlocals, stacksize, flags, codestring, constants, names, varnames, filename, name, firstlineno, lnotab, frevars [, cellvars])
```

创建一个新的代码对象。

```
MethodType(function, instance, class)
```

创建一个新的实例方法。

```
ModuleType(name [, doc])
```

创建一个新的模块对象。

### Notes

- 不应使用 `types` 模块来引用整数、列表或字典等内置对象的类型。在 Python 2 中，`types` 包含 `IntType` 和 `DictType` 等其他名称。然而，这些名称只是内置类型名称 `int` 和 `dict` 的别名。在现代代码中，你应该直接使用内置类型名称，因为在 Python 3 中 `types` 模块仅包含之前列出的名称。

## warnings

`warnings` 模块提供了发布和过滤警告信息的函数。与异常（`exceptions`）不同，警告旨在提醒用户潜在的问题，但不会产生异常或导致执行停止。`warnings` 模块的主要用途之一是通知用户可能在 Python 未来的版本中不再支持的弃用语言特性。例如：

```
>>> import regex
__main__:1: DeprecationWarning: the regex module is deprecated;  use the re module
>>>
```

与异常一样，警告被组织成类层次结构，描述一般的类别。以下列出了当前支持的类别：

| 警告对象 | 说明 |
|---|---|
| `Warning` | 所有警告类型的基类 |
| `UserWarning` | 用户定义的警告 |
| `DeprecationWarning` | 针对使用弃用特性的警告 |
| `SyntaxWarning` | 潜在的语法问题 |
| `RuntimeError` | 潜在的运行时问题 |
| `FutureWarning` | 警告特定功能的语义在未来的发布中将发生变化 |

这些类中的每一个在 `__builtin__` 模块以及 `exceptions` 模块中可用。此外，它们也是 `Exception` 的实例。这使得将警告转换为错误成为可能。

使用 `warn()` 函数发布警告。例如：

```
warnings.warn("feature X is deprecated.", RuntimeWarning)
warnings.warn("feature Y might be broken.", RuntimeWarning)
```

如果需要，可以对警告进行过滤。过滤过程可以更改警告信息的输出行为、忽略警告或将警告转换为异常。例如：

```python
warnings.filterwarnings(action="ignore",
message=".regex.*",
category=DeprecationWarning)
import regex  # 警告消息消失
```

也可以使用解释器的 `-W` 选项指定有限形式的过滤。例如：

```
% python -Wignore:the\ regex:DeprecationWarning
```

`warnings` 模块定义了以下函数：

```
warn(message[, category[, stacklevel]])
```

发布警告。`message` 是一个包含警告信息的字符串，`category` 是警告类（例如 `DeprecationWarning`），`stacklevel` 是一个整数，指定警告消息源的堆栈帧。默认情况下，`category` 为 `UserWarning`，`stacklevel` 为 `1`。

```
warn_explicit(message, category, filename, module[, registry]])
```

这是 `warn()` 函数的底层版本。`message` 和 `category` 的含义与 `warn()` 相同。`lineno` 和 `module` 显式指定警告的位置。如果省略 `registry`，则警告消息不会被抑制。

```
showing(message, category, filename, lineno[, file])
```

将警告写入文件。如果省略 `file`，则警告被写入 `sys.stderr`。

```
formatting(message, category, filename, lineno)
```

创建在发布警告时打印的字符串。

```
filterwarnings(action, message, category[,module[, lineno[, append]]]])
```

向警告过滤器列表添加条目。`action` 是 'error'、'ignore'、'always'、'default'、'once' 或 'module' 之一。该列表提供了每种操作的解释：

| 操作 | 说明 |
| --- | --- |
| 'error' | 将警告转换为异常 |
| 'ignore' | 忽略警告 |
| 'always' | 总是打印警告消息 |
| 'default' | 在警告发生的每个位置打印一次警告 |
| 'module' | 在警告发生的每个模块打印一次警告 |
| 'once' | 无论警告何时发生都打印一次警告 |

`message` 是一个正则表达式字符串，用于匹配警告消息。`category` 是如 `DeprecationError` 类的警告类。`module` 是匹配模块名的正则表达式字符串。`lineno` 是特定的行号或 0 以匹配所有过滤器。`append` 指定过滤器应被添加到列表 all（已检查列表）的末尾。默认情况下，新过滤器被添加到过滤器列表的开头。如果省略任何参数，它将默认为匹配所有警告的值。

```
resetwarnings()
```

重置所有警告过滤器。这会丢弃所有对 `filterwarnings()` 的调用以及通过 `-W` 指定的选项。

### Notes

- 当前活动过滤器列表可以在 `warnings.filters` 变量中找到。
- 当警告转换为异常时，警告类别变为异常类型。例如，`DeprecationWarning` 错误将抛出 `Deprecation` 异常。

## 第 13 章 Python 运行时服务

- `-W` 选项可用于在命令行指定警告过滤器。该选项的通用格式为

`-Waction:message:category:module:lineno`

其中每个部分的含义与 `filterwarning()` 函数相同。在这种情况下，`message` 和 `module` 字段是子字符串（而不是正则表达式），分别用于要过滤的警告消息的第一部分和模块名。

## weakref

`weakref` 模块用于提供对弱引用的支持。通常，对对象的引用会导致其引用计数增加——有效地保留该对象，直到引用消失。相反，弱引用提供了一种在不增加引用计数的情况下引用对象的方法。这在某些以异常方式管理对象的应用程序中非常有用。例如，在面向对象的程序中，你可能会实现诸如观察者模式的关系，弱引用可以帮助避免创建循环引用。这方面的示例见第 7 章的“内存管理”部分。

使用 `weakref.ref()` 函数创建弱引用，如下：
