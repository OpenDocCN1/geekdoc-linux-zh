

## 树节点方法

```python
def insertChild(self, child):
    child.parent = self
    bisect.insert(self.children, (child.orderKey(), child))
```

该方法将一个新的子节点插入到分支的子节点列表中，并让该分支成为此子节点的父节点。通过使用子节点的排序键结合 `bisect.insert()`，我们确保子节点能以最快速度和最高效率被放置到正确的位置。`insert()` 函数与 `insert_right()` 完全相同。

```python
def hasLeaves(self):
    if not self.children:
        return False
    return isinstance(self.children[0], LeafNode)
```

在表模型树中，拥有子节点的分支要么包含分支，要么包含叶子节点，但绝不会出现两者的混合。因此，如果一个分支完全没有子节点，显然它也没有叶子节点；类似地，如果它有子节点且第一个是叶子节点，那么它们全都是叶子节点。

至此，我们已经看完了整个分支节点类。接下来，我们将查看短得多的叶子节点类。

## 叶子节点类

```python
class LeafNode(object):
    def __init__(self, fields, parent=None):
        super(LeafNode, self).__init__(parent)
        self.parent = parent
        self.fields = fields
```

叶子节点中的字段即为该节点的列。

```python
def orderKey(self):
    return u"t".join(self.fields).lower()

def toString(self, separator="\t"):
    return separator.join(self.fields)

def __len__(self):
    return len(self.fields)
```

叶子节点的排序键是其字段以制表符分隔后的字符串连接。同样，其 `toString()` 方法返回字段的连接字符串。`__len__()` 方法返回字段数量；对于分支而言，它返回子节点的数量。

```python
def field(self, column):
    assert 0 <= column < len(self.fields)
    return self.fields[column]
```

该方法使得提取单个字段的值变得容易，同时断言该字段的列在有效范围内。

```python
def asRecord(self):
    record = []
    branch = self.parent
    while branch is not None:
        record.insert(0, branch.toString())
        branch = branch.parent
    assert record and not record[0]
    record = record[1:]
    return record + self.fields
```

表模型树中使用的“记录”概念是指从根节点到叶子父节点的所有分支的拼接，加上叶子本身——换言之，是用户完整的选路“路径”。就 Server Info 应用而言，这包括国家、州、城市、提供商、服务器和 IP 地址，其中国家、州和城市是分支，而每个叶子包含三个字段：提供商、服务器和 IP 地址。

要构建一条记录（一个字段列表），我们从叶子节点的父分支开始，并向上遍历分支树。每个分支的字符串都被前置添加到记录列表中。根分支没有字符串，因此我们从列表中移除该项。返回的列表是所有分支字符串加上叶子字符串的拼接。

## 表模型树

至此，我们已完成对节点的审查。表模型树是 `QAbstractItemModel` 的子类，它重新实现了许多我们预期的方法，如 `data()`、`headerData()`、`rowCount()` 和 `columnCount()`。此外，它提供了 `index()`、`parent()` 和 `nodeFromIndex()` 方法，这些方法通常是为树模型重新实现的。它还有一些额外方法，即 `load()` 和 `addRecord()`；这些用于加载表格数据并将其转换为由分支和叶子组成的树。我们将首先查看初始化程序，然后是加载数据的方法，最后是标准的模型/视图方法。

```python
class TreeOfTableModel(QAbstractItemModel):

    def __init__(self, parent=None):
        super(TreeOfTableModel, self).__init__(parent)
        self.columns = 0
        self.root = BranchNode("")
        self.headers = []
```

列的数量取决于所加载数据中的列数以及请求的嵌套级别。始终有一个根分支节点，它不包含文本，纯粹用作所有其他分支的父节点。表头是用作列标题的文本。

### 加载数据

```python
def load(self, filename, nesting, separator):
    assert nesting > 0
    self.nesting = nesting
    self.root = BranchNode("")
    exception = None
    fh = None
    try:
        for line in codecs.open(unicode(filename), "rU", "utf8"):
            if not line:
                continue
            self.addRecord(line.split(separator), False)
    except IOError, e:
        exception = e
    finally:
        if fh is not None:
            fh.close()
        self.reset()
        for i in range(self.columns):
            self.headers.append("Column #%d" % i)
        if exception is not None:
            raise exception
```

要加载的文件必须是一个文本文件，每行一条记录，每个字段由指定的分隔符分隔。文件必须编码为 UTF-8 Unicode（或者是 ASCII，因为它是 UTF-8 的子集）。空行将被忽略；任何其他行都将被视为一条记录并添加到树中。

一旦加载完成（无论成功与否），我们调用 `reset()` 以通知任何视图模型已发生巨大变化，并创建一些初始列标题。如果加载失败，我们随后会重新抛出异常，以便调用者处理。`columns` 变量在初始化程序中被设置为 0，在 `addRecord()` 中被设置为有意义的值。

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

为了具体说明，以 Server Info 应用为例，以下是发生的事情。当读取第一条记录时，我们有新的国家、新的州、新的城市、新的提供商等，因此不存在合适的分支。首先会创建一个国家分支，然后是州分支，接着是城市分支，最后是一个包含剩余提供商、服务器和 IP 地址字段的叶子。如果下一条读取的记录属于同一国家但属于新州，它将找到现有的国家节点并作为新州父节点使用。类似地，如果记录的国家和州已经有创建的分支，这些分支将被使用。但每当需要新分支时，循环体中的代码都会创建它。

当临时添加新记录时，我们调用 `reset()` 以通知任何视图发生了重大变化；但在从文件加载时，我们传递 `False`，并在所有记录读取完成后在调用代码中调用 `reset()`。

```python
def asRecord(self, index):
    leaf = self.nodeFromIndex(index)
    if leaf is not None and isinstance(leaf, LeafNode):
        return leaf.asRecord()
    return []
```

该方法提供用户所选择的“路径”的列表。它只对叶子节点有意义，因为只有叶子节点才能代表完整的路径。对于非叶子节点返回 `None` 也是一个同样好的设计选择。注意，我们使用 `nodeFromIndex()` 方法检索给定模型索引对应的节点：我们将很快讨论其工作原理。

```python
def rowCount(self, parent):
    node = self.nodeFromIndex(parent)
    if node is None or isinstance(node, LeafNode):
        return 0
```

