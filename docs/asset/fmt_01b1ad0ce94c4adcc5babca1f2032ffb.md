
#include <qlcdnumber.h>

# QLCDNumber

## 基类

`QFrame` `QObject` `QPaintDevice` `QWidget` `Qt`

## 构造函数

```
QLCDNumber(QWidget *parent = 0, const char *name = 0);
QLCDNumber(uint numDigits, QWidget *parent = 0,
           const char *name = 0);
```

## 方法

```
bool checkOverflow(double num) const;
bool checkOverflow(int num) const;
int intValue() const;
Mode mode() const;
int numDigits() const;
SegmentStyle segmentStyle() const;
virtual void setMode(Mode);
virtual void setDigits(int nDigits);
virtual void setStyle(SegmentStyle);
QSize sizeHint() const;
QSizePolicy sizePolicy() const;
bool smallDecimalPoint() const;
double value() const;
```

## 槽

```
void display(int num);
void display(double num);
void display(const QString &str);
virtual void setBinMode();
virtual void setDecMode();
virtual void setHexMode();
virtual void setOctMode();
virtual void setSmallDecimalPoint(bool);
```

## 信号

```
void overflow();
```

## 枚举

```
enum Mode { Hex, HEX=Hex, Dec, DEC=Dec, Oct, OCT=Oct, Bin,
             BIN=Bin };
enum SegmentStyle { Outline, Filled, Flat };
```

> 你可以在第 3 章中找到 `QLCDNumber` 小控件的示例。

![](img/c47d54674a4d92abc6eebed0dd05f5fb_454_0.png)

## QLabel

`QLabel` 小部件可以使用任何字体显示未排序的文本。

## 文件

```
#include <qlabel.h>
```

## 基类

`QFrame` `QObject` `QPaintDevice` `QWidget` `Qt`

## 继承自

`KDockWindow` `KImageTrackLabel` `KStatusBarLabel` `KURLL`

## 构造函数

```
QLabel(QWidget *parent, const char *name = 0, QFlags f = 0);
QLabel(const QString &text, QWidget *parent,
const char *name = 0, QFlags f = 0);
QLabel(QWidget *buddy, const QString &, QWidget *parent,
const char *name = 0, QFlags f = 0);
```

## 方法

```
int alignment() const;
bool autoResize() const;
QWidget *buddy() const;
int heightFixedWidth(int) const;
int indent() const;
Size minimumSizeHint() const;
QMovie *movie() const;
Pixmap *pixmap() const;
virtual void setAlignment(int);
virtual void setAutoMask(bool);
virtual void setAutoResize(bool);
virtual void setBuddy(QWidget *);
virtual void setIndent(int);
virtual void setTextFormat(const QString &);
Size sizeHint() const;
QSizePolicy sizePolicy(const QSizePolicy&) const;
QString text() const;
TextFormatFormat(const QString&) const;
```

## 槽

```
void clear();
virtual void setMovie(const QMovie &);
virtual void setIndent(int);
virtual void setNum(double);
virtual void setPixmap(const QPixmap &);
virtual void setText(const QString &);
```

![](img/c47d54674a4d92abc6eebed0dd05f5fb_455_0.png)

从第 2 章开始，书中有很多关于 `QLabel` 的示例。

## QLineEdit

`QLineEdit` 小部件是一个简单的单行文本编辑器，主要用于数据输入。

## 文件

```
#include <qlineedit.h>
```

## 基类

`QObject` `QPaint` `QWidget` `Qt`

## 继承自

`KAccelInput` `KDateInternalYearSelector` `KLineEdit`

`KPEdit` `KRestrictedLine`

## 构造函数

```
QLineEdit(QWidget *parent, const char *name = 0);
QLineEdit(const QString &, QWidget *parent,
      const char *name = 0);
```

## 方法

```
int alignment() const;
void backspace();
void copy() const;
void cursorLeft(bool mark, int steps = 1);
int cursorPosition() const;
void cursorRight(bool mark, int steps = 1);
void cursorWordBackward(bool mark);
void cursorWordForward(bool mark);
void cut();
void del();
QString displayText() const;
EchoMode echoMode() const;
bool edited() const;
void end(bool mark);
bool frame() const;
bool hasMarkedText() const;
void home(bool mark);
bool isReadOnly() const;
QString text() const;
int maxLength() const;
QSize minimumHint() const;
void paste();
void setAlignment(int flag);
virtual void setCursorPosition(int);
virtual void setEchoMode(EchoMode);
virtual void setEnabled(bool);
virtual void setFont(const QFont &);
virtual void setFrame(bool);
virtual void setMaxLength(int);
virtual void setPalette(const QPalette &);
void setReadOnly(bool); virtual void setSelection(int, int);
virtual void setValidator(const QValidator *);
QSize sizeHint() const;
QSizePolicy sizePolicy() const;
QString text() const;
bool validateAndSet(const QString &, int, int, int);
const QValidator *validator() const;
```

## 槽
