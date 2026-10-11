
```cpp
void addTab(QWidget *widget, const QString &);
void addTab(QWidget *child, const QIconSet &iconset, const QString &label);
void addTab(QWidget *widget, QTab *);
void changeTab(QWidget *widget, const QString &);
void changeTab(QWidget *child, const QIconSet &iconset, const QString &label);
QWidget *currentPage() const;
bool hasApplyButton() const;
bool hasCancelButton() const;
bool hasDefaultButton() const;
bool hasHelpButton() const;
bool hasOKButton() const;
void insertTab(QWidget *widget, const QString &, int index = -1);
void insertTab(QWidget *child, const QIconSet &iconset, const QString &label, int index = -1);
void insertTab(QWidget *widget, QTab *, int index = -1);
bool isTabEnabled(QWidget*) const;
bool isTabEnabled(const char*) const;
void removePage(QWidget*);
void setApplyButton(const QString &text);
void setApplyButton();
void setCancel(const QString &text);
void setCancel();
void setDefault(const QString &text);
void setDefault();
void setFont(const QFont &font);
void setHelpButton(const QString &text);
void setHelpButton();
void setOKButton(const QString &text = QString::null);
void setOKButton(const QString &text);
void setOKButton();
void setTabEnabled(QWidget*, bool);
void setTabEnabled(const char*, bool);
void show();
void showPage(QWidget*);
string tabLabel(QWidget*);
```

### Signals

```cpp
void aboutToShow();
void applyButtonPressed();
void cancelButtonPressed();
void defaultButtonPressed();
void helpButtonPressed();
void selected(const QString &);
```

> 参见第 5 章获取 `QTabDialog` 的示例。

## QTabWidget

`QTabWidget` 显示一行的可以使用鼠标单独选择的标签。

### File

```
#include <qwidget.h>
```

### Base Classes

`QObject` `QPaintDevice` `QWidget`

### Constructors

```cpp
QTabWidget(QWidget *parent = 0, const char *name = 0);
```

### Methods

```cpp
void addTab(QWidget *, const QString &);
void addTab(QWidget *child, const QIconSet &iconset, const QString &label);
```

### 474 第 3 部分 + 引用与力机制

```cpp
void addTab(QWidget *, QTab *);
void changeTab(QWidget *, const QString&);
void changeTab(QWidget *child, const QIconSet&iconset);
const QString &label);
QWidget *currentPage();
void insertTab(QWidget *, const QString&, int index = -1);
void insertTab(QWidget *child, const QIconSet&iconset,
const QString &label, int index = -1);
void insertTab(QWidget *, QTab *, int index = -1);
bool isEnabled(QWidget *) const;
int main();
QSize minimumSizeHint();
void removePage(QWidget *);
void setMargin(int);
void setTabEnabled(QWidget *, bool);
void setTabPosition(TabPosition);
void showPage(QWidget *) const;
QSize sizeHint() const;
QString tabLabel(QWidget *) const;
TabPosition tabPosition() const;
```

### 信号 (Signals)

```cpp
void selected(const QString&);
```

### 枚举 (Enums)

```cpp
enum TabPosition { Top, Bottom };
```

以下示例创建了一个包含四个部件的 `QTabWidget`，如图 18-23 所示。在栏的右端，窗口宽度不足以包含所有标签页。

```cpp
/* showtabwidget.cpp */
#include <application.h>
#include <qtabwidget.h>
#include <label.h>

int main(int argc, char *argv) {
  QLabel label;
  QApplication app(argc, argv);
  QTabWidget *tabwidget = new QTabWidget();
  label = new QLabel("The First Label", tabwidget);
  tabwidget->addTab(label, "First");
  label = new QLabel("The Second Label", tabwidget);
  tabwidget->addTab(label, "Second");
  label = new QLabel("The Third Label", tabwidget);
  tabwidget->addTab(label, "Third");
  label = new QLabel("The Fourth Label", tabwidget);
  tabwidget->addTab(label, "Fourth");
  tabwidget->show();
  app.setMainWidget(tabwidget);
  return(app.exec());
}
```

## 第 18 章 ◆ Qt 部件 475

![](img/c47d54674a4d92abc6eebed0dd05f5fb_492_0.png)

## QTextBrowser

`QTextBrowser` 部件在窗口中显示文本并提供系列定位方法。基础文本显示继承自 `QTextView`。可以提取高亮显示部分。

### 文件 (File)

```cpp
#include <textbrowser.h>
```

### 基类 (Base Classes)

| QFrame | QObject | QPaintDevice | QScrollView | QText | QWidget |

|---|---|---|---|---|---|

### 继承自 (Inherited By)

| KTextBrowser |

### 构造函数 (Constructors)

```cpp
QTextBrowser(QWidget *parent = 0, const char *name = 0);
```

### 方法 (Methods)
