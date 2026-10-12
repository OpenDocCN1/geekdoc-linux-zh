
对于右侧方法，我们可以使用这样的代码：

```python
try:
    load(args)
except (IOError, OSError), e:
    QMessageBox.warning(self, "File Error", unicode(e))
```

另一种方法，用于 `chap09/sdtexteditor.pyw` 和 `chap12/pagedesigner.pyw`，是在文件处理方法的内部进行所有的错误处理：

```python
fh = None
try:
    # open file and read data
except (IOError, OSError), e:
    QMessageBox.warning(self, "File Error", unicode(e))
finally:
    if fh is not None:
        fh.close()
```

在调用点，我们只需调用 `load(args)`，让 `load()` 方法本身向用户报告任何问题。

### 表 8.1 选定的 QDataStream 方法

| 语法 | 描述 |
|---|---|
| `s.atEnd()` | 如果已到达 `QDataStream` `s` 的末尾，则返回 True。 |
| `s.setVersion(v)` | 将 `QDataStream` `s` 的版本设置为 `v`，其中 `v` 为 `Qt_1_0`、`Qt_2_0`、……、`Qt_4_2` 或 `Qt_4_3` 之一。 |
| `s << x` | 将对象 `x` 写入 `QDataStream` `s`；`x` 可以是 `QBrush`、`QColor`、`QDate`、`QDateTime`、`QFont`、`QIcon`、`QImage`、`QMatrix`、`QPainterPath`、`QPen`、`QPixmap`、`QSize`、`QString`、`QVariant` 等类型。 |
| `s.readBool()` | 从 `QDataStream` `s` 读取一个 bool。 |
| `s.readDouble()` | 从 `QDataStream` `s` 读取一个 float。 |
| `s.readInt16()` | 从 `QDataStream` `s` 读取一个 16 位 int。也有 `readUInt16()` 方法。 |
| `s.readInt32()` | 从 `QDataStream` `s` 读取一个 32 位 int。也有 `readUInt32()` 方法。 |
| `s.readInt64()` | 从 `QDataStream` `s` 读取一个 64 位 long。也有 `readUInt64()` 方法。 |
| `x = QString()` `s >> x` | 从 `QDataStream` `s` 读取对象 `x`；`x` 必须已经存在（以便数据流知道要读取的数据类型），可以是 `<<` 可写入的任何类型。 |
| `s.writeBool(b)` | 将 bool `b` 写入 `QDataStream` `s`。 |
| `s.writeDouble(f)` | 将 float `f` 写入 `QDataStream` `s`。 |
| `s.writeInt16(i)` | 将 int `i` 作为 16 位 int 写入 `QDataStream` `s`。也有 `writeUInt16()` 方法。 |
| `s.writeInt32(i)` | 将 int `i` 作为 32 位 int 写入 `QDataStream` `s`。也有 `writeUInt32()` 方法。 |
| `s.writeInt64(l)` | 将 long `l` 作为 64 位 int 写入 `QDataStream` `s`。也有 `writeUInt64()` 方法。 |

### 使用 pickle 模块进行读写

Python 的标准 `pickle` 模块及其更快的 `cPickle` 对应模块可以将任意的 Python 数据结构保存到磁盘并重新加载回来。这些模块提供完全相同的功能和功能。它们之间的唯一区别在于 `pickle` 模块完全用 Python 实现，而 `cPickle` 模块用 C 实现。这些模块只理解 Python 标准库中的数据以及由它们构建的类。如果我们想要使用 PyQt 4.3 之前的版本 `pickle` PyQt 特有的数据类型，我们必须告诉 `pickle`（或 `cPickle`）模块如何处理它们。

```python
def _pickleQDate(date):
    return QDate, (date.year(), date.month(), date.day())

def _pickleQString(qstr):
    return QString, (unicode(qstr),)
```

`copy_reg.pickle(QDate, _pickleQDate)`

`copy_reg.pickle(QString, _pickleQString)`

`copy_reg` 模块用于指定如何读写非标准数据类型。通过调用 `copy_reg.pickle()` 并提供两个参数来提供相关信息。第一个参数是我们希望能够进行 pickle 操作的新式类，第二个参数是一个函数。该函数必须接受单个参数，即我们希望 pickle 的类的实例，并返回一个二元组（two-tuple），其中第一个元素是类本身，第二个元素是一个由标准 Python 类型组成的元组，该元组可以作为参数传入类的构造函数，以创建一个与传入实例具有相同值的实例。

利用这些信息，`pickle` 模块可以通过将类名作为文本存储，并将参数作为标准 Python 类型的元组来存储我们类的实例。然后，当我们需要将数据反序列化（unpickle，即加载）时，Python 可以使用 `eval()` 来重新创建我们的实例。

PyQt 4.3 包含对基本 Qt 数据类型的 pickle 支持，包括 `QByteArray`、`QChar`、`QColor`、`QDate`、`QDateTime`、`QKeySequence`、`QLine`、`QLineF`、`QMatrix`、`QPoint`、`QPointF`、`QPolygon`、`QRect`、`QRectf`、`QSize`、`QSizeF`、`QString`、`QTime` 以及所有 PyQt 枚举。这意味着我们可以“pickle”这些类型中的任意一个，而无需编写并注册我们自己的 pickle 函数。

```python
def savePickle(self):
    error = None
    fh = None
    try:
        fh = gzip.open(unicode(self.__fname), "wb")
        cPickle.dump(self.__movies, fh, 2)
    except (IOError, OSError), e:
        error = "Failed to save: %s" % e
    finally:
        if fh is not None:
            fh.close()
        if error is not None:
            return False, error
        self.__dirty = False
        return True, "Saved %d movie records to %s" % (
            len(self.__movies),
            QFileInfo(self.__fname).fileName())
```

我们可以轻松地将任何 Python 数据结构（包括递归数据结构）保存为 pickle。我们通过以二进制模式打开文件并使用 `dump()` 函数来实现这一点。在这个示例中，我们选择以压缩方式保存我们的 pickle（这可能会使文件大小减少约 50%），但我们也可以避免使用这种压缩，如下所示：

`fh = open(unicode(self.__fname), "wb")`

我们必须将文件名转换为 unicode，因为它是作为 `QString` 持有的。`open()` 的 `wb` 参数表示“以二进制模式写入”。`dump()` 函数接受一个 Python 数据结构（在本例中是我们 `[key, movie]` 列表的集合）、一个文件句柄和一个格式代码。我们总是使用格式代码 2，这意味着 pickle 二进制格式。

由于键（keys）是由 `key()` 方法生成的，我们实际上只需要保存 `Movie` 实例，而不需要保存 `[key, movie]` 列表。如果磁盘空间非常紧张，我们可能会这样做，但这要求我们在加载数据时重新生成键，因此这代表了磁盘空间与保存和加载速度之间的权衡。我们选择牺牲磁盘空间，以实现更快、更简单的保存和加载。
