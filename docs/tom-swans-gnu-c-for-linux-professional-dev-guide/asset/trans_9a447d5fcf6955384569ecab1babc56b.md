

list 和随机访问（你想吃掉你的蛋糕又想保留它），并非全无办法：考虑使用本章后面描述的 set、map 或 priority_queue。

> Note
> 以下各节中的示例编程取自 CD-ROM 上 src/c24 目录中的文件 list.cpp。

## DECLARING LISTS

下面的语句展示了构造不同种类列表容器的几种方法：

```
list<int> ilist(10);
list<double> flist(10, 1.0);
list<string> strlist(24);
```

第一行创建了一个可以存储 int 值的空列表。第二行创建了一个包含 10 个 double 值且每个都初始化为 1.0 的列表。第三行创建了一个包含 24 个字符串的列表。你可以在列表容器中存储其他类型的数据。然而，struct 和 class 对象需要以下成员：

- Default constructor
- Copy constructor
- Destructor
- Assignment operator=() function
- Equality operator==() function (must be const)
- Less-than operator<() function (must be const)
- Address-of operator&() function

你必须显式声明构造函数和析构函数，但运算符函数是可选的。除非类声明了指向已分配内存的指针，例如，否则你不必重载 operator=() 赋值函数。使用文件 coordinate.h 中的 TCoordinate 类（参见 Listing 24.1），下面的语句构造了类对象的列表：

```
list<TCoordinate> coords(10);
list<TCoordinate *> coordPtrs(10);
```

第一条语句创建了 10 个 TCoordinate 对象的列表。第二条语句创建了指向 TCoordinate 对象的指针列表。将对象插入第一个列表时可使用如下语句：

```
coords.insert(coords.begin(), TCoordinate(4, 5));
```

在这种情况下，因为容器存储的是指针，所以调用任何必要的析构函数是你的责任。例如，要从 coordPtrs 中移除一个已列出的对象需要两条语句：

```
delete coordPtrs.front();
coordPtrs.remove(coordPtrs.front());
```

第一条语句删除列表中第一个对象所分配的内存。第二条语句移除了指向该对象的现在无效的指针。

## USING LISTS

要确定列表中对象的数量，请调用 size() 函数。试试看。首先定义一个列表容器并用一些值填充它：

```
list<int> anyList;
for (int i = 0; i < 10; i++)
    anyList.insert(anyList.end(), i);
```

调用 empty() 和 size() 来确定列表是否为空，或者如果不为空，则显示其包含的元素数量：

```
if (anyList.empty())
    cout << "List is empty" << endl;
else
    cout << "List has " << anyList.size() << " elements" << endl;
```

有几种其他方法可以将对象插入列表容器。你可以使用前面示例中所示的 insert() 函数，也可以调用 push_front() 和 push_back() 在列表开头或结尾插入对象。给定 anyList 容器，使用如下代码向其头部和尾部添加对象：

```
anyList.push_back(1234);
anyList.push_front(4321);
```

> Tip
> 要显示本节中列表示例的内容，CD-ROM 上的示例 list.cpp 程序使用了以下输出语句：
> copy(c.begin(), c.end(),
>     ostream_iterator<int>(cout, " *"));

要插入多个初始化为特定值 的对象，以下代码本应可行但编译失败：

```
anyList.insert(anyList.begin(), 4, -1); // ???
```

GNU C++ 似乎不喜欢字面量的初始化值，而以下代码使用变量作为解决该问题的合理变通方法：

```
int value = -1;
anyList.insert(anyList.begin(), 4, value);
```

这将在列表容器中插入四个等于 -1 的整数对象。另一种插入对象的方法是使用迭代器。在搜索列表中特定值之后，通常会这样做，也许使用 find() 算法。首先，为容器的类定义一个迭代器：

```
list<int>::iterator p;
```

然后调用 find() 或其他搜索算法，然后进行插入：

```
p = find(anyList.begin(), anyList.end(), 8);
if (p != anyList.end())
    anyList.insert(p, -2);
```

使用 find() 时，传递两个定义容器中对象搜索范围的迭代器。还传递要查找的值，此处为 8。搜索后，如果迭代器 p 不等于 past-the-end 值，则它指向一个已列出的对象。将迭代器和要插入列表中的新对象值传递给 insert。实际上，你不必测试 p 的值，因为即使列表为空，find() 也会将 p 设置为 past-the-end 值，并且插入将在列表末尾进行，或开始一个新列表。

要从列表容器中移除对象，你有几个选择。调用 erase() 来移除特定元素，通常在如下示例代码中的搜索语句之后：

```
p = find(anyList.begin(), anyList.end(), 7);
if (p != anyList.end())
    anyList.erase(p);
```

这会在整数列表中搜索值 7，如果找到，则调用 erase() 从列表中移除该值。列表容器会自动删除任何已分配的内存并调用对象的类析构函数。然而，如果列表包含指针，则删除任何已分配内存是你的责任。

要移除列表中所有相等的值，请调用 remove() 并指定要定位的值：

```
anyList.remove(-1);
```

这会从 anyList 中移除所有等于 -1 的整数值。使用 erase() 的另一种形式来移除定义范围内的所有对象。通常，你会在搜索特定元素后这样做，如以下代码所示：

```
p = find(anyList.begin(), anyList.end(), 3);
anyList.erase(p, anyList.end());
```

使用前面定义的迭代器 p，第一条语句调用 find() 在列表中定位值 3。第二条语句调用 erase() 从该点到列表末尾移除所有对象。即使搜索到的对象未找到，此代码也能正确工作，因为如果 p 等于 past-the-end 值，第二条语句什么也不做。 （你可能仍会像前面所述那样测试 p 的值。）

列表通常用作栈和队列，其中对象从列表容器的前端和后端被推入和弹出。通过调用 pop_front() 移除列表的第一个对象。通过调用 pop_back() 移除最后一个对象。例如，此循环显示并移除 anyList 中的所有对象：

```
while (!anyList.empty()) {
    cout << anyList.front() << endl;
    anyList.pop_front();
}
```

