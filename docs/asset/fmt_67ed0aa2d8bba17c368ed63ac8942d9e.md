
```cpp
QVariant MyItemModel::data(const QModelIndex &index, int role) const
{
    if (!index.isValid())
        return QVariant();
    if (index.row() >= rowCount())
        return QVariant();
    if (role == Qt::DisplayRole)
        return QVariantGenerator::doFibonacci(index.row());
    else
        return QVariant();
}
```

图 03

## 使用 Qt 进行模型数据建模 - 第 2 部分

### 自定义结构

开发更复杂的模型可以使用`QAbstractTableModel`，它提供了一个二维列表。一个`AbstractListModel`可以被“管理”以显示多维数据。尽管开发者必须考虑一切，但某些场景无法通过框架提供的模型覆盖。创建一个自定义模型是解决此问题最简单的方法：你无需编写适配器层来将你的数据转换为现有模型可以理解的格式。

本质上，自定义模型仅仅是一个包装层，在数据和相关元素之间进行翻译。模型通常不具有用于存储项目的内部缓存或存储。

Qt 提供了一组用于自定义模型的基类。通过查看`QAbstractListModel`，我们可以得到一维列表。使用`QAbstractListModel`来访问存储在列表中的数据违背了本次练习的教学目的。让我们为你介绍一个名为`FibonacciNumberModel`的静态类。

![](img/df15b709d7e8fa8f2cd7af7eb08775e7_55_1.png)

上方修改`mainwindow.cpp`后生成的数字列表

```cpp
class FibonacciGenerator {
public:
    static int dOfFib(int i);
};
```

它的唯一目的是为了提供对以下方法的访问，该方法作为我们的生成器。我们传入一个整数并返回对应的斐波那契数：

```cpp
int FibonacciGenerator::dOfFib(int i) {
    if (i == 0)
        return 0;
    else if (i == 1)
        return 1;
    else
        return dOfFib(i-1) + dOfFib(i-2);
}
```

现在，是时候实现实际列表模型了。官方文档要求至少覆盖图 01 中的函数，其中`rowCount`和`columnCount`报告模型中存储的信息量。

我们为`rowCount`和`columnCount`返回值，其中包含了来自`fib`的信息。`columnCount`设置为一，我们可以使用`QAbstractListModel::column`的默认实现。

`data`方法返回要在在列表中显示的实际信息。在我们的示例中，它类似于图 02：布局非常复杂，因为它必须处理各种特殊情况。首先，模型提供的是`QModelIndex`类的实例而不是一组“正常”的坐标。必须对其进行拆解以获取关于要返回哪个项目的更多信息。其次，视图并不总是表现良好的。文档建议，如果参数无效，模型应该返回一个空的`QVariant`对象。

最后，模型可以设置为返回不同类型的数据。默认情况下，`QVariant`会尝试转换值，因此你可以创建一个不同的消费者来消耗不同类型的信息。然而，实际模型可以忽略`QVariant`的内容。

现在，是时候在项目骨架中创建表单并添加列表视图以验证`maincpp`中的功能了。（图 4）在当前状态下运行程序将产生一个项目列表，这对熟悉移动开发的人来说可能看起来熟悉。让我们利用此机会进行一下回顾：我们的视图由一个不存储任何自身数据的模型提供。它的作用是从数据源获取数据并以统一格式提供它。我们可以随后添加某种缓存，这不会改变类模型的行为。这种简单性被认为是 Qt 中模型-视图-控制器设计的优势。开发者在处理自定义模型时应该记住这一点。

```cpp
class MyItemModel : QAbstractListModel
{
    QOBJECT
public:
    explicit MyItemModel(QObject *parent = nullptr);
    QVariant data(const QModelIndex &index, int role = Qt::DisplayRole) const;
    int rowCount(const QModelIndex &parent = QModelIndex()) const;
    int columnCount(const QModelIndex &parent = QModelIndex()) const;
public slots:
};
```

图 01

```cpp
int MyItemModel::rowCount(const QModelIndex &parent) const
{
    return 0;
}
```

图 02

```cpp
int MyItemModel::columnCount(const QModelIndex &parent) const
{
    return 1;
}
```

```cpp
QVariant MyItemModel::data(const QModelIndex &index, int role) const
{
    if (!index.isValid())
        return QVariant();
    if (index.row() >= rowCount())
        return QVariant();
    if (role == Qt::DisplayRole)
        return QVariantGenerator::doFibonacci(index.row());
    else
        return QVariant();
}
```

图 03

## 使用 Qt 进行模型数据建模 - 第 2 部分

### 自定义结构

开发更复杂的模型可以使用`QAbstractTableModel`，它提供了一个二维列表。一个`AbstractListModel`可以被“管理”以显示多维数据。尽管开发者必须考虑一切，但某些场景无法通过框架提供的模型覆盖。创建一个自定义模型是解决此问题最简单的方法：你无需编写适配器层来将你的数据转换为现有模型可以理解的格式。

本质上，自定义模型仅仅是一个包装层，在数据和相关元素之间进行翻译。模型通常不具有用于存储项目的内部缓存或存储。

Qt 提供了一组用于自定义模型的基类。通过查看`QAbstractListModel`，我们可以得到一维列表。使用`QAbstractListModel`来访问存储在列表中的数据违背了本次练习的教学目的。让我们为你介绍一个名为`FibonacciNumberModel`的静态类。

![](img/df15b709d7e8fa8f2cd7af7eb08775e7_55_1.png)

上方修改`mainwindow.cpp`后生成的数字列表

```cpp
class FibonacciGenerator {
public:
    static int dOfFib(int i);
};
```

它的唯一目的是为了提供对以下方法的访问，该方法作为我们的生成器。我们传入一个整数并返回对应的斐波那契数：

```cpp
int FibonacciGenerator::dOfFib(int i) {
    if (i == 0)
        return 0;
    else if (i == 1)
        return 1;
    else
        return dOfFib(i-1) + dOfFib(i-2);
}
```

现在，是时候实现实际列表模型了。官方文档要求至少覆盖图 01 中的函数，其中`rowCount`和`columnCount`报告模型中存储的信息量。

我们为`rowCount`和`columnCount`返回值，其中包含了来自`fib`的信息。`columnCount`设置为一，我们可以使用`QAbstractListModel::column`的默认实现。

`data`方法返回要在在列表中显示的实际信息。在我们的示例中，它类似于图 02：布局非常复杂，因为它必须处理各种特殊情况。首先，模型提供的是`QModelIndex`类的实例而不是一组“正常”的坐标。必须对其进行拆解以获取关于要返回哪个项目的更多信息。其次，视图并不总是表现良好的。文档建议，如果参数无效，模型应该返回一个空的`QVariant`对象。
