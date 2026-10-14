

通过让 `accumulate()` 使用不同的函数对象，该算法可以对容器中的对象执行其他类型的数学运算。为了演示，示例程序计算了所有包含值的乘积——在本例中，等于 10 的阶乘。`accumulate()` 算法的参数略有不同：

```
long product =
    accumulate(v.begin(), v.end(), 1, multiplies<long>());
```

同样，`begin()` 和 `end()` 定义了容器中值的范围，结果被赋值给一个程序变量（`product`）。另外两个参数提供了一个起始值（`1`）和一个函数对象（`multiplies`）。在这种情况下，起始值必须为 1，因为我们要用容器中的对象与该值相乘。

> 注意
> 如前所述，根据你使用的 ANSI C++ 版本，`multiplies()` 可能被命名为 `times()`。

检查传递给 `accumulate()` 的函数对象的形式。在这个示例中，该语句为 `long` 类型构造了函数对象（使用 STL 的 `multiplies` 模板），并调用了该对象的 `operator()` 函数。

## 生成器函数对象

一种特别有用的函数对象类型称为生成器。这种函数具有记忆能力——也就是说，它能“记住”先前调用中的值。生成器函数的一个很好的例子是随机数生成器，它使用先前的值来计算随机序列中的下一个值。

传统的 C 程序员通常在函数调用之间使用静态或全局变量来保留值，从而编写生成器。这种方法的问题在于数据与其依赖的函数分离。使用类来封装函数的“记忆”是创建生成器函数的一种更干净且更不容易出错的方式。通过使用模板类，还可以将生成器应用于 STL 算法。

在查看完整示例之前，先观察一个简单的演示，它展示了使用函数生成器对象的基本技术。清单 23.9 `randfunc.cpp` 调用了 `random_shuffle()` 算法，你在本章前面的“随机访问迭代器”一节中已经见过它。该算法的一个变体可以调用一个函数来获取随机序列中的下一个数字。使用函数生成器对象，可以用自定义子例程替换算法的默认随机数生成器。

### 清单 23.9 randfunc.cpp

```
#include <iostream.h>
#include <stdlib.h>    // Need random(), srandom()
#include <time.h>      // Need time()
#include <algorithm>   // Need random_shuffle()
#include <vector>    // Need vector
#include <functional> // Need ptr_fun()

using namespace std;

// Data to randomize
int iarray[10] = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
vector<int> v(iarray, iarray + 10);

// Function prototypes
void Display(vector<int>& vr, const char *s);
unsigned int RandInt(const unsigned int n);

int main()
{
    srand(time(NULL)); // Seed random generator
    Display(v, "Before shuffle:");

    pointer_to_unary_function<unsigned int, unsigned int>*
    ptr_RandInt = ptr_fun(RandInt); // Pointer to RandInt()
    random_shuffle(v.begin(), v.end(), ptr_RandInt);

    Display(v, "After shuffle:");
    return 0;
}

// Display contents of vector vr
void Display(vector<int>& vr, const char *s)
{
    cout << endl << s << endl;
    copy(vr.begin(), vr.end(), ostream_iterator<int>(cout, " "));
    cout << endl;
}

// Return next random value in sequence modulo n
unsigned int RandInt(const unsigned int n)
{
    return random() % n;
}
```

编译并运行该程序，它会显示 `random_shuffle()` 算法应用于一个小整数数组前后的效果。输入以下命令：

```
$ g++ randfunc.cpp
$ ./a.out
Before shuffle:
1 2 3 4 5 6 7 8 9 10
After shuffle:
6 7 2 8 3 5 10 1 9 4
```

对于其随机数生成器，测试程序声明了一个返回 `unsigned int` 值的函数原型：

```
unsigned int RandInt(unsigned int n);
```

按照这里的编程方式，`RandInt()` 返回一个从 0 到 n-1 随机选择的值。程序定义了一个整数数组，并用它初始化一个向量 `v`：

```
int iarray[10] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
vector<int> v(iarray, iarray + 10);
```

现在，打乱向量中的值只需调用 `random_shuffle()` 算法即可。然而，由于 STL 中的一个怪癖，直接将 `RandInt()` 函数传递给 `random_shuffle()` 而不收到编译器警告是不可能的。为防止警告，首先使用以下语句定义一个指向该函数的指针：

```
pointer_to_unary_function<unsigned int, unsigned int>
ptr_RandInt = ptr_fun(RandInt);
```

这条略显冗长的语句使用 STL 的 `pointer_to_unary_function` 模板定义了一个变量（此处命名为 `ptr_RandInt`），并初始化为我们程序中 `RandInt()` 函数的地址。一元函数声明一个参数并返回一个值，在本例中两者都是 `unsigned int` 类型，如尖括号中所示。有了指向函数的指针，程序现在可以使用以下语句调用 `random_shuffle()`：

```
random_shuffle(v.begin(), v.end(), ptr_RandInt);
```

像往常一样，`begin()` 和 `end()` 定义了要操作的值范围。将函数指针传递给算法会使其调用该函数来获取一个用于打乱容器内容的随机值。在这个简单示例中，生成器仅调用标准 C 库的 `random()` 函数：

```
unsigned int RandInt(unsigned int n)
{
    return random() % n;
}
```

### 常量引用的麻烦

在清单 23.9 `randfunc.cpp` 中，将 STL 的 `ptr_fun` 对象直接传递给 `random_shuffle()` 以及类似的需要指向一元函数（一个参数和一个返回值）或二元函数（两个参数和一个返回值）指针的算法应该是可能的。然而，`ptr_fun()` 会生成对其中一种函数类型的常量引用，但 `random_shuffle()` 被编写为接收非常量参数。以下代码本应有效，但会产生编译器警告：

```
random_shuffle(v.begin(), v.end(), ptr_fun(RandInt));
```

表达式 `ptr_fun(RandInt)` 应该生成一个对 `RandInt()` 函数的引用，该引用对 `random_shuffle()` 是可接受的。然而，这条语句会导致编译器发出冗长的警告，其中部分内容为“从右值初始化非常量引用……”以及一堆令人困惑的模板实例化。尽管看起来复杂，这实际上是一个简单的问题——它是由 `ptr_fun()` 生成一个常量引用（被标识为“右值”，即赋值语句中等号右侧可能出现的对象）引起的。

