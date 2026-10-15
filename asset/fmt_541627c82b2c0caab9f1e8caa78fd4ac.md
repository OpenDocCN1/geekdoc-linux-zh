
## 代码实现：复制项

```cpp
const QString mimeType = "application/vnd.qtrac.pagesigner";
void MainWindow::copyItems(const QList<QGraphicsItem*>& items)
{
  QByteArray copiedItems;
  QData out(&copiedItems, QIODevice::WriteOnly);
  writeItems(out, items);
  MimeData *mimeData = new QMimeData;
  mimeData->setData(mimeType, copiedItems);
  Clipboard *clipboard = QApplication::clipboard();
  clipboard->setMimeData(mimeData);
}
```

此方法创建了一个空的`QByteArray`，然后使用我们之前（416）看到的`writeItems()`方法向其填充要复制的项。它在堆上创建了一个新的`QMimeData`对象，并提供代表我们自定义MIME类型的字节数组以识别数据格式。然后，我们获取系统剪贴板的指针，并将MIME数据传递给剪贴板——剪贴板也会接管该数据的所有权，因此我们不需要负责删除它。

## 代码实现：剪切项

```cpp
void MainWindow::editCut()
{
  QList<QGraphicsItem*> items = scene->selectedItems();
  if (items.isEmpty()) {
    return;
  }
  copyItems(items);
  QListIterator<QGraphicsItem*> i(items);
  while (i.hasNext()) {
    QScopedPointer<QGraphicsItem> item(i.next());
    scene->removeItem(item.data());
  }
  setDirty(true);
}
```

从场景中剪切项比复制稍微复杂，因为它们必须既被复制又被移除。该方法的起始与`editCopy()`方法相同，但在完成复制后，它会进入移除阶段——从场景中移除每个复制的项。

## 场景、项与操作

`QGraphics::removeItem`方法将该项从场景中移除，并将该项子项的所有权（递归地）交给调用者。在这里，我们立即删除被移除的项（以及它们的递归子项），以避免内存泄漏，就在复制的指针超出作用范围时，即每个循环结束时。在最后，我们调用`setDirty()`，因为剪切项（与仅复制不同）会改变场景。`setDirty()`槽会调用`updateUI()`槽，因此在剪切后，该操作将被启用；（➤ 436。）

## 代码实现：粘贴项

```cpp
void MainWindow::editPaste()
{
    QClipboard *clipboard = QApplication::clipboard();
    const QMimeData *mimeData = clipboard->mimeData();
    if (!mimeData)
        return;

    if (mimeData->hasFormat(MimeType)) {
        QByteArray copiedItems = mimeData->data(MimeType);
        QData in(&copiedItems, QIODevice::ReadOnly);
        // ... 此处根据原文内容结束
    }
}
```

*（注：原文在此处存在大量重复的“翻译”文本及乱码数据，根据“删除多余/无效内容”及“保留正文核心信息”的原则，已移除。）*

# 场景、项目与动作

按钮本身（从而调用了编辑对齐动作），或其菜单，在这种情况下它们可以点击其中一个特定的对齐动作。鉴于此，我们的代码必须考虑到可能调用的是特定的对齐动作，或者是编辑对齐动作本身。请注意，`updateUi()`槽(437)只有在至少选中了两个项目时才会激活对齐动作，因为如果选中了一个或没有选中项目，对齐就没有意义了。

我们将查看：

```cpp
void MainWindow::editAlignment()
{
    QAction *action = qobject_cast<QAction>(sender());
    if (action)
        return;

    Qt::Alignment alignment = static_cast<Qt::Alignment>(action->data().toInt());
    if (alignment != editAlignmentAction) {
        editAlignmentAction->setData(action->data());
        editAlignmentAction->setIcon(action->icon());
    }
}
```

我们通过查找是哪个动作调用了该槽。所需的对齐方式存储在动作的数据中，因此我们获取它供后续使用。如果该动作不是编辑对齐动作本身，我们就设置编辑对齐动作的数据及其图标以与之匹配。这确保了如果调用的是编辑对齐动作而不是特定的对齐动作，它将使用上次设置的特定对齐方式。

```cpp
QList<GraphicsItem>* items = scene->selectedItems();
Vector<double> coordinates;
populateCoordinates(alignment, &coordinates, items);
if (alignment == Qt::AlignLeft || Qt::AlignTop)
    offset = *std::min_element(coordinates.constBegin(),
        coordinates.constEnd());
else
    offset = *std::max_element(coordinates.constBegin(),
        coordinates.constEnd());
```

我们用于执行此操作的算法非常简单。我们为所需的对齐方式创建一个所有项目边缘坐标的向量，例如，如果是左对齐，则创建它们的`x`坐标；如果是底部对齐，则创建它们的`y`坐标加上高度。我们计算一个偏移量，该偏移量是最小坐标（用于左或顶对齐）或最大坐标（用于右或底对齐），并根据偏移量与其实际坐标之间的差异移动每个项目。

# 第 12 章：创建图形/视图场景

`std::min_element()`和`std::max_element()`函数由`STL`（标准模板库）在`<algorithm>`头文件中提供。这些函数接受一个起始和一个结束迭代器，并返回一个指向迭代器所引用序列中最小（最大）元素的迭代器。因此，在这里，我们直接使用`operator()`从迭代器中提取值。（如果想想避免使用`STL`，我们可以编写接受序列参数的自定义模板`min()`和`max()`函数，或者我们可以使用`qSort(coordinates); offset = coordinates.first();`来获取最小值，使用`coordinates.last()`来获取最大值。）
