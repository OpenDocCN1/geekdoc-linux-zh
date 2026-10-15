
```
double f1;          // 声明简单变量
double f2 = 3.14159; // 声明并初始化变量
double f3(3.14159); // 同上
double f4(f3);      // 声明 f4 并用 f3 初始化
double f5 = f4;      // 声明 f5 为 f4 的拷贝
```

第一个声明声明了一个名为 `f1` 的 `double` 类型变量。如果此声明是全局的，`f1` 将初始化为零。如果声明是局部于一个函数，`f1` 未初始化。第二个声明将一个字面值初始化到另一个 `double` 变量 `f2`。正如你可能知道的，这里显示的前两个声明是创建原生 C++ 类型简单变量最常见的方式，你在之前的章节中已经看到了这些技术的众多示例。

第三个声明将 `f3` 初始化为字面值 3.14159。第二和第三个声明在功能上是相同的，但前者更常见。第四个声明

创建 `t4`，并将 `t3` 的值复制到新变量中。第五个声明将 `t5` 声明为 `t4` 的副本。最后两个声明在功能上是相同的。

你可以用几乎相同的语句以这些相同的方式构造类对象。清单 12.3（`construct.cpp`）演示了构造一个稍作修改的 `TDate` 类类对象的五种方式。

## 清单 12.3 CONSTRUCT.CPP

```
#include <iostream.h>

// A class that encapsulates data and functions
class TDate {
private:
    int dt_month;
    int dt_day;
    int dt_year;
public:
    TDate();
    TDate(int month, int day, int year);
    void Display();
};

int main()
{
    TDate t1;                 // Requires default constructor
    TDate t2 = TDate(12, 31, 1999);  // Impractical, but allowed
    TDate t3(1, 1, 2000);     // Uses parameterized constructor
    TDate t4(t3);             // Makes t4 a copy of t3
    TDate t5 = t4;            // Copies t4 into t5

    t1.Display(); // Call member function for each object
    t2.Display();
    t3.Display();
    t4.Display();
    t5.Display();

    return 0;
}

// The TDate class default constructor
TDate::TDate()
{
    dt_month = 0;   // Initialize private data members to zero
    dt_day = 0;
    dt_year = 0;
}

// The TDate class parameterized constructor
TDate::TDate(int month, int day, int year)
{
    dt_month = month; // Assign values to private data members
    dt_day = day;
    dt_year = year;
}
```

```
// The TDate class Display member function
void TDate::Display()
{
 cout << dt_month << "/" << dt_day << "/" << dt_year << endl;
}
```

该程序构造了五个 `TDate` 对象 `t1` 到 `t5`，然后为每个对象调用 `Display()` 成员函数。下面的语句构造了一个名为 `t1` 的 `TDate` 类对象：

```
TDate t1;
```

这是构造类对象最常见的方式之一，其方法完全等同于声明任何其他类型的未初始化对象，例如 `double` 变量：

```
double f1;
```

但是，当类型是类时，它必须有一个默认构造函数来处理没有参数值声明的对象的创建。（本章后面“默认构造函数”一节将对此进行更多讨论。）

示例程序演示了构造对象的第二种但不切实际的方式。虽然你不太可能使用这种方法，但它演示了临时对象这一重要概念。这条语句：

```
TDate t2 = TDate(12, 31, 1999); // ???
```

大致等同于常见的传统语句：

```
double f2 = 3.14159;
```

这是创建和初始化 `double` 等简单类型对象的常见方式，但在使用类时，前面的 `TDate` 对象构造会使程序做比必要更多的工作。这是因为赋值运算符右侧的表达式创建了一个临时 `TDate` 对象，然后将其复制到一个新的 `TDate` 对象 `t2` 中。临时对象只在需要时存在，并且在其值被复制到 `t2` 后自动销毁。正如我在第 13 章“创建和销毁对象”中所解释的，临时对象很麻烦，并且可能导致错误。通常最好尽可能避免创建临时对象。

（它们也可以是相关类的对象，正如第 14 章“投资继承”所解释的那样。）下面的语句使用 `t3` 值的副本创建了一个名为 `t4` 的 `TDate` 对象：

`TDate t4( t3 );`

这会创建一个新对象 `t4`，并将 `t3` 的值复制到其中。该语句等同于下面的原生类型声明，后者创建一个 `double` 变量 `t4` 并将 `f3` 的值赋给它：

`double f4(f3);`

构造类对象的第五种也是最后一种方法也是将一个对象复制到另一个对象：

`TDate t5 = t4;`

这会创建一个新的 `TDate` 对象 `t5`，其值等于 `t4`。这与前一种方法完全相同，但使用了更直观的赋值运算符。它完全等同于原生类型语句：

`double f5 = f4;`

## 默认构造函数

默认构造函数没有参数，并且与所有构造函数一样，其名称与其类相同。在示例 `construct.cpp` 程序中，`TDate()` 默认构造函数单独实现如下（为了节省空间，我将各个语句移到了一行）：

```
TDate::TDate()
{
    dt_month = 0;  dt_day = 0;   dt_year = 0;
}
```

在程序的其他地方，用无参数创建对象会调用默认构造函数，该函数将对象中的每个数据成员赋值为零。默认的 `TDate()` 构造函数使诸如

`TDate t1;`

这样的声明成为可能。这会调用 `TDate()` 默认构造函数来初始化 `t1` 对象。然而，与原生类型变量不同，无论前面的声明是否在函数内部，这种情况都会发生——这是类对象声明与原生类型声明之间一个微妙但重要的区别。类对象总是由构造函数初始化。函数局部的原生类型变量在赋值之前是未初始化的。

## 复制构造函数

导致一个对象被复制到新创建对象的语句会调用一种特殊的构造函数，称为复制构造函数。当你使用如下语句创建对象时会发生这种情况（但请记住，第三个语句虽然允许，但不切实际，因为它会浪费地创建一个临时对象）：

```
TDate t4(t3);
TDate t5 = t4;
TDate t2 = TDate(12, 31, 1999);  // ???
```

复制构造函数的作用是将一个对象的值复制到一个新对象。通常，所需要做的只是将源对象的数据成员传递给目标对象；如果类没有显式声明复制构造函数，C++ 会自动生成一个来完成这项工作。这并不一定意味着编译器为你编写代码，但如果类没有声明复制构造函数，编译器会生成指令，在这些示例中，逐字节地将数据成员从一个 `TDate` 对象复制到另一个 `TDate` 对象。

当将一个对象赋值给另一个对象时，会发生一个相关操作。例如，以下语句：

```
t5 = t1;
```

该语句将 `t1` 的数据成员复制到 `t5`。为此，编译器生成指令，将所有数据字节从源对象复制到目标对象。然而，由于这两个对象此前已经构造完成，因此不会调用复制构造函数。构造函数只在新对象首次产生时被调用。

> 注意
>
> 对于像 `TDate` 这样的简单类，自动生成的复制构造函数和赋值指令完全够用。但是，当你需要更复杂的复制机制时——例如，如果类包含任何动态内存指针——你必须显式实现复制构造函数，并提供将一个对象赋值给另一个对象的机制。有关这些主题的更多信息，请参阅第 13 章“创建和销毁对象”中的“复制构造函数”。

## 内联构造函数

一种常见做法是直接在类声明中声明和实现构造函数。类中同时包含函数原型及其语句，而不是先在类中声明构造函数原型，然后再分别实现。清单 12.4（`inline.cpp`）演示了如何在新版 `TDate` 类中声明和实现构造函数。

### 清单 12.4 INLINE.CPP
