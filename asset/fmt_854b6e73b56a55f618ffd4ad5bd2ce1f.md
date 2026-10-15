
### Link 类实现

```cpp
nextNode(toNode)
{
    fromNode->addLink(this);
    nextNode->addLink(this);
    setPen(Qt::black);
}

Link::~Link()
{
    fromNode->removeLink(this);
    nextNode->removeLink(this);
}

Node * Link::fromNode() const
{
    return fromNode;
}

Node * Link::nextNode() const
{
    return nextNode;
}

void Link::setColor(const QColor& color)
{
    setPen(QPen(color));
}

QColor Link::color() const
{
    return pen().color();
}
```

### Node 类定义

```cpp
class Node : public QGraphicsItem
{
    Q_DECLARE_TRACES(Node)
  public:
    Node();
    void setText(const QString& text);
    QString text() const;
    void setColor(const QColor& color);
    QColor color() const;
    void setOutlineColor(const QColor& color);
    QColor outlineColor() const;
    void setBackgroundColor(const QColor& color);
    QColor backgroundColor() const;
    void addLink(Link* link);
    void removeLink(Link* link);
  private:
    QString text;
    QColor color;
    QColor outlineColor;
    QColor backgroundColor;
    QList<Link*> links;
};
```

### Node 基础方法实现

```cpp
Node::Node()
{
    color = Qt::black;
    outlineColor = Qt::black;
    backgroundColor = Qt::white;
}

void Node::setText(const QString& text)
{
    text = text;
}

QString Node::text() const
{
    return text;
}

void Node::setColor(const QColor& color)
{
    color = color;
}

QColor Node::color() const
{
    return color;
}

void Node::setOutlineColor(const QColor& color)
{
    outlineColor = color;
}

QColor Node::outlineColor() const
{
    return outlineColor;
}

void Node::setBackgroundColor(const QColor& color)
{
    backgroundColor = color;
}

QColor Node::backgroundColor() const
{
    return backgroundColor;
}

void Node::addLink(Link* link)
{
    links.append(link);
}

void Node::removeLink(Link* link)
{
    links.remove(link);
}
```

### Node 几何与绘制方法

```cpp
QRectF Node::boundingRect() const
{
    return QRectF(-50, -50, 100, 100);
}

void Node::paint(QPainter* painter, const QStyleOptionGraphicsItem* option, QWidget* widget) const
{
    (void)option;
    (void)widget;
    painter->setBrush(backgroundColor);
    painter->setPen(outlineColor);
    painter->drawRoundedRect(boundingRect(), 10, 10);
    painter->drawText(boundingRect(), Qt::AlignCenter, text);
}

QPath Node::shape() const
{
    return boundingRect();
}
```

如果不重新实现`shape()`，基类实现将回退到使用`boundingRect()`。在这种情况下，我们重新实现了`shape()`，以返回一个更精确的形状，该形状考虑了节点的圆角。

```cpp
    setLine(QLineF(myNode->pos(), myToNode->pos()));
}
```

## 基于项目的 Graphics View 渲染

Graphics View 架构使用边界矩形（bounding rectangle）来确定一个项是否需要绘制。这使得`GraphicsView`能够在任何给定时间只有部分项可见的情况下，非常快速地显示任意大小的场景。该形状被用于判断一个点是否在项内部，或者两个项是否发生碰撞。

```cpp
protected:
    void mouseDoubleClick(QGraphicsSceneMouseEvent *event);
    QVariant itemChange(GraphicsItemChange change,
                       const QVariant &value);
```

在`Diagram`应用程序中，我们将提供一个属性对话框用于编辑节点的位置、颜色和文本。为了方便起见，我们将允许用户通过双击节点来更改文本。

如果节点移动，我们必须确保任何相关的链接都随之更新。我们实现了`itemChange()`处理器来处理这个问题；每当节点的属性（包括其位置）发生变化时，该处理器就会被调用。我们不使用`mouseMoveEvent`来实现此目的，是因为当通过程序代码移动节点时，该方法不会被调用。

```cpp
private:
    QRect outlineRect() const;
    int roundness(double size) const;
    QSet<Link *> myLinks;
    QString myText;
    QColor myTextColor;
    QColor myBackgroundColor;
    QColor myOutlineColor;
```

`outlineRect()`私有函数返回由`Node`绘制的矩形，而`roundness()`则根据矩形的宽度和高度返回一个合适的圆角系数。

就像`Link`会跟踪它连接的节点一样，`Node`也会跟踪它的链接。当节点被删除时，所有与该节点相关的链接也会被删除。

我们现在准备好查看`Node`的实现，按照惯例从构造函数开始。

```cpp
Node::Node()
{
    myTextColor = Qt::darkGreen;
    myOutlineColor = Qt::darkBlue;
    myBackgroundColor = Qt::white;
    setFlags(ItemIsMovable | ItemIsSelectable);
}
```

我们初始化了颜色，并使节点项变为可移动和可选的。`z`值默认为`0`，我们将节点在场景中的位置留给调用者设置。

```cpp
Node::Node()
{
    foreach (Link *link, myLinks)
        delete link;
}
```

析构函数删除了节点所有的链接。每当一个链接被销毁时，它会从它连接的节点中移除自己。我们遍历链接集的（副本）而不是使用`deleteAll()`来避免副作用，因为链接集会被`Link`的析构函数间接访问。

```cpp
void Node::setText(const QString &text)
{
    prepareGeometryChange();
    myText = text;
    update();
}
```

当我们以影响外观的方式更改图形项时，我们必须调用`update()`来调度重绘。在项的边界矩形可能会变化的情况下（因为新文本可能比当前文本短或长），我们必须在执行任何会影响项边界矩形的操作之前，立即调用`prepareGeometryChange()`。

我们将跳过`text()`、`textColor()`、`outlineColor()`和`backgroundColor()`访问器，因为它们简单地返回对应的私有成员。

```cpp
void Node::setTextColor(const QColor &color)
{
    myTextColor = color;
    update();
}
```

当我们设置文本颜色时，我们必须调用`update()`来调度重绘，以便项用新颜色进行绘制。我们不需要调用`prepareGeometryChange()`，因为项的大小不会受颜色变化的影响。我们将省略轮廓和背景颜色的setter，因为它们在结构上与此setter相同。

```cpp
void Node::addLink(const Link *link)
{
    myLinks.insert(link);
}
```

```cpp
void Node::removeLink(const Link *link)
{
    myLinks.remove(link);
}
```

我们只需将给定的链接添加到节点的链接中。

```cpp
QRectF Node::outlineRect() const
{
  const int Padding = 8;
  QFontMetrics metrics = qApp->font();
  QRectF rect = metrics.boundingRect(myText);
  rect.adjust(-Padding, -Padding, +Padding, +Padding);
  rect.translate(-rect.center());
  return rect;
}
```

我们计算一个包含8像素边距的文本的矩形。`metrics`返回的边界矩形以(0, 0)为左上角。由于我们希望文本在项的中心居中，我们移动矩形使其中心位于(0, 0)。

尽管我们是以像素进行思考和计算的，但单位并不是。场景（或父项）可能会被缩放、倾斜或受抗锯齿影响，屏幕上显示的像素数量可能会不同。

```cpp
QRectF Node::boundingRect() const
{
  const int Margin = 1;
  return outlineRect().adjusted(-Margin, -Margin, +Margin, +Margin);
}
```

`GraphicsView`调用`boundingRect()`来判断项是否需要绘制。我们使用轮廓矩形，但留了一些边距，因为如果要绘制，此函数返回的矩形必须允许线条宽度。

```cpp
QPath Node::shape() const
{
  QRectF rect = outlineRect();
  QPath path;
  path.addRoundRect(rect, roundness(rect.width()),
  roundness(rect.height()));
  return path;
}
```

`GraphicsView`调用`shape()`进行细粒度的碰撞检测。通常我们可以省略它让项自己根据边界矩形计算形状。我们重新实现了它以返回代表圆矩形的`QPath`。结果，点击圆矩形之外边界矩形之内的区域不会选中项。当我们创建一个圆矩形时，可以传递可选参数来指定圆角的粗细。我们使用`roundness()`函数计算合适的值。

```cpp
void Node::paint(QPainter *painter,
             const QStyleOptionItem *option,
             QWidget *widget)
{
    QPen pen(myOutlineColor);
    if (option->state & QStyle::State_Selected) {
        pen.setStyle(Qt::DotLine);
        pen.setWidth(2);
    }

    painter->setPen(pen);
    painter->setBrush(myBackgroundColor);
    QRectF rect = outlineRect();
    painter->drawRoundedRect(rect, roundness(rect.width()),
                             roundness(rect.height()));
    painter->setPen(myTextColor);
    painter->drawText(rect, Qt::AlignCenter, myText);
}
```

`paint()`函数用于绘制项。如果选中，我们将线条样式更改为虚线并加粗；否则使用默认的1像素线条。还将画刷设置为背景颜色。

然后使用`roundness()`函数返回的圆角因子绘制与轮廓矩形同样大的圆矩形。最后，我们在圆矩形上方的轮廓矩形内居中绘制文本。

`QStyleOptionItem`类型参数是Qt中一个特殊的类，因为它提供了多个公共成员变量。这些包括布局方向、字体度、调色板、矩形、状态（选中、获取焦点等）、变换矩阵和细节水平。我们检查了状态以判断节点是否被选中。

```cpp
QVariant Node::itemChange(GraphicsItemChange change)
```

每当用户拖动节点时，`itemChange()`处理器就会以`ItemPositionHasChanged`作为第一个参数被调用。为了确保线条位置正确，我们遍历节点的链接集并告诉每个链接更新其端点。最后，我们调用基类的实现以确保它也收到通知。

```cpp
void Node::mouseDoubleClick(QGraphicsMouseEvent *event)
{
    QString text = QInputDialog::getText(event->widget(),
    tr("Edit Text"), tr("Enter new text:"),
    QLineEdit::Normal, myText);

    if (!text.isEmpty()) {
        setText(text);
    }
}
```

如果用户双击节点，我们会弹出一个对话框显示当前文本并允许他们更改。如果用户点击取消，将返回一个空字符串；因此，我们只在字符串非空时应用更改。稍后我们将看到其他属性（如节点的颜色）如何被更改。

```cpp
int Node::roundness(double size) const {
    int Diameter = 12;
    return 100 * Diameter / int(size);
}
```

圆角函数返回合适的圆角因子，以确保节点的角是直径为12的四弧。圆角因子必须在0（正方形）到99（完全圆）的范围内。

我们现在看到了两个自定义图形项类的实现。现在是时候看看它们是如何被使用的。`Diagram`应用程序是一个带有菜单和工具栏的标准主窗口应用程序。我们不会查看实现的所有细节，而是关注那些与graphics view架构相关的部分。我们将从查看`QMainWindow`子类定义的一个片段开始。

```cpp
class DiagramWindow : public QMainWindow {
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
