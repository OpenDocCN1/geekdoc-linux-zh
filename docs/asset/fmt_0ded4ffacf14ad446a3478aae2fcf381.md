
```
            printf("%d ", a[i][j]);

        }

        printf("\n");

    }

    return 0;

}
```

## 定义函数

当你定义一个函数时，我们编写执行预期任务的实际代码。因此，你必须在程序调用或引用函数之前提供该函数的定义，否则会发生编译错误。你可以使用以下语法定义函数：

```
return_type function_name(formal parameter list) {

    local variable declarations;

    executable statement 1;

    executable statement 2;

    executable statement 3;

    return (expression);

}
```

在上述语法中，`return_type` 是函数返回的数据类型。函数可以返回 `int`、`char` 或 C 语言中有效的任何其他数据类型。`function_name` 指的是函数的名称，`formal_parameter_list` 是传递给函数的参数列表。`formal_parameter_list` 是一个由逗号分隔的变量列表，当函数被调用时，接收来自主程序的值。在函数定义中用作局部标识符在函数外部无法被识别。函数定义也可以包含在函数内部声明的局部变量。此外，函数定义还包含了执行预期任务的可执行语句。函数的最后一条语句是 `return` 语句，用于返回函数的结果。

> 函数可能不返回值。在这种情况下，函数使用的返回类型为 `void`。在函数定义中，关键字 `void` 用作返回类型。它表示该函数不返回任何值。此类函数不使用 `return` 语句。

下面的代码段定义了一个两个数相加并返回和的函数：

```
int sum(int mark1, int mark2) {

    int total;

    total = mark1 + mark2;

    return (total);

}
```

在上述代码段中，`sum()` 函数定义的返回值为 `int`。该函数包含两个参数列表：`mark1` 和 `mark2`，它们都是 `int` 数据类型。函数定义包含了两个数（`mark1` 和 `mark2`）的相加并将并将加结果存储在变量 `total` 中，然后返回该变量的值。

让我们学习调用函数。

## 调用函数

调用或引用函数意味着从程序执行函数的代码。可以通过指定函数名后跟括号括起来并用逗号分隔的参数列表来调用函数。如果调用不需要任何参数，则在函数名后跟一对空括号。

你可以使用以下语法调用函数：

```
some_variable=function_name(actual_argument_list);
```

在上述代码中，`some_variable` 是存储函数返回值的变量。它必须是与函数返回相同的数据类型。`function_name` 是被调用的函数名，`actual_argument_list` 是传递给方法的实际参数列表。可以通过指定函数名后跟括号括起来并用逗号分隔的参数列表来调用函数。如果调用不需要任何参数，则在函数名后跟一对空括号。列表 5 显示如何在程序中定义和调用函数的示例。

## 数组与函数的使用

### 列表 5.5：定义和调用函数

```
#include <stdio.h>

int sum(int marks1, int marks2) {

    int total;

    total = marks1 + marks2;

    return(total);

}

int main() {

    int sub1, sub2;

    scanf("%d %d\n", &sub1, &sub2);

    int result = sum(sub1, sub2);

    printf("Total marks = %d\n", result);

    return 0;

}
```

以下是上述列表的输出：

- 输入 `sub1` 和 `sub2` 的分数
```
87
69
Total marks = 156
```

在列表 5.5 中，定义了 `sum` 函数，它返回一个整数值。`sum()` 函数接受两个整数值作为参数。

`result` 是一个参数，接收 `sum()` 函数返回的值。

让我们学习参数

## 理解参数和形式

参数（Arguments and parameters）是函数中使用的变量。参数是在调用函数时使用的变量，也称为实参（actual arguments）。参数是在函数定义中使用的变量，这些变量被称为形式参数（formal parameters）。例如，在列表 5 中，`sub1` 和 `sub2` 是参数，而 `marks1` 和 `marks2` 是参数。

在使用参数时，请记住参数的数量应与形式参数的数量相同。

让我们学习变量的作用域。

## 探索变量的作用域

变量的作用域是指变量在程序中的可见性。不同类型的变量用于函数定义内部以及函数定义外部。在某处声明的这些变量在程序的其他地方无法访问。根据变量的作用域，可以将其分为以下几类：

- 局部变量
- 全局变量

让我们讨论一下这两个变量的行为。

## 局部变量

在函数或代码块内部声明的变量被称为局部变量。这些变量仅在其声明的函数或代码块内可访问。如果你在函数外部访问该变量，会导致编译错误。在列表 5 中，`marks1` 和 `marks2` 是局部变量的示例。使用局部变量可以很容易跟踪变量名，因为每次函数调用都会创建新的变量。例如，在列表 5 中，`sum` 函数中声明的 `total` 变量就是局部变量的一个示例。

## 全局变量

在任何函数外部声明的变量被称为全局变量。这些变量可以从程序的任何部分访问。如果局部变量与全局变量具有相同的名称，则局部变量在其作用域内具有优先级。这被称为遮蔽（shadowing）。为了在函数内部访问全局变量，在 C++ 中使用了作用域运算符（`::`）。

```cpp
int x = 10;

void display() {

    int x = 5;

    printf("Local x: %d\n", x);

    printf("Global x: %d\n", ::x);

}
```

## 594 Comdex Linux n2 OpenOffice 课程

```
函数调用前 n 的值：20
函数调用后 n1 的值：20
函数调用后 n2 的值：10
```

在列表 5.8 中，调用了 `swap()` 函数。在这个函数中，参数是通过引用传递的方法传递的。在函数定义内部，我们交换两个变量的值。你会注意到，在函数定义内部对形式参数的修改也反映在（主）函数中。

让我们讨论一下递归函数。

# 使用递归函数

递归函数是一个调用自身的函数。递归函数用于计算某些类型的数学函数。如果你正在计算一个数字的阶乘，则将该数字乘以减1。你继续执行此操作直到达到1，以得到该数字的阶乘。换句话说，如果你要获取 5 的阶乘，你需要执行以下乘法：

```
5*4*3*2*1
```

在这个示例中，乘法是递归执行的，直到数字达到1。此示例计算的阶乘可以使用递归函数计算，如列表 5.9 所示。

```c
#include<stdio.h>

int fact(int n) {

    if(n<=1)
        return n;
    else
        return (n*fact(n - 1));

}

int main() {

    int n, fact1;

    printf("Enter a number:%d\n",
    scanf("%d", &n);

    fact1=fact(n);

    printf("Factorial value of the number = %d\n", fact1);

    return 0;

}
```
