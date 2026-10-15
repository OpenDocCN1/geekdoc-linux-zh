
```cpp
void DrawWidget::moveEvent(MouseEvent *e) {
    if (count < MAXPOINTS) {
        QPainter painter(this);
        points[count] = e->pos(); // 添加点
        painter.setPen(*color);
        painter.drawRect(points[count].x()-3, points[count].y()-3, 6, 6);
        count++;
    }
}
```

## 测试 DrawWidget

示例绘图部件的实现非常简单。创建一个应用程序部件、添加绘图部件并处理 X Windows 事件更为简单。包含 `main` 函数的测试文件 `main.cpp` 位于 `src/Qt/events` 目录。唯一需要的包含文件是 `draw.hxx`，因为 `draw.hxx` 包含了所需的 Qt 头文件：

```cpp
#include "draw.hxx"
```

# 用户界面编程

`main` 函数定义了 `QApplication` 类的实例和示例 `DrawWidget` 类的实例。`QApplication::setMainWidget` 指定绘图部件是应用程序中的顶层部件。`show` 方法继承自 `QWidget` 类并使绘图部件可见。`QApplication` 方法处理 X Windows `argv`；

```cpp
int main(int argc, char **argv) {
    QApplication app(argc, argv);
    DrawWidget draw;
    app.setMainWidget(&draw);
    draw.show();
    return exec();
}
```

这个简短的示例说明 Qt 类库确实封装了 X Windows 编程的大部分复杂性。如果需要，你可以将低级 Xlib 编程与 Qt 类库结合使用，但这通常不需要，因为 Qt 支持绘制原语。

图 31.1 显示了带有涂鸦的绘图程序。

图 31.1

`main.cxx` 程序使用了 `DrawWidget`。

![](img/66f6e6c242a0e6a79aeee4012c6ff547_549)

# 使用槽（Slots）处理事件

Qt C++ 类包含了各种实用的部件。查看所有不同 Qt 部件最好的方法可能是进入 Qt 分发中包含的示例目录，然后编译并运行所有示例。当我开始使用 Qt 时，这个练习大约需要 20 分钟，它是对 Qt 类库很好的介绍。

我们在本节将使用 Qt 部件类 `LCDNumber`。`LCDNumber` 部件在部件内部大字体显示数字。`LCDNumber` 类有一个设置显示数字的方法，对于我们的示例程序，我们想要定义两个增加减少数字的槽。正如后面所示，将点击 Qt 按钮产生的信号连接到这些槽很容易。

为了演示使用槽和信号处理事件，我们将创建一个新类 `StateLCDWidget`，它包含类头文件中定义的两个槽：

```cpp
void increaseValue();
void decreaseValue();
```

你将在下一节看到如何使用 Qt 部件的槽：在本节中，我们将实现 `StateLCDWidget` 类和两个槽。下面的列表显示了 `StateLCDWidget` 类的完整头文件，它位于 `src/qt/signals_slots` 目录下的 `state_lcd.hxx` 文件中（列表后有讨论）：

```cpp
#include <widget.h>
#include <lcdnumber.h>
```

### 用户界面的编程

第四部分

```cpp
class StateLCDWidget : public QWidget {
Q_OBJECT
public:
    StateLCDWidget(QWidget *parent=0, const char *name=0);
    public slots:
    void increaseValue();
    void decreaseValue();
protected:
    void resizeEvent(QResizeEvent *);
private:
    QLCDNumber *lcd;
    int value;
};
```

`qwidget.h` 和 `qlcdnumber.h` 头文件包含了 Qt 库中 `QWidget` 和 `LCDNumber` C++ 类的定义。对于实际应用，`StateLCDWidget` 通常会派自 `LCDNumber` 类，但为了演示如何定义槽（slots）的简单示例，通过包含关系来派生 `StateLCDWidget` 类会稍微简单一些。`StateLCDWidget` 类包含一个 `LCDNumber` 类的实例。

在 `state_lcd.hxx` 文件中，我们看到了一些看起来不合法的代码：

```cpp
Q_OBJECT

public slots:
    void increaseValue();
    void decreaseValue();
```

`Q_OBJECT` 符号导致 `moc` 工具生成“元对象协议”信息，允许在运行时检查对象以确定其某些类属性。对元对象协议的支持已内置在某些如 Common LISP/CLOS 这样的面向对象的编程系统中。Qt 的架构师基于对对象进行运行时内省（introspection）的思想构建系统，以支持将代码绑定到特定对象的槽上，而不是该类的所有实例。

> **注意**
>
> `slots` 令牌不是 C++ 中的保留字。

C++ 编译器会编译此内容，在 Qt 头文件 `qwidget.h` 中，`slots` 令牌被定义为空。当我们使用此小部件构建程序时，我们必须在 `Makefile` 中添加命令来运行 Qt 实用程序 `moc`，它会为该类创建一个带有额外代码的新 C++ 源文件。

### 使用 Qt 进行 GUI 编程

第 31 章

在位于 `state_lcd.cxx` 文件中的 `StateLCDWidget` 类实现之后，我们将再次查看 `moc`。我们需要两个文件来定义 `StateLCDWidget` 和 `QLCDNumber` 小部件：

```cpp
#include "state_lcd.hxx"
#include <qlcdnumber.h>
```

类构造函数非常简单；它调用父类 `QWidget` 构造函数并创建一个 `QLCDNumber` 类的实例，在 `LCDNumber` 实例中指定最大四个数字：

```cpp
StateLCDWidget::StateLCDWidget(QWidget *parent, const char *name)
  : QWidget(parent, name) {
  lcd = new QLCDNumber(4, this, "lcd")
}
```

需要 `resizeEvent` 方法来处理大小调整事件，并通过调用 `QLCDNumber` 类方法来实现：

```cpp
void StateLCDWidget::resizeEvent(QResizeEvent *) {
lcd->resize(width(), height() - 21);
}
```

在这里，`width` 和 `height` 用于计算 `LCDNumber` 实例的大小。`width` 和 `height` 方法指的是 `StateLCDWidget`；这些方法继承自 `QWidget` 类。类实现的其余部分是两个方法 `increaseValue` 和 `decreaseValue` 的定义，它们增加和减少私有变量：

```cpp
void StateLCDWidget::increaseValue() {
value++;
lcd->display(value);
}
```

```cpp
void StateLCDWidget::decreaseValue() {
value--;
lcd->display(value);
}
```

现在我们将讨论槽的创建和 Qt `moc` 工具。我们将涵盖在本节中定义的 `StateLCDWidget` 类以及下一节开发的 `UpDownWidget` 类对 `moc` 的使用。`Makefile` 文件中的以下规则规定了程序如何处理使用信号和槽的源文件：

```make
moc_state_lcd.hxx: state_lcd.hxx
$(MOC) state_lcd.hxx -o moc_state_lcd.cxx
```

```make
moc_up_down.cxx: up_down.hxx
$(MOC) up_down.hxx -o moc_up_down.cxx
```

![](img/66f6ec242e6a79a012cff547_)
