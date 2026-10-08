

## 访问修饰符

有两种访问修饰符用于控制变量被访问和修改的方式。第一种是 *const*，它也是 C 语言的一部分。第二种是 *volatile*，仅存在于 C++ 中。

当变量使用 *const* 修饰符声明时，它们的值在程序执行期间不能被修改。例如：

```cpp
const int hours_in_day = 24;
```

这创建了一个名为 *hours_in_day* 的整型变量，其值为 24。该值在程序执行期间不能被修改。

*volatile* 修饰符告诉编译器，变量的值可能被外部进程异步修改。此修饰符的意图是禁止编译器对该变量进行优化。编译器可能会通过引用该变量之前加载的值来减少开销从而进行优化。*volatile* 修饰符强制在每次使用变量时都重新获取其值。

例如，如果一个名为 *time* 的变量需要由计算机的时钟机制每秒更新一次，编译器不应复用之前获取的值。必须从计算机的时钟机制获取一个新值。变量 *time* 需要声明为：

```cpp
volatile int time;
```

这将确保变量 *time* 在每次被引用时都会被赋予一个新值。

## 动态内存分配

C++ 有两个用于动态内存分配的新运算符：`new` 和 `delete`。`new` 分配内存，`delete` 释放或分配给由 `new` 分配的内存。格式如下：

```cpp
pointer_variable = new data_type;
delete pointer_variable;
```

`pointer_variable` 是类型为 `data_type` 的指针。`new` 运算符分配足以容纳一个 `data_type` 类型值的内存，并返回指向该内存的指针。

`delete` 运算符释放 `pointer_variable` 所指向的内存。

使用 `new` 运算符时，可以通过在 `data_type` 之后的括号内指定值来初始化内存。例如：

```cpp
#include <iostream>
using namespace std;
int main()
{
    int *num_ptr;
    num_ptr = new int (346); // 初始化为 346
    if (!num_ptr)
    {
        cout << "Memory allocation failure.\n";
        return 1;
    }
    cout << "Memory was successfully allocated for num_ptr containing " << *num_ptr;
    delete num_ptr; // 清理内存
    return 0;
}
```

数组也可以使用 `new` 进行分配。要分配一维数组：

```cpp
pointer_variable = new variable_type[size];
```

Size 指的是数组中元素的数量。要释放动态分配的数组，请使用：

```cpp
delete []pointer_variable;
```

## 函数重载

函数重载是 C++ 的一项特性，允许两个或更多函数共享相同的名称，只要它们的参数声明不同即可。当函数共享相同名称时，它们被称为 *overloaded*（被重载的）。函数重载是 C++ 实现多态性的一种方式。

考虑以下程序：

```cpp
// 将函数重载三次

#include <iostream>
using namespace std;
void print_values( int x );// 函数原型 - 整型参数
void print_values( int x, int y);// 两个整型参数
void print_values(double z );// 双精度参数

int main()
{
    print_values(346);
    print_values(3, 346);
    print_values(10.25);
    return 0;
}

void print_values(int x )
{
    cout << "The value is " << x;
}

void print_values(int x, int y)
{
    cout << "The value is " << x << " and " << y;
}

void print_values(double z)
{
    cout << "The value is " << z;
}
```

`print_values()` 函数被重载了三次，使该函数能够接受三个不同的参数列表。

函数重载旨在用于紧密相关的操作。例如，重载名为 `square()` 的函数，一次用于整数的平方，另一次用于浮点数的平方根，这并不是好的编程实践。重载函数的变体之间并不紧密相关。如果 `square()` 函数接受一个整数并将其平方，并重载该函数以接受一个浮点数并将其平方，那么这种情况下的操作就是紧密相关的，并且重载是有意义的。

## 默认函数参数

如果调用函数时没有提供对应的值，C++ 允许参数具有默认值。例如，如果函数在参数列表中用一个整数和一个字符被调用，这些值中的每一个都可以被赋予默认值：

```cpp
void price_widgets(int num_widgets = 1, char widget_type = 'A')
{
    // 对 widgets 进行定价的代码
    ...
}
```

然后可以通过以下方式调用该函数：

```cpp
price_widgets( 3, 'D' ); // 向所有参数传递值
price_widgets( 7 ); // 传入 widget 的数量，
                 // 但使用 widget 类型的默认值
price_widgets(); // 两个参数都使用默认值
```

第一个函数调用向所有参数传递值。由于第二个函数调用没有提供 `widget_type` 的值，因此使用默认值 `A`。在第三个函数调用中，两个参数均未传递；使用 widget 数量的默认值 1 和 widget 类型的默认值 `A`。

## 类

类是 C++ 支持面向对象编程的基础。它允许程序以对象的形式编写。

关键字 `class` 用于定义新的数据类型，即一种可用于创建对象的数据类型。类定义了数据以及操作这些数据代码。将对象内部的数据成员和操作用于数据的函数打包在一起被称为 *encapsulation*（封装）。

当声明一个类时，会创建一个对象。对象是占据内存空间的物理存在，是类的实例。类的每个对象都有类中定义的数据的自己的副本。类声明的格式如下：

```cpp
class class_name {
    private data and functions
public:
    public data and functions
} object_list;
```

私有数据和函数只能被类内部的函数使用。任何私有数据和函数都是不可访问的，并受到来自外部干扰的保护。这种保护被称为数据隐藏。

如果一个程序管理银行账户，账户中的数据需要受到保护，以防止程序的其他部分尝试直接访问或更改账户余额。类通过将账户余额声明为私有来提供这种保护。一个类的示例可能如下：

```cpp
// 这创建一个银行账户类

class bank_acct {
    double acct_balance;
public:
    void init();
    double retrieve_balance();
    void update_balance();
    ...
};
```

默认情况下，类中的所有项都是私有的。在这个类中，`acct_balance` 是私有的，只能被 `bank_acct` 类的其他成员访问。在 `public` 说明符之后定义的所有项都可以被程序中的任何其他函数访问。通常，程序通过类的公共函数访问类内的私有项。函数 `init()`、`retrieve_balance()` 和 `update_balance()` 被称为成员函数，构成了公共接口。由于成员函数的原型位于类定义内部，因此不需要在其他地方进行原型声明。

在定义类之后，可以使用类名创建该类型的对象。类名成为一种新的数据类型说明符。要创建两个对象 `checking` 和 `savings`，使用以下语句：

```cpp
bank_acct checking, savings;
```

为了实现像 `retrieve_balance()` 这样的成员函数，必须通过用类名限定函数名来告诉编译器该函数属于哪个类。`retrieve_balance()` 函数的源代码如下：

```cpp
double bank_acct::retrieve_balance()
{
    return( acct_balance );
}
```

`::` 符号是范围解析运算符。这告诉编译器，此版本的函数 `retrieve_balance()` 属于类 `bank_acct`。

要从不是类一部分的程序部分调用成员函数，必须使用对象名和点运算符。以下是对对象 `checking` 的 `retrieve_balance()` 函数的调用：

