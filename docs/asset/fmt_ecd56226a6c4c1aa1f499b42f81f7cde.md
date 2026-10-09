
## 槽函数示例

这个槽函数是几乎所有槽函数的典型代表，它是 `timelog` 应用提供的槽函数：告诉模型执行工作，然后滚动到模型返回的索引，最后隐藏或显示已完成的任务。

被粘贴的任务包含了所有的子项及其子项（递归），但由于子项是折叠的且不可见的。`editUp()` 槽与 `editDown()` 几乎相同。`editPromote()` 和 `editDemote()` 槽也非常相似。

我们现在涵盖了足够的接口方法来提供背景。但在查看实现之前，我们必须首先查看使用的数据。

### 用于树模型的自定义项类

我们需要一个“项”类来表示每个任务。当我们使用 `StandardItems` 时，我们需要为名称和总时间准备项。但由于我们使用自定义模型，可以将所有数据存储在 `TaskItem` 中。

该类有两种功能：处理项数据的方法——以及管理子项的方法。正如我们在下一节所示，整个树由单个根项（未命名的 `TaskItem`）持有，其他任务都有子项。

`TaskItem` 的大部分方法都在头文件中，我们将分部分查看——两组方法和私有数据，从数据开始。

```cpp
private:
    int minutesForTask(boolToday) const;
    QString m_name;
    bool m_done;
    QList<QPair<DateTime, DateTime>> m_dateTimes;
    TaskItem *m_parent;
    QList<TaskItem*> m_children;
```

### 创建自定义模型

```cpp
TaskItem() { qDeleteAll(m_children); }
QString name() const { return m_name; }
void setName(const QString &name) { m_name = name; }
bool isDone() const { return m_done; }
void setDone(bool done) { m_done = done; }
QList<QPair<QDate, QDate>> dateTimes() const
{ return m_dateTimes; }
void addDateTime(const QDate &start, const QDate &end)
{ m_dateTimes << QPair(start, end); }
QString todays() const;
QString totalTime() const;
void incrementLastEndTime(int msec);
```

我们稍后会查看构造函数；但不会展示计算项目今日时长和总时长的方法，也不会增加最后一个结束时间的方法。

我们必须实现一个析构函数，因为 `TaskItem` 不是 `QObject` 的子类，因此我们需要自己接管任务的所有权。当删除一个项目时，会删除它所有的子节点，而子节点会删除它们自己的子节点，依此类递归，因此只需要删除树的根节点即可删除所有项目。

```cpp
TaskItem*parent() const { return m_parent; }
TaskItem*childAt(int row) const { return m_children.value(row); }
int rowOfChild(TaskItem *child) const
{ return m_children.indexOf(child); }
int childCount() const { return m_children.count(); }
bool hasChildren() const { return m_children.isEmpty(); }
QList<TaskItem*> children() const { return m_children; }
void insertChild(int row, TaskItem *item)
{ item->m_parent = this; m_children.insert(row, item); }
void addChild(TaskItem *item)
{ item->m_parent = this; m_children << item; }
void swapChild(int oldRow, int newRow)
{ m_children.swap(oldRow, newRow); }
TaskItem* takeChild(int row);
```

`childAt()` 方法使用 `QList::value()` 而不是 `QList::operator[]()` 是很有用的；这确保了如果给出一个范围外的行，将返回一个默认构造的值（即 0），而不是让程序崩溃。

当在特定行插入项目或在末尾添加项目时，重绘它是至关重要的。这是因为传递的 `TaskItem` 可能已经从树的某处被剪切或移动，因此已经有一个父节点，如果该父节点不是当前项目（通常也不是），那么就是错误的。

在 `taskitem.cpp` 文件中，只有两个方法与模型/视图编程相关：构造函数和 `takeChild()` 方法，我们将复习这两个方法。

```cpp
TaskItem::TaskItem(const QString &name, bool done, TaskItem *parent)
    : m_name(name), m_done(done), m_parent(parent)
{
    if (m_parent)
        m_parent->addChild(this);
}
```

如果使用空父节点创建一个新的任务项目，我们确保将其添加到父节点子节点列表的末尾。

```cpp
TaskItem::takeChild(int row)
{
    TaskItem *item = m_children.takeAt(row);
    Q_ASSERT(item);
    item->m_parent = 0;
    return item;
}
```

如果一个任务从树中被取出（即从其父节点的子节点列表中移除），我们必须将其父节点设置为 0，以反映没有项目拥有它的事实。这意味着返回的指针由我们负责，因此我们应该尽快删除它或将其插回树中，以避免产生内存泄漏的风险。

### 一个用于树的自定义 QAbstractModel 子类

为了为树实现一个既可编辑又可缩放大小的 `QAbstractModel` 子类，我们必须重新实现表 3.1 中列出的几乎或所有方法。然而，对于 `Timelog` 应用的任务数据——以及通常对于一般的树而言——我们不需要重新实现 `insertColumns()` 或 `removeColumns()`，因为所使用的列数是固定的。

为了支持使用拖放移动项目（及其子节点），我们还必须实现表 4.1 所示的与拖放相关的方法。拖放 API 要求我们能够对项目进行序列化和反序列化，正如我们看到的，可以使用加载和保存的方法来帮助。我们还想为视图提供移动项目的其他方法，为了支持这一点，我们通过自定义方法扩展了 `QAbstractModel` API：

```cpp
QModelIndex moveUp(const QModelIndex&);
ModelIndex moveDown(const QModelIndex&);
QModelIndex cut(const QModelIndex&);
```

#### 表 4.1 QAbstractItemModel 的拖放 API

| 方法 | 说明 |
|---|---|
| `dropMimeData(mimeData, dropAction, row, column, parent)` | 此方法在发生投放操作时被调用；它必须反序列化 `mimeData` 并使用它对给定行、列和父节点的项目执行指定的 `dropAction` |
| `mimeData(indexes)` | 返回一个 `QMimeData` 对象，其中包含与给定模型索引列表对应的序列化数据；该对象在模型内部用于生成投放所需的数据 |
| `mimeTypes()` | 返回 MIME 类型的 `QString` 列表 |
| `supportedDragActions()` | 返回拖动操作的按位或结果 |
| `supportedDropActions()` | 返回放置操作的按位或结果 |

```cpp
QModelIndex paste(const QModelIndex&);
ModelIndex promote(const QModelIndex&);
QModelIndex demote(const QModelIndex&);
```

### 创建自定义树模型

这种方法的实现对于所有类型的模型都是相似的。在特定情况下，我们让所有项目都变为可选且启用的，但仅允许任务名称被勾选、编辑以及进行拖放。正如我们很快将看到的，我们实现了拖放功能：如果拖动任务名称，整个任务（包括其项目）以及它的子任务都会被拖动。我们倾向于用户拖动名称而不是时间，因为这会让正在发生的事情变得更加清晰。

```cpp
const int ColumnCount = 3;

QVariant TreeModel::data(const QModelIndex &index, int role) const {
    if (!rootItem || !index.isValid() || index.column() < 0 ||
        index.column() >= ColumnCount)
        return QVariant();
    if (TaskItem *item = itemForIndex(index)) {
        if (role == Qt::DisplayRole || role == Qt::EditRole) {
            switch (index.column()) {
                case Name: return item->name();
                case Today: return item->todayTime();
                case Total: return item->totalTime();
                default: Q_ASSERT(false);
            }
        }
        if (role == Qt::CheckStateRole && index.column() == Name)
            return static_cast<int>(item->isDone()) ? Qt::Checked : Qt::Unchecked;
        if (role == Qt::TextAlignmentRole) {
            if (index.column() == Name)
                return static_cast<int>(Qt::AlignCenter | Qt::AlignLeft);
            return static_cast<int>(Qt::AlignCenter | Qt::AlignRight);
        }
        if (role == Qt::DecorationRole && index.column() == Today &&
            timedItem && index == timedItem && !m_icon.isNull())
            return m_icon;
    }
    return QVariant();
}
```

`data()` 方法是 Qt 模型/视图架构的关键，因为正是通过这个方法访问所有数据和绝大多数元数据。正如我们在讨论 `TableModel` 时提到的，此方法并不依赖于我们调用基类的实现；相反，对于任何我们没有自己处理的情况，我们必须始终返回一个无效的 `QVariant`。

`itemForIndex()` 方法根据模型索引从树中返回一个 `TaskItem`；稍后我们将回顾这个方法。

我们选择将 `Qt::DisplayRole` 和 `Qt::EditRole` 视为等同，因此如果请求任一角色的数据，我们都会返回它。我们的数据并没有很多“列”，我们只有一个任务项的树，但我们将列映射到数据中的特定字段，或者在时间项的情况下映射到计算出的值。我们还处理了 `Qt::CheckStateRole`，返回与任务完成状态对应的枚举。

对于文本对齐，我们选择将任务名称左对齐并将时间右对齐。如果请求了 `Qt::DecorationRole`，我们会使用图标——但仅当请求针对“今天”列且该项目是有计时的情况下。对于所有其他情况以及所有其他角色，我们返回一个无效的 `QVariant` 并让 Qt 来处理它们。

```cpp
TaskItem* TreeModel::itemForIndex(const QModelIndex& index) const {
    if (index.isValid()) {
        if (TaskItem* item = static_cast<TaskItem*>(index.internalPointer()))
            return item;
    }
    return rootItem;
}
```

每当创建一个 `QModelIndex` 时（使用 `QAbstractItemModel::createIndex` 方法），除了提供行和列之外，我们还可以提供一个指针（或数字 ID）。在该模型中，提供指向树中对应项的指针是非常常见的——正如我们所看到的，这就是我们在 `TreeModel` 中创建索引时所做的。这使得能够轻松获取给定模型索引的对应项指针——我们只需要请求模型的内部指针即可。如果没有指针或索引无效，我们返回一个指向根项的指针（如果没有向树中添加任何项目，则将为 0）。

```cpp
QVariant TreeModel::headerData(int section, Qt::Orientation orientation, int role) const {
    if (orientation == Qt::Horizontal && role == Qt::DisplayRole) {
        if (section == Name)
            return tr("Task/Subtask/...");
        else if (section == Today)
            return tr("Time (Today)");
        else if (section == Total)
            return tr("Time (Total)");
    }
    return QVariant();
}
```

Qt 的 `TreeView` 仅支持水平表头，因此当请求其中之一时，我们提供相应的名称。由于 `headerData()` 使用与 `data()` 相同的逻辑，通过依赖返回值而非基类调用，对于任何我们没有处理的情况，我们都返回一个无效的 `QVariant`。

```cpp
int TreeModel::rowCount(const QModelIndex &parent) const
{
    if (parent.isValid() && parent.column() != 0)
        return 0;
    TaskItem *parentItem = itemForIndex(parent);
    return parentItem ? parentItem->childCount() : 0;
}
```

一个项目的行数是它拥有的子项数量（但不包括其子项，因此计数不是递归的）。如果 `parent` 有效但列不是 0，我们必须返回 0，因为我们只允许第一列的项拥有子项。其他项获取父索引对应的任务项。如果 `parent` 索引无效，`itemForIndex()` 将正确地返回根项（如果树中没有项目，则为 0）。

```cpp
int TreeModel::columnCount(const QModelIndex &parent) const
{
    return parent.isValid() && parent.column() != 0 ? 0 : ColumnCount;
}
```

自定义的 `TreeModel` 与其他树模型一样，具有固定数量的列，这使得该方法的实现非常简单，并且类似于我们在邮政编码表模型中使用的方法。如果索引有效且列不是第一列（名称），那么我们被请求的是时间列的列数；这对于我们的模型没有意义，在这种情况下我们返回 0。

```cpp
QModelIndex TreeModel::index(int row, int column, const QModelIndex &parent) const
{
    if (!rootItem || row < 0 || column < 0 || column >= ColumnCount
        || (parent.isValid() && parent.column() != 0))
        return QModelIndex();
    TaskItem *parentItem = itemForIndex(parent);
    Q_ASSERT(parentItem);
    if (TaskItem *item = parentItem->childAt(row))
        return createIndex(row, column, item);
    return QModelIndex();
}

# 第 4 章. 模型/视图树模型
