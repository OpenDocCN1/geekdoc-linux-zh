
```cpp
result = result * index;

return result;
}
```
```
// ------------------------------------
```
```cpp
int main()
{
    // 重复调用 factorial() 函数来显示 1 到 10 之间
    // 数字的阶乘
    for ( unsigned int number = 1; number <= 10; number++ )
        cout << number << " !" << factorial( number ) << endl;
    return 0;
}
```

执行时，你应该看到以下结果：

![](img/0c86cf81300257fe2415e40f8fb03508_332_0.png)

下面的另一个函数将接收一个整数并将其乘以自身：

```cpp
int squareMyNumber( int startingNumber )
{
    return startingNumber * startingNumber;
}
```

我们可以调用 `squareMyNumber()` 然后显示它返回的结果：

```cpp
cout << "The square of 5 is " << squareMyNumber( 5 ) << endl;
```

这将显示：

The square of 5 is 25

或者，我们可以获取返回的结果并存储在变量中，其他语句可以使用该变量：

```cpp
int answer = squareMyNumber( 5 );
```

最后，我们可以获取返回的值并将其传入另一个函数调用：

```cpp
cout << "5 to the power of 4 is ";
cout << squareMyNumber( squareMyNumber( 5 ) );
```

这将显示：

5 to the power of 4 is 625

## 创建一个将字符串值转换为大写的函数

下一页的程序使用了示例之一来更改字符串值，使字母表中的任何字母都转换为大写。

这是通过 `makeUpperCase()` 函数实现的。将原始字符串值 `iTyped` 作为参数传递给函数，该参数在函数内部被命名为 `originalText`。然后函数使用 `for` 循环遍历 `originalText` 中的字符。

每个字符通过调用 `toupper()` 转换为大写。转换后的大写字符随后追加到一个名为 `finalText` 的新字符串中。

完成后，`makeUpperCase()` 将 `finalText` 返回给程序的 `main()` 函数，并在那里显示在屏幕上：

![](img/0c86cf81300257fe2415e40f8fb03508_333_0.png)

332 | 在树莓派上使用 C++ 编程 *

# 示例 10.4 -function_upper_case.cpp

```cpp
#include <iostream>    // 程序将使用键盘和屏幕
#include <string>      // 需要字符串对象
using namespace std;                // 将使用标准标识 cout 和 endl

// ------------------------------------------------------
string makeUpperCase(string originalText)
{
    string finalText = "";
    for (int i = 0; i < originalText.length(); i++)
    {
        finalText += toupper(originalText[i]);
    }
    return finalText;
}

// ------------------------------------------------------
int main()
{
    string iTyped;
    cout << "Enter a string: ";
    getline(cin, iTyped);
    cout << "Upper-case version: " << makeUpperCase(iTyped) << endl;
    return 0;
}
```
*(注：由于原文中 10.4 的 OCR 文本存在严重损坏，已根据上下文重构了功能性代码表示。)*

下面的程序调用 `checkPasswordOK` 函数来获取一个 `bool` 值（该值始终为 `true` 或 `false`）。这将指示特定密码的长度是否接受：

## 示例 10.7-function_check_length.cpp

```cpp
#include <iostream>    // 程序将使用键盘和屏幕
using namespace std;      // 将使用标准标识符 string, cin, endl

//----------------
bool checkPasswordOK(string password )
{
    // 检查密码长度是否在 8 到 12 个字符之间
    // 如果是则返回 true，如果不是则返回 false
    return password.length() >= 8 && password.length() <= 12;
}

//----------------
int main() {
    // 允许用户输入文本
    cout << "Please type a password (8-12 characters): ";
    string newPassword;
    cin >> newPassword;
    // 调用函数检查密码长度是否接受
    if ( checkPasswordOK(newPassword) )
        cout << "Thanks." << endl;
    else
        cout << "Not accepted!" << endl;
    return 0;
}
```

上述函数体只包含一个简单的 `return` 语句，它根据传递给函数的密码值的长度将表达式求值为 `true` 或 `false`。

`main()` 中的代码随后使用 `checkPasswordOK()` 的返回值来决定显示哪个消息。

长度为 8 个字符或以上，且在 12 个字符或以下的密码是可以接受的：

![](img/0c86cf81300257fe2415e40f8fb03508_337_0.png)

长度小于 8 个字符或大于 12 个字符的密码是不可接受的：

![](img/0c86cf81300257fe2415e40f8fb03508_337_1.png)

## 测试特定的整数是否为质数

此程序允许用户输入单个整数。然后它测试该数字是否为质数 - 质数是指只能被自身或数字 1 整除的数。

大部分工作由 `testForPrime()` 函数完成，该函数使用 `while` 循环检查范围内不同的数字是否能被该数整除且余数为零（1 和原始数字除外），如果是，则被测试的数字不能是质数。如果没有找到这样的因子，则意味着该数字是一个质数。

找到一个余数为零的数字意味着该数字是被测试数字的因子。如果找到了任何此类因子，则意味着被测试的数字不能是质数。

## 示例 10.8–function_prime.cpp

```cpp
#include <iostream>      // 程序将使用键盘和屏幕
#include <cstdlib>         // 程序使用 exit() 函数
using namespace std;      // 将使用标准标识符 cin, cout, endl
bool testForPrime(int numToTest) {
    int divisor = 2;
    bool foundExactDivision = false;
    while (divisor < numToTest) {
        if (numToTest % divisor == 0) {
            foundExactDivision = true;
            cout << divisor << " goes into " << numToTest << " " << endl;
            // // 取消 break 语句注释提高效率
            // // 将仅找到第一个因子
            // break;
        }
        divisor++;
    } // end of while
    return not foundExactDivision;
```
