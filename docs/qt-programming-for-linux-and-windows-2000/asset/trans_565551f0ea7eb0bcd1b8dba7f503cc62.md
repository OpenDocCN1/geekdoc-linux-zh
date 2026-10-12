
公共槽：

```
void setText( const QString &s ) { msg->setText( s ); }
```

保护槽：

```
virtual void byebye();
```

私有：

```
QLabel *msg;
```

```
};
```

dialog.cpp

```
#include "dialog.h"

dialog::dialog( const QString &msg, const QPixmap &pix )
{
	QWidget( 0, 0, WStyle_Dialog|WType_Modal )

	// Something for the title bar
	setCaption( tr( "Alert!" ) );

	// Use the same pixmap for a window icon
	setIcon( pix );

	// Vertical layout (overall)
	QBoxLayout *top = new QVBoxLayout( this );
	// Horizontal layout for an icon and a message
	QHBoxLayout *hb = new QHBoxLayout();

	// The icon and the message get all the vertical stretch
	top->addLayout( hb, 5 );

	QLabel *l = new QLabel( this );
	l->setPixmap( pix );
	
	hb->addWidget( l, 1 );
	msg = new QLabel( msg, this );
	hb->addWidget( msg, 2 );

	// An OK button
	QPushButton *pb = new QPushButton( tr("OK"), this );
	connect( pb, SIGNAL(clicked()), SLOT(byebye()) );
	top->addWidget( pb );
}

void
dialog::byebye()
{
	delete this;
}

#include <dialog.moc>
```

当然，使用 QMessageBox 类来执行此操作要容易得多，但这更好地说明了一个顶级小部件。

小部件标志值通常仅用于顶级小部件。以下是当前的小部件标志值及其含义（这些值可能会随着版本发布而变化，因此建议检查 qnamespace.h 文件并阅读 Qt 类的文档）。它们分为三组：影响类型、样式和修饰符的标志。

# 小部件类型标志

类型标志会影响应用程序和底层窗口系统如何对待该窗口。

- **WType_TopLevel**—将此小部件设置为顶级小部件，意味着它将具有窗口管理器装饰、边框等。
- **WType_Modal**—表示这是一个应用程序模态的顶级小部件。在关闭此小部件之前，应用程序中的其他顶级小部件无法接收输入。此小部件类型还隐含 `WStyle_Dialog` 样式。
- **WType_Popup**—将此小部件设置为应用程序模态的顶级小部件，其样式适合弹出菜单。
- **WType_Desktop**—表示这是窗口系统桌面。参见下面的 `WPaintDesktop` 修饰符标志。

# 小部件样式标志

样式标志决定窗口管理器将添加到小部件的窗口装饰，例如边框、调整大小控件等。

- **WStyle_Customize**—不提供窗口装饰、图标（系统菜单）、标题栏（标题）、按钮（最小化、最大化和关闭）或调整大小控件。这意味着你将使用 `WStyle_XXX` 小部件标志设置所有样式提示。这对闪屏界面本身非常有用。
- **WStyle_NormalBorder**—提供标准的窗口装饰、图标、标题栏、按钮和调整大小控件。你不能将此标志与 `WStyle_DialogBorder` 或 `WStyle_NoBorder` 结合使用。
- **WStyle_DialogBorder**—提供标题栏、图标和关闭按钮。此标志不能与 `WStyle_NormalBorder` 或 `WStyle_NoBorder` 结合使用。
- **WStyle_NoBorder**—提供无装饰的普通窗口。此标志不能与 `WStyle_NormalBorder` 或 `WStyle_DialogBorder` 结合使用。
- **WStyle_Title**—提供标题栏。
- **WStyle_SysMenu**—提供系统菜单图标。
- **WStyle_Minimize**—提供最小化按钮。
- **WStyle_Maximize**—提供最大化按钮。
- **WStyle_MinMax**—同时提供最小化和最大化按钮。
- **WStyle_Tool**—提供标题栏和关闭按钮。
- **WStyle_StayOnTop**—使窗口保持在其他窗口之上。
- **WStyle_Dialog**—提供适合对话框的外观。它具有标题栏、图标和关闭按钮。此标志将防止在系统任务栏上创建额外的图标，并且对话框将（通常——这取决于底层窗口系统）随父窗口一起最小化。
- **WStyle_ContextHelp**—添加上下文敏感帮助按钮。

# 小部件修饰符标志

修饰符标志改变其他标志值的行为。

- **WDestructiveClose**—当小部件接受 *closeEvent()* 或尝试忽略 *closeEvent()* 失败时，会导致小部件被销毁。
- **WPaintDesktop**—使小部件接收桌面的绘制事件。
- **WPaintUnclipped**—使所有 *painters* 以非裁剪方式绘制。此小部件的所有子小部件以及其前方（Z 顺序中高于此小部件）的所有小部件都不会裁剪画笔可以绘制的区域。
- **WPaintClever**—表示 Qt 不应尝试优化小部件的重绘，且底层窗口系统将直接将重绘事件传递给小部件。这可能会生成更多事件，但通常减小了将被重绘区域的尺寸（例如通过 expose 事件）。
- **WResizeNoErase**—表示小部件在调整大小时不应擦除其内容。这可以减少因使用 **WPaintClever** 而在调整大小过程中可能产生的闪烁。
- **WRepaintNoErase**—表示小部件负责绘制（和重绘）其所有像素。滚动、expose 事件、更新和焦点变化不会擦除内容。这可以减少因使用 **WPaintClever** 修饰符可能导致闪烁。
- **WMouseNoMask**—使带有蒙版的小部件（具有不规则形状的小部件）接收整个小部件窗口（始终为矩形或正方形）的鼠标事件。
- **WNorthWestGravity**—表示小部件的内容静态对齐到左上角。调整大小事件只会为新暴露的小部件内容创建重绘事件。

上述所有标志都可以组合以实现所需的特殊效果，尽管更高级（子类化）Qt 小部件的默认标志通常就足够了。

# QOBJECT 类

几乎所有 Qt 类都继承 QObject 类的行为。它是 Qt 对象模型的基类，提供了使信号/槽机制（下一节讨论）工作所需的功能。QObject 包含一个可选的对象名称值，并可以报告其类名（如果类定义中包含 Qt 特定关键字 **Q_OBJECT**）。它可以通过 *QObject::event()* 方法接收事件，为其他 QObject 过滤事件，并可以拦截其子对象的 event。QObject 管理父子对象树的方式与 QWidget 类似。如果你删除一个 QObject，其所有子对象将先被销毁。

可能会出现你需要在小部件的子类中使用 QObject 功能，但该小部件并不继承 QObject 的情况。一个好的例子是 **QListViewItem**。你可以使用 C++ 多重继承特性从 QObject 和 QListViewItem 派生一个新的类，但你必须始终首先从 QObject 派生。以下代码片段说明了其外观：

```cpp
#include <QObject.h>
#include <QListViewItem>

class myItem : public QObject, QListViewItem
{
    Q_OBJECT
  public:
    myItem(QMidget *p = 0, const char *n = 0 );
    ...};
```

如果你在 QListViewitem 之后从 QObject 派生，你会浪费大量时间试图弄清楚为什么你的槽和信号没有按预期工作。

虽然你很少会在本书中看到使用 QObject、QWidget 及其子类的名称参数的示例，但这样做通常是个好主意（我将其省略是因为它们使示例变大，并且我希望保持示例简单）。Qt 错误处理机制将报告经历或引发问题对象的名称。（虽然没有正式的 Qt 特定异常处理机制，但内置的错误处理机制通常足够了。）

表 2.3 列出了 QObject 类公开的方法：

# **表 2.3 QObject 类方法**

| **公共成员** | **用途** |
|:--------------------------------|:---------------------------------------------------------------------|
| `QObject(QObject * parent=0, const char * name=0)` | 构造函数 |
| `virtual QObject()` | 析构函数 |
| `virtual bool event(QEvent * )` | 接收对象的事件，如果事件被识别和处理则应返回 true |
| `virtual bool eventFilter(QObject *, QEvent *)` | 如果该对象已安装为其他对象的事件过滤器，则过滤事件 |
| `virtual QMetaObject * metaQObject()` | 返回指向此对象的元对象的指针 |
| `virtual const char * className()` | 返回此对象的类名，或者如果缺少 Q_OBJECT 关键字则返回无效名称 |
| `bool isa( const char * )` | 如果此对象匹配参数类类型则返回 true，否则返回 false |

（未完待续）

