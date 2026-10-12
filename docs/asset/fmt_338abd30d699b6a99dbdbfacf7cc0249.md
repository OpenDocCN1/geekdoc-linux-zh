
对于任何最简单的程序，Python 代码都被组织成“包”（packages）。包是一个被组在一个共同的顶层名称下的模块集合。这种分组有助于解决不同应用程序之间使用的模块名称的冲突，并使你的代码与其他人的代码分开。包的定义是创建一个具有独特名称的目录，并在该目录下放置一个空的 `__init__.py` 文件。然后，你可以根据需要在该目录中放置额外的 Python 文件和子包。例如，一个包的组织结构可能如下：

```
graphics/
  __init__.py
  primitive/
    __init__.py
    lines.py
    fill.py
    text.py
```

当包的任何部分被首次导入时，`__init__.py` 中的代码会首先执行（如果存在）。正如前面提到的，该文件可以是空的，但也可以包含执行包特定初始化的代码。如果导入深层嵌套的子模块，在遍历目录结构时遇到的所有 `__init__.py` 文件都会被执行。因此，语句 `import graphics.primitive.fill` 会首先执行 `graphics/` 目录下的 `__init__.py` 文件，然后执行 `primitive/` 目录下的 `__init__.py` 文件。

敏锐的 Python 用户可能会注意到，即使省略 `__init__.py` 文件，包仍然可以工作。这是 true——如果一个 Python 代码目录包含 `__init__.py`，你就可以将其作为一个包。然而，不明显的是，一个缺少 `__init__.py` 文件的目录实际上定义了另一种包，被称为“命名空间包”（namespace package）。这是大型库和框架用于实现插件系统的高级特性。在作者看来，这通常不是你想要的——在创建包时，你应该始终创建适当 `__init__.py` 文件。

## 8.10 包内部导入

`import` 语句的一个关键特性是，所有的模块导入都需要绝对路径或完全限定的包路径。这包括在包内部使用的 `import` 语句。例如，假设 `graphics.primitive.fill` 模块导入了 `graphics.primitive.lines` 模块。简单的 `import lines` 语句将不起作用。相反，你需要完全限定你的导入：

```python
from graphics.primitive import lines
```

遗憾的是，写出包名既繁琐又脆弱。例如，有时使用相对导入是有意义的：

```python
from . import lines
```

要将子模块作为主脚本运行，你需要使用 `-m` 选项。例如：

```bash
python3 -m graphics.primitive.fill
```

## 8.11 运行包子模块

要将子模块作为主脚本运行，你需要使用 `-m` 选项。例如：

```bash
python3 -m graphics.primitive.fill
```

## 8.12 控制包命名空间

包的主要目的是作为代码的顶层容器。有时用户只会导入顶层名称而不包含其他内容。例如：

```python
import graphics
```

此导入没有指定任何特定的子模块。也不会让包的任何其他部分可用。例如，你会发现这样的代码：

```python
import graphics
graphics.primitive.fill.floodfill(img,x,y,color) # 失败！
```

当给出一个顶层包导入时，唯一导入的文件是关联的 `__init__.py` 文件。在示例中，它是 `graphics/__init__.py` 文件。

`__init__.py` 文件的主要目的是构建和/或管理顶层包命名空间的内容。通常，这涉及从较低级别的子模块中导入选定的函数、类和其他对象。

例如，如果此示例中的图形由数百个低级函数组成，但其中大多数细节都封装在少数几个高层类中，那么 `__init__.py` 文件可能会选择只暴露这些类：

点击此处查看代码图像

```
# graphics/__init__.py
from .graph2d.plot2d import Plot2D
from .graph3d.plot3d import Plot3D
```

通过这个 `__init__.py` 文件，`Plot2D` 和 `Plot3D` 名称将出现在包的顶层。用户就可以像对待 `graphics` 是一个简单模块一样使用这些名称：

点击此处查看代码图像

```
from graphics import Plot2D
plt = Plot2D(100, 100)
plt.clear()
```

这对于用户来说方便得多，因为他们不需要知道你是是如何组织代码的。在某种意义上，你正在代码结构之上放置了一个更高层次的抽象。Python 标准库中的许多模块都是以这种方式构建的。例如，流行的 `collections` 模块实际上是一个包。`collections/__init__.py` 文件整合了来自几个不同位置定义，并将它们作为一个单一的命名空间呈现给用户。

## 8.13 控制包导出

一个问题涉及 `__init__.py` 文件与低级子模块之间的交互作用。例如，包的用户可能只关心位于顶层包命名空间中的对象和函数。然而，包的实现者可能需要担心将代码组织成可维护的子模块的问题。

为了更好地管理这种组织复杂性，包子模块通常通过定义 `__all__` 变量来声明显式的导出列表。这是一个应该被推送到包命名空间上一个层级的名称列表。例如：

点击此处查看代码图像

```
# graphics/graph2d/plot2d.py

__all__ = ['Plot2D']
```

class Plot2D:

相关的 `__init__.py` 文件随后使用如下的 *import* 语句来导入其子模块：

点击此处查看代码图像

```
# graphics/graph2d/__init__.py
```

```python
# 只从 .plot2d import 加载 __all__ 变量中显式列出的名称
```

```python
# 将 __all__ 传播到下一层（如果需要）
__all__ = plot2d, __all
```

这种提升过程一直持续到顶层包的 `__init__.py`。例如：

点击此处查看代码图像

```
# graphics/__init__.py
from .graph2d import *
from .graph3d import *
```

```python
# 整合导出内容
__all__ = [
    *graph2d.__all__,
    *graph3d.__all__
]
```

核心在于，包的每个组件都使用 `__all__` 变量显式声明其导出内容。`__init__.py` 文件随后向上传播这些导出。在实践中，这可能会变得复杂，但这种方法避免了将导出名称硬编码到 `__init__.py` 文件中的问题。相反，如果子模块想要导出某些内容，它的名称只需要在一个地方列出——`__all__` 变量。然后，通过“魔法”，它会传播到包命名空间中的正确位置。

值得注意的是，在用户代码中使用 * import 是不受推荐的，但在包的 `__init__.py` 文件中这是一种广泛的实践。它在包中有效的原因是它通常受到更多控制和局限——由 `__all__` 变量的内容驱动，而不是一种“随心导入一切”的随意态度。

## 8.14 包数据

有时包包含需要加载的文件（而非源代码）。在包内部，`__file__` 变量将提供有关特定源文件的位置信息。然而，包是复杂的。它们可能被封装在 ZIP 归文件中，或从异常环境中加载。`__file__` 变量本身可能不可靠，甚至未定义。因此，加载数据文件通常不是简单的将文件名传递给内置 `open()` 函数并读取数据。

要读取包数据，请使用 `pkgutil.get_data(package, resource)`。例如，如果你的包代码如下：

点击此处查看代码图像

```
mycode/
resources/
data.json
__init__.py
spam.py
yow.py
```

```python
# mycode/spam.py
import pkgutil
import json

def func():
    data = pkgutil.get_data('mycode', 'resources/data.json')
    if data:
        data = json.loads(data.decode('utf-8'))
        print(data)
```

## 8.15 模块对象

模块是一类对象。表 8.1 列出了常见的常见的属性：

| 属性 | 描述 |

|---|---|

| __name__ | 完整名称 |

| __doc__ | 文档字符串 |

| __dict__ | 模块字典 |

| __file__ | 文件名 |

| __package__ | 闭包名称 |

| 属性 | 描述 |

|---|---|

