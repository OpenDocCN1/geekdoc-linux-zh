
- 6. 漏洞排除（BUG BUSTER）：这段代码哪里有问题？

```cpp
class Shape()
{
public:
    Shape();
    virtual ~Shape();
    virtual Shape(const Shape&);
};
```

# 第 2 周

## 第 12 天

## 数组、C 字符串和链表

在之前的课程中，你声明了单个的 `int`、`char` 或对象。你通常想要声明一个对象的集合，例如 20 个 `int` 或一堆猫。今天，你将学习：

- 什么是数组以及如何声明数组
- 什么是字符串以及如何使用字符数组来创建它们
- 数组与指针之间的关系
- 如何在数组上使用指针算术

### 什么是数组？

*数组*（array）是同类型类型数据存储位置的集合，每个位置都存储相同类型的数据。每个存储位置被称为数组的*元素*（element）。

你通过编写类型、后跟数组名和下标（subscript）来声明数组。*下标*是数组中元素的数量，括在方括号中。下标的另一个词是偏移量（offset），因为它代表了从数组开始位置的距离。例如：

```cpp
long LongArray[25];
```

这个示例声明了一个包含 25 个 `long` 整数的数组，名为 `LongArray`。当编译器看到这个声明时，它会留出足够的内存来存放 25 个元素。由于每个 `long` 整数需要 4 个字节，此声明留出了 100 个连续字节的内存，如图 12.1 所示。

### 图 12.1
声明数组。

![](img/a66ce94ee9cc26e5c70f5604bcd3600c_399_0.png)

### 访问数组元素

你通过引用数组名的偏移量来访问数组的每个元素。数组元素从零开始。因此，第一个数组元素是 `arrayName[0]`。在 `LongArray` 示例中，`LongArray[0]` 是第一个元素，`LongArray[1]` 是第二个，依此类推。

这可能会有些困惑。数组 `SomeArray[3]` 有三个元素。它们是 `SomeArray[0]`、`SomeArray[1]` 和 `SomeArray[2]`。更通地说，`SomeArray[n]` 有 n 个元素，编号为从 `SomeArray[0]` 到 `SomeArray[n-1]`。

因此，`LongArray[25]` 的编号从 `LongArray[0]` 到 `LongArray[24]`。列表 12.1 显示了如何声明一个五个整数的数组并为每个元素填充值。

### 列表 12.1 使用整数数组

```cpp
1: //列表 12.1 - 数组
2: #include <iostream.h>
3:
4: int main()
5: {
6: int myArray[5];
7: int i;
8: for (int i=0; i<5; i++) // 0-4
9: {
10: cout << "Value for myArray[" << i << "]:";
11: cin >> myArray[i];
12: }
13: for (i = 0; i<5; i++) {
14: cout << i << ": " << myArray[i] << "\n";
15: return 0;
16: }
```

| Value for myArray[0]: | 3 |
| :--- | :--- |
| Value for myArray[1]: | 6 |
| Value for myArray[2]: | 9 |
| Value for myArray[3]: | 12 |
| Value for myArray[4]: | 15 |
| 0: | 3 |
| 1: | 6 |
| 2: | 9 |
| 3: | 12 |
| 4: | 15 |

第 6 行声明了一个名为 `myArray` 的数组，它包含五个整数变量。第 8 行建立了一个从 0 计数到 4 的循环，这是五个元素的正确偏移量。用户被提示输入值，该值被保存到数组正确的偏移量处。

第一个值保存在 `myArray[0]`，第二个保存在 `myArray[1]`，依此类推。第二个 for 循环将每个值打印到屏幕上。

> 数组从 0 开始，而不是从 1 开始。这是 C++ 初学者编写的程序中出现许多错误的原因。每当你使用数组时，记住一个包含 10 个元素的数组是从 `ArrayName[0]` 计数到 `ArrayName[9]`。`ArrayName[10]` 不被使用。

### 写入数组末尾

当你向数组中的元素写入一个值时，编译器根据每个元素的大小和下标来计算位置。假设你向 `LongArray[5]` 写入值，这是第六个元素。编译器将偏移量（5）乘以每个元素的大小——在本例中为 4。从数组开始移动相应的字节数并在该处写入。记住下标和偏移量是同义词。如果你向 `LongArray[5]` 写入，编译器会忽略该元素不存在的事实。它计算出应该的位置（20 字节），然后写入任意数据。其结果可能是不可预测的。如果你运气好，程序会崩溃。否则，你将得到奇怪的结果并很难找出问题所在。在 Linux 等健壮的系统中，崩溃不会影响系统。

### 列表 12.2 写入数组末尾

```cpp
1: //列表 12.2
2: // 展示了越界写入数组时会发生什么
3: // 数组
4:
5: #include <iostream.h>
6: int main()
7: {
8:     // 哨兵节点
9:     long sentinelOne[3];
10:    long targetArray[25]; // 要填充的数组
11:    long sentinelTwo[3];
12:    int i;
13:    for (i=0; i<3; i++)
14:        sentinelOne[i] = sentinelTwo[i] = 0;
15:
16: for (i=0; i<25; i++)
17:     targetArray[i] = 0;
18: cout << "Test 1: \n"; // 当前值（应为 0）
19: cout << "targetArray[0]: " << targetArray[0] << "\n";
20: cout << "targetArray[24]: " << targetArray[24] << "\n";
21:
22: for (i = 0; i<3; i++)
23: {
24:     cout << "sentinelOne[" << i << "]:";
25:     cout << sentinelOne[i] << "\n";
26:     cout << "sentinelTwo[" << i << "]:";
27:     cout << sentinelTwo[i] << "\n";
28: }
29:
30: cout << "\nAssigning...";
31: for (i = 0; i<=25; i++)
32:     targetArray[i] = 20;
33:
34: cout << "Test 2: \n";
35: cout << "targetArray[0]: " << targetArray[0] << "\n";
36: cout << "targetArray[24]: " << targetArray[24] << "\n";
37: cout << "targetArray[25]: " << targetArray[25] << "\n\n";
38:
39: for (i = 0; i<3; i++)
40: {
41:     cout << "sentinelOne[" << i << "]:";
42:     cout << sentinelOne[i] << "\n";
43:     cout << "sentinelTwo[" << i << "]:";
44:     cout << sentinelTwo[i] << "\n";
45: }
46:
47: return 0;
}
```

Test 1:
targetArray[0]: 0
targetArray[24]: 0

SentinelOne[0]: 0
SentinelTwo[0]: 0
SentinelOne[1]: 0
SentinelTwo[1]: 0
SentinelOne[2]: 0
SentinelTwo[2]: 0

Assigning...
Test 2:
targetArray[0]: 20
targetArray[24]: 20
targetArray[25]: 20

SentinelOne[0]: 20
SentinelTwo[0]: 0
SentinelOne[1]: 0
SentinelTwo[1]: 0
SentinelOne[2]: 0
SentinelTwo[2]: 0

第 9 行和第 11 行声明了两个初始化为值 0 的整数数组。如果写入内存的位置超过了 `targetArray` 的末尾，哨兵节点很可能会被改变。有些编译器在内存中向下计数；另一些则向上计数。由于这个原因，哨兵节点被放置在 `targetArray` 的两侧。

第 19-24 行确认了 Test 1 中的哨兵值。在第 33 行，`targetArray` 的成员都被初始化为 20，但计数器一直到了 25，这在 `targetArray` 中是不存在的。

这种顽恶的错误可能很难发现，因为 `SentinelOne[0]` 的值是在一段完全没有写入 `SentinelOne` 的代码中被改变的。在少数情况下，恶意程序可能会影响系统——主要是当它以 root 权限运行时。

列表 12.2 显示了写入数组末尾时会发生什么。

不要运行此程序；可能会导致非 Linux 系统崩溃！

### 栅栏柱错误（Fence Post Errors）

因为越界写入数组末尾是非常常见的，这种错误有自己的名字。它被称为“栅栏柱错误”。这指的是对于一个 10 英尺长的栅栏，如果每英尺需要一根柱，那么需要多少根柱的问题。大多数人的回答是 10，但你显然需要 11 根。图 12.2 这一点清晰可见。

### 数组、C字符串与链表

#### 图 12.2
栅栏柱错误（Fence post errors）。

![](img/a66ce94ee9cc26e5c70f5604bcd3600c_404_0.png)

> 有些程序员将 `ArrayName[0]` 称为第零元素。养成这种习惯是一个巨大的错误。如果 `ArrayName[0]` 是第零元素，那么 `ArrayName[1]` 是什么？第十？如果是如果是，当你看到 `ArrayName[24]` 时，你会发现它不是第 24 个元素，而是第 25 个？最好说 `ArrayName[0]` 位于偏移量零处是第一个元素。

注意：偏移量零和第一个元素——描述同一位置的不同数字。务必不要在脑海中混淆两者。

### 初始化数组

当你第一次声明数组时，可以初始化一个由内置类型（如整数和字符）组成的简单数组。在数组名之后，放入一个等号 (=) 和一组用大括号括起来的逗号分隔的值列表。例如，

```cpp
int IntegerArray[5] = { 10, 20, 30, 40, 50 };
```

声明 `IntegerArray` 为一个包含五个整数的数组。它将 `IntegerArray[0]` 赋值为 10，将 `IntegerArray[1]` 赋值为 20，以此类推。

如果你省略了数组的大小，将创建一个刚好容纳初始化项的数组。因此，如果你写成

```cpp
int IntegerArray[] = { 10, 20, 30, 40, 50 };
```

你将创建一个与上一个示例相同的数组。

如果你需要知道数组的大小，可以请求编译器进行计算。例如，

```cpp
const UShort IntegerArrayLength = sizeof(IntegerArray)/sizeof(IntegerArray[0]);
```

这会将 `UShort` 变量 `IntegerArrayLength` 设置为将整个数组的大小除以数组中每个条目的大小后得到的结果。该商就是数组中成员的数量。

你不能初始化的元素超过你为数组声明的数量。因此，

```cpp
int IntegerArray[5] = { 10, 20, 30, 40, 50, 60 };
```

将产生编译器错误，因为你声明了一个五个成员的数组却初始化了六个值。然而，以下操作是合法的：

```cpp
int IntegerArray[5] = { 10, 20 };
```

虽然未初始化的数组成员没有确定的值，但聚合类型将会被初始化为 0。因此，如果你没有初始化数组成员，其值将被设置为 0。

| 做法 | 不要这么做 |
|---|---|
| 让编译器设置初始化数组的大小。 | 不要手动写数组的末尾。 |
| 给数组赋予有意义的名字，就像对待任何变量一样。 | |
| 记住数组的第一个成员位于偏移量 0。 | |

### 声明数组

数组可以使用任何合法的变量名，但它们不能与其作用范围内的另一个变量或数组重名。因此，你不能同时拥有名为 `myCats[5]` 的数组和一个名为 `myCats` 的变量。

你可以使用 `const` 或枚举来规定数组尺寸。列表 12.3 阐述了这一点。

### 列表 12.3 在数组中使用 const 和 enum

```cpp
1: // Listing 12.3
2: // 使用 const 和枚举规定数组尺寸
3:
4: #include <iostream>
5: int main()
6: {
7: enum WeekDays { Sun, Mon, Tue,
8: Wed, Thu, Fri, Sat, DaysInWeek };
9: int Array[DaysInWeek] = { 10, 20, 30, 40, 50, 60, 70 };
10:
11: cout << "The value at Tuesday is: " << Array[Tue];
12: return 0;
13: }
```
