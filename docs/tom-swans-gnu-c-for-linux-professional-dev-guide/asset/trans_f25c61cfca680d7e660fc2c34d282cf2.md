
# 第17章
# 创建类模板

正如类是一种构建对象的蓝图，模板就是构建函数和类的蓝图。也称为参数化类型，模板为通用类和函数提供规范，这些类和函数能够自动适应新的用途。

> 注意
> 有关使用模板的更多信息，请参阅第23章“使用标准模板库（STL）”。

## 介绍类模板

模板通常用于创建通用函数和类，这些函数和类不绑定到任何特定数据类型。例如，排序函数就是一个很好的模板，因为排序算法不直接依赖于其操作的数据类型。将函数实现为模板可将其简化为最一般的形式。在编译程序时，C++ 使用模板生成或实例化一个实际的函数，该函数适用于特定类型的数据。

模板类同样具有通用性。一个极佳的例子是容器类，它提供搜索和其他功能，但可以处理从最基本的整数到复杂类对象等任何数据类型。

## 模板函数

模板函数描述了函数的通用属性。最常见的是，你将模板函数声明在单独的头文件中，并在各个模块中包含它们。模板函数通常如下所示：

```
template <class T>
void f(T param)
{
    // ... function body
}
```

保留字 template 开始声明，并且始终后跟包含一个或多个表达式的尖括号。在此示例中只有一个表达式——以单词 class 开始，后跟你选择的任何标识符。在本例中，我使用 T 表示“类型”。这里的单词 class 不一定指 C++ 类，而是指任何“类”数据类型。

模板的前言之后是正在以模板形式声明的项目。在此示例中，它是一个名为 f() 的函数，返回 void 并接收一个类型为 T 的单个参数。实际数据类型在程序使用模板时稍后指定——在此，T 只是指尚未定义类型的占位符。函数也可能返回占位符类型的值：

```
template <class FutureType>
FutureType AnyFunction(FutureType param)
{
    // ... function body
}
```

## 列表 17.1 MINMAX.H

```
#pragma interface

template <class T>
T max(T a, T b)
{
    if (a > b)
        return a;
    else
        return b;
}

template <class T>
T min(T a, T b)
{
    if (a < b)
        return a;
    else
        return b;
}
```

### 注意

minmax.h 中的 #pragma interface 指令可能不再需要。某些版本的 GNU C++ 需要它来帮助链接器解析模板函数和类的使用。

仔细查看模板函数 max() 的声明：

```
template <class T>
T max(T a, T b)
```

模板保留字首先出现，后跟包含占位符类型名 T 的尖括号。第二行将 max() 声明为返回类型为 T 的值并接收两个参数 a 和 b 的函数，a 和 b 也是类型 T。函数体是常见的 C++ 代码：

```
if (a > b)
    return a;
else
    return b;
```

a 和 b 的实际类型尚不为人知，我们仅假设这些类型的对象可以在表达式 (a < b) 中进行比较——如果不能，程序根本无法编译。模板函数 min() 也是类似编写的，但当然返回其两个参数中较小的值。

我们现在有两个函数 min() 和 max()，它们在本质上完全通用。它们可以操作任何数据类型，只要该类型对象可以进行比较。列表 17.2，tminmax.cpp，测试了这些函数并展示了如何为不同类型的数据实例化模板。

## 列表 17.2 TMIMAX.CPP

```
#include <iostream.h>

#pragma implementation "minmax.h"
#include "minmax.h"

// Instantiate template functions //
template int min(int, int);
template double min(double, double);
template char min(char, char);

template int max(int, int);
template double max(double, double);
template char max(char, char);

int main()
{
    int i1 = 100, i2 = 200;
    double d1 = 3.14159, d2 = 9.87654;
    char c1 = 'A', c2 = 'Z';

    cout << "max(i1, i2) = " << max(i1, i2) << endl;
    cout << "max(d1, d2) = " << max(d1, d2) << endl;
    cout << "max(c1, c2) = " << max(c1, c2) << endl;

    cout << "min(i1, i2) = " << min(i1, i2) << endl;
    cout << "min(d1, d2) = " << min(d1, d2) << endl;
    cout << "min(c1, c2) = " << min(c1, c2) << endl;

    return 0;
}
```

### 注意

> tminmax.cpp 中的 #pragma implementation 指令可能不再需要。它对应于模板函数头文件 minmax.h 中包含在模块中的 #pragma interface 指令。虽然在这个小型示例中并非严格必需，但这些指令有助于确保从模板创建的函数只有一个实例。较新版本的 GNU C++ 不需要这两个指令。

测试程序包含 minmax.h 头文件。使用该文件中的模板函数，编译器显式实例化实际函数，使用诸如

```
template int min(int, int);
```

这样的模板原型。这会导致编译器在模板函数中出现的每个类 T 的位置实现一个名为 min() 且类型为 int 的函数。结果是一个实际函数，返回两个整数参数的最小值，就好像你像这样编写了该函数：

```
int max(int a, int b)
{
    if (a > b)
        return a;
```
