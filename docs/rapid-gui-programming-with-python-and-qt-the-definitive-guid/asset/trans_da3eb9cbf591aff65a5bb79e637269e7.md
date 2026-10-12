
变为已勾选或未勾选，以及其他重要事件的发生，例如按钮被点击时（无论通过何种方式）。PyQt 中所有组件都有一组预定义信号。

每当信号被发出时，PyQt 默认会将其丢弃！若要关注某个信号，我们必须将其连接到一个槽。在 C++/Qt 中，槽是必须使用特殊语法声明的方法；但在 PyQt 中，它们可以是任意我们喜欢的可调用对象（例如，任意函数或方法），且在定义时不需要特殊语法。

大多数组件也具有预定义的槽，因此在某些情况下，我们可以将预定义信号连接到预定义槽，而不必做其他任何事情即可获得我们想要的行为。在这方面，PyQt 比 C++/Qt 更灵活，因为我们不仅可以连接到槽，还可以连接到任何可调用对象。此外，从 PyQt 4.2 开始，可以动态地为 QObjects 添加“预定义”信号和槽。让我们通过图 4.6 中所示的 *Signals and Slots* 程序来看看信号和槽在实际中是如何工作的。

![](img/9bfe0a027fcc8793bb087287001100dd_142_0.png)

**图 4.6** *Signals and Slots* 程序

QDial 和 QSpinBox 组件都有 valueChanged() 信号，当该信号被发出时，会携带新值。它们都有 setValue() 槽，该槽接受一个整数值。因此，我们可以将这两个组件相互连接，这样无论用户更改哪一个，都会相应地改变另一个：

```python
class Form(QDialog):
    def __init__(self, parent=None):
        super(Form, self).__init__(parent)

        dial = QDial()
        dial.setNotchesVisible(True)
        spinbox = QSpinBox()

        layout = QBoxLayout()
        layout.addWidget(dial)
        layout.addWidget(spinbox)
        self.setLayout(layout)

        self.connect(dial, SIGNAL("valueChanged(int)"),
                     spinbox.setValue)
        self.connect(spinbox, SIGNAL("valueChanged(int)"),
                     dial.setValue)

    self.setWindowTitle("Signals and Slots")
```

由于这两个组件以这种方式连接，如果用户移动旋钮——比如说数值为 20——旋钮将发出 valueChanged(20) 信号，进而导致调用 spinbox 的 setValue() 槽，参数为 20。但此时，由于其值现在已改变，spinbox 将发出 valueChanged(20) 信号，进而导致调用旋钮的 setValue() 槽，参数为 20。这看起来像是会导致无限循环。但实际上发生的情况是，如果值实际没有改变，valueChanged() 信号不会被发出。这是因为编写更改值槽的标准方法是首先将新值与现有值进行比较。如果值相同，则什么都不做并返回；否则，我们应用更改并发出信号以宣布状态变化。连接关系如图 4.7 所示。

![](img/9bfe0a027fcc8793bb087287001100dd_143_0.png)

现在让我们看看连接的通用语法。我们假设 PyQt 模块已经使用 from ... import * 语法导入，并且 s 和 w 是 QObjects，通常是组件，其中 s 通常代表 self。

```python
s.connect(w, SIGNAL("signalSignature"), functionName)
s.connect(w, SIGNAL("signalSignature"), instance.methodName)
s.connect(w, SIGNAL("signalSignature"),
          instance, SLOT("slotSignature"))
```

signalSignature 是信号的名称，以及括号内（可能为空的）逗号分隔的参数类型名称列表。如果信号是 Qt 信号，类型名称必须是 C++ 类型名称，例如 int 和 QString。C++ 类型名称可能相当复杂，每个类型名称可能包含 const、* 和 & 中的一个或多个。当我们将其写入信号（或槽）签名时，可以省略 const 和 &，但必须保留任何 *。例如，几乎所有传递 QString 的 Qt 信号都使用 const QString& 作为参数类型，但在 PyQt 中，仅使用 QString 就足够了。另一方面，QListView 有一个签名 itemActivated(QListViewItem*) 的信号，我们必须严格按照原样使用它。

PyQt 信号是在实际发出时定义的，可以拥有任意数量的任意类型的参数，我们稍后将会看到。

slotSignature 的形式与 signalSignature 相同，区别在于其名称是一个 Qt 槽的名称。槽的参数数量不得多于连接到它的信号的参数数量，但可以更少；多余的参数将被丢弃。对应的信号和槽参数必须具有相同的类型，因此例如，我们不能将 QDial 的 valueChanged(int) 信号连接到 QLineEdit 的 setText(QString) 槽。

在我们的旋钮和 spinbox 示例中，我们使用了 *instance.methodName* 语法，正如本章前面所示的示例应用程序那样。但当槽实际上是 Qt 槽而不是 Python 方法时，使用 SLOT() 语法效率更高：

```python
self.connect(dial, SIGNAL("valueChanged(int)"),
             spinbox, SLOT("setValue(int)"))
self.connect(spinbox, SIGNAL("valueChanged(int)"),
             dial, SLOT("setValue(int)"))
```

我们已经看到，可以将多个信号连接到同一个槽。同样，也可以将单个信号连接到多个槽。虽然很少见，但我们也只能将一个信号连接到另一个信号。在这种情况下，当第一个信号被发出时，它将导致它所连接的信号也被发出。连接使用 QObject.connect() 创建；可以使用 QObject.disconnect() 断开。实际上，我们很少需要自己断开连接，因为例如，PyQt 会自动断开涉及任何已被删除对象的连接。

到目前为止，我们已经了解了如何连接到信号，以及如何编写槽——它们是普通的函数或方法。我们知道信号被发出是为了表示状态变化或其他重要事件。但如果我们想创建一个发出自身信号的组件呢？使用 QObject.emit() 可以轻松实现。例如，下面是一个完整的 QSpinBox 子类，它发出自己定义的 atzero 信号，并且传递一个数字：

```python
class ZeroSpinBox(QSpinBox):
    zeros = 0

    def __init__(self, parent=None):
        super(ZeroSpinBox, self).__init__(parent)
        self.connect(self, SIGNAL("valueChanged(int)"), self.checkzero)

    def checkzero(self):
        if self.value() == 0:
            self.zeros += 1
            self.emit(SIGNAL("atzero"), self.zeros)
```

我们将 spinbox 自身的 valueChanged() 信号连接起来，使其调用我们的 checkzero() 槽。如果值恰好为 0，checkzero() 槽将发出 atzero 信号，并附带一个计数，表示它变为零的次数；这样传递额外数据是可选的。信号缺少括号这一点很重要：它告诉 PyQt 这是一个“短路”信号。

没有参数（因此也没有括号）的信号是短路 Python 信号。当发出这样的信号时，任何数据都可以作为额外参数传递给 emit() 方法，并作为 Python 对象传递。这避免了在 C++ 数据类型之间转换参数的开销，也意味着可以传递任意的 Python 对象，甚至是那些无法转换回 C++ 数据类型的对象。至少有一个参数的信号要么是 Qt 信号，要么是非短路 Python 信号。在这些情况下，PyQt 会检查该信号是否为 Qt 信号，如果否，则假定它是 Python 信号。在这两种情况下，参数都会被转换为 C++ 数据类型。

我们在表单的 `__init__()` 方法中连接该信号的方式如下：

```python
zerospinbox = ZeroSpinBox() ...
self.connect(zerospinbox, SIGNAL("atzero"), self.announce)
```

同样，我们不能使用括号，因为这是一个短路信号。为了完整性，以下是该槽在表单中连接的内容：

```python
def announce(self, zeros):
    print "ZeroSpinBox has been at zero %d times" % zeros
```

如果我们使用 `SIGNAL()` 函数并指定标识符但没有括号，我们就是在指定前面描述的短路信号。我们可以使用这种语法来发出短路信号，也可以用来连接它们。两种用途都在示例中展示了。

如果我们使用 `SIGNAL()` 函数并指定 *signalSignature*（一个可能为空、带括号的逗号分隔的 PyQt 类型列表），我们指定的要么是一个 Python 信号，要么是一个 Qt 信号。（Python 信号是在 Python 代码中发出的信号；Qt 信号是从底层 C++ 对象发出的信号。）我们可以使用这种语法来发出 Python 和 Qt 信号，并连接它们。这些信号可以连接到任何可调用对象，即任何函数或方法，包括 Qt 槽；也可以使用 `SLOT()` 语法和 *slotSignature* 连接。PyQt 会检查该信号是否为 Qt 信号，如果否，则假定它是 Python 信号。如果我们使用括号，即使对于 Python 信号，参数也必须可转换为 C++ 数据类型。

现在我们来看另一个例子，一个微小的自定义非 GUI 类，它有一个信号和一个槽，并展示了该机制不仅限于 GUI 类——任何 QObject 子类都可以使用信号和槽。

```python
class TaxRate(QObject):
    def __init__(self):
        super(TaxRate, self).__init__()
        self.__rate = 17.5
```
