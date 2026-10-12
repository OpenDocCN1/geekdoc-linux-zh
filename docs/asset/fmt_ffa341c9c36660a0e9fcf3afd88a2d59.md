
在类定义的第一行中，`class Stack(object)`语句声明`Stack`是一个对象。使用括号是 Python 继承的方式——在这种情况下`Stack`继承自`object`，它是所有 Python 类型的根。类定义中的方法使用`def`语句定义。每个方法中的第一个参数始终引用对象本身。按照习惯，`self`是该参数使用的名称。所有涉及对象属性的操作都显式地引用`self`变量。开头和结尾带有下线的方法是特殊方法。例如，`__init__`用于在对象创建后初始化它。

要使用类，可以编写如下代码：

```python
s = Stack()           # 创建一个栈
s.push("Dave")        # 向其推入一些东西
s.push(42)
s.push((3,4))
x = s.pop()          # x 获取 [3,4]
y = s.pop()          # y 获取 42
del s               # 销毁 s
```

在这个示例中，创建了任何新对象来实现该类。然而，栈与内置列表对象几乎完全相同。因此，另一种方法是继承自`list`并添加一个额外方法：

```python
class Stack(list):
    # 为栈接口添加 push() 方法
    # 注意：列表已经提供了 pop() 方法。
    def push(self, object):
        self.append(object)
```

通常情况下，在类内部定义的所有方法只适用于该类的实例（即创建的对象）。然而，可以定义不同类型的方法，例如让 C++ 和 Java 程序员熟悉的静态方法。例如：

```python
class EventHandler(object):
    @staticmethod
    def dispatcherThread():
        while (1):
            ...
            # 等待请求
```

```python
EventHandler.dispatcherThread()      # 像函数一样调用方法
```

在这种情况下，`@staticmethod`将随后的方法声明为静态方法。`@staticmethod`是使用装饰器的一个示例，该主题在第 6 章会有进一步讨论。

## 异常

如果程序中发生错误，将抛出一个异常，并出现如下的回溯追踪（traceback）消息：

```
Traceback (most recent call last):
File "foo.py", line 12, in <module>
IOError: [Errno 2] No such file or directory: 'file.txt'
```

回溯指示了发生的错误类型及其位置。通常，错误会导致程序终止。然而，你可以使用`try`和`except`语句来捕获并处理异常，如下：

```python
try:
    f = open("file.txt","r")
except IOError as e:
    print e
```

如果发生`IOError`，有关错误的详情将放在`e`中，控制权传递到`except`块中的代码。如果抛出其他类型的异常，它将传递给封装的代码块（如果有）。如果没有发生错误，`except`块中的代码将被忽略。当异常被处理时，程序执行将紧接最后一个`except`块之后的语句继续。程序不会返回到异常发生的位置。

`raise`语句用于信号异常。当抛出异常时，它将传递给封装的代码块（如果有）。如果没有发生错误，`except`块中的代码将被忽略。当异常被处理时，程序执行将紧接最后一个`except`块之后的语句继续。程序不会返回到异常发生的位置。

## 模块

程序中使用的所有值都是对象。对象由内部数据和执行涉及该数据的各种类型操作组成。在处理如字符串和列表等内置类型时，你已经使用过对象和方法。例如：

```python
items = [37, 42] # 创建一个列表对象
items.append(73) # 调用 append() 方法
```

## 获取帮助

在处理 Python 时，你有多个可以快速获取信息的来源。首先，当 Python 在交互模式下运行时，你可以使用`help()`命令获取有关内置模块和 Python 其它方面的信息。单独使用`help()`可以获取通用信息，而`help('modmodule')`也可以返回特定函数的信息。

大多数函数都有描述其用法的文档字符串。要使用文档字符串，请打印`__doc__`属性。示例：

```
>>> print subclass.__doc__
issubclass(C, B) : bool
```

返回类 C 是否为类 B 的子类（即派生类）。当使用元组作为第二个参数时，`issubclass(X, (A, B, ...))`是`issubclass(X, A)`或`issubclass(X, B)`或（等）的简写。

最后，但不是，大多数 Python 安装还包括`pydoc`命令，它可以返回有关 Python 模块的文档。在系统命令行提示符下简单输入`pydoc topic`即可。

## 2 词法规定与语法

本章描述了 Python 程序的语法和词法规定。主题包括行结构、语句分组、保留字、字面量、操作符、标记（tokens）源代码编码。

### 行结构与缩进

程序中的每条语句都以换行符结束。长语句可以使用行延续符（\）跨越多行，如下所示：

```python
a = math.cos(3 * (y - n)) + \
math.sin(3 * (y - n))
```

当三引号字符串、列表、元组或字典的定义跨越多行时，不需要行延续符。更通用地说，程序中由圆括号`(...)`、方括号`[...]`、大括号`{...}`或三引号的任何部分都可以不使用行延续符，因为它们表示了定义的开始和结束。

缩进用于表示不同的代码块，例如函数体、条件、循环和类。块中第一个语句的缩进量是任意的，但整个块的缩进必须保持一致。这是一个示例：

```python
if a:
    statement1      # 缩进一致
    statement2
else:
    statement3
    statement4      # 缩进不一致（错误）
```

如果函数、条件、循环或类的体很短且只包含一条语句，可以将其放在同一行，如下：

```python
if a:
    statement1
else:
    statement2
```

要表示空体或空块，请使用`pass`语句。示例：

```python
if a:
    pass
else:
    statements
```

虽然可以使用制表符（tabs）进行缩进，但不推荐这种做法。Python 社区普遍首于（并鼓励）使用空格。遇到制表符时，它们会被转换为移动到 8 倍数列所需的空格数（例如，出现在第 11 列的表格将插入空格以移动到第 16 列）。使用`-t`选项运行 Python，当同一个程序块内不一致地混合制表符和空格时会打印警告。`-tt`选项会将这些警告信息转换为`TabError`异常。

要在一行中放置多条语句，请用分号（;）分隔语句。包含单个语句的行也可以用分号结束，但这是没有意义的。

`#`字符表示延伸到行尾的注释。然而，出现在引号字符串内部的`#`不会启动注释。

最后，解释器在交互模式下运行时会忽略所有空行。在这种情况下，在输入跨越多行的语句时，空行表示输入的结束。

### 标识符与保留字

标识符是用于标识变量、函数、类、模块和其他对象的名称。标识符可以包含数字，但和下划线（`_`）必须以非数字字符开头。字母目前限于 ISO-Latin 字符集中的 A-Z 和 a-z。由于标识符区分大小写，因此`Foo`与`foo`不同。标识符中不允许特殊符号如`$`、`%`和`@`。`if`、`elif`和`for`等保留字不能用作标识符。以下列表列出了所有保留字：

```python
and               del             from            nonlocal        try
as               elif           global          not             while
assert          else           if               or              with
break           except         import          pass            yield
```
