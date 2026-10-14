
从技术上讲，函数对象是重载了函数调用运算符 operator()() 的任何结构或类的实例。通过重载这个运算符，可以构造 TAnyClass 类型的对象，并以这种方式将其用作函数：
TAnyClass object; // Construct object
object(); // Calls TAnyClass::operator()() function

你大概不会编写这样的代码，但在使用标准算法时，能够像函数一样“调用”对象的重要性就体现出来了。例如，程序可以通过如下方式将 object 传递给 for_each() 处理向量 v：
for_each(v.begin(), v.end(), object);

这将对容器中的每个值，针对定义的对象执行 TAnyClass::operator()() 函数。该对象可以定义静态变量，统计被调用的次数，或者根据 for_each() 从容器中传入的值执行各种其他任务。

STL 定义了几个对值执行数学运算的函数对象。由于它们是模板，因此可以处理任何类型的值，包括 long 和 double 等旧标准类型，也可以处理你自己重载了数学运算符的类。其中一些函数名称很直观，例如 plus() 和 multiplies()。类似地，比较函数对象如 greater() 和 less_equal() 用于比较两个值。

## 注意

> 某些 ANSI C++ 版本定义了一个 times() 函数对象。GNU C++ 将其命名为 multiplies()；不过，你可能会在 GNU 源文件中找到其中之一。关于其他函数对象的名称，请查看 function.h 头文件，它可能位于 /usr/include/g++ 中，并通过 #include<functional> 指令包含。

函数对象的一个有用示例是 accumulate() 算法。默认情况下，accumulate() 对容器中的值求和。请记住，这些值不一定是简单的——通过重载 operator+() 函数，这些值可以是类对象。然而，为了演示，清单 23.8（accum.cpp）使用 accumulate() 来对一组 long 整数求和。该程序还演示了如何教 accumulate() 使用函数对象来计算容器中值的乘积。

## 清单 23.8 ACCUM.CPP

```
#include <iostream.h>
#include <numeric> // Need accumulate()
#include <vector> // Need vector
#include <function.h> // Need multiplies() (or times())

#define MAX 10
vector<long> v(MAX); // Vector object

int main()
{
    // Fill vector using conventional loop
    //
    for (int i = 0; i < MAX; i++)
        v[i] = i + 1;

    // Accumulate the sum of contained values
    //
    long sum =
        accumulate(v.begin(), v.end(), 0);
    cout << "Sum of values == " << sum << endl;

    // Accumulate the product of contained values
    //
    long product =
        accumulate(v.begin(), v.end(), 1, multiplies<long>());
    cout << "Product of values == " << product << endl;

    return 0;
}
```

当你编译并运行该程序时，它会创建一个 long 整数的小型向量，初始化为值 1 到 10，然后显示这些值的和与乘积。输入以下命令以查看程序的输出：

```
$ g++ accum.cpp
$ ./a.out
Sum of values == 55
Product of values == 3628800
```

程序使用以下指令和语句定义一个包含 10 个 long 整数的向量：

```
#define MAX 10
vector<long> v(MAX);
```

然后，为了与众不同，main() 使用传统的 for 循环来初始化向量的值：

```
for (int i = 0; i < MAX; i++)
    v[i] = i + 1;
```

为了对向量 v 中的值求和，程序按如下方式调用 accumulate()，并将其结果赋值给 long 整数变量 sum：

```
long sum =
    accumulate(v.begin(), v.end(), 0);
```

和往常一样，begin() 和 end() 定义了向量中值的完整范围。第三个参数为累加提供初始值。在求和时，该初始值通常为零，如清单中所示。不过，它也可以是其他值。例如，后续语句可以将 sum 传递给 accumulate()，以计算两个或多个容器的累计总数。
