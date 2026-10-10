
```cpp
class Movie
{
public:
    Movie(const QString& title = "", int duration = 0);
    void setTitle(const QString& title) { myTitle = title; }
    QString title() const { return myTitle; }
    void setDuration(int duration) { myDuration = duration; }
    int duration() const { return myDuration; }

private:
    QString myTitle;
    int myDuration;
};
```

该类有一个不需要参数的构造函数（尽管它可以接受两个）。它还有一个拷贝构造函数和赋值运算符，由 `C++` 隐式提供。对于该类，成员级拷贝就足够了，因此不需要实现自己的拷贝构造函数和赋值运算符。

`Qt` 提供了两类用于遍历容器存储项目的迭代器：`Java` 风格迭代器和 `STL` 风格迭代器。`Java` 风格迭代器更容易使用，而 `STL` 风格迭代器可以与 `Qt` 的泛型算法结合，也非常强大。

每个容器类都有两种 `Java` 风格迭代器类型：只读迭代器和读写迭代器。它们的有效位置如图 `11.3` 所示。只读迭代器类为 `QVectorIterator<T>`、`QLinkedListIterator<T>` 和 `QListIterator<T>`。相应的读写迭代器名称中带有 `Mutable`（例如 `QMutableVectorIterator<T>`）。在本讨论中，我们将关注 `QList` 迭代器；链表和 `vector` 的迭代器具有相同的 `API`。

使用 `Java` 风格迭代器时需要记住的第一点是它们并不直接指向项目。相反，它们可以位于第一个项目之前、最后一个项目之后，或者两个项目之间。一个典型的迭代循环如下：

```cpp
QList<double> list;
...
QListIterator<double> i(list);
```

### 序列容器

```cpp
while (i.hasNext()) {
  do_something(i.next());
}
```

迭代器使用要遍历的容器进行初始化。此时，迭代器位于第一个项目之前。如果迭代器右侧有项，则调用 `hasNext()` 将返回 `true`。`next()` 函数返回迭代器右侧的项，并将迭代器移动到下一个有效位置。

反向遍历也类似，但我们必须先调用 `toBack()` 将迭代器置于最后一个项目之后：

```cpp
QListIterator<double> i(list);
i.toBack();
while (i.hasPrevious()) {
  do_something(i.previous());
}
```

如果迭代器左侧有项，`hasPrevious()` 函数返回 `true`；`previous()` 返回迭代器左侧的项并将迭代器后移一个位置。思考 `next()` 和 `previous()` 迭代器的另一种方式是，它们返回的是刚刚跳过的那个迭代器。

图 `11.4`。`previous()` 和 `next()` 对 `Java` 风格迭代器的影响

| A | B | C | D | E |
| :--- | :--- | :--- | :--- | :--- |
| | | | | |
| | previous() | | | next() |

可变迭代器提供了在迭代时插入、修改和删除项的函数。以下循环从列表中删除了所有负数：

```cpp
MutableListIterator<double> i(list);
while (i.hasNext()) {
  if (i.next() < 0.0)
    i.remove();
}
```

`remove()` 函数始终作用于最后跳过的那个项。它在反向遍历时也同样有效：

```cpp
MutableListIterator<double> i(list);
i.toBack();
while (i.hasPrevious()) {
  if (i.previous() < 0.0)
    i.remove();
}
```

同样，可变的 `Java` 风格迭代器提供了一个 `setValue()` 函数，用于修改最后跳过的那个项。以下是我们将负数替换为其绝对值的方法：

## 11. 容器类

```cpp
QMutableList<double> i(list);
while (i.hasNext()) {
  int val = i.next();
  if (val < 0.0) {
    i.setValue(-val);
  }
}
```

还可以通过调用 `insert()` 在当前位置插入项。随后迭代器将向前移动，指向新项和后续项之间。

除了 `Java` 风格迭代器外，每个序列容器类 `<T>` 都有两个 `STL` 风格的迭代器类型：`<T>::iterator` 和 `<T>::const_iterator`。两者的区别在于 `const` 迭代器不允许我们修改数据。

容器的 `begin()` 函数返回一个 `STL` 风格的迭代器，指向容器中的第一个项目（例如 `list[0]`），`end()` 返回一个指向“最后一个项目之后”的迭代器（例如，对于大小为 5 的列表，指向 `list[5]`）。图 `11.5` 显示了 `STL` 风格迭代器的有效位置。如果容器为空，`begin()` 等于 `end()`，通常为了此目的调用 `isEmpty()` 更方便。

| A | B | C | D | E |
|---|---|---|---|---|
| | begin() | | | end() |

**图 11.5.** `STL` 风格迭代器的有效位置

`STL` 风格迭代器的语法是模仿 `C++` 指针指向数组的模式。我们可以使用 `++` 和 `--` 运算符来获取下一个或上一个项，并使用一元运算符 `*` 来获取当前项。对于 `QVector<T>`，迭代器类型和 `const` 迭代器类型仅仅是 `T *` 和 `const T *` 的别名（这是因为 `QVector<T>` 将项存储在连续的内存位置）。

以下示例将 `QList<double>` 中的每个值替换为其绝对值：

```cpp
QList<double>::iterator i = list.begin();
while (i != list.end()) {
  *i = qabs(*i);
  ++i;
}
```

一些 `Qt` 函数返回一个容器。如果我们想使用 `STL` 风格的迭代器遍历函数的返回值，我们必须获取容器的副本并遍历该副本。例如，以下代码是遍历 `QSplitter::sizes()` 返回的 `QList<int>` 的正确方法：

```cpp
QList<int> list = splitter->sizes();
QList<int>::const_iterator i = list.begin();
while (i != list.end()) {
  do_something(*i);
  ++i;
}
```

以下代码是错误的：

```cpp
// 错误
QList<int> i = splitter->sizes().begin();
while (i != splitter->sizes().end()) {
  do_something(*i);
  ++i;
}
```

这是因为 `QSplitter::sizes()` 每次被调用时都会返回一个新的 `QList<int>` 值。如果我们不存储返回值，`C++` 会在我们开始执行之前自动销毁它，导致留下一个悬空迭代器。更糟糕的是，每次循环运行时，`QSplitter::sizes()` 都必须生成列表的新副本，直到遇到 `splitter->sizes().end()`。总结：使用 `STL` 风格迭代器时，始终对按值返回的容器副本进行遍历。

对于只读的 `Java` 风格迭代器，我们不需要拷贝。隐式共享（implicit sharing）的美妙之处在于，如果我们修改数据，数据就不会被复制。为了充分利用隐式共享，我们可以养成一些新习惯。其中一个习惯是在非 `const` 向量上使用 `at()` 函数而不是 `[]` 运算符进行只读访问。由于 `Qt` 容器无法判断 `[]` 是否出现在赋值符号左侧，它会假设最坏的情况并强制深拷贝。

当我们使用 `STL` 风格迭代器遍历容器时，会出现类似的问题。当我们在非 `const` 容器上调用 `begin()` 或 `end()` 时，`Qt` 会强制发生深拷贝。为了防止这种低效率，解决方案是尽可能使用 `const_iterator`、`constBegin()` 和 `constEnd()`。

`Qt` 对所有的容器以及许多类（包括 `QByteArray`、`QBrush`、`QFont`、`QImage`、`QPixmap` 和 `QString`）使用了隐式共享。这使得这些类作为函数参数和返回值按值传递非常高效。

相比之下，`STL` 鼓励我们通过非 `const` 引用传递向量以避免拷贝。

`Qt` 提供了另一种遍历序列容器项的方法，即 `foreach` 循环。它看起来如下：

```cpp
QLinkedList<Movie> list;

foreach (Movie movie, list) {
    if (movie.title() == "Citizen Kane") {
        std::cout << "Found Citizen Kane" << std::endl;
        break;
    }
}
```

`foreach` 伪关键字是用标准的 `for` 循环实现的。在循环的每次迭代中，迭代变量（`movie`）被设为一个新项，从容器中的第一个项目开始并向前推进。`foreach` 循环在进入循环时会自动获取容器的副本，因此如果容器在迭代期间被修改，循环也不会受到影响。

### 隐式共享的工作原理

隐式共享在后台自动运行，因此我们不需要在代码中进行任何操作来实现这种优化。但由于了解它的工作原理是有益的，我们将研究一个示例并查看底层发生了什么。该示例使用了 `QString`，它是 `Qt` 的隐式共享类之一。

```cpp
QString str1 = "Humpty";
QString str2 = str1;
```

我们将 `str1` 设置为 "Humpty"，并将 `str2` 设置为等于 `str1`。此时，两个 `QString` 都指向内存中的同一个内部数据结构。除了字符数据外，该数据结构还持有一个引用计数，指示有多少个 `QString` 指向该数据。由于 `str1` 和 `str2` 都指向相同的数据，引用计数为 2。

当我们修改 `str2` 时，它会首先对数据进行深拷贝，以确保 `str1` 和 `str2` 指向不同的数据结构，然后将更改应用于它自己的数据拷贝。`str1` 数据（"Humpty"）的引用计数变为 1，`str2` 数据（"Dumpty"）的引用计数为 1。引用计数为 1 意味着数据未被共享。

```cpp
str2.truncate(4);
```

当我们再次修改 `str2` 时，不会发生拷贝，因为 `str2` 数据的引用计数为 1。`truncate()` 函数直接作用于 `str2` 的数据，产生字符串 "Dump"。引用计数保持为 1。

```cpp
str1 = str2;
```

当我们将 `str2` 赋值给 `str1` 时，`str1` 数据的引用计数会降为 0，这意味着不再有任何 `QString` 指向 "Humpty" 数据。该数据将从内存中释放。两个 `QString` 都指向 "Dumpty"，该数据现在的引用计数为 2。

在多线程程序中，数据共享不被视为选项，因为引用计数中存在竞态条件。在 `Qt` 中，这不是问题。在内部，容器类使用汇编指令来执行原子引用计数。这项技术通过 `QSharedData` 和 `QSharedDataPointer` 类提供给 `Qt` 用户。

支持 `break` 和 `continue` 循环语句。如果体由单个语句组成，则不需要括号。与 `for` 语句一样，迭代变量可以在循环外定义，如下所示：

```cpp
LinkedList<Movie> list;
Movie movie;
...
```

## 11. 容器类

```cpp
foreach (movie, list) {
  if (movie.title() == "Citizen Kane") {
    std::cout << "Found Citizen Kane" << std::endl;
    break;
  }
}
```

对于包含逗号的数据类型的容器（例如 `QPair<QString, int>`），在循环外定义迭代变量是唯一的选择。

### 关联容器

关联容器通过键（key）进行索引，存储任意数量的同类型项。`Qt` 提供了两个主要的关联容器：`QMap<K, T>` 和 `QHash<K, T>`。

`QMap<K, T>` 是一种按键升序存储键-值对的数据结构，如图 `11.6` 所示。这种安排使得良好的查找和插入性能以及按键顺序迭代成为可能。在内部，`QMap<K, T>` 实现为跳跃表（skip-list）。

| Mexico City | 2235000 |
| :--- | :--- |
| Seoul | 22050000 |
| Tokyo | 34000000 |

图 `11.6`。`QString` 到 `int` 的映射

向 `map` 插入项的一种简单方法是调用 `insert()`：

```cpp
QMap<QString, int> map;
map.insert("eins", 1);
map.insert("sieben", 7);
map.insert("dreundzwanzig", 23);
```

或者，我们可以简单地如下所示为给定的键赋值：

```cpp
map["eins"] = 1;
map["sieben"] = 7;
map["dreundzwanzig"] = 23;
```

`[]` 运算符可用于插入也可用于检索。如果在非常量 `map` 中使用 `[]` 获取不存在的键的值，将创建一个带有给定键和空值的新项。为了避免无意创建空值，我们可以使用 `value()` 函数来检索项而不是 `[]`：

```cpp
int val = map.value("dreundzwanzig");
```

如果键不存在，则将使用值类型的默认构造函数返回默认值，且不会创建新项。对于基本类型和指针类型，将返回 0。我们可以将另一个默认值作为 `value()` 的第二个参数，例如：

```cpp
int seconds = map.value("delay", 30);
```

这等同于：

```cpp
int seconds = 30;
if (map.contains("delay"))
    seconds = map.value("delay");
```

`Map<K, T>` 的 `K` 和 `T` 类型可以是像 `int` 和 `double` 这样的基本数据类型、指针类型，或者具有默认构造函数、拷贝构造函数和赋值运算符的类。此外，`K` 类型必须提供 `operator<()`，因为 `Map<K, T>` 使用该运算符按升序存储项。

`Map<K, T>` 拥有两个方便函数：`key()` 和 `values()`，它们在处理小数据集时特别有用。它们返回包含 `map` 键的 `QList`。

# 关联容器

它们与 `std::map<K, T>` 的迭代器显著不同，后者是基于 `std::pair<K, T>` 的。

`foreach` 循环也适用于关联容器，但只作用于键值对中的值部分。如果我们同时需要项的键和值部分，可以在嵌套的 `foreach` 循环中调用 `keys()` 和 `values(const K&)` 函数，如下：

```cpp
QMultiMap<QString, int> map;
...
foreach (QString key, map.keys()) {
    foreach (int value, map.values(key)) {
        do_something(key, value);
    }
}
```

### 通用算法

`<QtAlgorithm>` 头声明了一系列全局模板函数，实现了针对容器的基本算法。这些函数大部分都是针对 `STL` 风格迭代器操作的。

`STL` 的 `<algorithm>` 头提供了更完整的通用算法集，适用于 `Qt` 容器。这些算法可以像使用 `STL` 容器一样用于 `Qt` 容器。如果你的所有平台上都有可用的 `STL` 实现，那么当 `Qt` 缺少某种算法时，可能不需要避免使用 `STL` 算法。在这里，我们将介绍最重要的 `Qt` 算法。

```cpp
QList list;
list << "Emma" << "Karl" << "James" << "Mariette";
QList::iterator i = qFind(list.begin(), list.end(), "Karl");
QList::iterator j = qFind(list.begin(), list.end(), "Petra");
```

`qBinaryFind()` 算法执行与 `qFind()` 类似的搜索，不同之处在于假设项按升序排列，并使用快速的二分查找而不是 `qFind()` 的线性查找。

`qFill()` 算法用特定值填充容器：

```cpp
QLinkedList<int> list(10);
qFill(list.begin(), list.end(), 1009);
```

与其他基于迭代器的算法一样，我们也可以通过改变参数在容器的部分区域上使用 `qFill()`。以下代码段将向量 的前五个项初始化为 100，后五个项初始化为 2013：

```cpp
QVector<int> vec(10);
qFill(vec.begin(), vec.begin() + 5, 1009);
qFill(vec.end() - 5, vec.end(), 2013);
```

`qCopy()` 算法将值从一个容器拷贝到另一个容器：
