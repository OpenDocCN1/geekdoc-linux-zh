
程序看起来如图 7.3 所示。我们可以将图像拖入各种程序（如 Gimp 或 Paint），并观察它发生了什么。

图 7.3：带有 Qt-4 logo 的 DragLabel

### 7.4.3 释放端

为了更好地理解第 196 页图 7.2 所示的拖放过程，我们现在实现一个与 `DragLabel` 互补标签部件，将其命名为 `DropLabel`。

每个应该接受释放的部件必须首先在其构造函数中激活此能力，使用 `setAcceptDrops(true)`。

```cpp
// droplabel/droplabel.cpp

#include <QtGui>

#include "droplabel.h"

DropLabel::DropLabel(QWidget *parent)
    : QLabel(parent)
{
    setAcceptDrops(true);
}
```

```cpp
// droplabel/droplabel.cpp (continued)

void DropLabel::dragEnterEvent(QDragEvent *event) {
    if (event && event->mimeData()) {
        const QMimeData* md = event->mimeData();
        if (md->hasImage() || md->hasUrls() || md->hasText()) {
            event->acceptProposedAction();
        }
    }
}
```

我们检查 `QMimeData` 对象的内容，一旦发现图像、某些 URL 或文本，就会通过 `acceptProposedAction()` 接受投放操作。否则，鼠标光标将显示一个 X，告知用户该部件将不会接受投放。如果你需要，可以在这里进行更精确的检查，但在此阶段进行过多的检查可能会防止组件及时发出可以接受拖放的信号。

如果你想在组件内部执行额外的检查（例如，仅允许在特定区域投放），可以实现 `dragMoveEvent()` 处理器。该函数接收一个 `QDragEvent` 指针，可以通过 `pos()` 检查其在组件中的当前位置。该方法也必须调用 `acceptProposedAction()`，以传递在特定点处是否应接受投放。然而，大多数组件和应用程序不需要处理此事件。

为了完整起见，我们还应该提到 `dragLeaveEvent()`。此事件处理器通常不需要，但在特殊情况下可以使用它来撤销由 `dragEnterEvent()` 或 `dragMoveEvent()` 对当前组件所做的更改。

#### dropEvent() 处理器

投放操作的核心部分是 `dropEvent()` 处理器；它用于解码 `mimeData()` 对象并处理拖放投放过程：

```cpp
// droplabel/droplabel.cpp (continued)

void DropLabel::dropEvent(QDragEvent *event) {
    QPixmap pix;

    if (event && event->mimeData()) {
        const QMimeData* data = event->mimeData();

        if (data->hasImage()) {
            pix = data->imageData().value<QPixmap>();
        } else if (data->hasUrls()) {
            for (const QUrl &url : data->urls()) {
                QFileInfo info(url.toLocalFile());
                if (info.exists() && info.isFile()) {
                    pix = QPixmap(url.toLocalFile());
                    if (pix.isNull()) {
                        break;
                    }
                }
            }
        } else if (data->hasText()) {
            QUrl url(data->text());
            QFileInfo info(url.toLocalFile());
            if (info.exists() && info.isFile()) {
                pix = QPixmap(url.toLocalFile());
            }
        }

        if (!pix.isNull()) {
            setPixmap(pix);
            resize(pix.size());
        }
    }
}
```

由于 `QMimeData` 对象是 `const` 的（即写保护的），我们不需要释放它的内存。

如果图像以数据流的形式存在 `QMimeData` 实例中（通过 `hasImage()` 确定），将其转换为 pixmap。由于 `imageData()` 返回一个 `QVariant`，且 `QPixmap` 是 `QtGui` 模块的一部分（而位于 `QtCore` 中的 `QVariant` 并不了解该模块），我们将利用 `QVariant` 模板方法 `value<type>()`，并将 `QPixmap` 作为类型参数传递。

如果 MIME 数据包含 URL，我们首先通过 `toLocalFile()` 将它们每一个转换为相应的本地文件路径。如果路径不是，该方法将返回一个空字符串。

使用 `QFileInfo`，我们检查路径以查看其是否存在，以及它是否引用了一个文件。如果是这种情况，我们将该文件读取为图像文件。如果不起作用，`pixmap` 将变成一个空对象，其 `isNull()` 将返回 `true`。一旦我们找到了有效的 URL，就会通过 `break` 跳过其他 URL。

有时出现的情况是 `QMimeData` 包含指向同一个对象的多个 URL。例如，KDE 桌面环境使用 `/` URL 引用外部数据媒体上的文件，同时也为非 KDE 程序提供匹配的 Unix 路径。

最后，如果其他方法都失败了，由于文件定位符也可以表示为未格式化的文本，我们会尝试将 MIME 数据中任何存在的文本部分解释为 URL，以便我们尝试从这里获取 pixmap。

如果我们的提取尝试之一成功，填充了数据的 pix 文件将成为新标签的 pixmap，我们可以调整标签以匹配 pixmap 的大小。

我们还将通过一个短小的测试程序对此示例进行测试。在这里我们实例化 `DropLabel` 而不是 `DragLabel`，并将其放大到 100x100 像素的初始大小，以便有足够的空间投放对象：

## 7.5 剪贴板

如果你将第 197 页 `DragLabel` 示例中的图像拖入 `DropLabel` 窗口，该组件将接受投放。如果你松开按钮，如图 7.4 所示，`DropWidget` 将接受该图形。得益于其解释 URL 的能力，程序还可以处理来自文件器的投放。

图 7.4：DropLabel 在接收带有 Qt-4 标志的投放后

![](img/b663c93885d7333a091a433460ee647f_202_0.png)

## 7.5 事件、拖放与剪贴板

`Clipboard` 类负责存储可以在应用程序之间粘贴的数据。与剪贴板以及拖放的交互由 `mousePressEvent()`、`dragEnterEvent()` 和 `dropEvent()` 方法处理。

## 7 事件、拖放与剪贴板

接下来，`dropEvent()` 的执行的操作与 `mousePressEvent()` 正好相反。它在首先检查指针的有效性后，从 `QDropEvent` 的 MIME 数据中克隆 MIME 数据，以便其可以将其传递到 `QClipboard` 实例中：

```cpp
// drag2clip/d2label.cpp (continued)

void D2clabel::dropEvent(QDropEvent *event) {
    if (event && event->mimeData()) {
        QApplication::clipboard()->setMimeData(cloneMimeData(
            event->mimeData()));
    }
}
```

图 7.5：Drag2Clip 在拖放系统与剪贴板之间起到调节作用。

![](img/b663c93885d7333a091a433460ee647f_205_0.png)

最后，`cloneMimeData()` 使用 `formats()` 方法，该方法包含所有以字符串列表形式存在的 MIME 类型。我们使用此列表配合 `data()` 方法来读取条目的数据及其 MIME 类型。通过这种方式，借助 `setData()` 创建一个新的 `QMimeData` 对象。这样，我们就获取了内容的精确拷贝：

```cpp
// drag2clip/d2label.cpp (continued)

QMimeData* D2clabel::cloneMimeData(const QMimeData *data) {
    if (!data) {
        return 0;
    }

    QMimeData *newData = new QMimeData;
    foreach (QString format, data->formats()) {
        newData->setData(format, data->data(format));
    }
    return newData;
}
```

用于验证此功能的测试应用程序实例化了 `D2clabel`，并将其大小设置为 400x150 像素，与之前的 `DropLabel` 一样，以便有足够的空间作为“放置区域”：

```cpp
// drag2clip/main.cpp

#include <QtGui>
#include "d2clabel.h"

int main(int argc, char* argv[])
{
    QApplication app(argc, argv);
    D2cLabel w;
    w.resize(400, 150);
    w.setWindowTitle(QObject::tr("Drag2Clip"));
    w.show();
    return app.exec();
}
```
