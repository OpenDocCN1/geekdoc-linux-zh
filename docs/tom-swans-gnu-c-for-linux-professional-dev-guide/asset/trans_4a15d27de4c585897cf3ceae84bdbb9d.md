
与所有 vector 容器一样，布尔 vector 的大小等于它所包含的值的数量。这不一定是容器的字节大小，如下面的语句所示：

```
cout << "vbool size == " << vbool.size() << endl;
cout << "vbool bytes == " << sizeof(vbool) << endl;
```

第一条语句报告的 `vbool` 大小为 16 个元素。第二条语句显示容器的字节大小是该值的两倍，即 32，这表明每个 `bool` 对象占用两个字节。

> **注意**
>
> `bit_vector` 类是 `vector<bool>` 类的同义词。这两个类都不是打包的位数组。

vector 的值被解释为 1 表示 `true`，0 表示 `false`。这意味着下面的语句显示的是 1 0，而不是可能预期的单词“true”和“false”：

```
cout << vbool[0] << " " << vbool[1] << endl;
```

## 调用 vector 函数

`vector` 模板提供了许多可调用的有用成员函数。我已经解释了其中一个函数 `reserve()`。另外两个函数 `front()` 和 `back()` 分别返回 vector 的第一个和最后一个元素：

```
cout << "First == " << vdouble.front() << endl;
cout << "Last == " << vdouble.back() << endl;
```

还有三个非常有用的函数是 `erase()`、`resize()` 和 `insert()`。为了演示这些函数，按如下方式定义一个包含六个整数的 vector：

```
int ia[6] = { 1, 2, 3, 4, 5, 6 };
vector<int> sixints(ia, ia + 6);
```

删除 vector 对象会使容器中的其他对象向上移动。例如，在调用 `find()` 定位到特定元素后，将返回的迭代器传给 `erase()` 即可删除该对象：

```
vector<int>::iterator p =
find(sixints.begin(), sixints.end(), 3);
sixints.erase(p);
```

在较早以前，`erase()` 不会改变 vector 的大小；因此，移动对象末尾的值会重复。正因如此，`erase()` 之后通常紧跟着调用 `resize()`，如下所示：

```
sixints.resize(5);
```

这样做无害，但已无必要。你也可以使用 `resize()` 增加 vector 中的元素数量。使用上一节中的空 `vint` 对象，下面的代码将其大小增加到 10，并向一个 vector 位置赋值：

```
if (vint.empty())
    vint.resize(10);
vint[3] = 123;
```

如果 vector 的大小等于零，则对 `empty()` 的调用为真。

调用 `insert()` 向 vector 中插入新值，并将其他值向下移动。下面的语句将值 99 插入 `sixints` vector 的第三个位置（第一个位置之后的第二个位置）：

```
sixints.insert(sixints.begin() + 2, 99);
```

使用 `pop_back()` 和 `push_back()` 函数可以将 vector 当作栈使用。下面的语句将值 123 压入到 vector 的末尾：

```
sixints.push_back(123);
```

调用不带参数的 `pop_back()` 来移除最后一个元素：

```
sixints.pop_back();
```

因为它不会返回被压入的值，而仅仅是移除它，所以要在调用 `pop_back()` 之前额外执行一步来保存该值。下面的语句将 `top` 设置为栈顶的值：

```
int top = sixints[sixints.size() - 1];
```

> **注意**
>
> 请参阅本章后面的“栈”一节，以了解更严格的栈容器类模板。

通过为其中一个容器调用 `swap()`，并将另一个容器作为参数传入，可以交换两个 vector。这会交换 vector `v` 和 `sixints`：

```
vector<int> v(6);
sixints.swap(v);
```

## 链表

链表是双向链接对象的线性集合。链表中的每个对象都包含两个可以指向另一个对象的指针。这种组织结构使链表成为一种非常高效的数据结构。无论对象顺序如何，链表只占用必要的空间，加上一点点额外空间用于链接，还可能有一些字节用于将每个内存块填充到最小分配大小。这使得链表成为在碎片化内存中存储数据的绝佳选择，从而可能比 vector 在有限内存中容纳更多信息，而 vector 中的对象在理论上是物理连续的。

链表对象的插入和删除绝对高效。删除链表中的第一个项所花的时间不会比删除最后一项多。同样，从链表中间删除对象不会导致其他对象移动，而只是要求容器调整几个链接。链表中没有空洞。

另一方面，当你需要快速访问数据时——例如在搜索匹配值时——链表并不是好的选择。链表中的搜索本质上是线性的，因此所花时间与所检查对象的数量成正比。对于快速随机访问数据，vector 可能比链表更合适。然而，如果你需要一种

