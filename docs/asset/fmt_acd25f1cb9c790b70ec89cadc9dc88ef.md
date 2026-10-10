
```cpp
    int column = currentColumn() - 1;

    while (row >= 0) {

        while (column >= 0) {

            if (text(row, column).contains(str)) {

                clearSelection();

                setCurrentCell(row, column);

                activateWindow();

                return;

            }

            --column;

        }

        column = ColumnCount - 1;

        --row;

    }

    QApplication::beep();

}
```

`findPrevious()` 槽与 `findNext()` 类似，不同之处它是反向遍历并停止在 `A1` 单元格。

# 实现其他菜单

我们现在实现“工具”和“选项”菜单的槽。这些菜单如图 4.7 所示。

| 工具 | 选项 |
|---|---|
| 重新计算 `F9` | 显示网格 |
| 排序... | 自动重新计算 |

**图 4.7.** 电子表格应用程序的“工具”和“选项”菜单

```cpp
void Spreadsheet::recalculate()
{
    for (int row = 0; row < RowCount; ++row) {
        for (int column = 0; column < ColumnCount; ++column) {
            if (cell(row, column)) {
                cell(row, column)->setDirty();
            }
        }
    }
    viewport()->update();
}
```

# 4. 实现应用程序功能

`recalculate()` 槽对应 `Tools::Recalculate`。它也会在需要时由 `Spreadsheet` 自动调用。

遍历所有单元格并在每个单元格上调用 `setDirty()`，将每个单元格标记为需要重新计算。当下一个 `QTableWidget` 单元格调用单元格的 `text()` 以获取电子表格中显示的值时，该值将会被重新计算。

然后，我们对视口调用 `update()` 以重绘整个电子表格。`QWidget` 中的重绘代码会调用每个可见单元格的 `text()` 来查看显示的值。由于我们对每个单元格都调用了 `setDirty()`，`text()` 的调用将使用最新计算的值。计算可能需要重新计算不可见的单元格，从而产生级联计算，直到每个需要重新计算并在视口中显示正确文本的单元格都完成了最新计算。计算是由 `Cell` 类执行的。

```cpp
void Spreadsheet::setAutoRecalcul(bool recalc) {
    autoRecalc = recalc;

    if (autoRecalc)
        recalculate();
}
```

`setAutoRecalulate()` 槽对应 `Options::Auto-Recalculate`。如果开启该功能，我们将立即重新计算整个电子表格以确保其是最新的；之后，将从 `somethingChanged()` 自动调用 `recalculate()`。

我们不需要为 `Options::ShowGrid` 实现任何内容，因为 `QWidget` 已经有一个继承自 `QTableView` 的 `setShowGrid(bool)` 槽。剩下的只有 `Spreadsheet::sort()`：

```cpp
void Spreadsheet::sort(const SpreadsheetCompare& compare) {
    QList<QString> rows;
    QTableWidgetSelectionRange range = selectedRange();
    int i;
    for (int i = 0; i < range.rowCount(); ++i) {
        QStringList row;
        for (int j = 0; j < range.columnCount(); ++j) {
            row.append(formula(range.topRow() + i,
                range.leftColumn() + j));
        }
        rows.append(row);
    }
}

qStableSort(rows.begin(), rows.end(), compare);

for (int i = 0; i < range.rowCount(); ++i) {
    for (int j = 0; j < range.columnCount(); ++j) {
        setFormula(range.topRow() + i, range.leftColumn() + j,
        rows[i][j]);
    }
}

clearSelection();

somethingChanged();
```

## 实现其他菜单（排序）

排序针对当前选择进行，并根据 `compare` 对象中存储的排序键和排序顺序重新排列行。我们用 `QStringList` 表示每行数据，并将选择项表示为行列表。我们使用 Qt 的 `qStableSort()` 算法，为了简单起见，按公式而非按值排序。该过程如图 4.8 和 4.9 所示。我们将在第 11 章中介绍 Qt 的标准算法和数据结构。

| | D | E | index | value |
|---|---|---|---|---|
| 2 | Edsger | Dijkstra | 1930-05-11 | 0 | `["Edsger", "Dijkstra", "1930-05-11"]` |
| 3 | Tony | Hoare | 1934-01-10 | 1 | `["Tony", "Hoare", "1934-01-10"]` |
| 4 | Niklaus | Wirth | 1934-02-15 | 2 | `["Niklaus", "Wirth", "1934-02-15"]` |
| 5 | Donald | Knuth | 1938-01-10 | 3 | `["Donald", "Knuth", "1938-01-10"]` |

**图 4.8.** 将选择作为行列表进行排序

`qStableSort` 函数接受一个起始迭代器、一个结束迭代器和一个比较函数。比较函数是一个接受两个参数（两个 `QStringList`）的函数，如果第一个参数“小于”第二个参数则返回 `true`，否则返回 `false`。我们作为比较函数传递的对象并不是真正的函数，但它可以像函数一样使用，稍后会看到。

| | C | D | E |
|---|---|---|---|
| 0 | Donald | Knuth | `["Donald", "Knuth", "1938-01-10"]` |
| 1 | Edsger | Dijkstra | `["Edsger", "Dijkstra", "1930-05-11"]` |
| 2 | Niklaus | Wirth | `["Niklaus", "Wirth", "1934-02-15"]` |
| 3 | Tony | Hoare | `["Tony", "Hoare", "1934-01-10"]` |

**图 4.9.** 排序逻辑（示例）

`qStableSort` 函数接受一个起始迭代器、一个结束迭代器和一个比较函数。比较函数是一个接受两个参数（两个 `QStringList`）的函数，如果第一个参数“小于”第二个参数则返回 `true`，否则返回 `false`。我们作为比较函数传递的对象并不是真正的函数，但它可以像函数一样使用，稍后会看到。

`QVariant` `evalExpression(const QString &str, int &pos) const;`
`QVariant` `evalTerm(const QString &str, int &pos) const;`
`QVariant` `evalFactor(const QString &str, int &pos) const;`

```cpp
mutable QVariant cachedValue;

mutable bool cacheIsDirty;

#endif
```

该类通过添加两个私有变量扩展了 `QTableWidgetItem`：

- `cachedValue`：将单元格的值缓存为 `QVariant` 格式。
- `cacheIsDirty`：如果缓存的值不是最新的，则为 `true`。

我们使用 `QVariant` 是因为某些单元格具有 `double` 值，而另一些具有 `QString` 值。

`cachedValue` 和 `cacheIsDirty` 变量使用 C++ 的 `mutable` 关键字声明。这允许我们在 `const` 函数中修改这些变量。否则，我们将在每次调用 `text()` 时都重新计算值，但那样会产生不必要的效率浪费。

注意类定义中没有 `Q_OBJECT` 宏。`Cell` 是一个纯 C++ 类，没有信号和槽函数。实际上，由于 `QTableWidgetItem` 派自于 `QObject`，在目前的状态下 `Cell` 无法拥有信号和槽。Qt 的项类没有派生自 `QObject`，是为了将它们的开销降到最低。如果需要信号和槽，可以在包含项的控件中实现，或者在特殊情况下使用对 `QObject` 的多继承。

这里是 `cell.cpp` 的开头。

```cpp
#include <QtGui>

#include "cell.h"

Cell::Cell()
{
    setDirty();
}
```

在构造函数中，我们只需要将缓存标记为“脏”（`dirty`）。不需要传递参数；当单元格通过 `setItem()` 插入到 `QTableWidget` 时，`TableWidget` 将自动获得它的所有权。

每个 `QWidgetItem` 都持有一些数据，每个数据“角色”（`role`）最多对应一个 `QVariant`。最常用的角色是 `Qt::EditRole` 和 `Qt::DisplayRole`。`editRole` 用于需要编辑的数据，而 `displayRole` 用于需要显示的数据。通常这两者的数据是相同的，但 `editRole` 对应单元格的公式，而 `displayRole` 对应单元格的值（公式求值的结果）。

## `QWidgetItem` 的类化

```cpp
QWidgetItem *Cell::clone() const
{
    return new Cell(*this);
}
```

当 `QWidget` 需要创建一个新单元格时会调用 `clone()` 函数——例如当用户开始在一个未使用过的空单元格中输入时。传递给 `QWidget::setItemPrototype()` 的实例是被创建的项目。对于 `Cell` 来说，成员级拷贝就足够了，我们依靠 C++ 自动创建的默认构造函数在 `clone()` 中创建新的 `Cell` 实例。

```cpp
void Cell::setFormula(const QString &formula)
{
    setData(Qt::EditRole, formula);
}
```

`setFormula()` 函数设置单元格的公式。它只是一个为了带上 `editRole` 调用 `setData()` 的便利函数。它从 `Spreadsheet::setFormula()` 调用。

```cpp
QString Cell::formula() const
{
    return data(Qt::EditRole).toString();
}
```

`formula()` 函数从 `Spreadsheet::formula()` 调用。与 `setFormula()` 一样，它是一个便利函数，因此用于获取项的 `EditRole` 数据。

```cpp
void Cell::setData(int role, const QVariant &value)
{
    QWidgetItem::setData(role, value);

    if (role == Qt::EditRole)
        setDirty();
}
```

如果我们有一个新公式，我们将 `cacheDirty` 设为 `true`，以确保在下次调用 `text()` 时重新计算单元格。

`Cell` 中没有定义 `text()` 函数，尽管我们在 `Spreadsheet::text()` 中对实例调用了 `text()`。`text()` 函数是 `QWidgetItem` 提供的一个便利函数；它等同于调用 `data(Qt::DisplayRole).toString()`。

```cpp
void Cell::setDirty()
{
    cacheDirty = true;
}
```

调用 `setDirty()` 函数是为了强制重新计算单元格的值。它只是将 `cacheDirty` 设置为 `true`，意味着 `cachedValue` 不再是最新的。在必要之前，不会执行重新计算。

# 4. 实现应用程序功能

```cpp
QVariant Cell::data(int role) const
{
    if (role == Qt::DisplayRole) {
        if (value().isValid()) {
            return value().toString();
        } else {
            return "####";
        }
    } else if (role == Qt::TextAlignmentRole) {
        if (value().type() == QVariant::String) {
            return int(Qt::AlignLeft | Qt::AlignVCenter);
        } else {
            return int(Qt::AlignRight | Qt::AlignVCenter);
        }
    } else {
        return QTableWidgetItem::data(role);
    }
}
```

`data()` 函数是从 `QTableWidgetItem` 重新实现的。如果角色为 `Qt::DisplayRole` 且使用 `Qt::editRole` 调用了公式，它将返回在电子表格中应显示的文本。如果使用 `Qt::TextAlignmentRole` 调用，它将返回适当的对齐方式。在显示情况下，它依赖于 `value()` 来计算单元格的值。如果值无效（因为公式错误），我们返回 `"####"`。

`data()` 中使用的 `value()` 函数返回一个 `QVariant`。`QVariant` 可以存储不同类型的值，例如 `double` 和 `QString`，并提供将变体转换为其他类型的函数。例如，对一个持有 `double` 值的变体调用 `toString()` 会产生该 `double` 值的字符串表示。使用默认构造函数构建的 `QVariant` 是一个“无效”变体。

```cpp
const QVariant Invalid;

QVariant Cell::value() const
{
    if (cacheDirty) {
        cacheDirty = false;
    }

    QString formulaStr = formula();

    if (formulaStr.startsWith('(')) {
        cachedValue = formulaStr.mid(1);
    } else if (formulaStr.startsWith('-=')) {
        cachedValue = Invalid;
        QString expr = formulaStr.mid(1);
        expr.replace("", "");
        expr.append(QChar::Null);
    }

    int pos = 0;
    cachedValue = evalExpression(expr, pos);

    if (expr[pos] != QChar::Null) {
        cachedValue = Invalid;
    } else {
        bool ok;
        double d = formulaStr.toDouble(&ok);
        if (ok) {
            cachedValue = d;
        } else {
            cachedValue = formulaStr;
        }
    }

    return cachedValue;
}
```
