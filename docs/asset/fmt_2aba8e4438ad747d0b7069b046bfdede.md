
```cpp
DirectoryViewer::DirectoryViewer(QWidget *parent)
: QDialog(parent) {

model = new QDirModel;
model->setReadOnly(false);
model->setSorting(QDir::DirsFirst | QDir::IgnoreCase | QDir::Name);

treeView = new QTreeView;
treeView->setModel(model);
treeView->header()->setStretchLastSection(true);
treeView->header()->setSortIndicator(0, Qt::AscendingOrder);
treeView->header()->setSortIndicatorShown(true);
treeView->header()->setClickable(true);

QModelIndex index = model->index(QDir::currentPath());
treeView->expand(index);
treeView->scrollTo(index);
treeView->resizeColumnContents(0);
```

一旦模型构建完成，我们使其变为可编辑并设置各种初始排序属性。然后，我们创建将显示模型数据的`QTreeView`。`QTreeView`的头部可以允许用户通过点击任何列标题来对排序，重复点击会在升序和降序之间切换。一旦树视图的头部设置完毕，我们获取当前目录的索引，并通过在需要时使用`expand()`展开其父级以确保该目录可见，同时使用`scrollTo()`滚动到位置。然后，我们确保第一列足够宽以显示其项而不会产生省略号（...）。

在此未显示的构造函数代码部分，我们将“创建目录”和“删除”按钮连接到槽函数以执行这些操作。我们不需要重命名按钮，因为用户可以通过按`F2`并输入来就地重命名。

```cpp
void DirectoryViewer::createDirectory()
{
    QModelIndex index = treeView->currentIndex();
    if (!index.isValid())
        return;

    QString dirName = QInputDialog::getText(this,
        tr("Create Directory"),
        tr("Directory name"));
    if (!dirName.isEmpty())
        if (model->mkdir(index, dirName).isValid())
            MessageBox::information(this, tr("Create Directory",
                tr("Failed to create the directory")));
}
```

如果用户在输入框中输入目录名称，我们尝试创建该名称作为当前目录的子目录。`QDir::mkdir`函数接收父目录的索引和新目录的名称，并返回它创建的目录的模型索引。如果操作失败，它将返回一个无效的模型索引。

```cpp
void DirectoryViewer::remove()
{
    QModelIndex index = treeView->currentIndex();
    if (!index.isValid())
        return;

    // ... 移除逻辑 ...
}
```

# 使用预定义模型

## 10. 视图类

`Qt`的预定义模型提供了方便的方法。在开始创建自定义模型之前，让我们首先回顾`Qt`的模型/视图架构。预定义模型提供了处理和查看数据的方便方法。然而，某些数据无法使用预定义模型进行高效处理。

预定义模型提供了方便的方法。在开始创建自定义模型之前，让我们首先回顾核心概念。`QSortFilterModel`提供了对数据的过滤和排序功能。树模型与表格模型类似，不同之处在于：与表格模型一样，顶层项的父级是根（一个无效的模型），但每个其他项都有父级。10.9 显示了不同模型的示意图。本节的第一个示例是一个显示相互关系货币值的只读表格模型。该应用程序如图 10.10 所示。

# 实现自定义模型

如果用户在输入框中输入目录名称，我们尝试创建该名称作为当前目录的子目录。

过滤器选项：

- 正则表达式
- 通配符
- 固定字符串

# 实现自定义模型

| 列表模型 | 表格模型 | 树模型 |
| :--- | :--- | :--- |
| 行 | 行 | 根 |
| 行 | 行 | 行 |
| 根 | 行 | 根 |

图 10.9. `Qt` 模型的原理示意图

该应用程序可以使用简单的表格来实现，但我们希望使用自定义模型来利用数据的某些属性以最大限地减少存储。如果我们存储 162 × 162 = 26244 个值；使用此处所示的自定义`CurrencyModel`，我们只需要存储 162 个值（每种货币相对于美元的值）。

![](img/930c1c6fda99d425284503ebcbc940ea_275_0.png)

图 10.10. 货币应用程序

`CurrencyModel`类将与标准的`QTableView`配合使用。`CurrencyModel`由一个`Map<String, double>`填充；每个键是货币代码，每个值是该货币相对于美元的值。这里有一个代码段显示了如何填充映射以及如何使用模型：

```cpp
QMap<String, double> currencyMap;
currencyMap.insert("AUD", 1.3259);
currencyMap.insert("CHF", 1.2970);
...
currencyMap.insert("SGD", 1.6901);
```

# 10. 视图类

```cpp
currencyMap.insert("USD", 1.0000);

CurrencyModel currencyModel;

currencyModel.setCurrencyMap(currencyMap);

TableView tableView;

tableView.setModel(&currencyModel);

tableView.setAlternatingRowColors(true);
```

我们可以查看该模型的实现，从它的头文件开始：

```cpp
class CurrencyModel : public QAbstractTableModel
{
public:
    CurrencyModel(QObject *parent = 0);

    void setCurrencyMap(const QMap<QString, double> &map);
    int rowCount(const QModelIndex &parent) const;
    int columnCount(const QModelIndex &parent) const;
    QVariant data(const QModelIndex &index, int role) const;
    QVariant headerData(int section, Qt::Orientation orientation, int role) const;
```

```cpp
private:
    QString currencyAt(int offset) const;
    QMap<QString, double> currencyMap;
```

我们选择为我们的模型派生`QAbstractTableModel`，因为它最贴合我们的数据源。`Qt`提供了几个模型类，包括`QAbstractList`、`QAbstractTableModel`和`QAbstractItem`；见图 10.1。`QAbstractItem`类用于支持各种模型，包括基于递归数据结构的模型，而`QAbstractList`和`QAbstractTableModel`类是为了为了方便使用一维或二维数据集提供的。

对于只读表格，我们必须重新实现三个函数：`rowCount()`、`columnCount()`和`data()`。在这种情况下，我们还重新实现了`headerData()`，并提供了一个初始化数据的函数（`setCurrencyMap()`）。

```cpp
CurrencyModel::CurrencyModel(QObject *parent)
: QAbstractTableModel(parent)
```

除了向基类传递父对象参数外，我们不需要在构造函数中做任何事情。

```cpp
int CurrencyModel::rowCount(const QModelIndex & /* parent */) const
{
    return currencyMap.count();
}
```

```cpp
int CurrencyModel::columnCount(const QModelIndex & /* parent */) const
{
    return currencyMap.count();
}
```

# 实现自定义模型

![](img/930c1c6fda99d425284503ebcbc940ea_277_0.png)

图 10.11. 抽象模型类的继承树

对于此模型，行和列数是货币映射中货币的数量。对于表格模型，父参数没有意义；它的存在是因为`rowCount()`和`columnCount()`继承自更通用的`QAbstractItem`基类，该类支持层级结构。

```cpp
QVariant CurrencyModel::data(const QModelIndex &index, int role) const
{
    if (!index.isValid())
        return QVariant();
    if (role == Qt::AlignmentRole)
        return int(Qt::AlignRight | Qt::AlignCenter);
    else if (role == Qt::DisplayRole) {
        QString rowCurrency = currencyAt(index.row());
        QString columnCurrency = currencyAt(index.column());

        if (currencyMap.value(rowCurrency) == 0.0)
            return "####";
        double amount = currencyMap.value(columnCurrency)
        / currencyMap.value(rowCurrency);

        return QString("%1").arg(amount, 0, 'f', 4);
    }
    return QVariant();
}
```

`data()`函数返回任何项的角色值。项被指定为`QModelIndex`。对于表格模型，`QModelIndex`的有趣组件是行和列号，可以通过`row()`和`col()`获取。

如果角色是`Qt::AlignmentRole`，我们返回一个适用于数字的对齐方式。如果显示角色是`Qt::DisplayRole`，我们查找每种货币的值并计算汇率。

我们可以将计算结果作为`double`返回，但这样我们就无法控制显示多少小数。相反，我们以格式化字符串的形式返回值。

```cpp
QVariant CurrencyModel::headerData(int section,
Qt::Orientation orientation,
int role) const
{
    if (role != Qt::DisplayRole)
        return QVariant();

    return currencyAt(section);
}
```

`headerData()`函数被视图调用以填充它的水平和垂直头部。`section`参数是行或列号。由于行和列的货币代码相同，我们不需要关心方向，只需返回给定部分的货币代码。

```cpp
void CurrencyModel::setCurrencyMap(const QMap<QString, double>&map)
{
    currencyMap = map;

    reset();
}
```

调用者可以使用`setCurrencyMap()`修改货币映射。`reset()`告诉使用模型的视图数据已失效；这强制它们请求新数据。

```cpp
QString CurrencyModel::currencyAt(int offset)
{
    return (currencyMap.begin() + offset).key();
}
```

`currencyAt()`返回货币映射中给定偏移量的键（货币代码）。正如我们所看到的，对于只读模型，这是困难的。自定义模型可以更高效，因为从货币 A 到 B 的距离与 B 到 A 相同，因此项是对角线镜像的。对于简单的表格，假设我们有三个货币 A、B 和 C。精心设计的模型只需要三个项 (A, B)、(A, C) 和 (B, C)。这里是设置和使用模型的方法：

```cpp
QString cities;
cities << "Arvika" << "Boden" << "Eskuna" << "Falun"
<< "Filipstad" << "Halmstad" << "Helsingborg" << "Karlstad"
<< "Kiruna" << "Kramfors" << "Motala" << "Sandviken"
<< "Skara" << "Stockholm" << "Sundsvall" << "Trelleborg";

CityModel cityModel;
cityModel.setCities(cities);

QTableView view;
view.setModel(&cityModel);
view.setAlternatingRowColors(true);
```

| Arvika | Boden | Eskuna | Falun |
|---|---|---|---|
| Arvika | 0 | 1063 | 280 |
| Boden | 1063 | 0 | 958 |
| Eskuna | 280 | 958 | 0 |
| Falun | 285 | 830 | 0 |
| Filipstad | 122 | 0 | 0 |
| Halmstad | 0 | 0 | 0 |

图 10.12. 城市应用程序

我们必须像之前的示例一样重新实现相同的函数。此外，我们还必须重新实现`setData()`和`flags()`以使模型可编辑。此外是类的定义：

```cpp
class CityModel : public QAbstractTableModel
{
    Q_OBJECT

public:
    CityModel(QObject *parent = 0);

    void setCities(const QStringList &cities);
    int rowCount(const QModelIndex &parent) const;

    int columnCount(const QModelIndex &parent) const;

    QVariant data(const QModelIndex &index, int role) const;

    bool setData(const QModelIndex &index, const QVariant &value, int role);

    QVariant headerData(const QModelIndex &index, Qt::Orientation orientation, int role) const;

    Qt::ItemFlags flags(const QModelIndex &index) const;

private:

    int offset(int row, int column) const;

    QStringList cities;

    QVector<int> distances;

};
```

对于这个模型，我们使用了两个数据结构：类型为`QList`的`cities`用于存储城市名称，以及类型为`QVector<int>`的`distances`用于存储每对唯一城市之间的距离。

```cpp
CityModel::CityModel(QObject *parent)
    : QAbstractTableModel(parent)
{
}
```

构造函数除了将父参数传递给基类外，没有执行其他操作。

```cpp
int CityModel::rowCount(const QModelIndex & /* parent */) const
{
    return cities.count();
}

int CityModel::columnCount(const QModelIndex & /* parent */) const
{
    return cities.count();
}
```

由于我们的城市是一个正方形网格，行数和列数等于列表中的城市数量。
