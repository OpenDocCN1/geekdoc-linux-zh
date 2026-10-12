

我们选择通过抛出异常来处理无效值。这是因为 `setFraction()` 通常是编程调用的，因此在正常运行过程中，绝不应传入超出范围的值。另一种方法是强制将分子和分母限制在范围内。这种处理方式被采用于赋予组件行为的键盘和鼠标事件处理器中，我们现在将转向这些处理器。

```python
def mousePressEvent(self, event):
    if event.button() == Qt.LeftButton:
        self.moveSlider(event.x())
        event.accept()
    else:
        QWidget.mousePressEvent(self, event)
```

当用户点击组件时，我们希望将分子设置为最接近的分数值。我们本可以在鼠标按下事件中执行计算，但鉴于我们不仅希望支持点击移动，还希望支持拖动金色三角形，因此我们将此代码分解为一个独立的 `moveSlider()` 方法，该方法接受鼠标的 x 坐标作为参数。改变分数后，我们接受该事件，表示我们已处理完毕。如果我们没有处理点击（例如，如果是右键点击），则调用基类实现，尽管严格来说这并非必要。

```python
def moveSlider(self, x):
    span = self.width() - (FractionSlider.XMARGIN * 2)
    offset = span - x + FractionSlider.XMARGIN
    numerator = int(round(self._denominator * \
               (1.0 - (offset / span))))
    numerator = max(0, min(numerator, self.__denominator))
    if numerator != self._numerator:
        self._numerator = numerator
        self.emit(SIGNAL("valueChanged(int,int)"),
                  self._numerator, self._denominator)
        self.update()
```

我们首先计算组件的“跨度”（即宽度减去水平边距）。然后找出鼠标点击（或拖动）在 x 轴上的位置，并计算分子作为组件宽度的比例。如果用户在左侧边距区域点击或拖动，我们将分子设为 0；如果他们在右侧边距区域点击或拖动，则将其设为等于分母（这样分数即为 1）。如果分子与之前不同，我们相应地设置实例变量，并发出一个信号，宣布数值已更改。随后我们调用 `update()` 来调度一个绘制事件（以移动金色三角形）。

我们选择发出一个 Python 非短路信号；同样容易的做法是去掉 `(int,int)` 使其成为一个短路信号。也可以使用 `_pyqtSignals_` 类属性来定义信号，尽管这对于要与 **Qt Designer** 集成的、用 PyQt 编写的自定义组件才真正有用。

```python
def mouseMoveEvent(self, event):
    self.moveSlider(event.x())
```

为了支持通过拖动金色三角形来改变分数，仅需要这个微小的方法即可。此方法仅在鼠标被拖动时调用，也就是说，当鼠标移动的同时左键被按下时。这是 **QWidget** 的标准行为——如果我们希望，可以通过调用 **QWidget**.setMouseTracking(True) 来为所有鼠标移动生成鼠标移动事件，而无论鼠标按键状态如何。

```python
def keyPressEvent(self, event):
    change = 0

    if event.key() == Qt.Key_Home:
        change = -self.__denominator
    elif event.key() in (Qt.Key_Up, Qt.Key_Right):
        change = 1
    elif event.key() == Qt.Key_PageUp:
        change = (self.__denominator // 10) + 1
    elif event.key() in (Qt.Key_Down, Qt.Key_Left):
        change = -1
    elif event.key() == Qt.Key_PageDown:
        change = -((self.__denominator // 10) + 1)
    elif event.key() == Qt.Key_End:
        change = self.__denominator
    
    if change:
        numerator = self.__numerator
        numerator += change
        numerator = max(0, min(numerator, self.__denominator))
        if numerator != self.__numerator:
            self.__numerator = numerator
            self.emit(SIGNAL("valueChanged(int,int)"), self.__numerator, self.__denominator)
            self.update()
            event.accept()
    else:
        QWidget.keyPressEvent(self, event)
```

对于键盘支持，我们希望 Home 键将分数设为 0，End 键设为 1，向上或向右箭头键移动到下一个更大的分数，向下或向左箭头键移动到下一个更小的分数。我们还设置了 PageUp 键向上移动十分之一，PageDown 键向下移动十分之一。

确保分子在范围内、设置实例变量等的代码，与我们在鼠标按下事件处理器中所做的完全相同。同样，我们将未处理的按键传递到基类实现中——该实现什么也不做，就像基类的鼠标点击处理器一样。

```python
def sizeHint(self):
    return self.minimumSizeHint()
```

我们决定组件的首选大小是其最小大小。严格来说，我们不必重新实现此方法，但这样做可以明确我们的意图。得益于我们在初始化程序中设置的大小策略，组件可以在水平方向上增长，占据所有可用的水平空间。

```python
def minimumSizeHint(self):
    font = QFont(self.font())
    font.pointSize(font.pointSize() - 1)
    fm = QFontMetricsF(font)
    return QSize(fm.width(FractionSlider.WSTRING) * \
                 self.__denominator,
                 (fm.height() * 4) + FractionSlider.YMARGIN)
```

`QFontMetricsF` 对象由 `QFont` 对象初始化，在此情况下是组件的默认字体。此字体继承自组件的父级，父级又继承自其父级，依此类推，顶层组件从 `QApplication` 对象继承其字体（以及颜色方案和其他用户设置），而 `QApplication` 本身则从底层窗口系统报告的用户偏好中获取这些设置。当然，我们可以忽略用户偏好，并在任何组件中设置显式字体。

`QFontMetricsF` 对象提供实际的度量值，即实际使用的字体度量值——这可能不同于指定的字体。例如，如果使用 Helvetica 字体，在 Linux 或 Mac OS X 上几乎肯定会找到并使用它，但在 Windows 上，可能会使用 Arial 作为替代。我们选择使用比用户首选字体小一级的字号来显示分数，这就是我们调用 `pointSize2()` 的原因（注：原文此处提及 pointSize2() 可能指代降低点号的逻辑，代码中实际为 `font.pointSize(font.pointSize() - 1)`，译文中保留了原文的逻辑描述）。

我们将组件的最小宽度设置为显示所有分数所需的宽度，假设每个分数宽三位数字，即两位数字加上两侧的一些空白边距。由于我们不包括水平边距，实际总宽度略小于此值。我们将组件的最小高度设置为单个字符高度的四倍，即足以容纳分数“段”（表示每个分数的矩形）、垂直线、分子和分母。与宽度类似，实际高度也略小于此值，因为我们只计算了垂直边距的一半。

> *PyQt 还有一个 `QFontMetrics` 类，它提供整数值而不是浮点值。类似地，PyQt 还有 `QLine`、`QLineF`、`QPoint`、`QPointF`、`QPolygon`、`QPolygonF`、`QRect`、`QRectF` 以及另外一些类。

在实现了键和鼠标事件处理器、设置了大小策略并实现了大小提示方法之后，我们使组件具备了适当的用户交互行为，并能够适应可能需要布局该组件的任何布局管理器。只剩下最后一件事要做：我们必须根据要求绘制组件。`paintEvent()` 相当长，因此我们将分部分来看。

```python
def paintEvent(self, event=None):
    font = QFont(self.font())
    font.setPointSize(font.pointSize() - 1)
    fm = QFontMetricsF(font)
    fracWidth = fm.width(FractionSlider.WSTRING)
    indent = fm.boundingRect("9").width() / 2.0
    if not X11:
        fracWidth *= 1.5
    span = self.width() - (FractionSlider.XMARGIN * 2)
    value = self.__numerator / float(self.__denominator)
```

我们首先获取我们想要使用的字体及其字体度量。然后我们计算 `fracWidth`（一个分数的宽度）以及每个分数分割线的缩进。`if` 语句用于补偿 X 窗口系统与其他窗口系统（如 Windows 和 Mac OS X）之间字体度量的差异。`span` 是组件的宽度（不含水平边距），`value` 是分数的浮点值。

布尔变量 `X11` 在底层窗口系统是 X 窗口系统时为 True，这通常见于 Linux、BSD、Solaris 和类似系统；在其他情况下（例如 Windows 和 Mac OS X）则为 False。它在文件开头，导入之后，使用以下语句设置：

```python
X11 = "qt_x11_wait_for_window_manager" in dir()
```

我们可以更清晰地写为：

```python
import PyQt4.QtGui
X11 = hasattr(PyQt4.QtGui, "qt_x11_wait_for_window_manager")
```

这些代码有效，是因为 `PyQt4.QtGui.qt_x11_wait_for_window_manager()` 函数仅在使用 X 窗口系统的系统上存在。我们在第 7 章中使用了类似的技术来检测 Mac OS X。

```python
painter = QPainter(self)
painter.setRenderHint(QPainter.Antialiasing)
painter.setRenderHint(QPainter.TextAntialiasing)
painter.setPen(self.palette().color(QPalette.Mid))
painter.setBrush(self.palette().brush(QPalette.AlternateBase))
painter.drawRect(self.rect())
```

