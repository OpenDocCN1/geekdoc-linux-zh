
当该程序编译后执行时，它会产生列表 6.11 所示的输出。

**列表 6.11。引用范围的输出，示例 1。**

```
5
a
```

列表 6.12 显示了另一个引用范围的示例。在这里发现了一个全局变量 `tmp`——也就是说，由于定义在 `main` 函数内部，因此整个程序都是知的——除了两个 `printnum` 和 `printchar` 函数的局部 `tmp` 变量之外。

**列表 6.12。引用范围，示例 2。**

```c
#include <stdio.h>

void printnum ( int ); /* 函数声明 */
void printchar ( char ); /* 函数声明 */

main ()
{
  double tmp; /* 定义一个全局变量 */
  tmp = 1.0; /* 注意：从用法上下文推断 */
  printnum (5);
  printchar ("a");
}
```
（注：列表 6.12 的 OCR 文本在源中严重碎片；我已根据提供的文本片段重建了逻辑流）。

## C++ 中的函数和运算符重载

重载是一项允许多个函数具有相同名称的技术。在至少两种情况下，你可能想要定义一个与现有函数同名的新函数：

- 当函数的现有版本没有完全实现所需的功能时，但在其他情况下它必须包含在程序中（例如标准库中的函数）
- 当同一个函数必须根据传递它的数据格式执行不同的操作时

在 C 语言中，只要旧函数名不在作用域内，你就可以重用函数名。函数引用作用域的确定方法与数据名称的作用域相同：在另一个函数的内部定义（而不仅仅是调用）的函数是该另一个函数的局部函数。

然而，当两个相似的 C 函数必须在同一个作用域内共存时，它们不能具有相同的名称。相反，你必须分配两个不同的名称，就像标准库中的 `strcpy` 和 `strncpy` 函数一样，它们都复制字符串，但方式略有不同。

C++ 通过允许重载函数名来规避这一限制。也就是说，C++ 语言允许你在函数参数的数量或类型不同的情况下下，在同一个引用作用域内重用函数名。

**列表 6.14. 函数重载示例。**

```cpp
#include <stdio.h>

void printvar (int tmp)
{
    printf("%d \n",tmp);
}

void printvar (char tmp)
{
    printf("a \n",tmp);
}

void main ()
{
    int numvar;
    char charvar;
    numvar = 5;
    printvar (numvar);
    charvar = 'a';
    printvar (charvar);
}
```

**列表 6.15. 重载函数的输出。**

```
5
a
```

重载之所以是因为 C++ 编译器每次在 `main` 内部调用 `printvar` 函数时都能确定参数的格式。如果重载函数位于库或另一个模块中，相关的头文件（如上面的 `stdio.h`）必须包含在此源代码模块中。该头文件包含了外部函数的原型，从而告知编译器在外部函数版本使用的参数格式。

标准的数学、逻辑和其他运算符也可以被重载。这种高级且强大的技术允许你自定义标准语言在代码特定点的操作方式。在重载 `+`、`MOD` 和 `OR` 等标准运算符时必须小心，以确保产生的操作是正确的且文档良好的。

## C++ 数据结构中的函数

C++ 支持面向对象编程的第二个特性（除重载外）是将函数与特定数据结构关联的能力。此类函数可以是公共的（任何代码都可以调用）、私有的（仅允许结构内部的函数调用）或允许限制访问。

在 C++ 中，你必须使用 `struct` 关键字定义数据结构。这些结构变成了语言的新类型（在结构定义范围内）。列表 6.16 重新访问了列表 6.3 中的结构，并为 `license` 结构添加了 `display` 函数。注意 C++ 中使用双斜号注释。这种双斜号告诉编译器忽略该行之后的所有内容。此外，注意此示例使用了 C++ 字符输出函数 `cout` 而不是 C 程序的 `printf`。

**列表 6.16. 为数据结构添加函数。**

```cpp
#include <iostream.h>

// 结构 = 新类型
struct license {
    char name[128];
    char address[3][128];
    int zipcode;
    int height, weight, month, day, year;
    char license_letter;
    int license_number;
    void display(); // 用于显示 license 类型的函数
};

// 现在为此数据类型定义 display 函数
void license::display()
{
    cout << "Name: " << name;
    cout << "Address: " << address[0];
    cout << " " << address[1];
    cout << " " << address[2] << " " << zipcode;
    cout << "Height: " << height << " inches";
    cout << "Weight: " << weight << " lbs";
    cout << "Date: " << month << "/" << day << "/" << year;
    cout << "License: " << license_letter << license_number;
}

int main()
{
    struct license newlicensee; // 定义一个 license 类型的变量
    newlicensee.name = "Joe Smith"; // 并初始化
    newlicensee.address[0] = "123 Elm Street";
    newlicensee.address[1] = "";
    newlicensee.address[2] = "Smalltown, AnyState";
    newlicensee.zipcode = 98765;
    newlicensee.height = 70;
    newlicensee.weight = 165;
    newlicensee.month = 1;
    newlicensee.day = 23;
    newlicensee.year = 97;
    newlicensee.license_letter = 'A';
    newlicensee.license_number = 567890;
    newlicensee.display(); // 显示此结构实例
}
```

**列表 6.17. 函数的输出。**

```
Name: Joe Smith
Address: 123 Elm Street Smalltown, AnyState
Height: 70 inches
Weight: 165 lbs
Date: 1/23/97
License: A567890
```

注意这里的三个引用指向同一个函数。首先，函数作为结构定义中的一个元素进行了声明。其次，定义了函数。最后，当创建 `license` 实例时，它的 `display` 函数被调用。

## C++ 中的类

重载和函数与数据结构的关联为面向对象的代码奠定了基础。C++ 类通过将数据和算法封装成新类型，扩展了数据结构的概念。类声明定义了对象的模板，但它不会分配内存或创建实例。程序必须声明该类型的实例（或对象）才能使用它。

### 在 C++ 中声明类

列表 6.18 展示了一个典型的 C++ 类。

**列表 6.18. 在 C++ 中声明类。**

```cpp
#include <iostream.h>

// 声明 Circle 类
class Circle {
private:
    double radius; // 私有数据成员
public:
    Circle (double rad); // 构造函数
    ~Circle (); // 析构函数
    double area (void); // 成员函数 - 计算面积
};

// 此类对象的构造函数
Circle::Circle(double radius)
{
    rad = radius;
}

// 此类对象的析构函数
Circle::~Circle()
{
    // 什么都不做
}
```
