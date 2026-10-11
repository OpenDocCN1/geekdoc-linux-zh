
```cpp
layout->addWidget(leftButton);

centerButton = new QPushButton(this);

centerButton->setText("Center");

layout->addWidget(centerButton);

rightButton = new QPushButton(this);

rightButton->setText("Right");

layout->addWidget(rightButton);

defaultButton = new QPushButton(this);

defaultButton->setText("Default");

layout->addWidget(defaultButton);

resize(10,10);

}

VBoxAlign::~VBoxAlign()

{

}
```

# 48

## 第一部分 ♦ 入门

```cpp
8   Layout *layout = new Layout();
9   layout->show();
10  app.setMainWidget(layout);
11  return(app.exec());
12 }
```

### LayoutLayout 头文件

```cpp
1 /* *layoutlayout.h */
2 #ifndef LAYLAYOUT_H
3 #define LAYLAYOUT_H

5 #include <qwidget.h>
6 #include <qlayout.h>
7 #include <qlcdnumber.h>
8 #include <qpbutton.h>
9 #include <qslider.h>

11 class LayoutLayout: public QWidget
12 {
13 public:
14     LayoutLayout(QWidget *parent=0, const char *name=0);
15     ~LayoutLayout() : {};
16 private:
17     QLCDNumber *lcd;
18     QPushButton *openButton;
19     QPushButton *saveButton;
20     QPushButton *saveasButton;
21     QPushButton *exitButton;
22     SliderSlider *slider;
23 };

25 #endif
```

该类定义包含了要显示的六个控件。尽管它们将由布局管理器放置和调整大小，但它们都是 `Layoutlayout` 控件类的成员变量。这里涉及到两个层级结构，但布局层级与控件层级无关。布局层级仅的作用是在地理位置上定位控件并调整大小；但为了起作用，每个控件（用于主窗口的顶层控件除外）必须在控件树中有一个父对象。

### LayoutLayout

```cpp
1 /* *layoutlayout.cpp */
2 #include "layoutlayout.h"

4 LayoutLayout::LayoutLayout(QWidget *parent,const char *name)
5     : QWidget(parent,name)
6 {
```

# 第 3 章 * 在窗口中布局控件 49

```cpp
7 QGridLayout *layout = new QGridLayout(this,2,2,3);
8 lcd = new QLCDNumber(this);
9 lcd->setNumDigits(2);
11 lcd->display(43);
12 lcd->setMinimumSize(100,100);
13 layout->addWidget(lcd,0,0);

15 QVBoxLayout *verticalLayout = new QVBoxLayout(this);
16 layout->addWidget(verticalLayout,0,1);

18 openButton = new QPushButton("Open",this);
19 openButton->setMinimumSize(openButton->sizeHint());
20 verticalLayout->addWidget(openButton);

22 saveButton = new QPushButton("Save",this);
23 saveButton->setMinimumSize(saveButton->sizeHint());
24 verticalLayout->addWidget(saveButton);

26 saveAs = new QPushButton("Save As...",this);
27 saveAs->setMinimumSize(saveAs->sizeHint());
28 verticalLayout->addWidget(saveAs);

30 exitButton = new QPushButton("Exit",this);
31 exitButton->setMinimumSize(exitButton->sizeHint());
32 verticalLayout->addWidget(exitButton);

34 slider = new QSlider(Qt::Horizontal,this);
35 slider->setMinimumSize(slider->sizeHint());
36 layout->addWidget(slider,1,0,1);

38 resize(10,10);
39 layout->activate();
40 )
```

主网格布局在第 7 行被创建为 2x2 网格。该参数指定它将作为 `Layout` 对象的主布局。网格布局在创建时也会在其所有内容周围安装一个 3 像素的边框。此控件要显示的每个项目都必须由此网格布局进行定位。（虽然可以在不包含在布局的情况下显示子控件，但它们在窗口中的位置将是预测的。）

第 9 行到第 13 行创建了一个 `QLCDNumber` 对象，用于显示两位数数字 43，并将其放置在网格的左上角。

第 15 行创建了一个垂直布局。该垂直布局没有指定父对象，因为它将是主布局的子级。事实上，紧下一行代码第 16 行调用了 `addLayout` 方法，将垂直布局插入到网格布局的右上角。这建立了层级结构：所创建的 `LayoutLayout` 对象位于顶层；第 7 行创建的 `QGridLayout` 位于下一层；第 15 行创建的 `QVBoxLayout` 位于第三层。注意，用于创建网格的参数将其确立为顶层容器。该参数未用于创建垂直布局，因此必须调用 `addLayout()` 来建立其层级结构。

> 一个 `QLayout` 在向其添加控件或布局之前必须有一个父对象。主布局必须是封装控件的子级，所有其他布局都必须是它的子级（或孙级）。

第 18 行到第 20 行创建了一个 `QPushButton` 并将其添加到垂直布局中。为按钮设置了最小尺寸，但没有最大尺寸，因此按钮将根据需要扩展以填充框。第 22 行到第 32 行在框中创建并添加了三个按钮。这导致了图 3-31 右上角所示的按钮列。

第 34 行到第 36 行创建了一个 `QSlider` 并将其附加到网格布局中，使其覆盖底部单元格。像按钮一样，它被分配了一个最小尺寸，但其大小是由网格布局要求的最小宽度和高度决定的。第 38 行调用 `resize()` 保证了 `Layout` 控件的初始大小是由网格布局要求的最小宽度和高度决定的。`Layout` 也是如图 3-12 所示的按钮组合。

![图 3-12](https://example.com/figure3-12.png)

# 第 3 章 在窗口中布局小部件

从尾部打包（packing）小部件的效果与从起始部相同，不同在于每个小部件都将放置在底部的下一个可用位置。第一个添加到底部的按钮是第 25 到 27 行创建的，并通过调用 `packEnd()` 添加的。在第 30 到 33 行创建并添加的按钮位于另一个从底部打包的按钮的正上方，而第 35 到 38 行的按钮则位于底部另外两个按钮的正上方。

当 `KContainerLayout` 调整大同时，执行的操作取决于小部件是如何添加的。从起始处添加的部件将保持在起始边缘（顶部或左侧），而从尾部添加的部件将保持在结束边缘（底部或右侧）。

要将打包布局的方向设置为水平方向，可以删除第 8 行的语句（因为水平是默认设置），或将其替换为以下内容：

```cpp
layout->setOrientation(KContainers::Horizontal);
```
