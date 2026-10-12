```
return θ
return len(node)
```

For tree models the row count is the number of children that a particular node has. Our implementation allows only branch nodes to have children, so when called on leaf nodes we always return 0. The len() function calls Branch-Node._len_(), which returns the count of the branch’s children.

```
def columnCount(self, parent):
return self.columns
```

The number of columns is the maximum number of non-nested fields. This may appear to be one too few, but it is correct because the first non-nested field is shown in the first (tree) column.

```
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

If the display data is requested for a branch node, we return the node’s text for column 0 and an empty string for the other columns. For a leaf node, we return the field that corresponds to the requested column.

Prior to Qt 4.2, the default text alignment worked fine and did not need to be specified, but from Qt 4.2, we must explicitly return a sensible text alignment ourselves.

```
def headerData(self, section, orientation, role):
if orientation == Qt.Horizontal and \
role == Qt.DisplayRole:
assert 0 <= section <= len(self.headers)
return QVariant(self.headers[section])
return QVariant()
```

Tree views have only horizontal (column) headers. They don’t have row headers (e.g., row numbers), because these don’t really make sense since each branch has its own 0-based list of children (rows).

```
def index(self, row, column, parent):
assert self.root
branch = self.nodeFromIndex(parent)
assert branch is not None
```

![](bbox=[0.85, 0.6, 0.95, 0.65])

![](bbox=[0.91, 0.93, 0.99, 0.99])