
这是因为 `QSplitter::sizes()` 每次被调用都会按值返回一个新的 `QList<int>`。如果我们不存储返回值，C++ 会在我们开始迭代之前自动销毁它，导致留下一个悬空迭代器。糟糕的是，每次运行循环时，由于 `splitter->sizes().end()` 调用，`QSplitter::sizes()` 必须生成列表的新副本。总结来说：

使用 STL 风格迭代器时，始终对按值返回的容器副本进行迭代。

对于只读的 Java 风格迭代器，我们不需要获取副本。迭代器在后台为我们获取了副本，确保我们始终遍历的是函数最初返回的数据。例如：

```cpp
QListIterator<int> i(splitter->sizes());

while (i.hasNext()) {
 do_something(i.next());
}
```

这样复制容器听起来很开销，但并不是，得益于称为隐式共享（implicit sharing）的优化。这意味着拷贝 Qt 容器几乎和拷贝单个指针一样快。只有当其中一个副本被修改时，数据才会实际复制——而这一切都在后台自动处理。

隐式共享的妙之处在于，它是一种我们不需要考虑的优化，它简单有效，无需任何干预。

在多线程程序中，数据共享通常被忽略一种选项，因为引用计数中存在竞态条件。在 Qt 中，这不是一个问题。在内部，容器类使用汇编指令执行原子引用计数。Qt 用户可以通过 `QSharedData` 和 `QSharedDataPointer` 类来使用这项技术。

该程序支持 `break` 和 `continue` 循环语句。如果循环体包含单个语句，则不需要大括号。就像 `for` 语句一样，迭代变量可以在循环外定义，如下所示：

```cpp
QLinkedList<Movie> list;
Movie movie;
...

foreach (movie, list) {
 if (movie.title() == "Citizen Kane") {
  std::cout << "Found Citizen Kane" << std::endl;
  break;
 }
}
```

对于包含逗号的数据类型（例如 `QPair<QString, int>`）的容器，在循环外定义迭代变量是唯一的选择。

## 关联容器

关联容器按键索引存储任意数量相同类型的项。Qt 提供了两个主要的关联容器类：`QMap<K, T>` 和 `QHash<K, T>`。

`QMap<K, T>` 是一种按键的升序存储键值对的数据结构，如图 11.6 所示。这种安排使得提供良好的查找和插入性能以及按键顺序迭代成为可能。在内部，`QMap<K, T>` 实现为跳表（skip-list）。

**图 11.6. 从 `QString` 到 `int` 的映射**

![](img/1bc72df8c60cf85926d3aefcc273027d_448_0.png)

向映射中插入项的一种简单方法是调用 `insert()`：

```cpp
QMap<QString, int> map;
map.insert("eins", 1);
map.insert("sieben", 7);
map.insert("dreiundzwanzig", 23);
```

或者，我们可以按照如下方式给给定的键赋值：

```cpp
map["eins"] = 1;
map["sieben"] = 7;
map["dreiundzwanzig"] = 23;
```

`[]` 运算符可用于插入和检索。如果在非 `const` 映射中使用 `[]` 检索不存在的键的值，将创建一个具有给定键和空值的新项。为了避免意外创建空值，我们可以使用 `value()` 函数来检索项，而不是 `[]`：

```cpp
int val = map.value("dreiundzwanzig");
```

如果键不存在，则将使用值类型的默认构造函数返回一个默认值，且不会创建新项。对于基本类型和指针类型，将返回 0。我们可以通过 `value()` 的第二个参数指定另一个默认值，例如：

```cpp
int seconds = map.value("delay", 30);
```

这等同于：

```cpp
int seconds = 30;
if (map.contains("delay"))
 seconds = map.value("delay");
```

`QMap<K, T>` 的 `K` 和 `T` 数据类型可以是像 `int` 和 `double` 这样的基本数据类型、指针类型，或者是那些定义了默认构造函数、拷贝构造函数和赋值运算符的类。此外，`K` 类型必须提供 `operator<()`，因为 `QMap<K, T>` 使用该运算符按键的升序存储项。

`QMap<K, T>` 拥有两个便利函数 `keys()` 和 `values()`，它们在处理较小的数据集时特别有用。它们返回包含映射的键和值的 `QList`。

映射通常是单值的：如果给现有的键分配一个新值，旧值将被新值替换，确保没有两个项共享相同的键。通过使用 `insertMulti()` 函数或 `QMultiMap<K, T>` 便利子类，可以拥有具有相同键的多个键值对。`QMap<K, T>` 有一个 `values(const K &)` 重载，它返回给定键的所有所有值的 `QList`。例如：

```cpp
QMultiMap<int, QString> multiMap;
multiMap.insert(1, "one");
multiMap.insert(1, "eins");
multiMap.insert(1, "uno");
QList<QString> vals = multiMap.values(1);
```

`QHash<K, T>` 是一种在哈希表中存储键值对的数据结构。它的接口几乎与 `QMap<K, T>` 相同，但它对 `K` 模板类型有不同的要求，并且通常提供比 `QMap<K, T>` 快多的查找。另一个区别是 `QHash<K, T>` 是无序的。

对存储在容器中的任何值类型的标准要求外，`QHash<K, T>` 的 `K` 类型还需要提供 `operator==()` 并被全局 `qHash()` 函数支持，该函数返回键的哈希值。Qt 已经为整数类型、指针类型、`QChar`、`QString` 和 `QByteArray` 提供了 `qHash()` 函数。

`QHash<K, T>` 为其内部哈希表自动分配质数量的桶（buckets），并在插入或删除项时调整其大小。还可以通过调用 `reserve()` 指定预期的项数来精调性能。

`qCopy()` 也可以用于拷贝同一个容器内的值，只要源范围和目标范围不重叠。在下一个代码段中，我们使用它将列表的最后两个项替换为前两个项：

```cpp
qCopy(list.begin(), list.begin() + 2, list.end() - 2);
```

`qSort()` 算法将容器中的项目按升序排序：

```cpp
qSort(list.begin(), list.end());
```

默认情况下，`qSort()` 使用 `<` 运算符来比较项目。要按降序排序项目，可以将 `qGreater<T>()` 作为第三参数传递（其中 `T` 是容器的数值类型），如下：

```cpp
qSort(list.begin(), list.end(), qGreater<int>());
```

我们可以使用第三个参数来定义自定义排序标准。例如，这里有一个“小于”比较函数，以忽略大小写的方式比较 `QString`：

```cpp
bool insensitiveLessThan(const QString &str1, const QString &str2)
{
 return str1.toLower() < str2.toLower();
}
```

对 `qSort()` 的调用变为：

```cpp
QStringList list;

...

qSort(list.begin(), list.end(), insensitiveLessThan);
```

`qStableSort()` 算法与 `qSort()` 类似，不同之处在于保证比较相等的项目在排序后的出现顺序与排序前相同。如果排序标准只考虑值的部分内容且结果对用户可见，那么这就非常有用。我们在第 4 章中使用 `qStableSort()` 实现了电子表格应用程序中的排序（第 92 页）。

`qDeleteAll()` 算法会对比容器中存储的每个指针调用 `delete`。这只对值类型为指针类型的容器才有意义。调用之后，这些项仍以悬空指针的形式存在于容器中，因此通常情况下我们还应该对容器调用 `clear()`。例如：

```cpp
qDeleteAll(list);
list.clear();
```

`qSwap()` 算法交换两个变量的值。例如：

```cpp
int x1 = line.x1();

int x2 = line.x2();

if (x1 > x2)
 qSwap(x1, x2);
```

最后，`<QtGlobal>` 头文件被每个其他 Qt 头文件包含，它提供了几个非常有用的定义，包括返回参数绝对值的 `qAbs()` 函数，以及返回两个值最小值或最大值的 `qMin()` 和 `qMax()` 函数。

## 字符串、字节数组和变体

`QString`、`QByteArray` 和 `QVariant` 是三个与容器有很多共同点的类，在某些场景下可以作为容器的替代方案。同样与容器一样，这些类使用隐式共享作为内存和速度优化。

我们将从 `QString` 开始。每个 GUI 程序都会使用字符串，不仅用于用户界面，通常还作为数据结构。C++ 原生提供了两种字符串：传统的 C 风格 `'\0'` 终止字符数组和 `std::string` 类。与这些不同，`QString` 持有 16 位的 Unicode 值。Unicode 包含 ASCII 和 Latin-1 子集并具有它们通常的数值。但由于 `QString` 是 16 位的，它可以表示数千个其他字符，用于编写世界上大多数语言。关于 Unicode 的更多信息，请参见第 18 章。

使用 `QString` 时，我们不需要担心分配足够内存或确保数据以 `'\0'` 结尾等晦涩细节。

从概念上说，`QString` 可以被视为 `QChar` 的向量（vector）。`QString` 可以嵌入 `'\0'` 字符。`length()` 函数返回整个字符串的大小，包括嵌入的 `'\0'` 字符。

`QString` 提供了一个二进制 `+` 运算符来连接两个字符串，以及一个 `+=` 运算符将一个字符串追加另一个。由于 `QString` 会自动在字符串数据的末尾预分配内存，通过重复追加字符构建字符串是非常快的。这里有一个结合了 `+` 和 `+=` 的示例：

```cpp
QString str = "User: ";

str += userName + "\n";
```

还有一个 `QString::append()` 函数，作用与 `+=` 运算符相同：

```cpp
str = "User: ";

str.append(userName);

str.append("\n");
```

另一种完全组合字符串的方法是使用 `QString` 的 `sprintf()` 函数：

```cpp
str.sprintf("%s %.1f%%", "perfect competition", 100.0);
```

该函数支持与 C++ 库中的 `sprintf()` 函数相同的格式说明符。在例中，`str` 被赋值为 "perfect competition 100.0%"。

另一种从其他字符串或数字构建字符串的方法是使用 `arg()`：

```cpp
str = QString("%1 %2 (%3s-%4s)")
 .arg("permissive").arg("society").arg(1950).arg(1970);
```

在这个示例中，"%1" 被替换为 "permissive"，"%2" 被替换为 "society"，"%3" 被替换为 "1950"，而 "%4" 被替换为 "1970"。结果是 "permissive society (1950s-1970s)"。存在多个 `arg` 重载来处理各种数据类型。某些重载具有额外的参数来控制字段宽度、数值基数或浮点精度。通常情况下，`arg()` 是比 `sprintf()` 好得多的解决方案，因为它是类型安全的，完全支持 Unicode 并允许翻译人员重新格式化。

`QString` 使用 `number()` 将数字转换为字符串：

```cpp
str = QString::number();

bool ok;

double d = str.number(&ok);
```

反向转换（从字符串到数字）通过 `toInt()`、`toLong()`、`toDouble()` 等实现。例如：

```cpp
if (fileName.toLower() == "readme.txt")

 ...
```

使用 `==` 运算符进行字符串比较是区分大小写的。如果我们在比较可见字符串，`localeAwareCompare()` 通常是正确的选择，如果我们想让比较忽略大小写，可以使用 `toUpper()` 或 `toLower()`。

例如：

```cpp
if (fileName.toLower() == "readme.txt")

 ...
```

一个非常频繁的需求是去除字符串中的空白（如空格、制表符和换行符）。`QString` 有一个函数可以消除字符串两端的空白：

```cpp
QString str = " BOB \t THE \nDOG \n";

qDebug() << str.trimmed();
```

字符串 `str` 可以被描绘为

B O B

\t T H E

\n D O G

\n

如果我们用另一个字符串替换字符串的某部分，可以使用 `replace()`：

```cpp
QString str = "a cloudy day";

str.replace(2, 6, "sunny");
```

结果是 "a sunny day"。代码可以重写为使用 `remove()` 和 `insert()`：

```cpp
str.remove(2, 6);

str.insert(2, "sunny");
```

首先，我们从位置 2 开始删除六个字符，得到字符串 "a day"（带有两个空格），然后我们在位置 2 处插入 "sunny"。

`replace()` 存在重载版本可以将第一个参数的所有出现处替换为第二个参数。例如，这里是如何将字符串中所有的 "&" 替换为 "&amp;"：

```cpp
str.replace("&", "&amp;");
```

`trimmed()` 返回的字符串是

B O B

\t

T H E

\n D O G

在处理用户输入时，我们通常希望在去除两端空白字符的同时，还希望将每一个一个或多个内部空白字符序列替换为单个空格。这就是 `simplified()` 函数的作用：

```cpp
QString str = " BOB \t THE \nDOG \n";

qDebug() << str.simplified();
```

`simplified()` 返回的字符串是

B O B

T H E

D O G

可以使用 `QString::split()` 将字符串拆分为包含子字符串的 `QStringList`：

```cpp
QString str = "polluter pays principle";

QStringList words = str.split(" ");
```

在前面的示例中，我们将字符串 "polluter pays principle" 拆分为三个子字符串："polluter""pays" 和 "principle"。`split()` 函数有一个可选的第二个参数，用于指定是否保留空子字符串（默认值）或丢弃。

`QStringList` 中的项可以使用 `join()` 合并成单个字符串。`join()` 的参数会被插入在每对连接的字符串之间。例如，这里展示了如何创建一个由 `QStringList` 中包含的所有字符串按字母排序并用换行符分隔的单个字符串：

```cpp
words.sort();

str = words.join("\n");
```

在处理字符串时，我们经常需要判断字符串是否为空。这通过调用 `isEmpty()` 或检查 `length()` 是否为 0 来完成。大多数情况下，从 `const char *` 字符串转换为 `QString` 是自动的，例如：

```cpp
str += " (1870)";
```

在这里，我们不需要形式地将 `const char *` 添加到 `QString`。要显式将 `const char *` 转换为 `QString`，只需使用 `QString` 强制转换，或调用 `fromAscii()` 或 `fromLatin1()`。（有关处理其他编码中的字面量字符串，请参见第 18 章。）

将 `QString` 转换为 `const char *`，使用 `toAscii()` 或 `toLatin1()`。这些函数返回一个 `QByteArray`，可以使用 `QByteArray::data()` 或 `QByteArray::constData()` 将其转换为 `const char *`。例如：

```cpp
printf("User: %s\n", str.toAscii().data());
```

为了方便起见，Qt 提供了 `qPrintable()` 宏，它的功能与 `toAscii().constData()` 相同：

```cpp
printf("User: %s\n", qPrintable(str));
```

当我们在 `QByteArray` 上调用 `data()` 或 `constData()` 时，返回的字符串由 `QByteArray` 对象所有。这意味着我们不需要担心内存泄漏；Qt 会我们回收内存。另一方面，我们必须注意不要长时间使用指针。如果 `QByteArray` 没有存储在变量中，它将在语句结束时自动删除。
