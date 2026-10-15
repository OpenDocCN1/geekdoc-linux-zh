
我们没有显示`BooleanParser`类，因为它与GUI或模型/视图编程无关。此示例的完整源代码随书提供。在实现如`BooleanModel`这样的树模型时，很容易出错，导致`QTreeView`行为异常。为了发现并解决自定义数据模型中的问题，Trolltech提供了`ModelTest`。要使用`ModelTest`，请从`http://labs.trolltech.com/projects/Itemview/Modeltest`下载并遵循`README`文件中的说明。在本节中，我们看到许多模型比这里展示的简单得多，项与模型索引之间是一一对应对应关系。Qt本身还提供了更多模型/视图示例，并附有详细文档。

## 代理

视图中的每个项通过代理（delegates）进行渲染和编辑。在大多数情况下，视图提供的默认代理已经足够了。如果我们对项的渲染有更细致的控制，可以通过使用自定义模型来实现目标：在我们的`data()`实现中，我们使用了`Qt::FontRole`、`Qt::TextColorRole`和`Qt::BackgroundColorRole`，默认代理会使用这些。例如，在之前显示的城市和货币示例中，我们处理了`Qt::AlignmentRole`以实现数字右对齐。

如果我们想要更大的控制权，可以创建自己的代理类，并将其设置到我们使用的视图上。图 10.15 显示的轨道编辑器对话框使用了自定义代理。它显示了音乐轨目的标题和时长。模型持有的数据将是简单的`QString`（标题）以及整数（秒），但持续时间将被拆分为分钟和秒，并可以使用`QTimeEdit`进行编辑。

![](img/930c1c6fda99d425284503ebcbc940ea_289_0.png)

图 10.15 轨道编辑器对话框

轨道编辑器对话框使用了`StatefulWidget`，这是一个在`QTableWidgetItems`上操作的便捷视图子类。数据以`Tracks`列表的形式提供：

```cpp
class Track {
public:
    Track(const QString& title = "", int duration = 0);
    QString title;
    int duration;
};
```

这里是构造函数的一个片段，展示了表格部件的创建和填充：

```cpp
TrackEditor::TrackEditor(QList<Track> *tracks, QWidget *parent)
    : QDialog(parent)
{
    this->tracks = tracks;
    tableWidget = new QTableWidget(tracks->count(), 2);
    tableWidget->setItemDelegate(new TrackDelegate(1));
    tableWidget->setHorizontalHeaderLabels(QString() << "Track" << QString() << "Duration");
    for (int row = 0; row < tracks->count(); ++row) {
        Track track = tracks->at(row);
        QTableWidgetItem *item0 = new QTableWidgetItem(track.title);
        tableWidget->setItem(row, 0, item0);
        QTableWidgetItem *item1
            = new QTableWidgetItem(QString::number(track.duration));
        item1->setTextAlignment(Qt::AlignRight);
        tableWidget->setItem(row, 1, item1);
    }
}
```

### 实现自定义代理

构造函数创建了一个表格部件，我们没有简单地使用默认代理，而是设置了自定义的`TrackDelegate`，并传递持有时间数据的列。我们首先设置列标题，然后遍历数据，用每个轨道的名称和持续时间填充行。

构造函数的其余部分以及`TrackEditor`类的其余部分没有意外，我们现在查看处理轨道数据渲染和编辑的`TrackDelegate`类。

```cpp
class TrackDelegate : public QItemDelegate {
public:
    TrackDelegate(int durationColumn, QObject *parent = 0);
    void paint(QPainter *painter, const QStyleOptionView &option,
               const QModelIndex &index) const;
    QWidget *createEditor(QWidget *parent,
                          const QStyleOptionView &option,
                          const QModelIndex &index) const;
    void setEditorData(QWidget *editor, const QModelIndex &index) const;
    void setData(QWidget *editor, QAbstractItemModel *model,
                 const QModelIndex &index) const;

private slots:
    void commitAndCloseEditor();

private:
    int durationColumn;
};
```

我们使用`QItemDelegate`作为基类，这样我们可以从默认代理实现中受益。如果我们想从零开始，也可以使用`QAbstractItemDelegate`。为了提供一个可以编辑数据的代理，我们必须实现`createEditor()`、`setEditorData()`和`setData()`。我们还实现了`paint()`来改变持续时间列的渲染。

```cpp
TrackDelegate::TrackDelegate(int durationColumn, QObject *parent)
{
    this->durationColumn = durationColumn;
}
```

```cpp
TrackDelegate::paint(QPainter *painter,
                    const QStyleOptionView &option,
                    const QModelIndex &index) const
{
    if (index.column() == durationColumn) {
        int secs = index.model()->data(index, Qt::DisplayRole).toInt();
        QString text = QString("%1s:%2")
            .arg(secs % 60, 2, 10, QChar('0'))
            .arg(secs / 60, 2, 10, QChar('0'));

        QStyleOptionViewItem myOption = option;
        myOption.displayAlignment = Qt::AlignRight | Qt::AlignCenter;
        drawDisplay(painter, myOption, myOption.rect, text);
        drawFocus(painter, myOption, myOption.rect);
    } else {
        QItemDelegate::paint(painter, option, index);
    }
}
```

> *Qt 4.4 预计将引入 `QItemDelegate` 类并将其作为默认代理。与 `QItemDelegate` 不同，`QStyledItemDelegate` 将依赖于当前状态来绘制其条目。*

由于我们想以“分钟:秒”的格式渲染持续时间，我们重新实现了`paint()`函数。`arg(i)`调用接收一个整数以渲染为字符串、字符串应有的长度、整数的基数（10 为十进制）以及填充字符。

为了对齐文本，我们使用了当前的样式选项并覆盖了默认对齐。然后我们调用`QItemDelegate::drawDisplay()`来绘制文本，随后调用`QItemDelegate::drawFocus()`，如果条目具有焦点它将绘制一个矩形，否则什么都不做。使用`drawDisplay`非常方便，特别是当配合我们自己的样式选项时。我们也可以直接使用`painter`进行绘制。

```cpp
QWidget* createEditor(QWidget *parent,
                      const QStyleOptionViewItem option,
                      const QModelIndex &index) const
{
    if (index.column() == durationColumn) {
        QTimeEdit *timeEdit = new QTimeEdit(parent);
        timeEdit->setDisplayFormat("mm:ss");
        connect(timeEdit, SIGNAL(finished()), this, SLOT(commitAndCloseEditor()));
        return timeEdit;
    } else {
        return QItemDelegate::createEditor(parent, option, index);
    }
}
```

我们只想控制持续时间，我们通过检查列来实现这一点。

```cpp
void TrackDelegate::commitAndCloseEditor()
{
    // ... (代码片段省略，原文此处有页码干扰)
}
```

### 10. 视图类小结

在本章中，我们对Qt的模型/视图架构进行了广泛概述。我们展示了如何使用视图子类、如何使用Qt的预定义模型以及如何创建自定义模型和自定义代理。但模型/视图架构非常丰富，我们没有空间涵盖它实现的所有功能。还可以使用多个视图来查看同一个模型。通过一个视图进行的任何编辑将自动反映在其他视图中。这种功能对于用户可能希望查看逻辑上相距很远的数据集特别有用。架构还支持选择：当两个或多个视图使用同一个模型时，每个视图都可以设为具有自己的独立选择，或者可以在视图之间共享选择。

虽然在本例中没有必要，但完全可以创建一个自定义代理，精细地控制模型中任何条目的编辑和渲染。我们选择控制特定的列，但由于`QModelIndex`被传递到我们重新实现的代理函数，我们可以根据列、行、矩形区域或这些组合进行控制，一直细化到所需的单个条目。

Qt的在线文档提供了条目视图编程及其实现它的类的全面覆盖。请访问`http://doc.qt.com/4/model-view.html`获取所有相关类的列表，并访问`http://doc.qt.com/4.3/model-view-programming.html`获取更多信息以及与Qt自带的相关示例的链接。

*   顺序容器
*   关联容器
*   泛型算法
*   字符串、字节数组与变体

![](img/930c1c6fda99d425284503ebcbc940ea_295_0.png)

## 11. 容器类

容器类是通用的模板类，用于在内存中存储泛型项目。C++已经作为标准模板库（STL）的一部分提供了许多容器，它包含在标准C++库中。

Qt提供了自己的容器类，因此对于Qt程序，我们可以同时使用Qt容器和STL容器。Qt容器的主要优势是它们在所有平台上的行为都是相同的，并且它们是隐式共享的（implicitly shared）。隐式共享（或“写时复制”）是一种优化技术，使得允许以值的方式传递容器而不会产生显著的性能开销。Qt容器还具有受Java启发的易于使用的迭代器，它们可以使用`QStream`进行流式处理，并且在可执行文件中生成的代码通常比相应的STL容器更少。最后，在Qt/Embedded Linux支持的某些平台上，Qt容器是唯一可用的。

Qt既提供了顺序容器（如`QVector<T>`、`QLinkedList<T>`和`QList<T>`）以及关联容器（如`QMap<K, T>`和`HashMap<K, T>`）。从概念上讲，顺序容器一个接一个地存储项目，而关联容器存储键值对。

Qt还提供了可以在任意容器上执行操作的泛型算法。例如，`qsort`算法对顺序容器进行排序，而`qfind`对排序后的容器执行二分查找。这些算法与STL提供的算法相似。

如果你已经熟悉STL容器，并且在目标平台上可以使用STL，那么你可能希望使用它们来替代或在Qt容器之外使用它们。有关关于STL类和函数的更多信息，一个很好的起点是SGI的STL网站：`http://www.sgi.com/tech/stl`。

在本章中，我们还将查看`QString`、`ByteArray`和`QVariant`，它们与容器有许多共同点。`QString`是贯穿Qt API使用的16位Unicode字符串。`ByteArray`是8位字符数组，常用于存储原始二进制数据。`QVariant`是一种可以存储大多数C++和Qt值类型的类型。

## 顺序容器

`QVector<T>`是一种类似于数组的数据结构，它将项目存储在内存中的相邻位置，如图 11.1 所示。`vector`与普通C++数组的区别在于，`vector`知道自己的大小并且可以调整大小。在`vector`末尾添加额外项目是高效的，而在`vector`的开头或中间插入项目可能会开销很大。

| 0 | 1 | 2 | 3 | 4 |
|---|---|---|---|---|
| 937.81 | 25.984 | 308.74 | 310.92 | 40.9 |

图 11.1。一个双浮点数的`vector`

如果我们预先知道需要多少个项目，我们可以在定义`vector`时给它一个初始大小，并使用`[]`运算符为项目赋值；否则，我们必须在之后调整`vector`的大小或追加项目。这里有一个指定初始大小的示例：

```cpp
QVector<double> vect;
vect[0] = 1.0;
vect[1] = 0.540302;
vect[2] = -0.416147;
```

这里是相同的示例，这次从空`vector`开始，并使用`append()`函数在末尾追加项目：

```cpp
QVector<double> vect;
vect.append(1.0);
vect.append(0.540302);
vect.append(-0.416147);
```

我们也可以使用`<<`运算符代替`append()`：

```cpp
vect << 1.0 << -0.416147;
```

遍历`vector`项目的一种方法是使用`[]`和`count()`：

```cpp
double sum = 0.0;
for (int i = 0; i < vect.count(); ++i)
    sum += vect[i];
```

在没有分配显式值的情况下创建的`vector`条目使用项目类的默认构造函数进行初始化。基本类型和指针被初始化为零。

在`QVector<T>`的开头或中间插入项目，或从这些位置移除项目，对于大型`vector`来说可能是无效的。出于这个原因，Qt提供了`QLinkedList<T>`，这是一种将项目存储在内存非相邻位置的数据结构，如图 11.2 所示。与`vector`不同，链表不支持随机访问，但它们提供了“常数时间”的插入删除。

| 937.81 | 25.984 | 308.74 | 310.92 | 40.9 |
|---|---|---|---|---|

**图 11.2.** 一个双浮点数的链表

链表不提供`[]`运算符，因此必须使用迭代器来遍历其项目。迭代器也用于指定项目的位置。例如，以下代码在 `"Clash"` 和 `"Ramones"` 之间插入了字符串 `"Tote Hosen"`：

```cpp
QLinkedList<QString> list;
list.append("Clash");
list.append("Ramones");

QLinkedList<QString>::iterator i = list.find("Ramones");
list.insert(i, "Tote Hosen");
```

我们本节更详细地查看迭代器。

`QList<T>`是一种“数组列表”，它在一个类中结合了`QVector<T>`和`QLinkedList<T>`最重要的优点。它支持随机访问，其接口类似于`QVector<T>`。除非我们要在数千个项目中进行插入，或者需要项目占用连续内存，否则`QList`通常是最合适的通用容器类。

`QStringList`是`QList<QString>`的子类，广泛用于Qt API。除了从基类继承的函数，它提供了一些额外的函数，使得字符串处理更加灵活。我们在本章的最后一节讨论`QStringList`（290页）。对于为止的所有容器类，值可以是基本类型、指针或符合前面描述的自定义类。这里是这样一个类的示例：
