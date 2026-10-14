

第一次调用 `find_first_of()` 定位到 `vowels` 字符串中的第一个字符。为了在下一个字符处继续搜索，循环中的最后一行语句在前一个位置加一处进行搜索。编译并运行此代码会显示索引和字符值：

```
a[ 0] == 'a'
a[ 4] == 'e'
a[ 8] == 'i'
a[14] == 'o'
a[20] == 'u'
```

## DEBUGGING string OBJECTS

没有影响 string 对象的特殊调试命令，但在显示字符串时，GNU 调试器会显示一些乍一看可能很奇怪的值。为了跟上进度，使用以下命令为调试编译 `sdeclare.cpp`，第 22.1 节清单，并将其加载到 gdb 中：

```
$ g++ -g -o sdeclare sdeclare.cpp
$ gdb --silent sdeclare
```

输入 `list 1` 然后 `list`（或仅 `l`）来列出一些行，直到找到构造 `sFromString` 的行（行号可能与你不同）：

```
(gdb) list
...
18 string sFromLiteral('Stringing in the rain');
19 string sFromString(sFromLiteral);
```

在第 19 行设置断点并运行程序直到该语句：

```
(gdb) b 19
Breakpoint 1 at 0x804a2de: file sdeclare.cpp, line 19.
(gdb) run
Starting program: /home/tswan/gpl/src/c22/sdeclare
Breakpoint 1, global constructors keyed to buffer () at sdeclare.cpp:19
19 string sFromString(sFromLiteral);
```

请注意，断点位于全局构造函数中，在 `main()` 执行之前被调用。程序在构造 `sFromString` 之前暂停。通过输入 `next` 命令执行该语句，然后打印字符串以检查其值：

```
(gdb) next
(gdb) print sFromString
$2 = {static npos = <optimized out>,
 static nilRep = <optimized out>,
 dat = 0x804d7b8 "Stringing in the rain"}
```

存在。它是对 GNU 调试器和编译器作者的赞誉，调试器不会简单地将这些值报告为未找到，而是知道它们是被有意删除的。然而，这对本书的技术编辑来说并非如此，所以也许这些值现在以某种方式被使用了。

如果你在跟随操作，输入 `c` 然后 `q` 以继续程序到结束并退出调试器。

## SUMMARY

标准 string 类为 C++ 程序中创建和使用字符字符串提供了一种新方法。虽然你可能继续使用 C 风格的以空字符结尾的 `char` 数组作为字符串，但本章描述的 ANSI C++ string 类由于许多原因而更优越。例如，string 对象通过抛出异常来报告错误，并且由于 string 类被设计为模板，它可以使用任何类型和大小的字符。本章介绍了 string 类并展示了如何创建 string 对象和调用 string 类成员函数的多个示例。

有关本章介绍主题的更多信息，请参阅以下章节：

- Chapter 16, “Handling Exceptions”
- Chapter 23, “Using the Standard Template Library (STL)”
- Chapter 24, “Building Standard Containers”
- Chapter 25, “Applying Standard Algorithms”

## CHAPTER 23

## Using the Standard Template Library (STL)

## STL COMPONENTS

STL 提供了大量模板类和函数，可在 OOP 和传统编程中使用。STL 的约 50 个算法完全通用，并且不依赖于任何特定数据类型。以下段落描述了三个基本的 STL 组件：

- **Iterators** 提供对容器中对象的访问。例如，一对迭代器定义了列表或向量中对象的范围。迭代器类似于指针，事实上，C++ 指针是一种迭代器。然而，迭代器也可以是类对象，为其定义了指针访问 `operator*()` 函数和其他类似指针的操作符。
- **Containers** 是 STL 中作为模板类提供的列表、向量和 deque（双端队列）等数据结构。要访问 STL 容器中的数据，程序使用由容器类导出的迭代器类型。
- **Algorithms** 是在容器中操作数据的模板函数。例如，STL 提供了 `sort()` 等算法来对向量中的数据进行排序，以及 `find()` 来搜索对象列表。这些函数对它们操作的数据的类型和结构没有任何特殊了解，因此几乎可以在从简单数组到高度复杂容器的任何结构上使用。

## HEADER FILES

为避免与其他头文件冲突，STL 的头文件去掉了通常的 .h 扩展名。要包含标准字符串、迭代器和算法，请使用以下指令：

```
```cpp
#include <string>
#include <iterator>
#include <algorithm>
```
```

如果你浏览这些和其他 STL 文件，你可能会遇到 `iterator.h` 和 `stl_iterator.h` 等头文件。避免通过这些名称引用此类文件，它们可能在各种 STL 实现中有所不同。为了获得最佳效果并确保可移植性，请使用不带 .h 后缀的纯文件名。表 23.1 列出了许多更常用的各种容器类的 STL 头文件。这不是一个完整列表，我将在本章和接下来的两章中在适当的时候介绍其他头文件。

