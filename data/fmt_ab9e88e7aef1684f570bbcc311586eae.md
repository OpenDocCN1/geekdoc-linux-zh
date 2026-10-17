
# 第 14 章 使用混合模式方法构建应用程序

以`Xt`前缀开头的函数和变量属于 Xt Intrinsics 工具包。以`Xm`前缀开头的函数和变量属于 Motif 工具包。函数`XtVaAppInitialize()`用于初始化 Xt Intrinsics 并打开显示器。`XtVaCreateWidget()`和`XtVaManagedWidget()`用于创建和操作 Motif 推按钮控件。`XtAddCallback()`用于将函数与推按钮的动作关联。在这种情况下，回调函数是`popup()`和`godly()`。

列表 14-1 中的简单程序演示了如何操作来自 Motif 或 Look Open 等控件 set 的控件。然而，快速应用方法要求你使用应用程序框架和来自类库的面向对象的控件。这些基于对象的控件在用于 Qt/KDE 或 Java 程序之前，必须先进行适配。由于 Qt、KDE 和 Java 有它们自己的控件 set，只有当你必须连接到使用 Motif 或 Xt Intrinsics 的现有代码时，才需要使用 Motif 或 Xt Intrinsics。如果你必须连接到 Motif 控件，可以使用接口类将 Motif 和 Xt Intrinsics 控件与 Qt 和 KDE 连接起来。Qt 中提供的接口类还将节省直接调用 Xt Intrinsics 时所需的某些代码。

## 接口类

接口类是为函数、数据或其他类提供封装的类。接口类充当一种外装，允许某个事物以与其正常不同的方式出现。接口类为函数、数据段或另一个类贴上一个不同的面孔。接口类也称为适配器类（adapter classes）。在书中，我们使用接口类来使非面向对象的代码看起来是面向对象的。我们还使用接口类来让 Java 类看起来像 C++ 类，让 C++ 类看起来像 Java 类。在面向对象的环境中，我们希望一切事物都看起来像一个对象或某个对象的一部分。接口类帮助我们实现这一目标。

创建接口类涉及的基本原理是封装。我们将非面向对象的代码或异源类（alien class）封装在我们所选择的类类型内部。例如，假设我们有一个普通变量和一个函数：

```cpp
int PenguinType;
void setPenguinType(int);
```

如果我们想为`PenguinType`和`setPenguinType()`提供一个接口类，我们需要将它们封装在一个类内部并提供访问它们的方法。例如：

```cpp
class penguin(
private:
    int PenguinType;
    void setPenguinType(int);
public:
    setPenguin(int);
int getPenguin();
...
```

`penguin`类是一个接口类。变量`PenguinType`和函数`setPenguinType()`被封装（隐藏）在`penguin`类中。获取`PenguinType`的唯一方法是通过`penguin`类定义的方法。在这种情况下，这些方法是`setPenguin`和`getPenguin()`。

注意`PenguinType`和`setPenguinType`是私有的。私有类只能通过类的方法进行访问。公共成员（如`setPenguin()`和`getPenguin()`）可以被任何人访问。由于非面向代码已封装在`penguin`类中，我们现在可以将其视为一个对象，并像任何其他面向对象的类型一样声明它。例如，在：

```cpp
penguin PenguinType;
```

`Penguin`是类型为`penguin`的对象。我们现在可以使用它的方法访问`PenguinType`：

```cpp
Penguin.setPenguin();
cout << PenguinType.getPenguin() << endl;
```

这允许我们在面向对象程序的语境中，以面向对象的方式访问`PenguinType`和`setPenguinType()`。我们可以使用`setPenguin()`和`getPenguin()`方法来访问我们的非面向数据，因为它们已经定义：

```cpp
penguin::setPenguin(int X) {
    PenguinType = X;
}
```

```cpp
int penguin::getPenguin(void) {
    return PenguinType;
}
```

现在，由于我们的非面向数据被封装在一个类中，我们还可以使用它来创建一个新类。例如：

```cpp
class puffin : public penguin,
private:
    int Wings;
public:
    void fly();
    void land();
```

## 列表 14-2：使用接口类的 Motif 推按钮示例

```cpp
// 列表 14-2
// 接口 类示例
// 使用 Motif 推按钮。
#include <Xt.h>
#include <X.h>
#include <iostream.h>
#include <Xt/RowColumn.h>
#include <Xt/MessageB.h>
#include <Xt/PushB.h>
#include <stdlib.h>
#include <stdio.h>

void goodby(Widget,void*,void*);
void popup(Widget,void*,void*);

goid goodby(Widget,void*,void*) {
	exit(0);
}

void popup(Widget,void*,void*) {
	cout << "Penguin Greetings" << endl;
}

void main(int argc,char *argv[]) {
	XtContext App;
	Widget TopLevel, Rc, Pb;
	XtSetLanguageProc(XtVaInitialize(NULL,NULL,NULL,
&App,"Open Source",
	NULL,0,
&argv,NULL,NULL,NULL));
	Rc = XtCreateWidget("rowcol",XtRowColumnWidgetClass,
	TopLevel,NULL);
	Pb = XtCreateManagedWidget("Join The Penguin Stampede",
	mPushButtonWidgetClass,
	Rc,NULL);
	AddCallback(Pb,XMnactivateCallback,popup,
	"Penguin Principle");
	Pb = XtCreateManagedWidget("Penguin Out",
	mPushButtonWidgetClass,
	Rc,NULL);
	XtCallback(Pb,XMnactivateCallback,goodby,
	"Penguin Principle");
	XtManage(Rc);
	XtRealizeWidget(TopLevel);
	AppMainLoop(App);
```
