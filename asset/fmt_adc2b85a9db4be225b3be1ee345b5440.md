
# 第 10 章 - 图形用户界面设计

## QButtonGroup 信号

所有信号都包含被选中控件的 ID 号。如果 `QButtonGroup` 是互斥的（包含单选按钮），它将只从组中发射一个信号：即被选中的控件。如果组是非互斥的，它将为用户的每次选择发射一个信号。你可以创建一个槽（slot）来处理这些信号。这在图 10-30 中所示。它展示了如果 `QButtonGroup` 包含单选按钮或复选框，它将如何发射信号，以及单个槽如何处理这些信号。

![](img/859df50987094e32dd2f5bb576f82bce_364_0.png)

## QButtonGroup 标题与对齐

`QButtonGroup` 显示组的标题。此标题应该描述组中的对象或设置：

```cpp
void setTitle(const char *Title)
```

可以通过调用 `setAlignment()` 方法将标题左对齐、右对齐或居中对齐：

```cpp
void setAlignment(int Align)
```

`Align` 可以有这些值：

- `AlignLeft` — 将标题左对齐
- `AlignRight` — 将标题右对齐
- `AlignCenter` — 将标题居中对齐

列表 10-7 创建了两个 `QButtonGroup` 对象。其中一个包含单选按钮，另一个包含复选框。

> 列表 10-7：一个构造两个包含单选按钮和复选框的 `QButtonGroup` 对象的程序

```cpp
#include <application.h>

#include <widget.h>

#include <qbuttongroup.h>

#include <radiobutton.h>

#include <qcheckbox.h>

int main(int argc, char *argv[])

{

    QApplication App(argc,argv);

    QWidget *Window = new QWidget();

    Window->setGeometry(100,100,250,400);

    QButtonGroup *Group1 = new QButtonGroup("Drives", Window);

    QRadioButton *hda1 = new QRadioButton("hda1", Window);

    QRadioButton *hdb1 = new QRadioButton("hdb1", Window);

    QRadioButton *hdc1 = new QRadioButton("hdc1", Window);

    Group1->insert(hda1);

    Group1->insert(hdb1);

    Group1->insert(hdc1);

    QButtonGroup *Group2 = new QButtonGroup("Install Packages", Window);

    QCheckBox *Java = new QCheckBox("Java", Window);

    QCheckBox *Ccheck = new QCheckBox("C++", Window);

    QCheckBox *Qt = new QCheckBox("Qt", Window);

    QCheckBox *KdeCheck = new QCheckBox("KDE", Window);

    QCheckBox *NoneCheck = new QCheckBox("None", Window);

    Group2->insert(Java);

    Group2->insert(Ccheck);

    Group2->insert(Qt);

    Group2->insert(KdeCheck);

    Group2->insert(NoneCheck);

    Group1->setAlignment(AlignLeft);

    Group2->setAlignment(AlignLeft);

    App.setMainWidget(Window);

    Window->show();

    return App.exec();

}
```

## 列表框（List Box）

列表框（List Box）是另一种选择控件。它是一个矩形框，包含一个对象的设置或值的列表。可以从列表中选择单个或多个值。选择是通过鼠标从列表中选择一个值然后双击它或按下 `Enter` 键完成的。当一个值或多个值被选中时，它们将以反色显示，直到被清除。列表框包含六或更多值。这些值可以以不可预测的方式排列，也可以进行排序。框在窗口上的位置是定的并具有固定大小。宽于列表的文本需要列表控件水平滚动。当然，列表将垂直滚动。

`Qt` 定义了一个列表框控件类。`QListBox` 定义了一个用于单选和多选的列表框控件。它声明在 `qlistbox.h` 中。它继承自 `QTableView`。图 10-32 显示了 `QListBox` 的类关系图。如你所示，`QListBox` 继承 `QTableView`，`QTableView` 继承 `QFrame`，`QFrame` 继承 `QWidget`。因此，`QWidget` 的公开保护方法对 `QListBox` 可用。

### 图 10-32：QListBox 的类关系图。

![](img/859df50987094e32dd2f5bb576f82bce_368_0.png)

这是 `QListBox` 的构造函数：

```cpp
QListBox::QListBox(QWidget *Parent=0,const char *Name=0,
    WFlags F=0)
```

你可以向列表框插入文本或像素图。存储在列表框中的项将有一个索引号。索引从 0 开始。列表框中的第一个项索引为 0。向列表框插入项有三种方法：

```cpp
QListBox::insertItem(const char *Text, int Index=-1)
```
