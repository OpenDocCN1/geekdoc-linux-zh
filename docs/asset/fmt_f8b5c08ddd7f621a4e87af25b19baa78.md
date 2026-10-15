
`vector a` 包含这 10 个整数值。`vector b` 被定义为一个具有 10 个可能值的容器。一条简单的语句将对象从容器 `a` 复制到 `b`：

```cpp
copy(a.begin(), a.end(), b.begin());
```

你也可以将最终迭代器保存在容器类导出的迭代器类型的变量中：

```cpp
vector<int>::iterator end =
    copy(a.begin(), a.end(), b.begin());
```

执行该语句后，`b.begin()` 和 `end` 定义了目标容器中被复制数据的范围。要按相反方向复制对象，请按如下方式使用 `copy_backward()`：

```cpp
copy_backward(a.begin(), a.end(), b.end());
```

请注意按正确顺序指定迭代器。`first` 和 `last` 迭代器按正向顺序定义源值的范围，但起始迭代器位于目标容器（`b`）的末尾。同样，你可以将生成的迭代器保存在变量中：

```cpp
vector<int>::iterator start =
    copy_backward(a.begin(), a.end(), b.end());
```

执行该语句后，`start` 和 `b.end()` 定义了被复制对象的范围。

> 提示
> 在大多数情况下，请使用 `copy()`，除非你在同一容器中复制对象，在这种情况下，可能需要使用 `copy_backward()` 来防止在复制过程中覆盖对象。

你还可以使用 `copy()` 将对象传输到输出流对象。这并非特殊情况，而是展示了 STL 在定义容器本质方面的多样性。例如，像 `cout` 这样的输出对象就是一个“容器”，你可以将对象复制到其中。所需的一切只是一个合适的迭代器，比如 STL 中定义的 `ostream_iterator`。以下语句使用 `copy()` 算法将向量容器中的所有值传输到标准输出对象 `cout`，并用空格分隔每个值：

```cpp
copy(b.begin(), b.end(),
     ostream_iterator<int>(cout, " "));
```

> **提示**
> 
> 要为你自己的输入或输出流迭代器定义类，请检查 STL 源文件 `iterator.h`，并以 `ostream_iterator` 或 `istream_iterator` 模板类作为设计基础。

## 计数算法

*算法：*

`count()`
`count_if()`

*示例程序：*

`count-ex.cpp`

使用 `count()` 和 `count_if()` 算法来确定容器中具有指定值或满足其他条件的对象数量。`count()` 算法需要两个输入迭代器：一个要搜索的常量值和一个用于保存结果计数的整数变量。该算法定义如下：

```cpp
void count(
    InputIterator first, InputIterator last,
    const DataType& value, Size& n)
```

前两个参数（与许多算法一样）是定义要检查对象范围的迭代器。`DataType` 引用值是要与每个对象进行比较的值。对于找到的每个匹配值，`count()` 都会递增 `Size` 引用 `n`。（我不知道为什么这个变量的类型被称为 `Size`。将其称为 `CounterType` 或类似的名称会更接近其用途。）

示例程序定义了一个整数向量，并使用以下语句将其设置为随机选择的值：

```cpp
vector<int> a(100);
srandom(time(NULL));  // Seed random generator
for (int i = 0; i < 100; i++)
    a[i] = random() % 100;
```

随后，一个 for 循环调用 `count()` 来查找数组中重复次数最多的值：

```cpp
for (int i = 0; i < 100; i++) {
    int v = *(a.begin() + i);
    int k = 0;
    count(a.begin(), a.end(), v, k);
    if (k > sum) {
        sum = k;        // Save current maximum sum
        value = v;      // Save associated search value
    }
}
```

循环中的第一条语句将向量数组中的每个连续值赋给 `v`。变量 `k`（`count()` 为每个匹配值递增）被初始化为零。对向量数组中的所有值调用 `count()`，并传递搜索参数 `v` 和计数器变量 `k`，即可定位所有重复值。这两个参数保存在其他地方声明的变量 `sum` 和 `value` 中，以供稍后显示。

另一个计数算法 `count_if()` 计算满足布尔谓词函数的指定值的数量。这种更通用的计数算法可以计算满足任何可想象条件的任何类型的值。`count_if()` 算法定义如下：

```cpp
void count_if(
    InputIterator first, InputIterator last,
    Predicate pred, Size n)
```

与 `count()` 一样，前两个参数是定义要搜索对象范围的迭代器。`Predicate`（`pred`）参数是一个布尔谓词函数（参见第23章“使用标准模板库（STL）”中“函数和函数对象”一节）。在大多数情况下，你会按照以下方式创建谓词函数：

```cpp
#include <functional>
...
template<class Arg>
class is_even : public unary_function<Arg, bool>
{
public:
    bool operator()(const Arg& arg1) {
        return (arg1 % 2) == 0;
    }
};
```

包含 `functional` 头文件，然后创建一个派生自 STL `unary_function` 模板的模板类。`Arg` 是与要搜索的容器中数据类型相同的占位符。谓词函数只需要一个重载运算符——`operator()`，它允许类的对象像函数名一样被调用。该函数的唯一参数是对容器中对象类型的常量引用。该函数根据对参数 `arg1` 的求值返回 `true` 或 `false` 布尔值。在本例中，如果值为偶数，则函数返回 `true`。类名 `is_even` 反映了函数的目的。

使用谓词函数，如示例程序语句所示，该语句统计向量数组中有多少个偶数值：

```cpp
count_if(a.begin(), a.end(), is_even<int>(), numEvens);
```

在两个迭代器之后，创建并调用函数对象。`count_if()` 算法将函数对象应用于指定范围内的每个值，并对每次匹配递增最终参数 `numEvens`。请务必在调用 `count_if()` 之前初始化此变量。

## FILLING ALGORITHMS

**Algorithms:**

- `fill()`
- `fill_n()`

**Sample program:** `fill-ex.cpp`

使用 `fill()` 和 `fill_n()` 算法向容器中填充值，或初始化非空数据结构。`fill()` 算法需要两个迭代器和一个要复制到定义范围中每个对象的值。该算法定义如下：

```cpp
void fill(
    ForwardIterator first, ForwardIterator last,
    const T& value)
```

另一个算法 `fill_n()` 与 `fill()` 工作方式相同，但只需要一个指定填充开始位置的迭代器。其他参数指定要从该位置填充的值的个数（`n`）以及要复制到该范围内每个值的值。该算法定义如下：

```cpp
OutputIterator fill_n(
    OutputIterator first,
    Size n, const T& value)
```

与返回 `void` 的 `fill()` 不同，`fill_n()` 返回一个输出迭代器，其值等于最后一个对象位置加一。因此，在调用 `fill_n()` 之后，第一个迭代器和函数结果定义了用指定值填充的对象范围。

为了演示如何使用 `fill()` 和 `fill_n()`，示例程序用以下语句定义并初始化一个向量：

```cpp
int data[10] = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
vector<int> a(data, data + 10);
```

要将值 2 到 9 替换为 99，程序执行以下语句：

```cpp
fill(a.begin() + 1, a.end() - 1, 99);
```
