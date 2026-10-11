
第 37 到 40 行使用 RGB 值指定颜色，但所有三个值都存储在单个整数中。为了方便起见，该值本身在第 38 行声明为十六进制值。该值的第一个字节被忽略——红色值为 `0xF0`，绿色为 `0xE0`，蓝色为 `0x00`。

第 42 到 44 行通过使用颜色映射表的索引来指定颜色。构造函数的第二个参数（数字 8）是颜色映射表中的索引，而第一个参数是一个包含 RGB 值的整数。索引值是一个无符号数，但如果你将其指定为 `0xFFFFFF`，索引将被忽略，而将使用 RGB 值。

第 46 到 48 行使用 RGB 值的十六进制字符来指定颜色。示例中使用的数字格式为 `"#RRGBB"`，也可以是 `"#RRGGBB"`、`#RRGGGGBB"` 甚至 `"#RRRGGGBB"`。定义颜色的软件检测开头的 `#` 字符，并将剩余字符串划分为等份以提取值。

第 50 到 72 行使用从文件 `/usr/lib/X11/rgb.txt` 条目创建的 `Color` 对象。这是一个纯文本文件，每行包含一个颜色名称和 RGB 值。例如：

```
60 179 123 MediumSeaGreen
32 178 100 LightSeaGreen
152 251 152 PaleGreen
  0 255 0 green
  0 250 154 MediumSpringGreen
```

该文件有 750 多条目，该文件随 X11 一起发布，因此你可以放心使用找到的名称。文件中没有 750 种唯一的颜色，几乎所有颜色都有多种。此外，如果你愿意，可以添加自己的名称，程序将找到它们，但你的应用程序将不可移植性。

## KColorDialog

你可以采取几种方法来设置应用程序中的颜色。你可以简单地忽略颜色并使用默认，为每个控件设置特定的颜色值，或者允许用户选择颜色。`KColorDialog` 示例演示了如何弹出颜色选择器。随后你弹出一个 `KColorDialog` 并获取用户提供的颜色信息。

图 11-3 中的应用程序主窗口底部有一个按钮，点击将弹出对话框。窗口顶部是当前所选颜色的十六进制 RGB（红、绿、蓝）值。窗口中心是一个显示颜色的区域。

![](img/c47d54674a4d92abc6eebed0dd05f5fb_264_0.png)

图 11-3：点击按钮更改颜色

# 246 第二部分 ♦ 逐步详解

ShowColor Header

```cpp
/* showcolor.h */
#ifndef SHOWCOLOR_H
#define SHOWCOLOR_H

#include <qwidget.h>
#include <qlabel.h>
#include <qstring.h>

class ShowColor: public QWidget {
    Q_OBJECT
public:
    ShowColor(QWidget*parent=0, const char *name=0);
private:
    QLabel *label;
    QWidget *widget;
    QColor color;
    QString colorName;
slots:
    void popup();
};

#endif
```

`ShowColor` 类是显示图 11-3 窗口的控件，它包含一个显示 RGB 值的标签和一个显示颜色的控件。标签是一个 `QColor` 对象，名称是一个 `QString`。当按钮被点击时，会调用 `popup()` 槽。

```cpp
/* showcolor.cpp */
#include <qcolor.h>
#include <qbutton.h>
#include <qlayout.h>
#include <kcolordialog.h>
#include <qapplication.h>
#include <font.h>
#include <qwidget.h>
#include <qlabel.h>
#include "showcolor.h"

int main(int argc, char **argv) {
    QApplication app(argc, argv);
    ShowColor showcolor;
    showcolor.show();
    return app.exec();
}

ShowColor::ShowColor(QWidget *parent, const char *name)
    : QWidget(parent) {
    QVBoxLayout *box = new QVBoxLayout(this);
    label = new QLabel("", this);
    widget = new QWidget(this);
    widget->setHeight(40);
    label->setAlignment(Qt::AlignCenter);
    box->addWidget(label);
    QPushButton *button = new QPushButton("Select Color", this);
    box->addWidget(button);
    connect(button, SIGNAL(clicked()), this, SLOT(popup()));
}

void ShowColor::popup() {
    QColor color = QColorDialog::getColor(color, this);
    if (color == QColorDialog::Accepted) {
        colorName = color.name();
        label->setText(colorName);
        widget->setBackground(color);
    }
}
```

颜色的优势在于它们是“纯净”的，意义是它们在不同的计算机上看起来非常相似。你还可以通过鼠标点击右上角的阴影框来选择颜色。当你在大框周围移动交叉准星指针时，你将使用右下角的 RGB 和 HSV 值。选择颜色的第三种方法是使用存储在底部集合中的自定义颜色之一。

自定义颜色对每个用户都是持久的，存储在文件 `~/.kde/share/config/kdeglobals` 中，并且每当 `KColorDialog` 弹出时就会被检索。

要添加自定义颜色，首先选择自定义颜色集合中的其中一个框。接下来，使用鼠标从左侧的系统颜色或右侧的颜色面板选择颜色。选中后，点击标记为“添加到自定义颜色”（Add to Custom Colors）的按钮即可将其插入。

## QColorGroup 中的 QColors

绘制一个组件时可能涉及多种颜色。例如，推按钮有一个背景颜色、顶部阴影色、底部阴影色以及文本颜色。必须有一个 `QColor` 对象供按钮用于绘制所有这些颜色。其他组件对颜色组有不同的需求。而且随着按钮的按下或鼠标悬过敏感组件，这些需求会发生变化。

`QColorGroup` 类的设计旨在将组件的所有颜色封装进单个单元中。由于有各种组件以及它们不同的形式，`QColorGroup` 需要包含广泛的颜色选择。表 11-2 列出了 `QColorGroup` 中包含的十四种颜色。

| 表 11-2 | QColorGroup 中包含的颜色 |

| :--- | :--- |

| 名称 | 描述 |

| Background (背景) | 此颜色用于几乎所有组件的背景。 |

| Base (基色) | 对于希望比定义的 Background 更浅的组件，这是其背景色。它通常是白色，但总是较浅的颜色。 |

| BrightText (亮文本) | 此颜色可用于在 Dark 作为背景时显示文本。 |

| Button (按钮) | 这是按钮的背景颜色。在绘制按钮其余部分之前，会用此颜色填充组件。 |

| ButtonText (按钮文本) | 此颜色可用于在 Button 作为背景时显示文本。 |

| Dark (深色) | 此颜色比 Button 颜色深，与 Light 配合用于为按钮绘制 3D 外观的阴影。 |

| Foreground (前景) | 此颜色用于组件表面的任何文字或绘图。 |

| Highlight (高亮) | 这是用于绘制高亮或选中项的背景颜色。 |

| HighlightedText (高亮文本) | 此颜色与作为背景的 Button 颜色对比，适用于显示文本。 |

| Light (浅色) | 此颜色比 Button 颜色和 Dark 都浅，用于阴影以赋予组件 3D 外观。 |

| Mid (中色) | 对于需要复杂阴影的组件，此颜色位于 Button 和 Dark 之间。 |

| Midlight (中亮) | 对于需要复杂阴影的组件，此颜色位于 Button 和 Light 之间。 |

| Shadow (阴影) | 此颜色非常深，用于明显的阴影。它通常是黑色。 |

| Text (文本) | 这是用于在组件表面上绘制文本的颜色。它通常（并非总是）与 Foreground 相同。 |
