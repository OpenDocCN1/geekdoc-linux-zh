
```cpp
if (alignment == Qt::AlignLeft || alignment == Qt::AlignRight) {
    for (int i = 0; i < items.count(); ++i)
        items(i)->moveBy(coordinates.at(i), 0);
} else {
    for (int i = 0; i < items.count(); ++i)
        items(i)->moveBy(0, coordinates.at(i));
}
setDirty(true);
```

在这里我们遍历每一个项目，根据所需的量对其进行水平或垂直移动，使其与最左侧（或最右侧，依此类推）项目对齐。一旦所有项目移动完毕，我们就调用 `setDirty()`，因为场景发生了显著变化。

从用户的角度来看，一旦他们调用对齐动作，选中的项目会立即吸附到新位置。在第 13 章中，我们将重新讨论这种方法，并展示如何对对齐进行动画处理，使用户更容易看出哪些项目移动了，同时让移动在视觉上更加优雅。

```cpp
void MainWindow::populateCoordinates(const Qt::Alignment &alignment,
    QVector<double>* *coordinates,
    QList<QGraphicsItem*> *items)
{
    QList<QGraphicsItem*> i(items);
    while (i.hasNext()) {
        QRect rect = i.next()->sceneBoundingRect();
        switch (alignment) {
            case Qt::AlignLeft:
                coordinates->append(rect.x()); break;
            case Qt::AlignRight:
                coordinates->append(rect.x() + rect.width()); break;
            case Qt::AlignTop:
                coordinates->append(rect.y()); break;
            case Qt::AlignBottom:
                coordinates->append(rect.y() + rect.height()); break;
        }
    }
}
```

# 场景、项目与动作

此方法遍历给定的项目列表，并用提供的双精度浮数向量填充相应的 `x` 或 `y` 坐标。`QGraphicsItem::sceneBoundingRect` 方法返回项目在场景坐标中的边界矩形。虽然使用 `QGraphicsItem::boundingRect()` 常见得多（它返回项目在项目坐标中的边界矩形），但在这里我们需要在场景内移动项目（即使它们对齐）。来自 `QGraphicsItem` API 的选方法以及该 API 使用的关键枚举，已在之前的表 11.1 到 11.7 (403–407) 中介绍过。

绘制程序的另一个要求是能够垂直或水平地分布项目。这意味着在给定三个或更多项目的情况下，保持两端固定，移动中间的一个或多个项目，使得每个项目之间的间隙相等。由于实现此功能不会教授更多关于图形/视图架构的知识，我们将此留作练习题。

在离开本小节之前，我们将回顾一个操作项目的槽。

```cpp
void MainWindow::selectionChanged() {
  QList<GraphicsItem*> items = scene->selectedItems();
  if (items.count() == 1) {
    if (QObject *item = dynamic_cast<QObject*>(items.at(0))) {
      if (item->property("brush").isValid())
        brushWidget->setBrush(item->property("brush").value<QBrush>());
      if (item->property("pen").isValid())
        penWidget->setPen(item->property("pen").value<QPen>());
      if (item->property("angle").isValid())
        transformWidget->setAngle(item->property("angle").toDouble());
      transformWidget->setShear(
        item->property("shearHorizontal").toDouble(),
        item->property("shearVertical").toDouble()
      );
    }
  }
  updateUI();
}
```

# 第 12 章：创建图形/视图场景

此槽连接到 `QGraphicsScene::selectionChanged()` 信号，我们利用它来确保工具箱反映选中项目的属性。（如之前所述，使用 `dynamic_cast<>` 使应用程序依赖 `RTTI`——运行时类型信息）。

我们在这里关注的是选择变化导致选中单个项目的情况。如果选中了多个项目，我们不知道应该显示哪一个画刷、画笔或变换属性，因此在这种情况下我们保持工具箱不变。

我们无法在选中多个项目时禁用工具箱，尽管可以一次性进行操作，例如旋转所有选中的项目或更改它们的画刷。

我们再次使用 Qt 的元对象系统使该方法尽可能通用，这样即使添加新项目也不需要更改它。（而且如前所述，我们可以使用 `qgraphics_item_cast()`）。

选了多少项目（无、一个或两个）会正确影响用户界面。如果没有选中项目，则工具箱控件应该禁用，因为它们无法产生影响；如果恰好选中了一个，“编辑选中项目”动作应该启用；如果选中了两个或更多项目，对齐动作应该启用。所有这一切都由我们即将展示的 `update()` 槽处理（► 436）。

# 场景、项与动作

## 显示与隐藏指南网格

显示指南网格最简单且合适的方法可能是通过 `QGraphicsScene::setBackgroundBrush()` 将场景背景设置为一个画刷，或者通过重新实现 `QGraphicsScene::drawBackground()` 方法。我们之所以没有选择这两种方法中的任何一种，完全是为了展示如何使用 `QGraphicsItemGroup`，以及如何对我们使用或操作的项进行选择性处理。

在 `Page Designer` 应用程序，我们有一个 `viewShowGridAction` 切换动作，它连接到 `viewShowGrid()` 槽，该槽负责创建和隐藏指南网格。

```cpp
void MainWindow::viewShowGrid(bool on) {
  if (gridGroup) {
    const int GridSize = 40;
    QPen pen(QColor(175, 175, 175, 127));
    gridGroup = new QGraphicsItemGroup();
    const int MaxX = static_cast<int>(std::ceil(scene->width()) / GridSize);
    const int MaxY = static_cast<int>(std::ceil(scene->height()) / GridSize);
    for (int x = 0; x <= MaxX; x += GridSize) {
      QGraphicsLineItem *item = new QGraphicsLineItem(x, 0, x, MaxY);
      item->setPen(pen);
      item->setValue(std::numeric_limits<int>::min());
      gridGroup->addToGroup(item);
    }
    scene->addItem(gridGroup);
    gridGroup->setVisible(on);
}
```

当调用此方法时，如果指南网格组不存在，我们会创建它——例如，因为应用程序刚刚启动，或者我们清空了场景。我们将绘制指南的笔设置为半透明的浅灰色。这意味着这是一个宽度为 1 像素的化妆画笔（`cosmetic pen`）。化妆画笔（无论宽度如何）在应用何种变换的情况下，始终按其指定的宽度绘制（宽度为 0 的情况被视为 1）。与之对比的是，非化妆画笔的宽度会根据任何生效的缩放按比例缩放。

我们创建一个新的 `QGraphicsItemGroup` 并计算场景中尽可能远的 `x` 和 `y` 坐标。然后，我们以 `GridSize` 为增量，从 `x` 坐标 0 迭代到 `MaxX`，在每次迭代中，我们创建一个标准的 `QGraphicsLineItem` 并传递 `(x1, y1, x2, y2)` 坐标。由于我们给了它两个相同的 `x` 坐标和不同的 `y` 坐标，因此我们创建了一条垂直线。我们将该线的指针设置为我们之前创建的那个，并给它一个很大的负 `z` 值，然后将其添加到组中。绘制水平线也有类似的循环，但这里为了简洁省略了，它在结构上与所示的相同。

当 `QGraphicsItem` 被创建时，所有的图形标志都是禁用的，因此，例如，默认情况下用户无法移动或选择该图形项。这种行为正是我们指南所需要的。

一旦所有线条项都已创建并添加到组中，该组就会被添加到场景中。最后，我们根据信号传递的槽参数的布尔值，显示或隐藏该组（以及它包含的所有线条项）。

顺便提一下，`<cmath>` 中的 `std::ceil` 函数返回大于等于其参数的最小整数，而 `<limits>` 中的 `std::numeric_limits<int>::min` 函数返回最小（即最负）的整数。

我们在这里还没有涵盖的一种方法是 `editClearTransforms()`；我们将稍后介绍；在“图形项变换”（`Graphics Item Transformations`）子章节 453 的结尾。

## 保持用户界面更新

将应用程序状态的变化反映到用户界面的一种“懒”方法是完全不进行反映。通过这种方法，用户可以随时间调用任何动作，每个动作都负责检查该操作是否合理，如果不合理则什么都不做。例如，我们可以让“粘贴”动作保持启用状态，即使没有可粘贴的内容；同样地，如果没有选择任何项（因此没有可复制的内容），我们也让“复制”动作保持启用状态。

遗憾的是，让每个动作都保持启用状态会让用户感到困惑。例如，他们可能会调用“粘贴”动作并疑惑为什么什么都没有出现。因此，我们倾向于根据应用程序的状态启用或禁用动作以及停靠窗口（`dock widgets`）内部的控件。这并不总是容易的。例如，如果用户选择了一个框、一个笑脸和一个文本项，我们应该启用哪些工具箱控件？我们可以启用适用于所有选中项的工具箱或工具箱，在这种情况下我们只启用变换工具箱。对于 `Page Designer`，我们决定这样做对用户来说不方便，相反，我们启用适用于至少一个选中项的每个工具箱。所以，在这种情况下，我们启用了变换、画笔和画刷工具箱，尽管文本项没有画笔或画刷属性。这种效果良好，因为如果我们更改了（例如）画刷，更改将被文本项安全地忽略，但将正确应用到任何选中的框和笑脸项。

在 `Page Designer` 中，每当发生重大变化时，就会调用 `setDirty()` 槽。在“保存”动作的情况下，它带 `false` 参数调用，因为保存后场景不再是“脏”的（未修改）。但对于大多数其他变化，它带 `true` 调用（这是其参数的默认值）。

```cpp
void MainWindow::setDirty(bool on)
{
    setMimeData(on);
    updateUI();
}
```

与其维护自己的“脏”成员变量，我们可以使用主窗口的 `windowModified` 属性。每当脏状态发生变化时，我们就调用 `updateUI()`（在其他地方也会被调用——例如在 `editCopy()` 和 `selectionChanged()` 中），以适当地启用或禁用应用程序的动作和工具箱控件。

```cpp
void MainWindow::updateUI()
{
    fileAction->setEnabled(isWindowModified());
    bool hasItems = scene->hasItems();
    fileSaveAction->setEnabled(hasItems);
    fileExportAction->setEnabled(hasItems);
    btnPrintAction->setEnabled(hasItems);
    int selected = scene->selectedItems().count();
    editSelectedItemAction->setEnabled(selected == 1);
    editCopyAction->setEnabled(selected >= 1);
    editCutAction->setEnabled(selected >= 1);
    QClipboard *clipboard = QApplication::clipboard();
    const QMimeData *mimeData = clipboard->mimeData();
    editPasteAction->setEnabled(mimeData &&
        (mimeData->hasFormat(mimeType) || mimeData->hasText()));
    editAlignmentAction->setEnabled(selected >= 2);
    editTransformsAction->setEnabled(selected >= 1);
    transformWidget->setEnabled(selected >= 1);
    bool hasBrushProperty;
    bool hasPenProperty;
    selectionProperties(&hasBrushProperty, &hasPenProperty);
    brushWidget->setEnabled(hasBrushProperty);
    penWidget->setEnabled(hasPenProperty);
}
```

# 场景、项目与动作

```
}
}
}
```

该方法遍历每个选中的项目，检查它是否具有画刷（`brush`）或笔（`pen`）属性。我们包含了一个微小的效率优化方法：如果画刷和笔属性都为真，我们知道可以立即返回。（如前所述，使用 `dynamic_cast()` 使得应用程序依赖于 `RTTI` 的可用性，尽管这是可以避免的；424 ◄）

# 增强 QGraphicsView

`GraphicsView` 类本身不支持缩放功能，因此我们创建了一个微小的子类（所有实现都在头文件中），它提供了必要的功能，并借此开启了抗锯齿和橡皮筋选择的支持。以下是 `GraphicsView` 类的完整定义：

```cpp
class GraphicsView : public QGraphicsView
{
    Q_OBJECT
public:
    explicit GraphicsView(QWidget *parent=0) : QGraphicsView(parent)
{
        setDragMode(RubberBandDrag);
        setRenderHints(QPainter::Antialasing|
        QPainter::TextAntialasing);
    }
public slots:
    void zoomIn() { scaleBy(1.1); }
    void zoomOut() { scaleBy(1.0 / 1.1); }
protected:
    void wheelEvent(QWheelEvent *event)
{
        scaleBy(std::pow(4.0 / 3.0, -event->delta() / 240.0)));
    }
private:
    void scaleBy(double factor) { scale(factor, factor); }
};
```

在构造函数中，我们首先开启橡皮筋拖动模式。这意味着如果用户点击并拖动，就会拉出一个橡皮筋（即一个矩形，在某些平台上填充有半透明颜色），每个接触矩形的项目都会被选中。默认拖动模式是 `QGraphicsView::NoDrag`，它什么都不做。我们支持一种拖动模式：

`QGraphics::ScrollHandDrag`；设置此项时，点击并拖动将滚动视图。

为了支持缩放，我们提供了两个槽，其中一个用于缩放视图。我们还重新实现了鼠标轮处理器，以便根据滚轮旋转距离进行比例缩放——向前移动时缩小，向后移动时放大。`Wheels::delta()` 报告滚轮旋转的“步数”（每步通常对应于滚轮旋转 15°），其中正值表示向前移动，负值表示向后移动。来自 `<cmath>` 头文件的 `std::pow()` 函数将其第一个参数提升到第二个参数指定的幂次。本质上，我们做的是每转一轮，就按 `1/x` 的因子增加或减少缩放。所有的缩放都由私有方法 `scaleBy()` 完成，它简单地调用 `scale()` 方法水平和垂直地保持视图的纵横比例。

默认情况下，`QView` 使用鼠标轮事件进行滚动，通过重新实现 `wheelEvent()` 处理器，我们有效地禁用了这种行为。只有当鼠标位于滚动器上时，用户才能使用鼠标轮滚动。

# 创建工具箱 Widget
