
![](img/f80199d101da92d953f18eaa6205b48e_130_3.png)

## STEP 3

你可以使用斜杠和星号注释多行：

```
/* This comment can
 cover several lines
 without the need to add more slashes */
```

只需记住用相反的星号和斜杠结束块注释。

![](img/f80199d101da92d953f18eaa6205b48e_130_4.png)

## STEP 6

对于块注释，在 C++ 中在注释块的每一行添加星号是一种良好的做法。这也有助于你记住在继续编写代码之前关闭注释块：

```
/* This comment can
 * Cover several lines
 * Without the need to add more slashes */
```

幸运的是，Geany 会自动执行此操作，但在其他 IDE 中使用时请注意这一点。

```
/* This comment can
 * cover several lines
 * without the need to add more slashes */
```

## 变量

使用 C++ 时变量与使用 Python 时略有不同。在 Python 中，你只需说明 `a` 等于 10，变量就会被分配。然而，在 C++ 中，变量在使用前必须先声明其类型。

### THE DECLARATION OF VARIABLES

你可以通过代码中的语句声明 C++ 变量。你可以声明几种不同的变量类型。它的工作原理如下。

## STEP 1

打开一个新空白 C++ 文件并输入通常的代码头：

```
#include <iostream>
using namespace std;

int main()
{
}
```

![](img/f80199d101da92d953f18eaa6205b48e_131_0.png)

## STEP 2

先从简单开始，创建两个变量 `a` 和 `b`，一个值为 10，另一个为 5。你可以使用数据类型 `int` 声明这些变量。在大括号内输入：

```
int a;
int b;

a = 10;
b = 5;
```

![](img/f80199d101da92d953f18eaa6205b48e_131_1.png)

## STEP 3

你可以构建并运行代码，但它不会做太多事情，只是将值 10 和 5 存储到整数 `a` 和 `b` 中。忽略关于变量设置但未使用的警告，代码仍然有效。要输出变量的内容，请添加：

```
cout << a;
cout << "\n";
cout << b;
```

`cout << "\n"`; 部分只是在输出 10 和 5 之间放置一个新行。

![](img/f80199d101da92d953f18eaa6205b48e_131_2.png)

## STEP 4

自然地，你可以声明一个新变量，称为 `result` 并输出一些简单的算术运算：

```
int result;

result = a + b;
cout << result;
```

按照屏幕截图将以上内容插入代码中。

![](img/f80199d101da92d953f18eaa6205b48e_131_3.png)

## STEP 5

你可以在声明变量时立即为其赋值。你输入的代码可以如下所示：

```
int a = 10;
int b = 5;
int result = a + b;

cout << result;
```

![](img/f80199d101da92d953f18eaa6205b48e_132_0.png)

## STEP 6

特定于 C++，你也可以使用以下方法在声明变量时立即为其赋值：

```
int a (10);
int b (5);
```

然后，从 C++2011 标准开始，使用大括号：

```
int result {a+b};
```

![](img/f80199d101da92d953f18eaa6205b48e_132_1.png)

## STEP 7

你可以创建全局变量，即在任何函数之外声明并在整个代码中的任何函数中使用的变量。到目前为止你使用的是局部变量：在函数内部使用的变量。例如：

```
#include <iostream>
using namespace std;
int StartLives = 3;

int main ()
{
    StartLives = StartLives - 1;
    cout << StartLives;
```

![](img/f80199d101da92d953f18eaa6205b48e_132_2.png)

## STEP 8

上一步创建了变量 `StartLives`，它是一个全局变量。例如在游戏中，玩家的生活取决于他们表现的好坏。当玩家重新开始游戏时，`StartLives` 会返回到其默认状态 3。在这里我们分配了 3 条生命，然后减去 1，剩下 2 条生命。

![](img/f80199d101da92d953f18eaa6205b48e_132_3.png)

## STEP 9

现代 C++ 编译器比大多数程序员给予它的信用更智能。虽然你可以为变量声明许多数据类型，但实际上你可以使用 `auto` 功能：

```
#include <iostream>
using namespace std;
auto pi = 3.141593;

int main()
{
    double area, radius = 1.5;
    area = pi * radius * radius;
    cout << area;
```

![](img/f80199d101da92d953f18eaa6205b48e_132_4.png)

## STEP 10

虽然我们说在第 3 步中忽略警告，但警告和错误之间存在区别。在这种情况下，它只是一个简单的警告。新的数据类型 `double` 表示双精度浮点值，这使得代码更准确。结果应为 7.06858。从本质上讲，你通常可以处理警告，但不能处理错误。

![](img/f80199d101da92d953f18eaa6205b48e_132_5.png)

## 数据类型

变量，如你所见，存储程序员稍后可以调用并根据需要操作的信息。变量只是保留的内存位置，存储程序员根据使用的数据类型分配的值。

### THE VALUE OF DATA

在 C++ 中，程序员可用的数据类型有很多，例如整数、浮点数、布尔值、字符等等。人们普遍认为有七种基本数据类型，通常称为原始内置类型；然而，如果代码中需要，你也可以创建自己的数据类型。

| Type | Command |
|---|---|
| Integer | int |
| Floating Point | float |
| Character | char |
| Boolean | bool |
| Double Floating Point | double |
| Wide Character | wchar_t |
| No Value | void |

通过添加 `cout.precision()` 函数并在括号内添加值，但即使这样你仍然受限于 `double` 数据类型的精度。例如，尝试以下代码：

```
#include <iostream>
using namespace std;
double PI = 3.141592653589793238463;
```

```
int main()
{
    cout << PI;
}
```

![](img/f80199d101da92d953f18eaa6205b48e_133_0.png)

这些基本类型还可以使用以下修饰符进行扩展：Long、Short、Signed 和 Unsigned。基本上，这意味着修饰符可以扩展每种数据类型的最小和最大范围值。例如，`int` 数据类型的默认值范围为 -2147483648 到 2147483647，你会同意这是一个相当大的值。

现在，如果你使用其中一个修饰符，范围就会改变：

`Unsigned int` = 0 to 4294967295

`Signed int` = -2147483648 to 2147483647

`Short int` = -32768 to 32767

`Unsigned Short int` = 0 to 65,535

`Signed Short int` = -32768 to 32767

`Long int` = -2147483647 to 2147483647

`Signed Long int` = -2147483647 to 2147483647

`Unsigned Long int` = 0 to 4294967295

自然地，你可以使用没有修饰符的基本类型，因为每种数据类型都提供了足够的范围。然而，使用修饰符被认为是良好的 C++ 编程实践。
