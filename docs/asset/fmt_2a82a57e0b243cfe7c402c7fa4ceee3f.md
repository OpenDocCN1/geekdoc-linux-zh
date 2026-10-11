
```cpp
const QString *dir() const;
const QString *dirPath() const;
static QString *getExistingDirectory(QObject *, QEvent * =
const QString &dir = QString::null, QWidget *parent = 0,
const char *name = 0);
static QString *getExistingDirectory(const QString &dir,
QWidget *parent, const char *name, const QString &caption);
static QString *getFileName(const QString &initially = QString::null,
const QString &filter = QString::null, QWidget *parent = 0,
const char *name = 0);
static QString *getFileName(const QString &initially,
const QString &filter, QWidget *parent, const char *name,
const QString &caption);
static QStringList getOpenNames(
const QString &filter = QString::null,
const QString &dir = QString::null, QWidget *parent = 0,
const char *name = 0);
static QStringList getOpenFileNames(const QString &filter,
const QString &dir = QString::null, QWidget *parent = 0,
const char *name, const QString &caption);
static QString *getSaveFileName(
const QString &initially = QString::null,
const QString &filter = QString::null, QWidget *parent = 0,
const char *name = 0);
static QString *getSaveFileName(const QString &initially,
const QString &filter, QWidget *parent, const char *name,
const QString &caption);
static QFileIconProvider *iconProvider(QFileIconProvider *);
bool isContentsPreviewEnabled() const;
bool setIsPreviewEnabled() const;
Mode mode() const;
PreviewMode previewMode() const;
void rereadDir();
void resortDir();
void selectAll(bool b);
```

## QHeader

`QHeader`控件是一个用于控制多个列标题的大小和位置的容器。

### 文件

```
#include <qheader.h>
```

### 基类

`QObject` `QPaintDevice` `QWidget` `Qt`

### 构造函数

```cpp
QHeader(QWidget *parent = 0, const char *name = 0);
QHeader(int, QWidget *parent = 0, const char *name = 0);
```

### 方法

```cpp
int addLabel(const QString&, int size = -1);
int addIcon(const QIcon&, const QString&, int size = -1);
int cellAt(int) const;
int cellPos(int) const;
int cellSize(int) const;
int count() const;
QIconSet *iconSet(int section) const;
bool isClickEnabled(int section = 1) const;
bool isMovingEnabled() const;
bool isResizable(int section = -1) const;
string label(int section) const;
```

### 槽

```cpp
virtual void setOffset(int pos);
```

### 信号

```cpp
void clicked(int section);
void indexChange(int section, int fromIndex, int toIndex);
void moved(int, int);
void pressed(int section);
```

`void released(int section);`

`void sectionClicked(int);`

`void sizeChange(int section, int oldSize, int newSize);`

以下示例创建了一个具有四列的`QHeader`，其文本长度不一。可以使用鼠标调整每个列头的大小。即使文本被遮挡，列头也会保持分配给它们的所有宽度。如图 18-5 所示，表头可能会延伸到窗口末之外。列标题也可以根据显示所需的所需的进行扩展。`QHeader`控件发出的信号组可用于维护下方对应列的大小和状态。

```cpp
/* showheader.cpp */
#include <application.h>
#include <header.h>
```

![](img/c47d54674a4d92abc6eebed0dd05f5fb_448_0.png)

# QHGroupBox

`QHGroupBox`是一种容器控件，用于在水平行上组织一组小部件。

### 文件

```
#include <qgroupbox.h>
```

### 基类

`QFrame` `QGroupBox` `Object` `QPaintDevice` `Qt`

### 构造函数

```cpp
QHGroupBox(QWidget *parent = 0, const char *name = 0);

QHGroupBox(const QString &title, QWidget *parent = 0,

const char *name = 0);
```

以下示例在`QGroupBox`控件内部包含四个标签。如图 18-6 所示，`QGroupBox`控件继承自`QFrame`，因此它会在小部件周围显示边框，并可以可选地显示标题。

```cpp
/* showgroupbox.cpp */
#include <application.h>
#include <qgroupbox.h>
#include <qlabel.h>

int main(int argc, char **argv) {
    QApplication app(argc, argv);
    QGroupBox *groupbox = new QGroupBox();
    new QLabel("First", groupbox);
    new QLabel("Second", groupbox);
    new QLabel("Third", groupbox);
    new QLabel("Fourth", groupbox);
    groupbox->setTitle("Group Box Title");
    groupbox->show();
    app.setWidget(groupbox);
    return(app.exec());
}
```

![](img/c47d54674a4d92abc6eebed0dd05f5fb_449_0.png)

## QIconView

`QIconView`显示一组图标并允许用户进行选择。

### 文件

```cpp
#include <qiconview.h>
```

### 基类

`QFrame` `QObject` `QPaintDevice` `QScrollView` `QWidget` `Qt`

### 继承自

`KIconView` `KIconCanvas`

### 构造函数

```cpp
QIconView(QWidget *parent = 0, const char *name = 0,
WidgetFlags f = 0);
```

### 方法
