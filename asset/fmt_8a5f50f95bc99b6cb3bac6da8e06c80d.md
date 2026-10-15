
`using namespace std;` // 将使用标准标识符 `cout` 和 `endl`

`int main()`

{

    `cout` << "..." << `endl`;

    `sleep`(1);

    `cout` << "\v..." << `endl`;

    `sleep`(1);

    `cout` << "\v..." << `endl`;

    `sleep`(1);

    `cout` << "..." << `endl`;

    `return` 0;

}
```

## `\t` 制表符

`\t` 字符创建一个水平间隙，在屏幕上显示任何后续字符之前向右移动。（记住：“tab”一词是“tabulate”的缩写，意思是“制成表格”。）

### 示例 4.10 - tab_char.cpp

```cpp
#include <iostream>      // 程序将在屏幕上显示一些文本
#include <unistd.h>       // 用于 `sleep` 函数
using namespace std; // 将使用标准标识符 `cout` 和 `endl`
int main()
{
    cout << "..." << endl;
    sleep(1);
    cout << "\t..." << endl;
    sleep(1);
    cout << "\t..." << endl;
    sleep(1);
    cout << "..." << endl;
    return 0;
}
```

## `\v` 垂直制表符

`\v` 制表符告诉计算机向下移动到屏幕的下一行。它不影响当前的水平位置，只改变垂直位置。

`\v` 字符告诉计算机向下移动到屏幕的下一行。

### 示例 4.11 - vertical_tab.cpp

```cpp
#include <iostream>      // 程序将在屏幕上显示一些文本
#include <unistd.h>       // 用于 `sleep` 函数
using namespace std; // 将使用标准标识符 `cout` 和 `endl`
int main()
{
    cout << "..." << endl;
    sleep(1);
    cout << "\v..." << endl;
    sleep(1);
    cout << "\v..." << endl;
    sleep(1);
    cout << "..." << endl;
    return 0;
}
```

# 逐个字符显示文本并使用 `sleep()` 减速

### 示例 4.14 - sleep.cpp

```cpp
#include <iostream>
#include <unistd.h> // 程序将在屏幕上显示一些文本
// 使用 `sleep()` 函数在执行期间进行暂停
using namespace std;      // 将使用标准标识符字符串, `cout` 和 `endl`
int main() {
    string message = "mmmOooOOOOOOooo!!!";
    cout << endl << endl << endl;      // 显示 3 个空行
    // 显示牛
    cout << "^" << endl;
    cout << "/\\" << endl;
    cout << "|" << endl;
    cout << "\\_/" << endl;
    // 开启粗体格式的转义序列
    cout << "\e[m";
    // 逐字母显示消息，每个字母延迟 1 秒
    for ( unsigned int position = 0; position < message.length(); position++) {
        cout << message.at( position ) << flush;
        sleep(1);
    } // 循环结束
    // 返回正常格式的转义序列
    cout << "\e[0m";
    cout << endl << endl << endl;      // 显示 3 个空行
    return 0;
}
```

上面的代码引入了几个新技巧。首先，它使用 `at()` 函数从消息的特定位置提取单个字符。它还使用 `for` 循环通过 `position` 变量来控制从消息中提取哪些字符。循环从消息的第一个字符开始，每次移动一个位置，一直直到最后一个字符。

在提取完每个字符后，程序都会在屏幕上显示它：

```cpp
cout << message.at( position ) << flush;
```

注意，字符串值中的字符是从位置 0 开始单独编号的，因此消息中的第一个字符位于位置 0，而不是位置 1。这就是为什么 `for` 循环从值 0 开始。我们称该字符串值是“零索引”的（zero-indexed）。

上面的语句使用了一个特殊字符 `flush`，它将在下一页详细解释。

102 | 在树莓派上使用 C++ 学习编程

在显示消息的每个字符后，程序调用了 `sleep()` 函数：

```cpp
sleep( 1 );
```

`sleep()` 函数会导致计算机暂停指定的时间（以秒为单位）。因此，`sleep( 1 )` 使计算机在显示消息 `mmmooooooooooo!!!` 中的每个字母后暂停 1 秒。

为了在你的程序中使用 `sleep()` 函数，你需要使用额外的代码库：

```cpp
#include <unistd.h>
```

这是 UNIX 标准库，允许你调用或激活特殊的操作系统函数。

然而，存在一个问题。理论上，告诉计算机逐个字符即时显示程序并暂停 1 秒，但在实践中，你会发现树莓派在延迟几秒钟后一次性显示出整行文本。

这是因为计算机试图通过将发送到输出通道（channel-out）的不同内容分组来提高程序的效率。当它遇到 `endl` 字符时，它会在单次操作中将所有内容作为一行完成的文本显示在屏幕上。

# 使用 `flush` 字符清除输出通道

我们可以通过“刷新”（flushing）输出通道（通往屏幕的路径）的内容，强制树莓派立即显示单个字符。任何等待显示的数据都会直接被放到屏幕上，而不会有任何进一步的延迟。

向输出通道发送一个名为 `flush` 的特殊字符（定义在 `std` 命名空间中），会告诉屏幕立即显示当前等待的任何内容。计算机不会等待任何其他显示语句——它将立即更新屏幕。

因此，之前的程序使用 `flush` 告诉计算机立即显示单个字符：

```cpp
cout << message.at( position ) << flush;
```

现在，牛消息中的每个单个字符都一个接一个显示在屏幕上，随后是一秒的暂停，而不是一次性显示。

![](img/0c86cf81300257fe2415e40f8fb03508_104_0.png)

关于处理文本和字符的更多细节，请参见“第 8 章：字符和文本字符串”。

这个特殊字符的最后一个示例使用了 `\b` 退格来调整文本行的位置：

# 示例 4.15 - backspace_char.cpp

```cpp
#include <iostream>      // 程序将在屏幕上显示一些文本
#include <unistd.h>       // 使用 `sleep()` 函数在执行期间进行暂停
using namespace std;    // 将使用标准标识符 `cout` 和 `flush`
int main() 
{
    // 显示原始消息
    cout << "Ready in... 3" << flush;
    sleep(1);
    // 使用退格字符向左移动一位并显示 "2"
    cout << "\b2" << flush;
    sleep(1);
    // 使用退格字符向左移动一位并显示 "1"
    cout << "\b1" << flush;
    sleep(1);
    // 使用回车字符回到行首
    cout << "\rAll systems GO!" << endl;
    sleep(1);
    return 0;
}
```

在显示第一条消息“Ready in...”后，`sleep()` 暂停 1 秒。

有几个 `cout` 语句使用了 `\b` 退格和 `flush` 字符，告诉屏幕立即覆盖并重绘其内容。例如，下方的 `cout` 语句使用 `\b` 退格字符在屏幕同一行上向左移动一个字符，然后用 "2" 代替原始的 "3"：

```cpp
cout << "\b2" << flush;
```

再次，该语句在倒计时期间使用 `flush` 字符立即更新显示：

```
Ready in... 1
```

最后一条语句使用 `\r` 回车字符回到行首，然后显示文本：

```cpp
```
