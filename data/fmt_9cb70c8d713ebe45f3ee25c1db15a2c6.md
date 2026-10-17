
```cpp
void IconEditor::setImagePixel(const QPoint &pos, bool opaque)
{
    int i = pos.x() * zoom;
    int j = pos.y() * zoom;

    if (image.rect().contains(i, j)) {
        if (opaque) {
            image.setPixel(i, j, penColor().rgba());
        } else {
            image.setPixel(i, j, qRgba(0, 0, 0, 0));
        }
        update(pixelRect(i, j));
    }
}
```

`setImagePixel()` 函数从 `mousePressEvent()` 和 `mouseMoveEvent()` 中调用，用于设置或清除像素。`pos` 参数是鼠标在小部件上的位置。

第一步是将鼠标位置从小部件坐标转换为图像坐标。这是通过将鼠标位置的 `x()` 和 `y()` 分除以缩放因子来实现的。接下来，我们检查该点是否在正确的范围内。可以使用 `QImage::rect()` 和 `QRect::contains()` 轻松完成此检查；这实际上检查了 `i` 是否在 0 到 `image.width() - 1` 之间，以及 `j` 是否在 0 到 `image.height() - 1` 之间。

根据 `opaque` 参数，我们设置或清除图像中的像素。清除像素实际上是将其设置为透明。我们必须将画笔 `QColor` 转换为 32 位 ARGB 值以供 `QImage::setPixel()` 调用。最后，我们调用 `update()` 并传入一个需要重绘区域的 `QRect`。

现在我们已经回顾了成员函数，将回到构造函数中使用的 `Qt::WA_StaticContents` 属性。该属性告诉 Qt，当小部件调整大小时，小部件的内容不会改变，且内容将固定在小部件的左上角。Qt 使用此信息来避免在调整小部件大小时无谓地重绘已经显示的区域。如图 5.5 所示。

**图 5.5. 调整 Qt::WA_StaticContents 小部件的大小**

![](img/1bc72df8c60cf85926d3aefcc273027d_189_0.png)

通常，当调整小部件大一时，Qt 为小部件的整个可见区域生成一个绘制事件。但如果创建小部件时使用了 `Qt::WA_StaticContents` 属性，则绘制事件的区域将限制为之前未显示的像素。这意味着如果小部件被调整为更小的尺寸，则不会生成任何绘制事件。

`IconEditor` 小部件现在已经完成了。利用前面章节中的信息和示例，我们可以编写代码将 `IconEditor` 作为一个窗口使用、作为 `QMainWindow` 的中心部件、作为布局内部的子部件，或作为 `QScrollArea` 内部的子部件（第 152 页）。在下一节中，我们将看到如何将其与 Qt Designer 集成。

## 将自定义小部件集成到 Qt Designer

在 Qt Designer 中使用自定义小部件之前，我们必须让 Qt Designer 感知到它们。有两种技术可以实现这一点：“提升”（promotion）方法和插件（plugin）方法。

提升方法是最快最简单的方法。它包含选择一个与我们希望自定义小部件具有相似 API 的内置 Qt 小部件，并在 Qt Designer 的自定义小部件对话框（如图 5.6 所示）中填写一些关于该小部件的信息。自定义小部件就可以用于使用 Qt Designer 开发的表单，尽管在编辑或预览表单时，它将由关联的内置 Qt 小部件表示。

**图 5.6. Qt Designer 的自定义小部件对话框**

[查看全尺寸图像]

![](img/1bc72df8c60cf85926d3aefcc273027d_190_0.png)

以下是使用这种方法在表单中插入 `HexSpinBox` 小部件的方法：

1. 从 Qt Designer 的小部件框中将其拖到表单上，以创建一个 `QSpinBox`。
2. 右键点击计数器，从右键菜单中选择“提升为自定义小部件”（Promote to Custom Widget）。
3. 在弹出的对话框中填充，“HexSpinBox”作为类名，“hexspinbox.h”作为头文件。

大功告定！`uic` 生成的代码将包含 `hexspinbox.h` 而不是 `<QSpinBox>` 并实例化 `HexSpinBox`。在 Qt Designer 中，`HexSpinBox` 小部件将由 `QSpinBox` 表示，允许我们设置 `QSpinBox` 的所有属性（例如范围和当前值）。

提升方法的缺点是自定义小部件特有的属性在 Qt Designer 中无法访问，且小部件不会以其自身的身份渲染。这两个问题都可以通过使用插件方法解决。插件方法需要创建一个 Qt 可以在运行时加载并用于创建小部件实例的插件库。为了展示其工作原理，我们将上一节的 `IconEditor` 集成为插件。首先，我们必须子类 `QDesignerWidgetInterface` 并实现一些虚函数。这里是类定义：

```cpp
#include <QDesignerWidgetInterface>

class IconEditorPlugin : public QObject, public QDesignerWidgetInterface
{
    Q_OBJECT
public:
    IconEditorPlugin(QObject *parent = nullptr);
    QString name() const;
    QString includeFile() const;
    QString group() const;
    QIcon icon() const;
    QString toolTip() const;
    QString whatsThis() const;
    bool isContainer() const;
    QWidget *createWidget(QWidget *parent);
};
```

`IconEditorPlugin` 子类是一个封装 `IconEditor` 小部件的工厂类。它派自 `QObject` 和 `QDesignerWidgetInterface`。

```cpp
IconEditorPlugin::IconEditorPlugin(QObject *parent)
: QObject(parent)
{
}
```

构造函数是简单的。

```cpp
QString IconEditorPlugin::name() const
{
    return "IconEditor";
}
```

`name()` 函数返回插件提供的小部件名称。

```cpp
QString IconEditorPlugin::includeFile() const
{
    return "iconeditor.h";
}
```

`includeFile()` 函数返回指定小部件头文件。

```cpp
QString IconEditorPlugin::group() const
{
    return tr("Image Manipulation Widgets");
}
```

`group()` 函数返回自定义小部件所属的小部件框组。

```cpp
QIcon IconEditorPlugin::icon() const
{
    return QIcon(":/images/iconeditor.png");
}
```

`icon()` 函数返回用于在 Qt Designer 小部件框中表示自定义小部件的图标。在这里，我们假设 `IconEditorPlugin` 关联资源文件中有一个适用于图标的项目。

```cpp
QString IconEditorPlugin::toolTip() const
{
    return tr("An icon editor widget");
}
```

`toolTip()` 函数返回鼠标悬停在 Qt Designer 小部件框中的自定义小部件时显示的工具提示。

```cpp
QString IconEditorPlugin::whatsThis() const
{
    return tr("This widget is presented in Chapter 5 of <i>C++ GUI Programming with Qt 4</i> as an example of a custom Qt widget.");
}
```

```cpp
bool IconEditorPlugin::isContainer() const
{
    return false;
}
```

`isContainer()` 函数如果小部件可以包含其他小部件则返回 true；否则返回 false。

```cpp
QWidget *IconEditorPlugin::createWidget(QWidget *parent)
{
    return new IconEditor(parent);
}
```

Qt Designer 调用 `createWidget()` 函数来创建一个给定父部件的小部件类实例。

```cpp
Q_EXPORT_PLUGIN2(iconeditorplugin, IconEditorPlugin)
```

在实现插件类的源文件末尾，我们必须使用 `Q_EXPORT_PLUGIN2()` 宏使插件对 Qt Designer 可用。第一个参数是我们想要给插件起的名称；第二个参数是实现该插件的类名。

构建插件的 `.pro` 文件如下：

```pro
TEMPLATE = lib
CONFIG += designer plugin release
HEADERS = ../iconeditor/iconeditor.h \
           iconeditorplugin.h
SOURCES = ../iconeditor/iconeditor.cpp \
           iconeditorplugin.cpp
RESOURCES = iconeditorplugin.qrc
DESTDIR = $$[QT_INSTALL_PLUGINS]/designer
```

`qmake` 构建工具内置了一些预定义变量。其中之一是 `$$QT_INSTALL_PLUGINS`，它包含了 Qt 目录内部插件目录的路径。当你输入 `make` 或 `nmake` 来构建插件时，它会自动将其安装到 Qt 的 `plugins/designer` 目录。一旦插件构建完成，就可以像使用任何 Qt 内置小部件一样在 Qt Designer 中使用 `IconEditor` 小部件。

如果你想将多个自定义小部件集成到 Qt Designer 中，你可以为每个小部件创建一个插件，也可以通过派自 `QDesignerCustomWidgetCollectionInterface` 将它们合并为一个插件。

## 双缓冲

双缓冲是一种 GUI 编程技术，它由将小部件渲染到离屏位图（pixmap）并将位图拷贝到显示器上组成。在 Qt 的早期版本中，这种技术被频繁用于消除闪烁并提供更灵敏的用户界面。

在 Qt 4 中，`QWidget` 会自动处理，因此我们很少需要担心小部件闪烁。尽管如此，如果小部件的渲染复杂且需要频繁使用，显双缓冲仍然是有益的。我们可以将位图永久存储在小部件中，随时准备处理下次绘制事件，并在每收到绘制事件时将位图拷贝到小部件。这当我们想要进行微小修改（例如画一个橡皮带）时特别有用，而无需反复重新计算整个小部件的渲染。

我们将通过回顾图 5.7 和 5.9 显示的 `Plotter` 自定义小部件来结束本章。该小部件使用了双缓冲，并展示了 Qt 编程的其他几个方面，包括键盘事件处理、手动布局和坐标系。

**图 5.7. 缩放 Plotter 小部件**

[查看全尺寸图像]

![](img/1bc72df8c60cf85926d3aefcc273027d_195_0.png)

对于需要图表或绘图小部件的实际应用程序，与其像我们这里这样创建一个自定义小部件，我们很可能会使用现成的第三方小部件。例如，我们可能会使用来自 `http://www.ics.com/` 的 `GraphPak`，来自 `http://www.kdab.net/` 的 `KD Chart`，或者来自 `http://qwt.sourceforge.net/` 的 `Qwt`。

`Plotter` 小部件显示指定为坐标向量的一条或多条曲线。用户可以在图像上画一个橡皮带，`Plotter` 将缩放橡皮带包围的区域。用户通过点击图表上的一点、按住左键将鼠标拖到另一个位置、然后释放鼠标键来绘制橡皮带。Qt 提供了 `QRubberBand` 类来绘制橡皮带，但在这里我们自己绘制，以便对外观进行更精细的控制并演示双缓冲。

用户可以通过多次绘制橡皮带来反复缩放，使用 `Zoom Out` 按钮缩小，然后使用 `Zoom In` 按钮重新放大。`Zoom In` 和 `Zoom Out` 按钮在它们第一次可用时出现，这样如果用户不缩放图表，它们就不会占用显示。`Plotter` 小部件可以持有任意数量曲线的数据。它还维护了一个 `PlotSettings` 对象栈，每个对象对应于特定的缩放级别。

让我们回顾一下这个类，从 `plotter.h` 开始：

```cpp
#ifndef PLOTTER_H
#define PLOTTER_H

#include <QMap>
#include <QPixmap>
#include <QVector>
#include <QWidget>

class QToolButton;
class PlotSettings;

class Plotter : public QWidget
{
 Q_OBJECT
public:
    Plotter(QWidget *parent = 0);
    void setPlotSettings(const PlotSettings &settings);
    void setCurveData(int id, const QVector<QPointF> &data);
    void clearCurve(int id);
    QSize minimumSizeHint() const;
    QSize sizeHint() const;

public slots:
    void zoomIn();
    void zoomOut();

protected:
    void paintEvent(QPaintEvent *event);
    void resizeEvent(QResizeEvent *event);
    void mousePressEvent(QMouseEvent *event);
    void mouseMoveEvent(QMouseEvent *event);
    void mouseReleaseEvent(QMouseEvent *event);
    void keyPressEvent(QKeyEvent *event);
    void wheelEvent(QWheelEvent *event);

private:
    void updateRubberBand();
    void refreshPixmap();
    void drawGrid(QPainter *painter);
    void drawCurves(QPainter *painter);

    enum { Margin = 5 };
    QToolButton *zoomInButton;
    QToolButton *zoomOutButton;
    QMap<int, QVector<QPointF>> curveMap;
    QStack<PlotSettings> zoomStack;
    bool rubberBandShown;
    QRect rubberBand;
    QPixmap pixmap;

    void update();
    void scroll(int dx, int dy);
};
#endif
```

我们从 `plotter.h` 开始回顾这个类。我们从 `plotter.h` 开始包含头文件，并声明 `Plotter` 的成员函数。在 `QWidget` 类中，我们重写了 `minimumSizeHint()` 和 `sizeHint()`。在 `Plotter` 类中，我们提供了 `zoomIn` 和 `zoomOut` 槽。现在我们查看实现文件：
