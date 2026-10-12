
```python
    def rate(self):
        return self._rate

    def setRate(self, rate):
        if rate != self.__rate:
            self._rate = rate
            self.emit(SIGNAL("rateChanged"), self._rate)
```

`rate()` 和 `setRate()` 方法都可以被连接，因为任何 Python 可调用对象都可以用作槽。如果税率发生变化，我们会更新私有的 `_rate` 值并发射自定义的 `rateChanged` 信号，将新的税率作为参数传递。我们还使用了更快的短路语法。如果我们想使用标准语法，唯一的区别在于信号将被写为 `SIGNAL("rateChanged(float)")`。如果我们将 `rateChanged` 信号连接到 `setRate()` 槽，由于存在 `if` 语句判断，不会发生无限循环。让我们看看该类在实际中的使用方式。首先，我们将声明一个在税率变化时被调用的函数：

```python
def rateChanged(value):
    print "TaxRate changed to %.2f%%" % value
```

现在让我们尝试一下：

```python
vat = TaxRate()
vat.connect(vat, SIGNAL("rateChanged"), rateChanged)
vat.setRate(17.5)     # 不会发生变化（新税率相同）
vat.setRate(8.5)      # 将发生变化（新税率不同）
```

这将导致控制台仅输出一行：“TaxRate changed to 8.50%”。

在早期的示例中，当我们将多个信号连接到同一个槽时，我们并不关心是谁发射了该信号。但有时我们希望将两个或更多信号连接到同一个槽，并希望该槽根据调用者的不同表现出不同的行为。在本节的最后一个示例中，我们将解决这一问题。

![](img/9bfe0a027fcc8793bb087287001100dd_146_0.png)

**图 4.8 Connections 程序**

图 4.8 中显示的 Connections 程序包含五个按钮和一个标签。当其中一个按钮被点击时，使用信号和槽机制来更新标签的文本。以下是表单的 `__init__()` 方法中第一个按钮的创建方式：

```python
button1 = QPushButton("One")
```

其他所有按钮以相同的方式创建，只是变量名称和传递给它们的文本不同。

我们将从最简单的连接开始，这是由 `button1` 使用的。以下是 `__init__()` 方法中的 `connect()` 调用：

```python
self.connect(button1, SIGNAL("clicked()"), self.one)
```

我们为这个按钮使用了一个专用方法：

```python
def one(self):
    self.label.setText("You clicked button 'One'")
```

将按钮的 `clicked()` 信号连接到响应此情况的单一方法，可能是最常见的连接场景。

但如果大多数处理过程是相同的，只有根据哪个特定按钮被按下而进行一些参数化呢？在这种情况下，通常最好将每个按钮连接到同一个槽。实现这一点有两种方法。一种是使用偏函数应用来包装带有参数的槽，这样当槽被调用时，它会带有调用它的按钮作为参数。另一种是询问 PyQt 告诉我们哪个按钮调用了该槽。我们将展示这两种方法，从偏函数应用开始。

+ 偏函数应用 63

回到第 65 页，我们创建了一个包装函数，它使用了 Python 2.5 的 `functools.partial()` 函数或我们自己简单的 `partial()` 函数：

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

使用 `partial()`，我们现在可以将槽和按钮名称包装在一起。因此，我们可能会倾向于这样做：

```python
self.connect(button2, SIGNAL("clicked()"),
              partial(self.anyButton, "Two")) # 对于 PyQt 4.0-4.2 是错误的
```

不幸的是，这在 PyQt 4.3 之前的版本中不起作用。包装函数是在 `connect()` 调用中创建的，但一旦 `connect()` 调用完成，包装函数就会超出作用域并被垃圾回收。从 PyQt 4.3 开始，使用 `functools.partial()` 创建的包装器在这种类型的连接中被特殊处理。这意味着被连接到的函数不会被垃圾回收，因此前面显示的代码将正确工作。

+ PyQt 4.3

对于 PyQt 4.0、4.1 和 4.2，我们仍然可以使用 partial()：我们只需要保留对包装函数的引用——我们不会在 `connect()` 调用之外使用该引用，但它是表单实例的属性这一事实将确保在表单存在期间包装函数不会超出作用域，因此将正常工作。因此，实际的连接是这样建立的：

```python
self.button2callback = partial(self.anyButton, "Two")
self.connect(button2, SIGNAL("clicked()"),
            self.button2callback)
```

当 button2 被点击时，anyButton() 方法将被调用，并带有包含文本 "Two" 的字符串参数。以下是该方法的样子：

```python
def anyButton(self, who):
    self.label.setText("You clicked button '%s'" % who)
```

我们可以使用刚才展示的 partial() 函数将此槽用于所有按钮。实际上，我们可以完全避免使用 partial() 并获得相同的结果：

```python
self.button3callback = lambda who="Three": self.anyButton(who)
self.connect(button3, SIGNAL("clicked()"),
            self.button3callback)
```

+ Lambda 调用函数 61-3

在这里，我们创建了一个由按钮名称参数化的 lambda 函数。它的工作原理与 partial() 技术相同，并调用相同的 anyButton() 方法，只是使用 lambda 来创建包装器。

button2callback() 和 button3callback() 都调用 anyButton()；它们之间的唯一区别是第一个传递 "Two" 作为参数，而第二个传递 "Three"。

+ PyQt 4.1.1

如果我们使用的是 PyQt 4.1.1 或更高版本，并且使用 lambda 回调，我们自己就不必保留对它们的引用了。这是因为 PyQt 在用于创建连接中的包装器时对 lambda 进行了特殊处理。（这与预计将在 PyQt 4.3 中扩展到 functools.partial() 的特殊处理相同。）因此，我们可以直接在 connect() 调用中使用 lambda。例如：

```python
self.connect(button3, SIGNAL("clicked()"),
            lambda who="Three": self.anyButton(who))
```

包装技术工作得非常好，但还有另一种方法稍微复杂一些，但在某些情况下可能很有用，特别是当我们要避免包装调用时。这种其他技术用于响应 button4 和 button5。以下是它们的连接：

```python
self.connect(button4, SIGNAL("clicked()"), self.clicked)
self.connect(button5, SIGNAL("clicked()"), self.clicked)
```

请注意，我们没有包装它们都连接到的 clicked() 方法，因此乍一看似乎没有办法知道是哪个按钮调用了 clicked() 方法。* 然而，实现清楚地表明，如果我们想区分的话是可以做到的：

```python
def clicked(self):
    button = self.sender()
    if button is None or not isinstance(button, QPushButton):
        return
    self.label.setText("You clicked button '%s'" % button.text())
```

在槽内部，我们总是可以调用 sender() 来发现发射信号的 QObject 是谁。（如果槽是使用普通方法调用 invoked 的，这可能是 None。）虽然我们知道我们只将按钮连接到了这个槽，但我们仍然小心地进行检查。我们使用了 isinstance()，但也可以使用 hasattr(button, "text") 代替。如果我们将所有按钮都连接到这个槽，它将正确地为所有四个按钮工作。

一些程序员不喜欢使用 sender()，因为他们认为这不是良好的面向对象风格，所以当他们遇到这类需求时，倾向于使用偏函数应用。

实际上还有另一种技术可以产生包装函数和参数的效果。它利用了 QSignalMapper 类，其使用示例将在第 9 章中展示。

在某些情况下，槽可能是作为信号的结果被调用的，而槽中执行的处理直接或间接导致最初调用该槽的信号再次被调用，从而导致无限循环。这种循环在实际中很少见。两个因素有助于减少循环的可能性。首先，一些信号仅在发生实际变化时发射。例如，如果 QSpinBox 的值由用户更改或通过 setValue() 调用在程序上更改，它仅在新值与当前值不同时发射其 valueChanged() 信号。其次，一些信号仅作为用户操作的结果发射。例如，QLineEdit 仅当文本由用户更改时发射其 textEdited() 信号，而不是当文本在代码中通过 setText() 调用更改时。

如果似乎出现了信号-槽循环，自然首先要检查的是代码逻辑是否正确：我们是否真的在执行我们认为在做的处理？如果逻辑是正确的，但我们仍然有循环，我们可能能够通过改变我们连接到的信号来打破循环——例如，用仅作为用户交互结果发射的信号替换那些作为程序化更改结果发射的信号。如果问题持续存在，我们可以使用 QObject.blockSignals() 来阻止代码中某些地方的信号发射，这是所有 QWidget 类继承的，并且

> 在 PyQt 编程风格中，约定俗成地让槽具有与其连接到的信号相同的名称。

![](img/9bfe0a027fcc8793bb087287001100dd_149_0.png)

