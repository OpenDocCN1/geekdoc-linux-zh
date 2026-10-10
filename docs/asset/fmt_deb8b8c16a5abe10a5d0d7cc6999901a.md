
当我们创建想要手动绘制的 `QGraphicsItem` 子类时，我们通常会重新实现 `boundingRect()` 和 `paint()`。如果没有重新实现 `shape()`，基类的实现将回退到 `boundingRect()`。在这种情况下，我们重新实现了 `shape()`，以返回一个考虑了节点圆角的更准确的形状。

图形视图架构使用边界矩形来确定项是否需要绘制。这使得 `QGraphicsView` 能够非常快速地显示任意大的场景，即使在任何时刻只有一部分项可见的。`shape` 用于判断一个点是否在项内部，或者两个项是否碰撞。

```cpp
protected:
    void mouseDoubleClickEvent(QGraphicsSceneMouseEvent *event);
    QVariant itemChange(GraphicsItemChange change, const QVariant &value);
```

在 `Diagram` 应用程序中，我们将提供一个属性对话框来编辑节点的位置、颜色和文本。作为额外的便利，我们将允许用户通过双击节点来更改文本。

如果节点被移动，我们必须确保任何相关的链接都相应地更新。我们重新实现了 `itemChange()` 处理器来处理这个问题；每当项的属性（包括它的位置）发生变化时，它就会被调用。我们不为此目的使用 `mouseMoveEvent()` 的原因是，当通过程序移动节点时，它不会被调用。

```cpp
private:
    QRectF outlineRect() const;
    int roundness(double size) const;
    QSet<Link *> myLinks;
    QString myText;
    QColor myTextColor;
    QColor myBackgroundColor;
    QColor myOutlineColor;
};
```

`outlineRect()` 私有函数返回由 `Node` 绘制的矩形，而 `roundness()` 根据矩形的宽度或高度返回合适的圆角系数。

就像 `Link` 跟踪它连接的节点一样，`Node` 也跟踪它的链接。当节点被删除时，所有与节点相关的链接也会被删除。

我们现在准备好查看 `Node` 的实现了，按照习惯从构造函数开始。

```cpp
Node::Node()
{
    myTextColor = Qt::darkGreen;
    myOutlineColor = Qt::darkBlue;
    myBackgroundColor = Qt::white;
    setFlags(ItemMovable | ItemSelectable);
}
```

我们初始化颜色，并使项可移动且可选择。`z` 值将默认为 0，我们将位置交给调用者设置。

```cpp
Node::~Node()
{
    foreach (Link *link, myLinks)
        delete link;
}
```

析构函数删除节点的链接。当一个链接被销毁时，它会从它连接的节点中移除自己。我们遍历链接集的副本而不是使用 `deleteAll()` 以避免副作用。

```cpp
void Node::setText(const QString &text)
{
    prepareGeometryChange();
    myText = text;
    update();
}
```

当我们以影响外观的方式更改图形项时，必须调用 `update()` 来调度绘制。在边界矩形可能会变化的情况下（例如新文本比当前文本短或长），我们必须在执行任何影响边界矩形的操作之前调用 `prepareGeometryChange()`。跳过 `text()`、`textColor()` 和 `backgroundColor()` getter，因为它们简单地返回私有成员。

```cpp
void Node::setTextColor(const QColor &color)
{
    myTextColor = color;
    update();
}
```

当我们设置文本颜色时，必须调用 `update()` 来调度绘制，以便使用新颜色绘制项。我们不需要调用 `prepareGeometryChange()`，因为项的大小不受颜色改变的影响。我们将省略轮廓和背景颜色的 setter，因为它们与此 setter 结构相同。

```cpp
void Node::addLink(Link *link)
{
    myLinks.insert(link);
}

void Node::removeLink(Link *link)
{
    myLinks.remove(link);
}
```

在这里简单地将给定的链接添加到节点的链接集合中。

```cpp
QRectF Node::outlineRect() const
{
    const int Padding = 8;
    QFontMetricsF metrics = qApp->font();
    QRectF rect = metrics.boundingRect(myText);
    rect.adjust(-Padding, -Padding, +Padding, +Padding);
    rect.translate(-rect.center());
    return rect;
}
```

我们使用这个私有函数计算一个包含节点文本带有 8 像素边距的矩形。字体度量函数返回的边界矩形以 `(0, 0)` 为左上角。由于我们希望文本与项的中心点对齐，因此我们将矩形移动使其中心位于 `(0, 0)`。虽然我们以像素进行思考和计算，但该单位在意义上是概念性的。

```cpp
QRectF Node::boundingRect() const
{
    const int Margin = 1;
    return outlineRect().adjusted(-Margin, -Margin, +Margin, +Margin);
}
```

`boundingRect()` 函数由 `QGraphicsView` 调用，用于判断该项是否需要绘制。我们使用了轮廓矩形，但增加了一些额外的外边距，因为如果需要绘制轮廓，从此函数返回的矩形必须至少容纳画笔宽度的一半。

```cpp
QPainterPath Node::shape() const
{
    QRectF rect = outlineRect();
    QPainterPath path;
    path.addRoundRect(rect, roundness(rect.width()), roundness(rect.height()));
    return path;
}
```

`shape()` 函数由 `QGraphicsView` 用于精细粒度的碰撞检测。通常情况下，我们可以省略它，让该项根据边界矩形自己计算形状。在这里，我们重新实现了它，返回一个表示圆角矩形的 `QPainterPath`。结果是，点击位于圆角矩形之外但在边界矩形之内的区域将不会选中该项。

当我们创建一个圆角矩形时，可以传递可选参数来指定圆角的圆润度。我们使用私有函数 `roundness()` 计算合适的值。

```cpp
void Node::paint(QPainter *painter,
                 const QStyleOptionGraphicsItem *option,
                 QWidget * /* widget */)
{
    QPen pen(myOutlineColor);

    if (option->state & QStyle::State_Selected) {
        pen.setStyle(Qt::DotLine);
        pen.setWidth(2);
    }

    painter->setPen(pen);
    painter->setBrush(myBackgroundColor);
    QRectF rect = outlineRect();
    painter->drawRoundRect(rect, roundness(rect.width()), roundness(rect.height()));

    painter->setPen(myTextColor);
    painter->drawText(rect, Qt::AlignCenter, myText);
}
```

`paint()` 函数是绘制该项的地方。如果该项被选中，我们会将画笔样式更改为虚线并将其加粗；否则，使用默认的 1 像素实线。我们还设置了画刷以使用背景颜色。

然后，我们绘制一个与轮廓矩形一样大的圆角矩形，但使用了由 `roundness()` 私有函数返回的圆角因子。最后，我们在轮廓矩形之上绘制居于圆角矩形的文本。

类型为 `QStyleOptionGraphicsItem` 的 `option` 参数是 Qt 中一个不常见的类，因为它提供了几个公共成员变量。这些包括当前的布局方向、字体属性、调色板、矩形、状态（选中、“具有焦点”以及许多其他）、变换矩阵和细节水平。在这里，我们检查了 `state` 成员以查看节点是否被选中。

```cpp
QVariant Node::itemChange(GraphicsItemChange change,
                          const QVariant &value)
{
    if (change == ItemPositionHasChanged) {
        foreach (Link *link, myLinks)
            link->trackNodes();
    }
    return QGraphicsItem::itemChange(change, value);
}
```

每当用户拖动节点时，`itemChange()` 处理器就会被调用，并将 `ItemPositionHasChanged` 作为第一个参数。为了确保连线位置正确，我们遍历了节点的链接集合，并告诉每条线更新其线的端点。最后，我们调用基类的实现以确保它也能收到通知。

```cpp
void Node::mouseDoubleClickEvent(QGraphicsSceneMouseEvent *event)
{
    QString text = QInputDialog::getText(event->widget(),
                                         tr("Edit Text"), tr("Enter new text:"),
                                         QLineEdit::Normal, myText);
    if (!text.isEmpty())
        setText(text);
}
```

如果用户双击节点，我们会弹出一个对话框显示当前文本并允许他们更改它。如果用户点击“取消”，将返回一个空字符串；因此，我们只在字符串非空时才应用更改。稍后我们将看到其他节点属性（如节点的颜色）是如何更改的。

```cpp
int Node::roundness(double size) const
{
    const int Diameter = 12;
    return 100 * Diameter / int(size);
}
```

`roundness()` 函数返回合适的圆角因子，以确保节点的角是直径为 12 的四分之一圆。圆角因子必须在 0（正方形）到 99（完全圆角）之间。

我们现在已经看到了两个自定义图形项类的实现。现在是时候看看它们实际上是如何被使用的。`Diagram` 应用程序是一个带有菜单和工具栏的标准主窗口应用程序。我们不会查看实现的所有细节，而是关注那些与图形视图架构相关的部分。我们将从查看 `QMainWindow` 子类定义的一个片段开始。

```cpp
class DiagramWindow : public QMainWindow
{
    Q_OBJECT
public:
    DiagramWindow();
private slots:
    void addNode();
    void addLink();
    void del();
    void cut();
    void copy();
    void paste();
    void bringToFront();
    void sendToBack();
    void properties();
    void updateActions();
private:
    typedef QPair<Node *, Node *> NodePair;
    void createActions();
    void createMenus();
    void createToolBars();
    void setZValue(int z);
    void setupNode(Node *node);
    Node *selectedNode() const;
    Link *selectedLink() const;
    NodePair selectedNodePair() const;
    QMenu *file;
    QMenu *edit;
    QToolBar *editBar; // 原文中此处为 editBar
    QAction *exitAction;
    QAction *propertiesAction;
    QGraphicsScene *scene;
    QGraphicsView *view;
    int minZ;
    int maxZ;
    int seqNumber;
};

DiagramWindow::DiagramWindow()
{
    scene = new QGraphicsScene(0, 0, 600, 500);
    view = new QGraphicsView;
    view->setScene(scene);
    view->setDragMode(QGraphicsView::RubberBandDrag);
    view->setRenderHints(QPainter::Antialiasing | QPainter::TextAntialiasing);
    setCentralWidget(view);
    minZ = 0;
    maxZ = 0;
    seqNumber = 0;
    createActions();
    createMenus();
    createToolBars();
    connect(scene, SIGNAL(selectionChanged()), this, SLOT(updateActions()));
    setWindowTitle(tr("Diagram"));
}
```

我们创建一个图形场景，起点为 `(0,0)`，宽度为 600，高度为 500。然后我们创建一个图形视图来可视化该场景。在下一个示例中，我们不直接使用 `QGraphicsView`，而是对其进行子类化以自定义其行为。可点击项可以通过点击选取。将拖动模式设置为 `QGraphicsView::RubberBandDrag` 意味着用户也可以框选择。`minZ` 和 `maxZ` 数字被 `sendToBack()` 和 `bringToFront()` 函数使用。序列号用于赋予初始文本。

```cpp
void DiagramWindow::addNode()
{
    Node *node = new Node;
    node->setText(tr("Node %1").arg(seqNumber + 1));
    setupNode(node);
}
```

该函数将新添加或粘贴的节点位于场景中。使用序列号确保新节点在不同的位置添加，而不是重叠。我们清除当前选择并只选择新添加的节点。`bringToFront()` 调用确保新节点比任何其他节点靠前。

```cpp
void DiagramWindow::setupNode(Node *node)
{
    node->setPos(QPoint(80 + (100 * (seqNumber % 5)),
                         80 + (50 * ((seqNumber / 5) % 7))));
    scene->addItem(node);
    ++seqNumber;
    scene->clearSelection();
    node->setSelected(true);
    bringToFront();
}

void DiagramWindow::bringToFront()
{
    ++maxZ;
    setZValue(maxZ);
}

void DiagramWindow::sendToBack()
{
    --minZ;
    setZValue(minZ);
}

void DiagramWindow::setZValue(int z)
{
    Node *node = selectedNode();
    if (node)
        node->setZValue(z);
}
```

`bringToFront()` 槽函数增加了 `maxZ` 值，然后将所选中节点的 `z` 值设置为 `maxZ`。`sendToBack()` 槽使用 `minZ` 并具有相反的效果。它们都是根据私有函数 `setZValue()` 来定义的。

```cpp
Node *DiagramWindow::selectedNode() const
{
    QList<QGraphicsItem *> items = scene->selectedItems();
    if (items.count() == 1) {
        return dynamic_cast<Node *>(items.first());
    } else {
        return 0;
    }
}
```

通过调用 `QGraphicsScene::selectedItems()` 可以获取场景中所有选中项目的列表。`selectedNode()` 函数的设计是：当只选中一个节点时返回该节点，否则返回空指针。如果恰好选中了一个项，如果该项是 `Node`，则转换将产生一个 `Node` 指针；如果该项是 `Link`，则产生空指针。

还有一个 `selectedLink()` 函数，如果恰好选中了一个项且该项是 `Link`，它将返回所选中 `Link` 项的指针。

```cpp
void DiagramWindow::addLink()
{
    NodePair nodes = selectedNodePair();
    if (nodes == NodePair())
```
