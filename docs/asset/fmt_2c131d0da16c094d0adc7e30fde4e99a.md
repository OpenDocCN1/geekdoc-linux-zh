
*(注：原文文本第20-35行逻辑存在代码片段错乱或重复，翻译时已根据语意进行了逻辑对齐)*

`FollowMouse`构造函数从第16行开始，初始化`QSplitter`。第19行创建了`QMultiEdit`。第20行将其设置为只读，第21行开启了鼠标追踪。

第23行创建了`MouseSensor`实例。第24行设置其最小宽度为80。

第26-27行将`sensor`的`description`信号连接到`this`的`newline`槽。

第29行调整窗口大小为10。第31行的`newline`槽接收一个`QString`参数。

第33行将字符串追加到`edit`中。

每当选中顶部按钮时，就会调用`relButton`的`grabMouse()`方法，导致`relButton`捕获鼠标。向`grabMouse()`传递光标定义会在捕获期间修改光标的外观。由于是由`relButton`执行了捕获，它是唯一对鼠标做出响应的控件，并且它通过调用`releaseMouse()`将鼠标控制权返回给系统。

## 修改光标的外观

你可以使用一组标准的内置光标来通知程序的当前状态。更改光标的方法位于`QWidget`中，因此任何显示对象都可以更改其光标。

当你更改光标的外观时，该更改仅适用于你指定的区域。例如，如果你更改了顶层窗口的光标，标题栏将不会改变，但作为你顶层窗口子控件或孙控件的每个控件都会发生改变。然而，如果其中一个子控件有自己的光标设置，它（以及它的所有后代）将继承它自己的设置。

下面的示例允许你在所有标准光标中进行动态选择。你可以将一个光标应用到整个窗口，并将另一个光标应用到窗口内的单个按钮。如图 8-3 所示，光标名称列在左侧。每当选中某个光标名称时，它就会成为整个窗口的默认光标。使用右侧的“Select”按钮会将当前选中的光标更改为其自身的私有光标——也就是说，它的光标不再继承自父控件。

> 图 8-3：光标选择列表

![](img/c47d54674a4d92abc6eebed0dd05f5fb_203_0.png)

### CursorMouse Header

```cpp
1 /* cursormouse.h */
2 #ifndef CURSORMOUSE_H
3 #define CURSORMOUSE_H
```

# 第 8 章 ✦ 鼠标与键盘 185

```cpp
4
5 #include <layout.h>
6 #include <qpushbutton.h>
7
8 class CursorMouse: public QWidget
(
10 Q_OBJECT
11 public:
12 CursorMouse(QWidget *parent=0, const char *name=0);
13 private:
14 QQPushButton *selectButton;
15 QQPushButton *exitButton;
16 int cursorID;
17 slots:
18 void changeCursor(int);
19 void selectCursor();
20 void shutdown();
21 );
22
23 #endif
```

`CursorMouse`类包含三个槽。其中两个用于更改光标，第三个用于退出程序。在第16行定义的`cursorID`存储当前选中光标的 ID。

### CursorMouse

```cpp
1 /* cursormouse.cpp */
2 #include <kapp.h>
3 #include <qcursor.h>
4 #include <qlistbox.h>
5 #include "cursourse.h"
6
7 struct cursStruct {
8 QCursor name;
9 int number;
10 curs[] = {
11 "ArrowCursor",ArrowCursor,
12 "UpArrowCursor",UpArrowCursor,
13 "CrossCursor",CrossCursor,
14 "WaitCursor",WaitCursor,
15 "IbeamCursor",IbeamCursor,
16 "SizeCursor",SizeCursor,
17 "SizeHorCursor",SizeHorCursor,
18 "SizeDiagCursor",SizeBDagCursor,
19 "SizeDiagCursor",SizeDiagCursor,
20 "SizeAllCursor",SizeAllCursor,
21 "BlankCursor",BlankCursor,
22 "SplitVCursor",SplitVCursor,
23 "SplitHCursor",SplitHCursor"}
```

# 186 第二部分 - 步步为营

```cpp
24      (*PointingHandCursor*.PointingHandCursor ),
25      ("BitmapCursor*.BitmapCursor \)
26 );
27
28  int main(int argc, char **argv)
29  {
30      KApplication app(argc,argv,"cursormouse");
31      CursorMouse = new CursorMouse();
32      cursormouse->show();
33      app.setMainWindow(cursormouse);
34
35      return(app.exec());
36  }
37  CursorMouse::CursorWidget(QWidget *parent,const char *name)
38      : QWidget(parent,name)
39  {
40      QHBoxLayout *horlayout = new QHBoxLayout(this);
41      QList *list = new QList(this);
42      for(int i=0; i<size(curs)/size(cursStruct); i++)
43          list->insertItem(curs[i].name);
44      horlayout->addWidget(list);
45      connect(list,SIGNAL(highlighted(int)),
46               this,SLOT(changeCursor(int)));
47  }
48
49  QVBoxLayout *vertlayout = new QVBoxLayout(this);
50  selectButton = new QPushButton("Select");
51  selectButton->setMinimumSize(selectButton->sizeHint());
52  vertlayout->addWidget(selectButton);
53  connect(selectButton,SIGNAL(clicked()),
54           this,SLOT(selectCursor()));
55
56
57  exitButton = new QPushButton("Exit");
58  exitButton->setMinimumSize(exitButton->sizeHint());
59  vertlayout->addWidget(exitButton);
60  connect(exitButton,SIGNAL(clicked()),
61           this,SLOT(shutdown()));
62
63  CursorMouse::changeCursor(int id)
64  {
65      cursorID = id;
66      setCursor(curs[cursorID].name);
67  }
68
69  CursorMouse::selectCursor()
70  {
71      for(int i=0; i<size(curs)/size(cursStruct); i++)
72          list->setCurrentItem(i);
73  }
74
75  void CursorMouse::shutdown()
76  {
77      close();
78  }
```
