
```cpp
cin >> anotherFloat;

cout << "Stored as " << anotherFloat << endl;

// 让用户输入单个单词 - 不允许空格

string myString;

cout << "Enter a string using cin..." << endl;

cin >> myString;

cout << "Stored as " << myString << endl;

// 让用户输入单个字符

char myChar;

cout << "Enter a char..." << endl;

cin >> myChar;

cout << "Stored as " << myChar << endl;

// 让用户输入整数

int anotherInt;

cout << "Enter an integer..." << endl;

cin >> anotherInt;

cout << "Stored as " << anotherInt << endl;

// 让用户输入允许空格的字符串

string anotherString;

cout << "Enter a string using getline..." << endl;

getline(cin, anotherString);

cout << "Stored as " << anotherString << endl;

return 0;

}
```

```cpp
// 获取用户输入一个整数

int anotherInt;

cout << "Enter another integer..." << endl;

cin >> anotherInt;

cout << "Stored as " << anotherInt << endl;

// 在下一次输入前清除 channel-in 中任何未使用的字符

cin.clear();

cin.ignore(INT_MAX, '\n');

// 获取用户输入字符串 - 允许空格

string anotherString;

cout << "Enter another string using getline..." << endl;

getline(cin, anotherString);

cout << "Stored as " << anotherString << endl;

// 获取用户输入字符串 - 允许空格

string oneMoreString;

cout << "Enter one more, oneString using getline..." << endl;

getline(cin, oneMoreString);

cout << "Stored as " << oneMoreString << endl;

return 0;
```

在用户输入每个值后，程序会使用以下语句来清除键盘缓冲区：

```cpp
cin.clear();
cin.ignore(INT_MAX, '\n');
```

`clear()` 函数会重置因无效字符而设置的任何错误指示。`ignore()` 函数告诉 Pi 跳过当前正在在 `cin channel-in` 流中等待的任何 `\n` 换行字符。

`INT_MAX` 告诉计算机最大的整数值是多少。这允许我们的程序尽可能从输入通道中清除尽可能多的字符，以防有人在程序运行时输入了大量不想要的数据。

正如之前在 `第 3 章：数据类型与值，INT_MAX` 中解释的那样，`INT_MAX` 是定义在 `<climits>` 库中的一个特殊值，因此在程序开头需要额外的指令：

```cpp
#include <climits>
```

运行程序时，无论你输入超过一个单词，即使代码使用了 `cin` 也没关系。任何多余字符都会被忽略并丢弃，准备让 Pi 接受你输入的下一个值。你可以在下一页看到结果。

第 4 章：键盘输入与屏幕输出 | 121

```text
Enter a float...
1.25
Stored as 1.25
Enter another float...
2.7
Stored as 2.75
Enter a string using cin...
More than one word!
nEnter a char...
@
Stored as @
Enter another integer...
32
Stored as 32
Enter another string using getline...
Many words on one line.
Stored as Many words on one line.
Enter one more string using getline...
More many words, all on one line.
Stored as More many words, all on one line.
```

一个简单的程序：接收一些数据作为输入，进行处理并显示结果。

我们通过尝试处理一些无效输入来说说明有效数据的重要性。

接下来的程序允许你输入两个整数值，然后这些值将被相加并显示在屏幕上：

## 示例 4.25 - value_of_inputs.cpp

```cpp
#include <iostream>    // 程序将使用屏幕和键盘

using namespace std;    // 将使用标准标识符 cin, cout, endl

int main()
{
    int firstInt, secondInt, sum;
    // 获取用户输入第一个整数
    cout << "Enter 1st integer... ";
    cin >> firstInt;
    // 获取用户输入第二个整数
    cout << "Enter 2nd integer... ";
    cin >> secondInt;
    // 将两个整数相加并存储结果
    sum = firstInt + secondInt;
    // 在屏幕上显示结果
    cout << "The sum of the integers is " << sum << endl;
    return 0;
}
```

你使用键盘输入的值被存储在两个不同的变量中：`firstInt` 和 `secondInt`。这些值由计算机相加，结果存储在一个新的整数变量中，称为 `sum`。`sum` 的值将显示在屏幕上。（（我们假设你不会不小心输入某些文本而不是整数。）

尝试运行程序并输入两个整数 - 你应该能看到显示正确的和。反之，如果你向程序提供某些文本（例如 `"tomato"` 这个值），你将看到一个关于计算机如何处理无效数据的线索。

以下是我的 Pi 上发生的情况：

![](img/0c86cf81300257fe2415e40f8fb03508_124_0.png)

如果用户为一个或两个输入输入了无效值，那么尝试相加数据是没有意义的。输入 `"tomato"` 而不是数字被 Pi 解释为值 `0`。

# 使用键盘验证输入的输入的数字

当你的程序期望用户输入数字时，你如何确保没有输入字母或其他符号呢？我们如何才能检查输入的值确实是一个有效数字？

一旦值输入到 `cin`，我们可以使用 `good()` 成员函数检查该值的状态：

```cpp
int myInt;
cin >> myInt;
if (cin.good())
    cout << "This was a valid integer" << endl;
else
    cout << "This was NOT a valid integer" << endl;
```

在使用 `good()` 检查 `cin` 内容中的无效字符后，你的程序可以决定是合理地处理该值，还是丢弃输入的字符，如下流程所示：

![](img/0c86cf81300257fe2415e40f8fb03508_124_0.png)

第 4 章：键盘输入与屏幕输出 | 123

## 示例 4.26 - validate_int.cpp

```cpp
#include <iostream>    // 程序将使用屏幕和键盘
#include <limits>       // 需要 INT_MAX
using namespace std;    // 将使用标准标识符 cin, cout, endl

int main() {
    int myInt;
    bool needValue = true;
    // 重复请求数字
    do {
        cout << "Enter a number...";
        cin >> myInt;
        // 是否有效
```
