
QLineEdit 组件是一个文本编辑器，用户可以输入文本并对现有文本进行修改。

### File

```
#include <multilineedit.h>
```

### 基类

`QFrame` `QObject` `QPaintDevice` `Widget`

### 继承自

`QLineEdit`

### 构造函数

```
QMultiLineEdit(QWidget *parent = 0, const char *name = 0);
```

### 方法

```
int alignment() const;
bool atBeginning() const;
bool atEnd() const;
bool autoUpdate() const;
void cursorPosition(int *line, int *col) const;
void cursorBackward(bool mark);
void cursorForward(bool mark);
static int defaultTabStop();
EchoMode echoMode() const;
bool edited() const;
void getCursorPosition(int *line, int *col) const;
int hMargin() const;
virtual void insertAt(const QString&, int line, int col, bool mark = FALSE);
virtual void insertLine(const QString&, int line = -1);
bool isOverwriteMode() const;
bool isReadOnly() const;
bool isUndoEnabled() const;
int length() const;
int maxLength() const;
int minWidth() const;
QSize minimumSize() const;
int numLines() const;
virtual void removeLine(int line);
virtual void setAlignment(int flags);
virtual void setCursorPosition(int *line, int *col, bool mark = FALSE);
static void setDefaultTabStop(int);
virtual void setEchoMode(EchoMode);
virtual void setVisibleLines(int lines);
virtual void setFont(const QFont&);
virtual void setMargin(int);
virtual void setMaxLength(int);
virtual void setSelection(int row_from, int col_from, int row_to, int col_to);
void setUndoEnabled(bool);
virtual void setValidator(const QValidator *);
virtual void setWordWrap(WordWrap mode);
virtual void setColumnCount(int);
virtual void setPolicy(WrapPolicy policy);
QSize sizeHint() const;
QSize textSize() const;
QString text() const;
QString textLine(int line) const;
int undoDepth() const;
const QValidator *validator() const;
WordWrap wordWrap() const;
int wrapColumnCount(int) const;
WrapPolicy wrapPolicy() const;
```

### 槽

```
void append(const QString &);
void clear();
void copy() const;
void copyText() const;
void cut();
void deselect();
void insert(const QString&);
void paste();
void redo();
void selectAll();
virtual void setOverwriteMode(bool);
virtual void setReadOnly(bool);
virtual void setText(const QString &);
void undo();
```

### 信号

```cpp
void redoAvailable(bool);
void returnPressed();
void textChanged();
void undoAvailable(bool);
```

### 枚举

```cpp
enum EchoMode { Normal, NoEcho, Password };
enum WordWrap { NoWrap, WidgetWidth, FixedPixelWidth, FixedColumnWidth };
enum WrapPolicy { AtWhitespace, Anywhere };
```

第 8 章包含了使用 `QLineEdit` 组件的示例。

![](img/c47d54674a4d92abc6eeb0dd05f5fb_470_0.png)

## QPopupMenu

`QPopupMenu` 是一个弹出的菜单。它通常作为菜单栏或父弹出菜单的成员。

### File

```
#include <popupmenu.h>
```

### 基类

```
QFrame QMenuDataObject QPaintDevice QWidget
```

### 继承自

```
QMenu QPopupMenu
```

### 构造函数

```
QPopupMenu(QWidget *parent = 0, const char *name = 0);
```

### 方法

```
bool constWhatsThis() const;
int exec();
int exec(QPoint &pos, int indexAtPoint = 0);
void hide();
int idAT(int index) const;
int idAT(const QPoint &pos) const;
```

# 454 第 III 部分 + 参考与机制

```cpp
int insertTearOffHandle(int id = -1, int index = -1);
bool isCheckable() const;
void popup(QPoint &pos, int indexAtPoint = 0);
virtual void setVisibleItem(int);
virtual void setCheckable(bool);
virtual void setFont(const QFont &);
void show();
QSize sizeHint() const;
void updateItem(int id);
```

## 信号

- void aboutToShow();
- void activated(int itemId);
- void activatedRedirect(int itemId);
- void highlighted(int itemId);
- void highlightedRedirect(int itemId);

你可以在第 6 章中找到许多 `QPopupMenu` 的示例。

![](img/c47d54674a4d92abc6eebed0dd05f5fb_471_0.png)

## QPrintDialog

`QDialog` 部部件是一个接口，允许用户通过应用程序进行配置和控制打印。

### 文件

```cpp
#include <qprintdialog.h>
```

### 基类

`QDialog` `QObject` `QPaintDevice` `QWidget` `Qt`

### 构造函数

```cpp
QPrintDialog(QPrinter *, QWidget *parent = 0, const char *name = 0);
```

### 方法

```cpp
void addButton(QPushButton *but);
static bool getPrinterSetup(QPrinter *);
QPrinter *printer() const;
void setPrinter(QPrinter *, bool = FALSE);
```

`QPrintDialog` 的示例使用一个 `Q` 对象来打印图 18-12 所示对话框框。
