
加速器可以连接到任何类型的部件，只要它派生自`QObject`。快捷键通常用作菜单列表中频繁选择项目的快捷方式。`QPopupMenu`有一种非常方便的方法，使用`QAccel`对象来关联快捷键：

```cpp
insertItem(const char *Text, const QObject *Receiver,
const char *Member, int Accel=0)
```

使用此版本的`insertItem()`，你可以将插入的项目与动作和快捷键连接起来。`Text`是项目描述，`Accel`是组合键。快捷键显示在项目文本旁边。

这是使用这种方法的优点之一：快捷键会与菜单项一起显示。使用加速器对象则不是这样，你必须手动将快捷键添加到菜单中。与这种方法相比，使用`QAccel`对象也有一些优势。例如，可以向对象中插入多个组合键。你可以通过关联的`ID`数字来引用它们。它们还可以被临时禁用和启用。列表 6-3 是一个在菜单项中同时使用这两种技术的程序。

> 列表 6-3：一个在弹出菜单中使用快捷键的程序

```cpp
// 列表 6-3
// 一个使用 QAccel 对象和
// QPopupMenu::insertItem() 将快捷键与
// 动作连接的程序。
```

```cpp
#include <menubar.h>
#include <popupmenu.h>

#include <application.h>
#include <qkeycode.h>
#include <qaccel.h>
#include <qlineedit.h>
#include <qlabel.h>

int main(int argc, char *argv[]) {
    QApplication App(argc, argv);

    QWidget *Window = new QWidget();
    Window->setGeometry(10,160,250,250);

    QLineEdit *EditBox = new QLineEdit(Window);
    EditBox->setGeometry(10,150,200,30);

    QLabel *Label = new QLabel("Remove this Label*",Window);

    QMenuBar *MenuBar = new QMenuBar();
    QMenu *Menu1 = new QMenu();
    QMenu *Menu2 = new QMenu();

    MenuBar->insertMenu("Choice 1", Menu1);
    Menu1->insertAction("Choice 2", Menu2);

    Menu2->insertAction("Edit Box,Ctrl + E");
    Menu2->insertAction("Label,Shift + L");

    // 构建加速器对象并插入快捷键
    QAccel *Accelerators = new QAccel(Window);
    Accelerators->insertItem(CTRL + Key_E,200);
    Accelerators->insertItem(SHIFT + Key_L,300);

    // 使用两种方法将快捷键与动作连接起来
    Menu1->insertAction("Quit",qApp,SLOT(quit()),ALT_Key_F4);
    Accelerators->connectItem(200,EditBox,SLOT(clear()));
    Accelerators->connectItem(300,Label,SLOT(clear()));

    App.setMainWidget(Window);
    Window->show();

    return App.exec();
}
```
