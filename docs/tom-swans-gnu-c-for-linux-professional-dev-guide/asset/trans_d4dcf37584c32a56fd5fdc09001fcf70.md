
作为一种模板，`find()` 算法并不针对特定数据类型，而是使用占位符来表示使用模板时提供的实际数据类型。其中一个占位符名为 `InputIterator`。这种迭代器可以是任何具备某些能力的对象类型，例如可以使用 `!=` 运算符进行比较、可以通过 `++` 递增。另一个占位符名为 `T`，表示容器中数据的类型。

> 提示
> 不必在 STL 源文件中查找 `InputIterator` 的类型声明。这只是一个任意名称，并非已定义的类型；当 `find()` 模板函数被实例化时，它才会成为真实类型。

`find()` 算法声明了三个参数。前两个是 `InputIterator` 类型的迭代器，名为 `first` 和 `last`。第三个参数是 `T` 类型对象的常量引用，此处名为 `value`。`find()` 算法的语句展示了如何使用模板占位符替代真实数据类型，在完全不了解被搜索数据类型的情况下，编写出一个完全通用的搜索函数。请仔细查看该算法的 `while` 语句：

```
while (first != last && *first != value) ++first;
```

该语句在第一个迭代器不等于 last，且 first 所指向的值不等于搜索参数时执行。只要这个条件不成立，循环就会递增 `first`。该算法完全通用，可以搜索任何类型的容器，例如 list、vector 或数组。

搜索结束后，`first` 要么指向等于搜索参数的对象，要么等于 `last`，在后一种情况下表示搜索失败。`find()` 算法直接返回该值。

> 注意
> 在上述 `find()` 算法中，请注意：如果找不到搜索参数，那么不断递增 `first` 最终必须使其等于 `last`。如果 `first` 和 `last` 指向不同容器中的值，则该算法可能永远不会结束。虽然编译器不会阻止这种情况，但只要合理使用，这通常不会造成任何问题。

## 输出迭代器

输出迭代器默认只写，通常用于将数据从一个位置复制到另一个位置。由于输出迭代器不能用于读取对象，因此永远不会在搜索或其他类型的算法中使用它们。例如，`copy()` 算法可以通过输出迭代器指定目标位置，将对象从一个数据结构传输到另一个数据结构。但是，该迭代器不能用于读取被复制的值。为此，需要另一个输入迭代器（或其派生类型）。

为了演示如何使用输出迭代器，清单 23.3（outiter.cpp）使用 `copy()` 算法将一组 double 值数组传输到 vector 容器中。你可能会使用类似的技术，将使用数组的传统 C 程序升级为使用 STL 容器类的程序。（所演示的技术也可用于为测试程序初始化容器，例如本章及接下来两章中的测试程序。）

### 清单 23.3 OUTITER.CPP

```cpp
#include <iostream.h>
#include <algorithm>  // Need copy()
#include <vector>     // Need vector

using namespace std;

double darray[10] =
    {1.0, 1.1, 1.2, 1.3, 1.4, 1.5, 1.6, 1.7, 1.8, 1.9};

vector<double> vdouble(10);

int main()
{
    vector<double>::iterator outputIterator = vdouble.begin();
    copy(darray, darray + 10, outputIterator);
    while (outputIterator != vdouble.end()) {
        cout << *outputIterator << endl;
        outputIterator++;
    }
    return 0;
}
```

编译并运行该程序，它使用 `copy()` 算法显示得到的 double 值 vector：

```text
$ g++ outiter.cpp
$ ./a.out
1
1.1
...
1.9
```

该程序定义了一个包含 10 个 double 值的普通数组，初始化为 1.0、1.1、……、1.9。它还定义了一个足以容纳 10 个值的 `vector<double>` 容器。`main()` 中的第一条语句声明并初始化了该 vector 的一个名为 `outputIterator` 的迭代器。为了让它指向容器的第一个对象，该语句将容器 `vdouble` 的 `begin()` 函数结果赋给 `outputIterator`。将该迭代器传递给 `copy()` 算法，即可将值从普通数组传输到 vector 容器：

```
copy(darray, darray + 10, outputIterator);
```

前两个参数定义了要复制的源值范围。在本例中，迭代器是指向全局 `darray` 的指针。第三个参数是一个输出迭代器，它定义了对象传输目标位置的起点。你可能想知道这条语句如何“知道”要复制的对象类型，其实这些信息隐含在所涉及的迭代器类型中。像 `darray` 这样的指针以及 `darray + 10` 这样的指针表达式不仅仅是地址值——它们是带类型的指针，在本例中是指向 double 类型值的指针。同样，`outputIterator` 也“知道”它所属的容器类型。
