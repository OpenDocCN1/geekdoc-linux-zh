
当布局方向为水平时，`packStart()` 方法在左侧插入小部件，而 `packEnd()` 方法在右侧插入。结果见图 3-13。

| container | | | | | |
| --- | --- | --- | --- | --- |
| startONE | startTWO | startTHREE | endTWO | endONE |

**图 3-13:** 水平组织小部件的 `KContainerLayout`

## KContainer 实例

本章中之前所有的示例都是内部创建了某种布局管理器的小部件。然而，由于 `KContainerLayout` 也是一个小部件，因此它可以被扩展而不仅仅是被使用。也就是说，该小部件不再拥有布局对象，它本身就是一个布局对象。以下创建一个能够包含其他小部件的小部件的示例。

### Main

```cpp
/* main.cpp */
#include <kapp.h>
#include "iscontainer.h"

int main(int argc, char **argv)
{
  KApplication app(argc, argv);
  ISContainer *iscontainer = new ISContainer();
  iscontainer->show();
  app.setMainWidget(iscontainer);
  return(app.exec());
}
```

该小部件 own任何其他小部件一样被对待。它在第 8 行创建，并在第 10 行设置为主窗口小部件。无论它是有布局组件还是本身就是布局组件，只要它是一个小部件即可。

## IsContainer Header

```cpp
/* iscontainer.h */
#ifndef ISCONTAINER_H
#define ISCONTAINER_H

#include <qwidget.h>
#include <kcontainer.h>
#include <QPushButton.h>

class IsContainer: public KContainerLayout
public:
 IsContainer(QWidget *parent=0, const char *name=0);
 ~IsContainer();
private:
 QPushButton *One;
 QPushButton *Two;
 QPushButton *Three;

};
#endif
```

该类定义与之前示例中的类的区别在于，在第 8 行，`IsContainer` 继承自 `KContainerLayout` 而不是直接继承自 `QWidget`。`IsContainer` 类仍然是一个小部件，因为 `KContainerLayout` 继承自 `QWidget`。

## IsContainer

```cpp
/* iscontainer.cpp */
#include "iscontainer.h"

IsContainer::IsContainer(QWidget *parent, const char *name)
: KContainerLayout(parent,name)
{
 setOrientation(KContainerLayout::Vertical);

 One = new QPushButton(this);
One->setText("BUTTON ONE");
One->setMinimumSize(One->sizeHint());
packStart(One);
Two = new QPushButton(this);
Two->setText("BUTTON TWO");
Two->setMinimumSize(Two->sizeHint());
packStart(Two);

Three = new QPushButton(this);
Three->setText("BUTTON THREE");
Three->setMinimumSize(Three->sizeHint());
packStart(Three);

resize(10,10);
}
```

`Widget`类等由第 5 行的代码初始化。第 7 行将方向设置为垂直。第 9 到 22 行通过调用 `packStart()` 为容器添加三个按钮。结果布局如图 3-14 所示。

![](img/c47d54674a4d92abc6eebed0dd05f5fb_76_0.png)

带有三个子部件的小部件容器布局

## 小部件内部的小部件（水平）

由于 `KContainerLayout` 是一个小部件并且具有包含其他小部件的能力，它可以包含 `KContainerLayout` 小部件。以下示例是垂直 `KContainerLayout` 小部件中的水平 `KContainerLayout` 小部件集合。该示例还展示了创建容器并添加子部件时使用不同组合的效果。

### Main

```cpp
/* main.cpp */
#include <kapp.h>
#include "horizlayout.h"
int main(int argc, char **argv)
{
 QApplication app(argc,argv,"horizlayout");
 HorizLayout *horizlayout = new HorizLayout();
 horizlayout->show();
 app.setMainWidget(horizlayout);
return(app.exec());
}
```

### HorizLayout Header

```cpp
/* horizlayout.h */
#ifndef HORIZLAYOUT_H
#define HORIZLAYOUT_H

#include <qwidget.h>
#include <kcontainer.h>
#include <QPushButton.h>

class HorizLayout: public QWidget
public:
 HorizLayout(QWidget *parent=0, const char *name=0);
 ~HorizLayout();
private:
 void add(KContainerLayout *layout, int count, bool homogeneous, bool expand, bool fill);
};
#endif
```

### HorizLayout

```cpp
/* horizlayout.cpp */
#include "horizlayout.h"
#include <QLabel.h>

HorizLayout::HorizLayout(QWidget *parent, const char *name)
: QWidget(parent,name)
{
 KContainerLayout *layout = new KContainerLayout(this,
 NULL,
 KContainerLayout::Vertical,
 FALSE,
 0,
 TRUE);

int count = 1;
add(layout,count++,FALSE,TRUE,TRUE);
add(layout,count++,TRUE,TRUE);
add(layout,count++,FALSE,TRUE);
add(layout,count++,TRUE,TRUE);
add(layout,count++,FALSE,FALSE);
add(layout,count++,TRUE,FALSE);
add(layout,count++,FALSE,FALSE);
add(layout,count++,TRUE,FALSE);

layout->sizeFit();
}

void HorizLayout::add(KContainerLayout *outer, int count, bool homogeneous, bool expand, bool fill)
{
 QPushButton *button;

 QString str("%1").arg(count);
 if (homogeneous)
```
