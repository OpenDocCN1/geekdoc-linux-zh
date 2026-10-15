
```python
# 按唯一字母的数量对单词列表进行排序
result = sorted(words, key=lambda word: len(set(word)))
```

当 `lambda` 表达式包含自由变量（未作为参数指定的变量）时，需要小心。考虑这个示例：

点击此处查看代码图片

```
x = 2
f = lambda y: x * y
x = 3
g = lambda y: x * y # --> 输出 30
print(f(10))
print(g(10)) # --> 输出 30
```

在这个示例中，你可能期望调用 `f(10)` 输出 20，这反映了 `x` 在定义时的值为 2。然而，事实并非如此。作为一个自由变量，`f(10)` 的求值使用的是求值时 `x` 所具有的任何值。它可能与 `lambda` 函数定义时的值不同。这种行为有时被称为 `late binding`。

如果在定义时捕获变量的值非常重要，可以使用默认参数：

点击此处查看代码图片

```
x = 2
f = lambda y, x=x: x * y
x = 3
g = lambda y, x=x: x * y # --> 输出 20
print(f(10))
print(g(10)) # --> 输出 30
```

这之所以有效，是因为默认参数的值只在函数定义时求值，从而捕获了 `x` 的当前值。

## 5.15 高阶函数

Python 支持 `高阶函数` 的概念。这意味着函数可以作为参数传递给其他函数，放入数据结构中，并作为函数的返回值返回。函数被称为 `first-class objects`，这意味着处理函数的方式与处理任何其他类型的数据没有区别。这里有一个接受另一个函数作为输入并在延迟后调用它的示例——例如，为了模拟云端微服务的性能：

点击此处查看代码图片

```python
import time

def after(seconds, func):
    time.sleep(seconds)
    func()
```

```python
# 示例用法
def greeting():
    print('Hello World')

after(10, greeting)    # 10秒后打印 'Hello World'
```

在这里，传递 `after()` 的 `func` 参数是所谓 `callback function` 的一个示例。这指的是 `after()` “回调用”了作为参数提供的函数。

当函数作为数据被传递时，它隐式地携带了与定义该函数的环境相关的信息。例如，假设 `greeting()` 函数使用了如下变量：

点击此处查看代码图片

```python
def main():
    name = 'Guido'
def greeting():
    print('Hello', name)
after(10, greeting)    # 输出：'Hello Guido'

main()
```

在这个示例中，变量 `name` 被 `greeting()` 使用，但它是外部函数 `main()` 的局部变量。当 `greeting` 被传递给 `after()` 时，该函数记住了它的环境并使用所需的 `name` 变量的值。这依赖于被称为 `closure` 的特性。闭包是一个函数以及一个包含执行函数体所需的所有变量的环境。

当你基于延迟求值或延迟求值的概念编写代码时，闭包和嵌套函数非常有用。上面显示的 `after()` 函数就是该概念的范例。它接收一个不会立即求值的函数——该求值会在之后的某个时间点发生。这是在其他上下文中常见的编程模式。例如，程序可能拥有仅在响应事件（按键按下、鼠标移动、网络数据包到达等）时执行的函数。在所有这些情况下，函数的求值都被延迟到某些事情发生。当函数最终执行时，闭包确保了函数能够获得它需要的内容。

你也可以编写创建并返回其他函数的。例如：

点击此处查看代码图片

```python
def make_greeting(name):
    def greeting():
        print('Hello', name)
    return greeting
```

```python
f = make_greeting('Guido')
g = make_greeting('Ada')
```

```python
f() # 输出：'Hello Guido'
g() # 输出：'Hello Ada'
```

在这个示例中，`make_greeting()` 函数并没有执行任何有趣的计算。相反，它创建并返回了一个执行实际工作的函数 `greeting()`。那项工作只有在该函数被求值时才会发生。

在这个示例中，两个变量 `f` 和 `g` 持有了了两个不同的函数。（注：原文中的 OCR 文本似乎包含重复或碎片化的部分，但逻辑遵循对闭包的解释）。

关于闭包的一个警告是，如果不理解它，可能会导致意料之外的行为。例如，如果闭包中使用的变量发生了变化，闭包将使用更新后的值。

## 5.16 回调函数中的参数传递

回调函数的一个极具挑战性的问题是参数传递。考虑之前编写的 `after()` 函数：

点击此处查看代码图片

```python
import time

def after(seconds, func):
    time.sleep(seconds)
    func()
```

在这段代码中，`func()` 被硬编码为不带参数的调用。如果你想传递额外参数，你就没机会了。例如，你可能会尝试：

点击此处查看代码图片

```python
def add(x, y):
    print(x + y)

after(10, add(2, 3)) # 失败：立即调用了 add
```

在这个示例中，`add(2, 3)` 立即运行并返回 5。随后 `after()` 函数在 10 秒后尝试执行 `5()` 时崩溃。这绝对不是你想要的结果。然而，如果 `after()` 被带参数调用，似乎没有明显的方法让其工作。

在这种情况下，一种解决方案是使用 `lambda` 将计算封装成一个零参数函数。例如：

点击此处查看代码图片

```python
after(10, lambda: add(2, 3))
```

这种小型零参数函数有时被称为 `thunk`。基本上，它是一个在最终作为零参数函数调用时才会被求值的表达式。这是一种通用的方法，用于延迟任何表达式的求值，并在实际需要该值时调用函数。

作为 `lambda` 的替代方案，你可以使用 `functools.partial()` 来创建一个部分求值的函数：

点击此处查看代码图片

```python
from functools import partial

after(10, partial(add, 2, 3))
```

`partial()` 创建了一个可调用对象，其中一个或多个参数已经指定并缓存。它可以作为使不规则的函数匹配回调和其他应用程序中预期的签名的有用方法。这里是使用 `partial()` 的更多示例：

点击此处查看代码图片

```python
def func(a, b, c, d):
    print(a, b, c, d)
```

```python
f = partial(func, 1, 2)    # 固定 a=1, b=2
f(3, 4)                   # func(1, 2, 3, 4)
f(10, 20)               # func(1, 2, 10, 20)
```

```python
g = partial(func, 1, 2, d=4)   # 固定 a=1, b=2, d=4
g(3)                    # func(1, 2, 3, 4)
g(10)                   # func(1, 2, 10, 4)
```

`partial()` `lambda` 也可以用于类似的目的，但这两种技术之间存在重要的语义区别。对于 `partial()`，参数在 `partial` 函数第一次被定义时就会进行评估和绑定。而对于零参数的 `lambda`，参数是在稍后 `lambda` 函数实际执行时才进行评估和绑定的（所有内容的评估都是延迟的）。为了说明这一点：

点击此处查看代码图片

```python
>>> def func(x, y):
...    return x + y
...
>>> a = 2
>>> b = 3
>>> f = lambda: func(a, b)
>>> g = partial(func, a, b)
>>> a = 10
>>> b = 20
>>> f()    # 使用 a, b 的当前值
30
>>> g()    # 使用 a, b 的初始值
5
>>>
```
