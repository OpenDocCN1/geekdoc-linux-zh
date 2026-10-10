
我们在 `Ticker` 中重新实现了四个事件处理器，其中三个是我们之前没见过的：`timerEvent()`、`showEvent()` 和 `hideEvent()`。

让我们来看实现：

```cpp
#include <QtGui>

#include "ticker.h"

Ticker::Ticker(QWidget *parent)
    : QWidget(parent)
{
    offset = 0;
    myTimerId = 0;
}
```

构造函数将 `offset` 变量初始化为 0。绘制文本的 `x` 坐标源自 `offset` 值。定时器 ID 总是非零的，因此我们使用 0 来表示没有启动定时器。

```cpp
void Ticker::setText(const QString &newText)
{
    myText = newText;
    update();
    updateGeometry();
}
```

`setText()` 函数设置要显示的文本。它调用 `update()` 请求重绘，并调用 `updateGeometry()` 通知负责 `Ticker` 小部件的任何布局管理器尺寸提示（size hint）发生了变化。

```cpp
QSize Ticker::sizeHint() const
{
    return fontMetrics().size(0, text());
}
```

`sizeHint()` 函数返回文本所需的空间作为小部件的理想尺寸。`QWidget::fontMetrics()` 返回一个 `QFontMetrics` 对象，可以通过它查询获取与小部件字体相关的信息。在这种情况下，我们请求给定文本的大小。（`QFontMetrics::size()` 的第一个参数是一个简单字符串不需要的标志，所以我们只需传递 0 即可。）

```cpp
void Ticker::paintEvent(QPaintEvent * /* event */)
{
    QPainter painter(this);
    int textWidth = fontMetrics().width(text());
    if (textWidth < 1)
        return;
    int x = -offset;
    while (x < width()) {
        painter.drawText(x, 0, textWidth, height(),
                         Qt::AlignLeft | Qt::AlignVCenter, text());
        x += textWidth;
    }
}
```

`paintEvent()` 函数使用 `QPainter::drawText()` 绘制文本。它使用 `fontMetrics()` 来确定文本所需的水平空间，然后根据考虑 `offset` 的情况下，多次绘制文本以填满小部件的整个宽度。

```cpp
void Ticker::showEvent(QShowEvent * /* event */)
{
    myTimerId = startTimer(30);
}
```

`showEvent()` 函数启动一个定时器。调用 `QObject::startTimer()` 返回一个 ID 数字，我们稍可以用它识别该定时器。`QObject` 支持多个独立的定时器，每个定时器都有自己的时间间隔。在调用 `startTimer()` 后，Qt 大约每 30 毫秒生成一次定时器事件；精度取决于底层操作系统。

我们本可以在 `Ticker` 构造函数中调用 `startTimer()`，但通过仅在小部件真正可见时让 Qt 生成定时器事件，我们可以节省一些资源。

```cpp
void Ticker::timerEvent(QTimerEvent *event)
{
    if (event->timerId() == myTimerId) {
        ++offset;
        if (offset >= fontMetrics().width(text()))
            offset = 0;
        scroll(-1, 0);
    } else {
        QWidget::timerEvent(event);
    }
}
```

系统按间隔调用 `timerEvent()` 函数。它将 `offset` 加 1 以模拟移动，并在文本宽度处折回。然后它使用 `QWidget::scroll()` 将小部件的内容向左滚动一个像素。调用 `update()` 代替 `scroll()` 就足够了，但 `scroll()` 更高效，因为它只是移动了屏幕上现有的像素，并仅为小部件新显示的区域（在本例中为 1 像素宽的条带）生成绘制事件。

如果定时器事件不是我们感兴趣的定时器，我们将其传递给基类。

```cpp
void Ticker::hideEvent(QHideEvent * /* event */)
{
    killTimer(myTimerId);
    myTimerId = 0;
}
```

`hideEvent()` 函数调用 `QObject::killTimer()` 来停止定时器。定时器事件是底层的，如果我们需要多个定时器，跟踪所有的定时器 ID 会变得很繁琐。在这种情况下，为每个定时器创建一个 `QTimer` 对象通常更简单。`QTimer` 在每个时间间隔处发射 `timeout()` 信号。`QTimer` 还为单次定时器（仅超时一次的定时器）提供了方便的接口，正如我们在第 6 章（第 158 页）中看到的。

## 7. 事件处理

![](img/1bc72df8c60cf85926d3aefcc273027d_273_0.png)

### 重新实现事件处理器

安装事件过滤器

在密集处理期间保持响应式

事件是由窗口系统或 Qt 自身响应各种情况而生成的。当用户按下或释放按键或鼠标按钮时，会生成按键事件或鼠标事件；当窗口首次显示时，会生成一个绘制事件，告诉新可见的窗口它需要绘制自己。大多数事件是响应用户操作生成的，但某些事件（如定时器事件）是由系统独立生成的。

当我们使用 Qt 编程时，很少需要考虑事件，因为当发生重要事情时，Qt 小部件会发射信号。只有当我们编写自己的自定义小部件或想要修改它的行为时，事件就变得有用了。

### 重新实现事件处理器

在 Qt 中，事件是子类的实例。Qt 处理超过百种类型的事件，每种类型都由一个枚举值标识。例如，`QEvent::type()` 对于鼠标按键事件返回 `QEvent::MouseButton`。许多事件类型所需的信息比纯 `QEvent` 对象能存储的更多；例如，鼠标事件需要存储是哪个鼠标按钮触发了事件，以及在事件发生时指针的位置。

事件通过对象继承自 `QObject` 的 `event()` 函数通知。`QWidget` 中的 `event()` 实现将最常见的事件类型转发给特定的事件处理器。

在前面的章节中实现 `MainWindow`、`IconEditor` 和 `Plotter` 时，我们已经看到了许多事件处理器。`QEvent` 参考中列出了许多其他类型的事件，也可以创建自定义事件类型并由我们自己分发事件。在这里我们将回顾两个值得进一步解释的常见事件类型：按键事件和定时器事件。

按键事件通过重新实现 `keyPressEvent()` 和 `keyReleaseEvent()` 来处理。`Plotter` 小部件重新实现了 `keyPressEvent()`。通常情况下，我们只需要重新实现 `keyPressEvent()`，因为释放释放重要的是修饰键 Ctrl、Shift 和 Alt，我们可以在 `keyPressEvent()` 中使用 `QKeyEvent::modifiers()` 检查这些。例如，如果我们正在实现一个 `CodeEditor` 小部件，其区分 Home 和 Ctrl+Home 的精简 `keyPressEvent()` 如下所示：

```cpp
void CodeEditor::keyPressEvent(QKeyEvent *event)
{
    switch (event->key()) {
    case Qt::Key_Home:
        if (event->modifiers() & Qt::ControlModifier) {
            goToBeginningOfDocument();
        } else {
            goToBeginningOfLine();
        }
        break;
    case Qt::Key_End:
        ...
    default:
        QWidget::keyPressEvent(event);
    }
}
```

Tab 键和 Backtab（Shift+Tab）键是特殊情况。`QWidget::event()` 在调用 `keyPressEvent()` 之前处理它们，其语义是将焦点传递给焦点链中的下一个或上一个小部件。这种行为通常是我们想要的，但在 `CodeEditor` 小部件中，我们可能希望让 Tab 缩进一行。那么 `event()` 的重新实现将如下：

```cpp
bool CodeEditor::event(QEvent *event)
{
    if (event->type() == QEvent::KeyPress) {
        QKeyEvent *keyEvent = static_cast<QKeyEvent *>(event);
        if (keyEvent->key() == Qt::Key_Tab) {
            insertAtCurrentPosition('\t');
            return true;
        }
    }
    return QWidget::event(event);
}
```

如果事件是按键，我们将 `QEvent` 对象强制转换为 `QKeyEvent` 并检查按了哪个键。如果键是 Tab，我们将进行一些处理并返回 `true` 以告诉 Qt 我们已经处理了该事件。如果我们返回 `false`，Qt 将把事件传递给父小部件。

实现按键绑定的一种更高级的方法是使用 `QAction`。例如，如果 `goToBeginningOfLine()` 和 `goToBeginningOfDocument()` 是 `CodeEditor` 小部件中的公共槽函数，且 `CodeEditor` 被用作 `MainWindow` 类中的中心部件，我们可以通过以下代码添加按键绑定：

```cpp
MainWindow::MainWindow()
{
    editor = new CodeEditor;
    setCentralWidget(editor);

    goToBeginningOfLineAction = new QAction(tr("Go to Beginning of Line"), this);
    goToBeginningOfLineAction->setShortcut(tr("Home"));
    connect(goToBeginningOfLineAction, SIGNAL(activated()),
            editor, SLOT(goToBeginningOfLine()));

    goToBeginningOfDocumentAction = new QAction(tr("Go to Beginning of Document"), this);
    goToBeginningOfDocumentAction->setShortcut(tr("Ctrl+Home"));
    connect(goToBeginningOfDocumentAction, SIGNAL(activated()),
            editor, SLOT(goToBeginningOfDocument()));

    ...
}
```

这使得很容易向菜单或工具栏添加命令，正如我们在第 3 章中看到的那。如果命令没有出现在用户界面中，可以将 `QAction` 对象替换为 `QShortcut` 对象，这是 `QAction` 内部用于支持按键绑定的类。

默认情况下，在小部件上使用 `QAction` 或 `QShortcut` 设置的按键绑定只要包含该小部件的窗口激活就会启用。可以使用 `QAction::setShortcutContext()` 或 `QShortcut::setContext()` 进行更改。另一种常见的事件类型是定时器事件。虽然大多数其他事件类型是用户操作的结果，但定时器事件允许应用程序按定期执行处理。定时器事件可以实现闪烁光标和其他动画，或仅仅刷新显示。

为了演示定时器事件，我们将实现图 7.1 所示的 `Ticker` 小部件。该小部件显示一个文本横幅，每 30 毫秒向左滚动一个像素。如果小部件比文本宽，则文本会重复所需的次数以填充小部件的整个宽度。

**图 7.1. `Ticker` 小部件**

![](img/1bc72df8c60cf85926d3aefcc273027d_276_0.png)

这是头文件：

代码视图：

```cpp
#ifndef TICKER_H
#define TICKER_H

#include <QWidget>

class Ticker : public QWidget
{
    Q_OBJECT
    Q_PROPERTY(QString text READ text WRITE setText)
public:
    Ticker(QWidget *parent = 0);
    void setText(const QString &newText);
    QString text() const { return myText; }
    QSize sizeHint() const;
protected:
    void paintEvent(QPaintEvent *event);
    void timerEvent(QTimerEvent *event);
    void showEvent(QShowEvent *event);
    void hideEvent(QHideEvent *event);
private:
    QString myText;
    int offset;
    int myTimerId;
};

#endif
```

我们在 `Ticker` 中重新实现了四个事件处理器，其中三个是我们在之前未见过的：`timerEvent()`、`showEvent()` 和 `hideEvent()`。

现在让我们回顾一下实现：

```cpp
#include <QtGui>

#include "ticker.h"

Ticker::Ticker(QWidget *parent)
    : QWidget(parent)
{
    offset = 0;
    myTimerId = 0;
}
```

构造函数将 `offset` 变量初始化为 0。绘制文本的 `x` 坐标来源于 `offset` 值。定时器 ID 总是非零的，因此我们使用 0 表示没有启动定时器。

```cpp
void Ticker::setText(const QString &newText)
{
    myText = newText;
    update();
    updateGeometry();
}
```

`setText()` 函数设置要显示的文本。它调用 `update()` 请求重绘，并调用 `updateGeometry()` 通知负责 `Ticker` 小部件的任何布局管理器尺寸提示（size hint）发生了变化。

```cpp
QSize Ticker::sizeHint() const
{
    return fontMetrics().size(0, text());
}
```

`sizeHint()` 函数返回文本所需的空间作为小部件的理想尺寸。`QWidget::fontMetrics()` 返回一个 `QFontMetrics` 对象，可以通过查询它获取与小部件字体相关的信息。在这种情况下，我们请求给定文本所需的尺寸。（`QFontMetrics::size()` 的第一个参数是一个简单字符串不需要的标志，所以我们只需传递 0 即可。）

```cpp
void Ticker::paintEvent(QPaintEvent * /* event */)
{
    QPainter painter(this);
    int textWidth = fontMetrics().width(text());
    if (textWidth < 1)
        return;

    int x = -offset;
    while (x < width()) {
        painter.drawText(x, 0, textWidth, height(),
                         Qt::AlignLeft | Qt::AlignVCenter, text());
        x += textWidth;
    }
}
```

`paintEvent()` 函数使用 `QPainter` 绘制文本。它使用 `fontMetrics()` 确定文本所需的空间，并根据需要重复绘制以填充小部件的宽度，将其考虑入。

```cpp
void Ticker::showEvent(QShowEvent *)
{
    myTimerId = startTimer(30);
}
```

`showEvent()` 函数启动定时器。调用 `startTimer()` 返回一个 ID，稍后可以用它标识定时器。定时器事件是底层的，如果我们需要多个定时器，跟踪所有定时器 ID 将变得繁琐。在这种情况下，为每个定时器创建一个 `QTimer` 对象通常更简单。`QTimer` 在每个间隔发射 `timeout()` 信号。`QTimer` 还为单次定时器（超时一次的定时器）提供了方便的接口，正如我们在第 6 章（第 158 页）所示。

```cpp
void Ticker::timerEvent(QTimerEvent *event)
{
    if (event->timerId() == myTimerId) {
        ++offset;
        ...
    }
}
```
