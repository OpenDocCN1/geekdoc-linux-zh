

的求值结果。Lambda 函数可以是闭包，这将在后文讨论。在这个例子中，我们将 Lambda 函数赋值给了变量 `cube`，现在我们可以使用它，例如：`cube(3)`，这将返回 27。

一些 Python 程序员不喜欢 lambda；当然，既然可以使用 `def` 创建任何我们想要的函数，lambda 并非必需。然而，当我们开始学习 GUI 编程时，我们会看到 lambda 有用的场景，虽然我们也展示了不使用 lambda 的替代方案。

## 动态函数创建

Python 解释器从 `.py` 或 `.pyw` 文件的顶部开始读取。当解释器遇到 `def` 语句时，它会执行该语句，从而创建函数并将 `def` 后面的名称绑定到该函数。任何不在 `def` 语句内部（或不在 `class` 语句内部，我们将在下一章中看到）的代码都会直接执行。

Python 不能调用未定义的函数或使用未定义的对象。因此，单个文件中的 Python 程序倾向于具有类似 Pascal 的结构，从上到下有很多函数定义，并在最后调用其中一个函数以开始处理流程。

与 C++ 和 Java 不同，Python 程序没有固定的入口点，名称 “main” 也不特殊。Python 解释器只是从第一行开始依次执行它遇到的代码。例如，这是一个完整的 Python 程序：

```python
#!/usr/bin/env python

def hello():
    print "Hello"

def world():
    print "World"

def main():
    hello()
    world()

main()
```

解释器执行 `def hello()`，即创建 `hello()` 函数，然后创建 `world()` 函数，接着创建 `main()` 函数。最后，解释器遇到一个函数调用，即 `main()`（在这种情况下，解释器执行该函数调用，此时我们通常认为程序执行开始了。

Python 程序员通常只在顶层放置一条语句，即调用他们希望首先执行的那个函数。他们通常将这个函数称为 `main()`，并从中调用其他函数，从而形成与 C++ 和 Java 使用的结构类似的结构。

由于 `def` 语句在运行时执行，因此可以根据不同情况使用不同的定义。这特别有用，当我们想使用某个 Python 版本中的功能，但该功能在早期版本中不可用，而不强制用户升级时。

例如，Python 2.4 引入了 `sorted()` 函数。如果我们有一些代码需要 `sorted()`，但部分用户使用 Python 2.3，部分用户使用 2.4 或更高版本怎么办？我们可以简单地依赖 2.4 或更高版本的 `sorted()` 方法，并为旧版 Python 提供我们自己等效的函数：

```python
import sys
if sys.version_info[:2] < (2, 4):
    def sorted(items):
        items = list(items)
        items.sort()
        return items
```

我们首先导入 `sys` 模块，该模块提供 `version_info` 元组。然后我们使用这个元组获取主版本号和次版本号。只有当版本低于 2.4 时，我们才定义自己的 `sorted()` 函数。请注意，我们还可以比较元组：Python 可以比较数据结构，包括嵌套的数据结构，只要它们包含的所有类型都可以比较即可。

## 函数偏应用

正如我们将在开始 GUI 编程时所见，有时我们会遇到需要调用特定函数的情况，但我们在编写代码时实际上已知其中一个参数是什么。例如，我们可能有几个按钮，它们都需要调用同一个函数，但根据哪个按钮触发了调用而在某种方式下进行参数化。

在最简单的情况下，我们想要存储一个函数（即指向函数的对象引用），以便稍后可以调用它。像这样存储的函数被称为 *回调*。这里是一个简单的例子：

```python
def hello(who):
    print "Hello", who

def goodbye(who):
    print "Goodbye", who

funclist = [hello, goodbye]
# 稍后
for func in funclist:
    func("Me")
```

这打印了 “Hello Me”，然后打印了 “Goodbye Me”。这里，我们存储了两个函数，然后稍后调用了它们。请注意，每次调用 `func()` 时，我们传递了相同的参数 "Me"。既然我们预先知道参数是什么，如果能以某种方式将被调用的函数和我们要使用的参数打包成一个可调用对象，那就太好了。

解决这个问题的方法是 *函数偏应用*（也称为“柯里化”），意思是我们拿一个函数及其零个、一个或多个参数，并将它们包装成一个新函数，当该函数被调用时，它会使用我们包装的参数以及调用时传入的其他任何参数来调用原始函数。这种被包装的函数被称为 *闭包*，因为它们在创建时封装了部分调用上下文。

为了了解其工作原理，让我们想象一个非常简单的 GUI 程序，其中有两个按钮，按下时会调用同一个 `action()` 函数。（我们现在先不担心如何将按钮点击转化为函数调用；这很容易，并在第 4 章中有完整解释。）

```python
def action(button):
    print "You pressed button", button
```

现在，当我们创建按钮时，我们自然知道它们是哪个，所以我们希望告诉第一个按钮执行 `action("One")` 调用，告诉第二个按钮执行 `action("Two")` 调用。但这给我们带来了问题。我们知道我们要调用什么，但我们不希望调用发生在按钮被按下之前。因此，例如，我们希望给第一个按钮一个函数，该函数包装了 `action()` 和参数 "One"，以便当第一个按钮被按下时，它可以以正确的参数调用 `action()`。

所以，我们需要的是一个函数，它接受一个函数和一个参数，并返回一个函数，该函数在被调用时会以原始参数调用原始函数。在 Python 2.5 中，假设我们之前定义了 `action()`，这很容易做到：

```python
import functools

buttonOneFunc = functools.partial(action, "One")
buttonTwoFunc = functools.partial(action, "Two")
```

`functools.partial()` 函数接受第一个参数为函数，然后接受任意数量的其他参数，并返回一个函数，该函数在被调用时，会使用传入的参数以及调用时给出的任何额外参数来调用传入的函数。

因此，当调用 `buttonOneFunc()` 时，它将简单地调用 `action("One")`，正如我们所希望的那样。正如我们之前提到的，函数名称只是一个恰好引用函数的对象引用，因此它可以像其他任何对象引用一样作为参数传递。

但这让早期版本 Python 的用户处于什么境地？我们可以提供我们自己非常简单的且功能较弱的 `partial()` 版本。例如：

```python
def partial(func, arg):
    def callme():
        return func(arg)
    return callme
```

在 `partial()` 函数内部，我们创建一个内部函数 `callme()`，当被调用时，它将调用传递给 `partial()` 函数的函数和参数。创建 `callme()` 函数后，我们返回指向它的对象引用，以便稍后可以调用它。

这意味着我们现在可以写：

```python
buttonOneFunc = partial(action, "One")
buttonTwoFunc = partial(action, "Two")
```

理想情况下，如果 `functools.partial()` 可用，我们最好使用它，否则回退到我们自己的简单 `partial()` 函数。嗯，既然我们可以在运行时定义函数，这是完全可能的：

```python
import sys

if sys.version_info[:2] < (2, 5):
    def partial(func, arg):
        def callme():
            return func(arg)
        return callme
else:
    from functools import partial
```

`if` 语句确保如果使用的 Python 版本低于 2.5，我们会创建一个 `partial()` 函数，它接受一个函数和一个参数，并返回一个函数，该函数在被调用时会使用传入的参数调用传入的函数。但如果使用的是较新版本的 Python，我们就使用 `functools.partial()` 函数，这样在我们的代码中我们总能调用 `partial()`，而实际使用的将是创建的那个版本。

现在，就像以前一样，我们可以写：

```python
buttonOneFunc = partial(action, "One")
buttonTwoFunc = partial(action, "Two")
```

只是这次代码将同时适用于旧版和新版 Python。我们定义的 `partial()` 函数几乎是最简单的可能版本。也可以创建更复杂的包装器，它们可以在包装时接受位置参数和关键字参数，并在调用时接受额外的位置参数和关键字参数；`functools.partial()` 已经提供了这种功能。我们从第二部分开始在某些地方使用 `partial()`，但在每种情况下，如果无法使用 Python 2.5 或更高版本，都可以使用本节中显示的简单 `partial()` 函数。

