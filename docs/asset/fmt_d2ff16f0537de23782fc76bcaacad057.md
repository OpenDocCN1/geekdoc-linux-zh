
```cpp
int main(int argc, char *argv) {

  KApplication app(argc,"showrestrictedline");

  KRestrictedLine restrictedline = new KRestrictedLine();

  restrictedline->setValidChars("aeiouAEIOUY");

  restrictedline->show();

  app.setMainWindow(restrictedline);

  return(app.exec());

}
```

![](img/c47d54674a4d92abc6eebed0dd05f5fb_576_0.png)

# RootPermIcon

`KRootPermIcon` 控件显示图标以指示当前用户是否具有 root 权限。

## 文件

```
#include <kauthicon.h>
```

## 基类

```
KAuthIcon QObject QDevice QWidget
```

## 构造函数

```
KRootPermIcon(QWidget *parent = 0, const char *name = 0);
```

## 方法

```
bool status() const;
```

## 槽

```
void updateStatus();
```

以下示例使用 `KRootPermIcon` 控件作为顶层窗口，并将根据用户是否具有 root 权限显示图 19-44 所示的图标之一。

```cpp
/* showrootpermsicon.cpp */

#include <kapp.h>

#include <kauthicon.h>

int main(int argc,char **argv)

{

    KApplication app(argc,argv,"showrootpermsicon");

    KRootPermIcon *rootpermsicon = new KRootPermIcon();

    rootpermsicon->show();

    app.mainWidget(rootpermsicon);

    return(app.exec());

}
```

![](img/c47d54674a4d92abc6eebed0dd05f5fb_577_0.png)

## KRuler

`KRuler` 显示一个像尺子一样带有标记和标签的垂直或水平窗口。

## 文件

```
#include <kruler.h>
```

## 基类

```
QObject QPaintDevice Widget
```

## 构造函数

```
KRuler(direction dir, QWidget *parent = 0, const char *name = 0, WFlags f = 0, allowLines = TRUE);
KRuler(direction dir, int widgetWidth, QWidget *parent = 0, const char *name = 0, WFlags f = 0, allowLines = TRUE);
```

## 方法

```
int getMaxDistance() const;
int getOffset() const;
int getLength() const;
bool getFixedWidth() const;
int getLittleDistance() const;
int getMaxValue() const;
int getMediumDistance() const;
metric_style getRulerStyle() const;
int getMinValue() const;
int getOffset() const;
paint_style getRulerStyle() const;
double getPixelMark() const;
bool getBigMarks() const;
bool getEndMarks() const;
bool getLittleMarks() const;
bool getMediumMarks() const;
bool getPointer() const;
bool getTinyMarks() const;
paint_style getTickStyle() const;
int getTinyDistance() const;
int getValue() const;
void setBigDistance(int);
void setEndLabel(const QString &);
void setLength(int);
void setLittleDistance(int);
void setMaxValue(int);
void setMediumDistance(int);
void setMinValue(int);
void setOffset(int);
void setPixelMark(double);
void setRange(int min, int max);
void setRulerStyle(KRuler::metric_style);
void setRulerStyle(KRuler::paint_style);
void setTickStyle(KRuler::paint_style);
void setTinyMarks(int);
void setValue(int);
void setValueBigMark(int);
void setValueLittleMark(int);
void setValueMediumMark(int);
void showBigLabel(bool);
void showBigMarks(bool);
void showEndLabel(bool);
void showEndMarks(bool);
void showMarkLabel(bool);
void showLittleMarks(bool);
void showMediumLabel(bool);
void showMediumMarks(bool);
void showPointer(bool);
void showTinyMarks(bool);
void slide(int count = 1);
void slideup(int count = 1);
```

## 槽

```
void slotEndOffset(int);
void slotNewOffset(int);
void slotNewValue(int);
```

## 枚举

```
enum direction { horizontal, vertical };
enum metric_style { custom=0, pixel, millimetres, centimetres, metres };
enum paint_style { flat, raised, sunken };
```

以下示例程序显示了图 19-45 中的 `KRuler`：

```cpp
/* showruler.cpp */

#include <kapp.h>

#include <kruler.h>

int main(int argc, char **argv) {

    KApplication app(argc, argv, "showruler");

    KRuler *ruler = new KRuler(KRuler::horizontal);

    ruler->setRulerStyle(KRuler::pixel);

    ruler->setLength(1000);

    ruler->setScale(750);

    ruler->showBigMarks(TRUE);

    ruler->showTinyMarks(FALSE);

    ruler->showMediumMarks(FALSE);

    ruler->showLittleMarks(FALSE);

    ruler->showEndMarks(FALSE);

    ruler->showEndLabel(FALSE);

    ruler->show();

    app.setMainWidget(ruler);

    return(app.exec());

}
```

![](img/c47d54674a4d92abc6eebed0dd05f5fb_579_0.png)

图 19-45: 简单的 `KRuler`

# KSelector

`KSelector` 控件是一个基类，用于用于在窗口内选择水平或垂直位置的控件。

## 文件

```
#include <kselect.h>
```
