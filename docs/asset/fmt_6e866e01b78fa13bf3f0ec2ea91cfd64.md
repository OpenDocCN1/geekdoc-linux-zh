
```cpp
33 }
34 void Reminder::closeEvent(QCloseEvent *event)
35 {
36
37 QString str;
38 QConfig *config =
39 new QConfig(QDir::homePath() + "/.remember");
40 config->setGroup("Geometry");
41 config->writeEntry("width");
42 str.setNum(window.width());
43 config->writeEntry("height");
44 str.setNum(window.height());
45 config->writeEntry("xPosition");
46 str.setNum(windowPosition.x());
47 config->writeEntry("yPosition");
48 str.setNum(windowPosition.y());
49 config->sync();
50 delete config;
51
52 event->accept();
53 }
54 void Reminder::configure(
55 {
56 int width;
57 int height;
58 int x;
59 int y;
60 QString str;
61
62 QConfig *config =
63 new QConfig(QDir::homePath() + "/.remember");
64 config->setGroup("Geometry");
65 width = config->readNumEntry("width",100);
66 height = config->readNumEntry("height",100);
67 x = config->readNumEntry("xPosition",10);
68 y = config->readNumEntry("yPosition",10);
69
70 windowSize = QSize(width,height);
71 windowPosition = QPoint(x,y);
72
73 resize(windowSize);
74 move(windowPosition);
75 }
```

程序的 `main()` 函数从第8行开始。它创建了一个 `Remember` 小部件用作顶层窗口。在第12行，窗口显示之前，调用了 `configure()` 方法来读取配置数据并设置窗口的大小和位置。

第17行的 `paintEvent()` 方法使用一个 `QPainter` 对象，该对象会自动缩放其绘图以适应实际窗口大小。为了实现这一点，你调用 `setWindow()` 来建立宽度和高度的最大值，并使用这些维度填充矩形中的图形。图 17-4 显示了不同尺寸的 `Remember` 窗口。

![](img/c47d54674a4d92abc6eebed0dd05f5fb_429_0.png)

`Reminder` 小部件持续跟踪其当前的大小和位置。每当窗口大小发生时，就会调用第26行的 `resizeEvent()` 方法，每当窗口移动时，就会调用第30行的 `moveEvent()` 方法。这对方法不断更新存储在 `windowSize` 和 `windowPosition` 中的值。

每当应用程序被关闭时，就会调用第34行的 `closeEvent()` 方法。为了保存当前配置设置，通过在用户主目录下打开名为 `.remember` 的文件来创建一个 `KConfig` 对象。静态方法 `QDir::homePath()` 返回当前用户主目录的完整路径，这意味着每个用户为该程序使用一个独立的配置文件。

第40行的 `setGroup()` 调用指定了组名称——它位于包含配置信息的文件的内部。一个文件中可以有任意数量的组，相同的键值对可以出现在任意数量的组中。在任何时刻，`KConfig` 对象只能处理一个组，但你可以从一个组切换到另一个组。第40行的 `setGroup()` 调用指定了组名称——它位于包含配置信息的文件的内部。一个文件中可以有任意数量的组，相同的键值对可以出现在任意数量的组中。在任何时刻，`KConfig` 对象只能处理一个组，但你可以从一个组切换到另一个。

```
width=100
height=100
xPosition=10
yPosition=10
```

`Reminder` 是应用程序的顶层窗口。第12行和第13行的 `windowSize` 和 `windowPosition` 值存储了持续更新的窗口几何信息。

第17行的 `paintEvent()` 方法使用一个 `QPainter` 对象，该对象会自动缩放其绘图以适应实际窗口大小。为了实现这一点，你调用 `setWindow()` 来建立宽度和高度的最大值，并使用这些维度填充矩形中的图形。图 17-4 显示了不同尺寸的 `Remember` 窗口。

`Reminder` 小部件持续跟踪其当前的大小和位置。每当窗口大小发生时，就会调用第26行的 `resizeEvent()` 方法，每当窗口移动时，就会调用第30行的 `moveEvent()` 方法。这对方法不断更新存储在 `windowSize` 和 `windowPosition` 中的值。

每当应用程序被关闭时，就会调用第34行的 `closeEvent()` 方法。为了保存当前配置设置，通过在用户主目录下打开名为 `.remember` 的文件来创建一个 `KConfig` 对象。静态方法 `QDir::homePath()` 返回当前用户主目录的完整路径，这意味着每个用户为该程序使用一个独立的配置文件。

第40行的 `setGroup()` 调用指定了组名称——它位于包含配置信息的文件的内部。一个文件中可以有任意数量的组，相同的键值对可以出现在任意数量的组中。在任何时刻，`KConfig` 对象只能处理一个组，但你可以。

# Qt Widgets

`Widget` 是一个可显示类。在 Qt 中，所有类都继承自 `QWidget`。

## 第三部分 ✦ 参考与机制

### 第18章

#### 本章内容

- 确定每个小部件的构造函数特征
- 确定每个小部件所需的头文件
- 确定每个小部件的父类和子类
- 确定每个小部件可用的槽和信号
- 通过每个小部件的小示例开始学习

#### 继承自

`KColorButton` `KDialogButton` `KDirectionButton`

`KDockButton_Private` `IconButton` `KKeyButton` `KTabButton`

`QToolBar` `QCheckBox` `QRadioButton`

`QButton`

### QPushButton

该部件显示为一个包含文本的凸起矩形，会对鼠标做出响应并改变外观。

```cpp
#include <qbutton.h>
```

#### 基类

```cpp
QObject QPaintDevice QWidget
```

#### 构造函数

`QButton(QWidget *parent = 0, const char *name = 0, WFlags f = 0);`

#### 方法

`int accel() const;`

`bool autoRepeat() const;`

`bool autoResize() const;`

`bool focusNextPrevChild(bool next);`

`QButtonGroup *group() const;`

`bool isDown() const;`

`bool isToggle() const;`

`bool isOn() const;`

`bool isToggleButton() const;`

`const QPixmap *pixmap() const;`

`virtual void setAccel(int);`

`virtual void setAutoRepeat(bool);`

`virtual void setResize(bool);`

`virtual void setDown(bool);`

`virtual void setPixmap(const QPixmap &);`

`ToggleState state() const;`

`string text() const;`

`Toggle toggleType() const;`

#### 槽

`void animateClick();`

`void toggle();`

#### 信号

`void clicked();`

`void pressed();`

`void released();`

`void stateChanged(int);`

`void toggled(bool);`

#### 举举

`enum ToggleType ( SingleShot, Toggle, Tristate );`

`enum ToggleState ( Off, NoChange, On );`

# 第 18 章 ♦ Qt 控件 417
