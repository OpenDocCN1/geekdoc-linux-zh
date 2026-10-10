
系统剪贴板通过`QApplication::clipboard()`静态函数可用。通过调用`QClipboard::setText()`，我们将文本放入剪贴板中，不仅供本应用程序使用，也供支持纯文本的其他应用程序使用。使用制表符和换行符作为分隔符的格式被许多应用程序（包括 Microsoft Excel）所理解。`TableWidget::selectedRanges()`函数返回选择范围列表。在构造函数中，为了方便起见，我们定义了一个`selectedRange()`函数来返回选择范围：

```cpp
TableWidgetSelectionRange Spreadsheet::selectedRange() const
{
    QList<TableWidgetSelectionRange> ranges = selectedRanges();
    if (ranges.isEmpty())
        return TableWidgetSelectionRange();
    return ranges.first();
}
```

如果有选择，返回第一个（也是唯一的），因为`ContiguousSelection`模式会将当前单元格视为被选中。但为了防止程序中出现没有当前单元格的情况，我们处理了这种情况。

代码视图：

```cpp
void Spreadsheet::paste()
{
    TableWidgetSelectionRange range = selectedRange();
    QString str = QApplication::clipboard()->text();
    QStringList rows = str.split("\n");
    int numRows = rows.count();
    int numColumns = rows.first().count('\t') + 1;
    if (range.rowCount() * range.columnCount() != 1
        && (range.rowCount() != numRows || range.columnCount() != numColumns)) {
        QMessageBox::information(this, tr("Spreadsheet"),
            tr("无法粘贴信息，因为复制和粘贴区域的大小不符。"));
        return;
    }
    for (int i = 0; i < numRows; ++i) {
        QStringList columns = rows[i].split("\t");
        for (int j = 0; j < numColumns; ++j) {
            int row = range.topRow() + i;
            int column = range.leftColumn() + j;
            if (row < RowCount && column < ColumnCount)
                setFormula(row, column, columns[j]);
        }
    }
    somethingChanged();
}
```

`paste()`槽对应粘贴。我们获取剪贴板上的文本并调用静态函数`QString::split()`将字符串拆分为`QStringList`。每一行都是列表中的一个字符串。

接下来，我们确定复制区域的尺寸。行数是`QStringList`中字符串的数量，列数是第一行中制表符的数量加 1。如果只选择了一个单元格，我们使用该单元格作为粘贴区域的左上角；否则，我们使用当前选择作为粘贴区域。

为了执行粘贴，我们遍历行并再次使用`QString::split()`将每一行拆分为单元格，但这次使用制表符作为分隔符。图 4.6 描述了这些步骤。

**图 4.6 将剪贴板文本粘贴到电子表格**

![](img/1bc72df8c60cf85926d3aefcc273027d_154_0.png)

```cpp
void Spreadsheet::del()
{
  QList<QTableWidgetItem *> items = selectedItems();

  if (!items.isEmpty()) {
    foreach (QTableWidgetItem *item, items)
      delete item;
    somethingChanged();
  }
}
```

`del()`槽对应“编辑|删除”。如果存在选中项，该函数将删除它们并调用`somethingChanged()`。只需对选择区域中的每个`Cell`对象使用`delete`即可清除单元格。`QTableWidget`会察到它的`QTableWidgetItems`被删除，如果其中任何项目是可见的，它将自动重绘自己。如果我们使用被删除单元格的位置调用`cell()`，它将返回一个空指针。

```cpp
void Spreadsheet::selectCurrentRow()
{
  selectRow(currentRow());
}

void Spreadsheet::selectCurrentColumn()
{
  selectColumn(currentColumn());
}
```

`selectCurrentRow()`和`selectCurrentColumn()`函数对应“编辑|选择|行”和“编辑|选择|列”菜单选项。它们的实现依赖于`QTableWidget`的`selectRow()`和`selectColumn()`函数。我们不需要实现“编辑|全选”的功能，因为那是`QTableWidget`继承的函数`QAbstractItemView::selectAll()`。

```cpp
void Spreadsheet::findNext(const QString &str, Qt::CaseSensitivity cs)
{
  int row = currentRow();
  int column = currentColumn() + 1;
  while (row < RowCount) {
    while (column < ColumnCount) {
      if (text(row, column).contains(str, cs)) {
        clearSelection();
        setCurrentCell(row, column);
        activateWindow();
        return;
      }
      ++column;
    }
    column = 0;
    ++row;
  }
  QApplication::beep();
}
```

`findNext()`槽从光标右侧的单元格开始，向右移动直到到达最后一列，然后从下一行的第一列继续，以此类推，直到找到文本或到达最后一个单元格。例如，如果当前单元格是 C24，我们将搜索 D24、E24、...Z24，然后是 A25、B25、C25、...Z25，以此类推直到 Z999。

如果我们找到了匹配项，将清除当前选择，将单元格光标移动到匹配的单元格，并使包含电子表格的窗口变为活动状态。如果没有找到匹配项，我们将让应用程序发出蜂声，表示搜索未成功。

```cpp
void Spreadsheet::findPrevious(const QString &str, Qt::CaseSensitivity cs)
{
  int row = currentRow();
  int column = currentColumn() - 1;
  while (row >= 0) {
    while (column >= 0) {
      if (text(row, column).contains(str, cs)) {
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

`findPrevious()`槽与`findNext()`类似，不同之处它是反向遍历并在 A1 单元格停止。

## 实现其他菜单

现在我们将为“工具”菜单和“选项”菜单实现槽。这些菜单如图 4.7 所示。

**图 4.7. 电子表格应用程序的“工具”和“选项”菜单**

![](img/1bc72df8c60cf85926d3aefcc273027d_157_0.png)

```cpp
void Spreadsheet::recalculate()
{
  for (int row = 0; row < RowCount; ++row) {
    for (int column = 0; column < ColumnCount; ++column) {
      if (cell(row, column))
        cell(row, column)->setDirty();
    }
  }
  viewport()->update();
}
```

`recalculate()`槽对应“工具|重新计算”。它也会在必要时由`Spreadsheet`自动调用。

我们遍历所有单元格，并对每个单元格调用`setDirty()`，将每一个都标记为需要重新计算。下一次`QTableWidget`调用`Cell`的`text()`以获取在电子表格中显示的值时，该值将会被重新计算。然后我们在`viewport()`上调用`update()`来重绘整个电子表格。`QTableWidget`中的重绘代码随后会调用每个可见单元格的`text()`来获取显示的值。由于我们对每个单元格都调用了`setDirty()`，对`text()`的调用将使用新计算的值。计算可能需要重新计算不可见的单元格，产生级联计算，直到每个需要重新计算以便在视口中显示正确文本的单元格都已完成计算。计算是由`Cell`类执行的。

```cpp
void Spreadsheet::setAutoRecalculate(bool recalc)
{
  autoRecalc = recalc;
  if (autoRecalc)
    recalculate();
}
```

`setAutoRecalculate()`槽对应“选项|自动重新计算”。如果开启该功能，我们将立即重新计算整个电子表格以确保它是最新的；之后，将从`somethingChanged()`自动调用`recalculate()`。

我们不需要为“选项|显示网格”实现任何内容，因为`QTableWidget`已经有了`setShowGrid()`方法，我们稍后会实现它。

```cpp
void Spreadsheet::sort()
{
  QList<QStringList> rows;
  QTableRange range = selection();

  for (int i = 0; i < range.rowCount(); ++i) {
    QStringList row;
    for (int j = 0; j < range.columnCount(); ++j) {
      row << item(i, j)->text();
    }
    rows << row;
  }
  // ... 排序逻辑 ...
}
```

`sort()`方法使用`qStableSort()`根据指定的标准对选中单元格进行排序。使用稳定排序确保了具有相同键的相对顺序被保留。

比较逻辑定义在`SpreadsheetCompare`类中，它实现了`()`运算符。在`spreadsheet.h`中，`SpreadsheetCompare`类定义如下：

```cpp
class SpreadsheetCompare
{
public:
  bool operator()(const QStringList &row1,
 const QStringList &row2) const;

  enum { KeyCount = 3 };
  int keys[KeyCount];
  bool ascending[KeyCount];
};
```

`SpreadsheetCompare`类很特殊，因为它实现了`()`运算符。这允许我们像使用函数一样使用该类。此类类被称为函数对象（或仿函数）。为了理解仿函数如何工作，我们从一个简单的示例开始：

```cpp
class Square
{
public:
  int operator()(int x) const { return x * x; }
}
```

`Square`类提供了一个函数`operator()(int)`返回参数的平方。通过将函数命名为`operator()(int)`而不是`compute(int)`，我们获得了像使用函数一样使用`Square`对象的能力：

```cpp
Square square;
int y = square(5);
// y 等于25
```

现在来看一个涉及`SpreadsheetCompare`的示例：

```cpp
QStringList row1, row2;
SpreadsheetCompare compare;
...

if (compare(row1, row2)) {
 // row1 小于 row2
}
```

`compare`对象可以像普通的`compare()`函数一样被使用。此外，它的实现可以访问所有的排序键和排序顺序，这些存储在成员变量中。

这种方案的替代方案是将排序键和顺序存储在全局变量并使用普通的`compare()`函数。然而，通过全局变量通信是不优雅的，可能会导致微妙的错误。仿函数是与`qStableSort()`等模板函数交互的一种更强大的模式。

在`spreadsheet.cpp`中

这是用于比较两个电子表格行的函数实现：

```cpp
bool SpreadsheetCompare::operator()(const QStringList &row1,
 const QStringList &row2) const
{
  for (int i = 0; i < KeyCount; ++i) {
    int column = keys[i];
    if (column != -1) {
      if (row1[column] != row2[column]) {
        return ascending[i] ? (row1[column] < row2[column])
                            : (row1[column] > row2[column]);
      }
    }
  }
  return false;
}
```

```cpp
if (row1[column] != row2[column]) {
    if (ascending[i]) {
        return row1[column] < row2[column];
    } else {
        return row1[column] > row2[column];
    }
}
}
}
return false;
```

如果第一行小于第二行，运算符返回`true`；否则返回`false`。`qStableSort()`函数使用此函数的结果进行排序。

`SpreadsheetCompare`对象的`keys`和`ascending`数组在`MainWindow::sort()`函数中被填充（见第 2 节）。每个键都存储一个列索引，或 -1（"None"）。

我们按顺序对每个键比较两行行中对应的单元格条目。一旦发现差异，我们就会返回相应的`true`或`false`值。如果所有比较结果相等，我们返回`false`。`qStableSort()`函数使用排序前的顺序来解决平局情况；如果`row1`原本在`row2`之前且两者互不为“小于”，那么在结果中`row1`仍然会在`row2`之前。这就是`qStableSort()`与其不稳定的兄弟`qSort()`的区别。

我们现在已经完成了`Spreadsheet`类。在下一节中，我们将回顾`Cell`类。该类用于存储单元格公式，并提供了对`QTableWidgetItem::data()`函数的重新实现，`Spreadsheet`间接通过`QTableWidgetItem::text()`函数调用该函数，以显示单元格公式计算的结果。

## 子类 QTableWidgetItem

`Cell`类派自`QTableWidgetItem`。该类的设计旨在与`Spreadsheet`良好地工作，但它对该类没有特定的依赖，理论上可以用于任何`QTableWidget`。以下是头文件：

代码视图：
