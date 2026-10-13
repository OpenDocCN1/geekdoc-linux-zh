
### `addRecord` 方法

```python
def addRecord(self, fields, callReset=True):
    assert len(fields) > self.nesting
    root = self.root
    branch = None
    for i in range(self.nesting):
        key = fields[i].lower()
        branch = root.childWithKey(key)
        if branch is not None:
            root = branch
        else:
            branch = BranchNode(fields[i])
            root.insertChild(branch)
            root = branch
    assert branch is not None
    items = fields[self.nesting:]
    self.columns = max(self.columns, len(items))
    branch.insertChild(LeafNode(items, branch))
    if callReset:
        self.reset()
```

要添加一条记录，字段数量必须大于嵌套级别。我们使用的逻辑与我们在第 14 章中填充 `QTreeWidget` 内部模型时看到的类似。对于每个作为分支的字段，我们查找具有相同键的现有分支。如果我们找到了，就将其作为当前根分支；否则，我们创建一个新分支，将其作为当前根分支的子节点插入，并让新分支成为当前根分支。随着循环的进行，我们逐渐向下遍历树，创建所需的任何分支，直到到达最底层的分支。

一旦循环遍历了所有必要的分支，并创建了之前不存在的分支，我们可以创建一个非嵌套字段的列表，并将其作为当前（最底层）分支的子叶子节点添加。

为了具体说明，以 `Server Info` 应用为例，以下是发生的事情。当读取第一条记录时，我们有新的国家、新的州、新的城市、新的提供商等，因此不存在合适的分支。首先会创建一个国家分支，然后是州分支，接着是城市分支，最后是一个包含剩余提供商、服务器和 IP 地址字段的叶子。如果下一条读取的记录属于同一国家但属于新州，它将找到现有的国家节点并作为新州父节点使用。类似地，如果记录的国家和州已经有创建的分支，这些分支将被使用。但每当需要新分支时，循环体中的代码都会创建它。

当临时添加新记录时，我们调用 `reset()` 以通知任何视图发生了重大变化；但在从文件加载时，我们传递 `False`，并在所有记录读取完成后在调用代码中调用 `reset()`。

### `asRecord` 方法

```python
def asRecord(self, index):
    leaf = self.nodeFromIndex(index)
    if leaf is not None and isinstance(leaf, LeafNode):
        return leaf.asRecord()
    return []
```

该方法提供用户所选择的“路径”的列表。它只对叶子节点有意义，因为只有叶子节点才能代表完整的路径。对于非叶子节点返回 `None` 也是一个同样好的设计选择。注意，我们使用 `nodeFromIndex()` 方法检索给定模型索引对应的节点：我们将很快讨论其工作原理。

### `rowCount` 方法

```python
def rowCount(self, parent):
    node = self.nodeFromIndex(parent)
    if node is None or isinstance(node, LeafNode):
        return 0
```

```python
return θ
return len(node)
```

对于树模型，行数是指特定节点拥有的子节点数量。我们的实现只允许分支节点拥有子节点，因此当在叶节点上调用时，我们总是返回 `0`。`len()` 函数调用 `Branch-Node._len_()`，该方法返回分支子节点的数量。

### `columnCount` 方法

```python
def columnCount(self, parent):
    return self.columns
```

列数是非嵌套字段的最大数量。这看起来可能少了一列，但这是正确的，因为第一个非嵌套字段显示在第一个（树）列中。

### `data` 方法

```python
def data(self, index, role):
    if role == Qt.TextAlignmentRole:
        return QVariant(int(Qt.AlignTop|Qt.AlignLeft))
    if role != Qt.DisplayRole:
        return QVariant()
    node = self.nodeFromIndex(index)
    assert node is not None
    if isinstance(node, BranchNode):
        return QVariant(node.toString()) \
            if index.column() == 0 else QVariant(QString(""))
    return QVariant(node.field(index.column()))
```

如果请求分支节点的显示数据，我们返回第 `0` 列的节点文本以及其他列的空字符串。对于叶节点，我们返回与请求列对应的字段。

在 `Qt 4.2` 之前，默认文本对齐工作正常，无需指定，但从 `Qt 4.2` 开始，我们必须显式地返回一个合理的文本对齐。

### `headerData` 方法

```python
def headerData(self, section, orientation, role):
    if orientation == Qt.Horizontal and \
            role == Qt.DisplayRole:
        assert 0 <= section <= len(self.headers)
        return QVariant(self.headers[section])
    return QVariant()
```

树视图只有水平（列）标题。它们没有行标题（例如行号），因为每个分支都有自己的基于 `0` 的子节点（行）列表，因此行标题没有实际意义。

### `index` 方法

```python
def index(self, row, column, parent):
    assert self.root
    branch = self.nodeFromIndex(parent)
    assert branch is not None
    return self.createIndex(row, column,
            branch.childAtRow(row))
```

`index()` 方法必须返回具有给定行和列且是给定父项子项的数据项的模型索引。在分支和叶子的树模型中，这意味着我们必须返回父项的第 `row` 个子项的模型索引。

我们首先找到给定父模型索引的分支节点，然后返回一个模型索引，该索引具有给定的行和列，其父项是（分支）节点的第 `row` 个子节点。

### `parent` 方法

```python
def parent(self, child):
    node = self.nodeFromIndex(child)
    if node is None:
        return QModelIndex()
    parent = node.parent
    if parent is None:
        return QModelIndex()
    grandparent = parent.parent
    if grandparent is None:
        return QModelIndex()
    row = grandparent.rowOfChild(parent)
    assert row != -1
    return self.createIndex(row, 0, parent)
```

`parent()` 方法必须返回给定子项的父项的模型索引。在分支和叶子的树模型中，这是子项的祖父项的第 `row` 个子项。

我们首先找到子节点的父节点的父节点（即子项的祖父项）。然后我们返回一个模型索引，该索引具有父节点在祖父项的子节点列表中占据的行号，第 `0` 列（因为所有父项都是分支，且分支只有第 `0` 列），以及父项为子项的父节点。

此处展示的 `index()` 和 `parent()` 方法的实现相当微妙。然而，对于采用分支和叶子方法的树模型而言，这些是标准实现，因此其代码在大多数情况下可以直接“原样”复制。
