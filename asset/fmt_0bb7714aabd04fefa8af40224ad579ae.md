
### 函数声明

`int insertButton(const QPixmap &pixmap, int id);`

`void QPopup *popup, bool enabled = true, const QString &text,`

`int index = -1);`

`void insertCombo(QList *list, int id, bool writable,`

`const char *signal, QObject *receiver,`

`const char *slot, bool enabled = true,`

`const QString &tooltip = QString::null, int size = 0,`

`int index = -1);`

`void QComboBox::QPolicy policy = QComboBox::AtBottom;`

`int insertCombo(QList *list, int id, bool writable,`

`const char *signal, QObject *receiver,`

`const char *slot, bool enabled = true,`

`const QString &tooltip = QString::null, size = 0,`

`int index = -1);`

`void QComboBox::QPolicy policy = QComboBox::AtBottom;`

`int insertCombo(const QString &text, int id, bool writable,`

`const char *signal, QObject *receiver,`

`const char *slot, bool enabled = true,`

`const QString &tooltip = QString::null, size = 0,`

`int index = -1);`

`void QComboBox::QPolicy policy = QComboBox::AtBottom;`

`void insertComboList(int index, const QString &text, index);`

`void insertComboList(int index, QList *list, index);`

`void removeComboList(int index, const QString *list, index);`

`void insertLineSeparator(int index = -1);`

`int insertInserted(const QString *text, int ID,`

`const char *signal, QObject *receiver,`

`const char *slot, bool enabled = true,`

`const QString &tooltip = QString::null, size = 0,`

`int index = -1);`

`void insertSeparator(int index = -1);`

`void insertWidget(int index, int width, QWidget *widget,`

`int index = -1);`

`bool isButton(int index);`

`int maxWidth();`

`virtual QSize maxSize() const;`

`virtual QSize minimumSize() const, index;`

`void removeItem(int index);`

`void saveState();`

`void setAutoRepeat(int index, bool flag = true);`

`void setBarPos(BarPosition pos);`

`void setButton(int id, bool flag);`

`void setButtonIcon(int id, const QString &icon);`

`void setButtonPixmap(int id, const QPixmap &pixmap);`

`void setCurrentComboItem(int id, int index);`

`void setDelayedPopup(int id, QPopupMenu *popup,`

`bool toggle = false);`

`void setContextMenu(bool enable = true);`

`void setFlat(bool flag);`

`void setFullSize(bool flag = true);`

`void setSize(int size);`

`void setSize(int size, bool update);`

`void setText(const QString &text, bool update);`

`void setItemSize(int id, bool size = true);`

`void setItemStyle(int id, bool style = true);`

`void setLineText(int id, const QString &text);`

`void setHeight(int h);`

`void setWidth(int w);`

`void setTitle(const QString& title);`

`void setXML(int id, const QString&file, QDomDocument&xml);`

`void showItem(int id);`

`virtual QSize sizeHint() const;`

`virtual QSizePolicy sizePolicy() const;`

`void toggleButton(int id);`

`void updateRects(bool resize = false);`

`virtual int widthForHeight(int height) const;`

### Signals

`void clicked(int id);`

`void doubleClicked(int id);`

`void highlighted(int id);`

`void changed(int id);`

`void modeChanged();`

`void moved(BarPosition pos);`

`void pressed(int);`

`void released(int);`

`void toggled(int id);`

### Enums

`enum IconText { IconLeft=0, IconTextRight, TextOnly, IconTextBottom };`

`enum BarStatus { Toggle, Show, Hide };`

`enum BarPosition { Top=0, Left, Right, Bottom, Floating, Flat };`

![](img/c47d54674a4d92abc6eebed0dd05f5fb_593_0.png)

在第 6 章中有多个 `KToolBar` 小部件的示例。

# KToolButton

`KToolBar` 小部件内部使用 `KToolButton` 显示响应鼠标的按钮。

`KToolButton` 通过调用 `KToolBar` 的 `insertButton()` 方法之一构造。使用 ID 编号，调用 `KToolBar` 方法 `getButton()` 可以获取按钮指针，从而可以使用此处列的方法。

文件

```
#include <ktoolbarbutton.h>
```

基类

```
QObject QPaintDevice QWidget Qt
```

### 构造函数

```
KToolButton(const QString &icon, int id, QWidget *parent,
const char *name = nullptr, const QString &txt = QString::null);
KToolButton(const QPixmap &pixmap, int id, QWidget *parent,
const char *name = nullptr, const QString &txt = QString::null);
KToolButton(const QWidget *parent = nullptr, const char *name = nullptr);
```

方法
