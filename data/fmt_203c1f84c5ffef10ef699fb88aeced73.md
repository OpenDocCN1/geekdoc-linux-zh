
`virtual void show(QWidget *parent);`

## 信号

```cpp
void openURL(const QString &url);
void sendEmail(const QString &name, const QString &email);
```

## own举

```cpp
enum LayoutType { AbtPlain=0x0001, AbtTabbed=0x0002,
AbtImageLeft=0x0004,
AbtImageRight=0x0010, AbtImageOnly=0x0020,
AbtProduct=0x0040,
AbtKDEDefaults=AbtTabbed|AbtTitle|AbtImageLeft,
AbtAppStandard=AbtTabbed|AbtTitle|
AbtImageAndTitle=AbtPlain|AbtTitle|AbtImageOnly };
```

# 第 19 章 ♦ KDE Widgets 497

你可以在第 5 章中找到 `KAboutDialog` 的示例。

# KAboutKDE

`KAboutKDE` 对话框基于 `KAboutDialog`，并配置为标准的 KDE 格式显示。

## 文件

```cpp
#include <kaboutkde.h>
```

## 基类

```cpp
KAboutDialog KDialog KDialogBase QDialog QObject QDevice QWidget
```

## 构造函数

```cpp
KAboutKDE(QWidget *parent = 0, const char *name = 0, bool modal = true);
```

第 5 章提供了 `KAboutDialog` 标准形式的示例。

# KAboutWidget

`KAboutWidget` 使用多种格式显示关于应用程序的信息。它提供了一组可以用于插入的方法。

## 文件

```cpp
#include <kaboutdialog.h>
```

## 基类

```cpp
QObject QDevice QWidget
```

## 构造函数

```cpp
KAboutWidget(QWidget *parent = 0, const char *name = 0);
```

## 方法

```cpp
void addContributor(const QString &name, const QString &email,
const QString &url, const QString &work);
void adjust();
void setAuthor(const QString &name, const QString &email,
const QString &url, const QString &work);
void setLogo(const QPixmap &);
void setMaintainer(const QString &name, const QString &url, const QString &work);
void setVersion(const QString &name);
```

## 信号

```cpp
void openURL(const QString &url);
void sendEmail(const QString &name, const QString &email);
```

第 5 章提供了将 `KAboutWidget` 作为 `KDialog` 主小部件的示例。

![](img/c47d54674ad92abc6eeb0dd05f5_15_0.png)

## KAccelMenu

`KAccelMenu` 小部件是简化 `KAccel` 和 `KDialog` 使用的辅助类。

## 文件

```cpp
#include <accelmenu.h>
```

## 基类

```cpp
QFrame MenuData QObject QDevice Popup QWidget
```

## 构造函数

```cpp
KAccelMenu(KAccel *k, QWidget *parent = 0, const char *name);
```

## 方法

```cpp
int insert(const QPixmap &pixmap, const char *text,
const char *action, QObject *receiver,
const char *member, KAccel *accel = 0);
int insert(const char *text, const char *action,
QObject *receiver, const char *member, KAccel *accel = 0);
int insert(const QPixmap &pixmap, const char *text,
const char *action, QObject *receiver,
const char *member, KAccel *accel = 0);
int insert(const char *text, const char *action,
QObject *receiver, const char *member, KAccel *accel = 0);
```

# KAnimWidget

## 小部件

`KAnimWidget` 通过顺序显示单个像素图来产生动画。

## 文件

```cpp
#include <kanimwidget.h>
```

## 基类

```cpp
QFrame QObject QPaintDevice QWidget
```

## 构造函数

```cpp
KAnimWidget(const QStringList &icons, int size = 0,
QWidget *parent = Q, const char *name);
KAnimWidget(QWidget *parent = Q, const char *name);
```

## 方法

```cpp
void setIcons(const QStringList &icons);
void setLayout(int size);
void start();
void stop();
```

## 信号

```cpp
void clicked();
```

以下示例通过加载像素图 `flag1.png` `flag4.png` 并将其作为连续的动画帧显示图 19-3 所示的窗口。它将在应用程序的 `share/small` 目录中查找图标，并在 `~/.kde/animwidget` 目录中查找。

```cpp
/* showanimwidget.cpp */
#include <app.h>
#include <kanimwidget.h>
#include <stringlist.h>
```

```cpp
int main(int argc, char **argv)
{
Application app(argc, argv,"animwidget");
QString icons;
Widget *widget = new QWidget();
ics.append("flag1");
ics.append("flag2");
ics.append("flag3");
ics.append("flag4");
KAnimWidget *animwidget = new KAnimWidget(icons,widget);
widget->show();
app.setMainWindow(widget);
return (app.exec());
}
```

图 19-3：由 `KAnimWidget` 控制的动画序列的一帧。

![](img/c47d54674a4d92abc6eeb0dd05f5fb_516_0.png)

# KAuthIcon

`KAuthIcon` 是设计用于指示用户是否有（或被拒绝）执行某些操作的小部件基类。

## 文件

```cpp
#include <kauthicon.h>
```

## 基类

```cpp
QObject QPaintDevice QWidget Qt
```

## 继承自

```cpp
KRootPermsIcon KWritePermission
```

## 构造函数

```cpp
KAuthIcon(QWidget *parent = 0, const char *name = 0);
```

## 方法

```cpp
virtual QSize sizeHint() const;
virtual bool status() const = 0;
```

## 槽

```cpp
```
