

## 清单 23.1（续）

```cpp
iarray[20] = 50;
int* ip = find(iarray, iarray + SIZE, 50);
if (ip == iarray + SIZE)
    cout << "50 not found in array" << endl;
else
    cout << *ip << " found in array" << endl;
return 0;
}
```

在包含了 I/O 流和 STL 算法的头文件后（注意 algorithm 没有常见的 .h 后缀），示例程序告诉编译器使用 std 命名空间。这是可选的，由于在这样一个小程序中不太可能发生名称冲突，你可以删除这一行。

为了提供数据结构，程序使用常量 SIZE 定义了一个全局整数数组。因为它是全局变量，数组在运行时会被自动初始化为全零值。下面的语句使用 STL 的 find() 算法来搜索插入到索引 20 处的值 50：

```cpp
iarray[20] = 50;
int* ip = find(iarray, iarray + SIZE, 50);
```

对于 find()，程序传递了三个参数，这些参数的类型在许多 STL 算法中都很典型。前两个参数是迭代器，定义了要搜索的值范围。由于 C 和 C++ 数组等价于指针，表达式 iarray 指向数组中的第一个值。同样，第二个参数 iarray + SIZE 等于尾后值——在本例中，即数组中最后一个对象之后的一个元素。第三个参数是要定位的值，在本例中是 50。find() 算法返回与其前两个参数类型相同的迭代器，在本例中是一个整数指针，测试程序将其赋给 ip。

### 提示

> 请记住，STL 使用模板。因此，STL 算法会根据它们所使用的数据类型自动调整自身。

为了确定 find() 是否成功，示例程序使用以下语句将 ip 与尾后值进行比较：`if (ip == iarray + SIZE) ...`

如果表达式为真，则迭代器等于尾后值。由于该值不指向任何有效对象，这意味着搜索参数不在指定范围内。但如果 ip 不等于尾后值，则它指向一个有效对象，因此可以安全地使用表达式 *ip 解引用该指针，如输出语句所示：`cout << *ip << " found in array" << endl;`

务必记住，测试算法返回的迭代器是否等于 NULL 是不正确的。不要使用这样的代码：

```cpp
int* ip = find(iarray, iarray + SIZE, 50);
if (ip != NULL) ... // ??? incorrect
```

使用 STL 算法时，只需测试 `ip` 是否等于尾后值，无论该值对于特定容器而言是什么。虽然在本例中它是一个 C++ 指针，但其使用必须符合 STL 迭代器的规则。本章及接下来两章中的其他简单清单提供了具体示例，说明如何正确使用多种不同类型的迭代器。

## 容器迭代器

尽管如上一节所示，C++ 指针就是迭代器，但更常见的做法是使用容器类导出的迭代器。这些类型的迭代器的使用方式与 `iterdemo.cpp` 中完全相同，但你可以不将迭代器声明为指针变量，而是调用容器函数来获得一个迭代器对象，用于 `find()` 等算法。两个典型的容器函数是 `begin()` 和 `end()`。在大多数类型的容器中，它们表示对象的完整范围。有些容器还通过 `rbegin()` 和 `rend()` 函数提供反向迭代器，用于以相反顺序指定对象范围。

为了演示容器迭代器，清单 23.2（vectdemo.cpp）创建了一个 `vector`——STL 中与 C++ 数组等价的容器——并使用迭代器在容器中搜索某个值。该程序是上一节中传统 C++ 程序 iterdemo.cpp 的 STL 等价版本。

```cpp
#include <iostream.h>
#include <algorithm>
#include <vector>

using namespace std;

vector<int> intVector(100);

void main()
{
    intVector[20] = 50;
    vector<int>::iterator intIter =
        find(intVector.begin(), intVector.end(), 50);
    if (intIter != intVector.end())
        cout << "Vector contains value " << intIter << endl;
    else
        cout << "Vector does not contain 50" << endl;
}
```

程序使用标准 vector 容器类模板定义了一个包含 100 个 int 值的 vector。这一语句为 int 类型的数据元素实例化了 vector 模板：

`vector<int> intVector(100);`

该语句还调用了 vector 类的构造函数，为 100 个指定类型的对象预留空间。（第 24 章“构建标准容器”详细解释了构造容器对象的方法。）

