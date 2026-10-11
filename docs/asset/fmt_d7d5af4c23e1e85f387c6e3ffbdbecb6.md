
你的程序在尝试使用此类指针之前会对其进行检查，测试它是否持有 `NULL` 值。这将告诉你指针是否可用。如果指针持有 `NULL` 值，则程序不应尝试跟随它。如果指针持有 `NULL` 以外的任何值，可以假设该指针持有一个可用的内存地址，该地址将指向内存中的有用数据。

例如：

```cpp
// 检查指针是否指向某些数据，如果是，则跟随指针
if ( pTemperatureToDisplay != NULL )
    cout << *pTemperatureToDisplay;
else
    cout << "No temperature data to display.";
```

这里是修改后的程序，它将正确检测到没有可显示的温度数据：

## 示例 12.7-null_pointer.cpp

```cpp
#include <iostream>        // 程序将在屏幕上显示一些文本

using namespace std;               // 将使用标准标识符 cout 和 endl

int main()
{
    // 创建一个指向 float 值的指针
    float* pTemperatureToDisplay;
    pTemperatureToDisplay = NULL;

    // 检查指针是否指向某些数据，如果是，则跟随指针
    if ( pTemperatureToDisplay != NULL )
        cout << *pTemperatureToDisplay;
    else
        cout << "No temperature data to display." << endl;

    cout << endl;

    return 0;
}
```

# 使用指针创建并访问存储在堆上的动态数据

到为止的示例使用的是指向静态数据的地址。程序也可以在动态内存中创建数据值。上一个示例中的数据很容易地存储在堆上，而不是静态内存中。

要在堆上创建一个新值，程序使用 `new` 运算符。作为 `new` 操作的一部分，必须告诉计算机要创建什么类型的数据。还会告诉它应该分配什么值：

```cpp
new string("Monster Island")
```

上述操作告诉计算机创建一个字面量值为 `"Monster Island"` 的字符串。计算机返回数据存储在堆上的内存地址。

为了以后使用该字符串值，你需要知道数据存储在内存的哪个位置。你可以保留 `new` 操作返回的内存地址以供以后使用，使用指针变量存储该地址：

```cpp
string* pHolidayDestination = new string("Monster Island");
```

上述语句意味着：

- 创建一个指向字符串的新指针并将此指针命名为 `pHolidayDestination`。
- 设置该值为 `"Monster Island"`。

上述操作告诉计算机在堆上创建一个字面量值为 `"Monster Island"` 的字符串。计算机返回数据存储在堆上的内存地址。这里的结构体如下：

```cpp
struct point2D
{
  float xCoord;
  float yCoord;
  string textDescription;
};
```

这可能在堆上创建一个指向 `point2D` 结构体的指针。下面的语句这样做，创建一个名为 `pFirstPoint` 的指针。通过 `new` 运算符创建了结构体，就可以开始为各个成员赋值：

```cpp
point2D* pFirstPoint = new point2D;
```

为了以后使用该字符串值，你需要知道数据存储在内存的哪个位置。你可以保留 `new` 操作返回的内存地址以供以后使用，使用指针变量存储该地址：

```cpp
string* pHolidayDestination = new string("Monster Island");
```

上述语句意味着：

- 创建一个指向字符串的新指针并将此指针命名为 `pHolidayDestination`。
- 设置该值为 `"Monster Island"`。

上述操作告诉计算机在堆上创建一个字面量值为 `"Monster Island"` 的字符串。计算机返回数据存储在堆上的内存地址。这里的结构体如下：

```cpp
struct point2D
{
  float xCoord;
  float yCoord;
  string textDescription;
};
```

这可能在堆上创建一个指向 `point2D` 结构体的指针。下面的语句这样做，创建一个名为 `pFirstPoint` 的指针。通过 `new` 运算符创建了结构体，就可以开始为各个成员赋值：

由于这可能在堆上创建一个指向 `point2D` 结构体的指针。下面的语句这样做，创建一个名为 `pFirstPoint` 的指针。通过 `new` 运算符创建了结构体，就可以开始为各个成员赋值：

```cpp
pFirstPoint->xCoord = -10;
pFirstPoint->yCoord = 5;
pFirstPoint->textDescription = "Crashed alien spaceship";
```

处理大量数据的一种可能方法是将其存储在堆上，而使用程序中的普通静态内存来存储指针。这里的示例使用了之前示例中的二维点结构体，但此程序动态地使用了 2D 点。

## 示例 12.8 - heap.cpp

```cpp
#include <iostream>      // 程序将在屏幕上显示一些文本
using namespace std;               // 将使用标准标识符 cout 和 endl
// ---------------------
// 创建新结构体。多个变量将在稍后使用。
struct point2D {
    float xCoord;
    float yCoord;
    string textDescription;
}
// ------------------------------------
// 函数接收 point2D 指针作为参数并显示关于点的数据。
void displayPoint( point2D* pPoint ) {
    // 检查指针是否为 NULL
    // 如果不是 NULL 指针，则跟随指针并显示关于点的数据
    if ( pPoint != NULL ) {
        // 跟随指针显示点的数据值
        cout << pPoint->textDescription;
        cout << " ", "位于坐标 (";
        cout << pPoint->xCoord;
        cout << " ", "";
        cout << pPoint->yCoord;
        cout << ")" endl;
    } // 结束 if
} // 结束函数
// -------------------------------------
// 程序的主函数
int main() {
    // 在堆上创建一个 point2D 的新实例
    point2D* pFirstPoint = new point2D;

    // 设置成员的值
    pFirstPoint->xCoord = -10;
    pFirstPoint->yCoord = 5;
    pFirstPoint->textDescription = "Crashed alien spaceship";

    // 调用函数显示数据
    displayPoint(pFirstPoint);

    // 释放堆上分配的内存
    delete pFirstPoint;

    return 0;
}
// -------------------------------------
// 待下一页继续...
```

继续...
