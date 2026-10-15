
```c
printf("%d\n",tmp);

}

void printchar (char inputchar) {

  char tmp;

  tmp = inputchar;

  printf("%c\n",tmp);

}
```

当在各自函数中使用局部 `tmp` 变量时，`tmp` 不会被修改，如输出所示：

1.234
5
1.234
a
1.234

C++ 提供了一种方法，在同名局部变量处于作用域时指定全局变量。在变量名前加缀 `::` 运算符始终解析为全局实例。因此，列表 23.11 中在 `main` 中定义的 `tmp` 变量可以通过标签 `::tmp` 在打印函数访问。

## 自动化、编程与修改源代码

### 第六部分

没有使用相同的局部变量名。这意味着在必要时，可以改进库函数而不而不影响现有代码。无论该库是包含可重用的应用程序代码，还是作为与编译器相关的运行时库分发，这一点都是成立。

> 注意
> 运行时库是编译模块的集合，用于执行常见的 C、C++ 和 UNIX 函数。这些代码编写非常严谨，经过了调试并经过了高度优化。例如，`printf` 函数需要机器指令来格式化各种输出字段、将它们发送到标准输出设备，并检查是否存在 I/O 错误。由于这涉及到许多机器指令，如果在程序中的每次调用中都重复该序列，效率将会非常低。相反，开发者会编写一个单一的通用的 `printf` 函数，并将其放在标准库中。当你的程序被编译时，编译器会生成所有预先写的程序，而不是在源代码每次发生调用时都重新创建逻辑。

变量的引用作用域（Variable scope of reference）是一项语言特性，它允许小型 C 和 C++ 程序被设计成独立函数，同时根据需要组合成更大的实用程序。这种灵活性是 UNIX 的特点，UNIX 是第一个基于 C 语言构建的操作系统。正如你在本章其余部分看到的，变量的引用作用域也使得 C++ 中的面向对象编程成为可能。

## C++ 中的函数重载与运算符载

重载（Overloading）是一种允许多个函数具有相同名称的技术。在至少两种情况下，程序员可能想要定义一个与现有函数同名的新函数：

- 当现有版本的函数没有执行精确的功能时，但它必须包含在程序中（例如来自标准库的函数）。
- 当同一个函数必须根据传递给它的数据格式以不同的方式运行时。

在 C 中，只要旧函数不在作用域内，函数名就可以重用。函数名的引用作用域的确定方式与数据名称的作用域相同：在另一个函数的定义内部定义（而不仅仅是调用）的函数，该函数是该函数的局部的。

当两个相似的函数可以在同一个作用域内共存时，它们不能具有相同的名称。相反，必须分配不同的名称，就像标准库中的 `strcpy` 函数一样，每个函数都复制字符串，但实现方式略有不同。

## C 和 C++ 编程
### 第 23 章

C++ 通过允许重载函数名来绕过限制。也就是说，C++ 语言允许程序员在同一个引用作用域内重用函数名，只要参数在数量或类型上不同。

列表 23.12 显示了函数重载示例。此程序定义并调用了 `printvar` 函数的两个版本，一个是列表 23.11 中的 `printnum`，另一个是 `printchar`。

### 列表 23.12。重载函数的示例。

```
#include <stdio.h>

void printvar(int tmp)

{

    printf("%d \n",tmp);

}

void printvar(char tmp)

{

    printf("%c \n",tmp);

}

void main ()

{

    int numvar;

    char charvar;

    numvar = 5;

    printvar(numvar);

    charvar = 'a';

    printvar(charvar);

}
```

以下是程序执行时的输出：

5
a

之所以能够重载，是因为 C++ 编译器能够确定每次从 `main` 调用 `printvar` 函数时发送的参数格式。编译器根据这些格式构成对函数正确版本的调用。如果重载函数位于库或另一个模块中，则必须在此源代码模块中包含相关的头文件（如 `stdio.h`）。头文件包含外部函数的原型，告知编译器在函数的外部版本中使用的函数和参数格式。

标准的数学、逻辑和其他运算符也可以被重载。这是一项高级且强大的技术，允许程序员精确自定义标准语言特性如何在特定数据结构上或代码的特定点上运行。在重载 `+`、`MOD`、`OR` 等标准运算符时必须非常小心，以确保结果操作运行正确、限制在代码中适当的出现处，并有良好的文档。

![](img/740d39911bdfa3e99eeee27a7e4e7e4fa_504_0.png)

## C++ 数据结构中的函数

C++ 支持面向对象编程的第二个特性（除重载外）是将函数与特定的数据结构或格式关联的能力。此类函数可以是公共的（供任何代码调用），可以是私有的（仅供该数据结构内的其他函数调用），也可以允许有限的访问。

C++ 中的数据结构必须使用 `struct` 关键字定义，并成为语言新增的新数据类型（在结构定义的作用域内）。列表 23.13 重顾了列表 23.3 的结构，并添加了一个 `display` 函数来打印我们的 `license` 结构实例。注意 C++ 中指定注释的另一种方式是使用双斜杠。这告诉编译器忽略该行之后的所有内容。

另外注意列表 23.13 使用了 C++ 字符输出函数 `cout` 而不是 C 语言例程 `printf`。

### 列表 23.13。向数据结构添加函数。

```
#include <iostream.h>
//
// struct structure = new datatype
struct license {
    char name[128];
    char address[3][128];
    int zipcode;
    int height, weight, month, day, year;
    char license_letter;
    int license_number;
void display(void)
// 将有一个显示许可证类型的函数
};
void license::display() {
    cout << "Name: " << name << "; ";
    cout << "Address: " << address[0] << " " << address[1] << " " << address[2] << " " << zipcode << "; ";
    cout << "Height: " << height << " inches\n";
    cout << "Weight: " << weight << " lbs\n";
    cout << "Date: " << month << "/" << day << "/" << year << "; ";
    cout << "License: " << license_letter << license_number << ";";
}
```

```
main() {
    struct license licensee; // 定义一个 license 类型的变量
    newlicense.name = "John Smith"; // 并初始化
    newlicense.address(0) = "123 Elm Street";
    newlicense.address(1) = "";
    newlicense.address(2) = "Smalltown, AnyState";
}
```

## C 和 C++ 编程
### 第 23 章

```
newlicense.zipcode = "98765";
newlicense.height = 70;
newlicense.weight = 160;
newlicense.month = 1;
newlicense.day = 23;
newlicense.year = 97;
newlicense.license_letter = A;
newlicense.license_number = 56790;
```

```
newlicense.display(); // 显示此结构实例
```
