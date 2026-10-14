
## 注释

```cpp
    而不需要添加更多斜杠

}

out << "And Greetings from C++!"
```

- 步骤2 然而，你也可以在行末尾添加注释，以更好地描述其内容：

`cout << "Hello, world!"; // 这行输出单词 'hello, world.' \n 表示一个新行。`

注意，你不要在注释末尾加分号。这是因为这是被编译器忽略的行。

`helloworld.cpp`

```cpp
#include <iostream>

using namespace std;

int main() {
    // 我的第一个 C++ 程序
    cout << "Hello, world!"; // 这行输出单词 'hello, world.' \n 表示一个新行。
    // 这个注释
    注释行
    而不需要添加更多斜杠
}

out << "And Greetings from C++!"
```

- 步骤5 显然，如果你尝试编译代码时报错，提示缺少大括号 `}` 仅仅几次，那么可能是时候回去纠正了。代码编辑器中的颜色有助于你识别注释所在。

`helloworld.cpp`

```cpp
#include <iostream>

using namespace std;

int main() {
// 我的第一个 C++ 程序
    // 这个注释
    注释行
    而不需要添加更多斜杠
}

out << "And Greetings from C++!"
```

- 步骤3 你可以使用斜杠加星号来注释掉几行：

> // 这个注释
> 覆盖几行
> 而不需要添加更多斜杠 /*

只需记住用相反的星号和斜杠结束块即可。

- 步骤6 对于块注释，在 C++ 中一个良好的习惯是在注释的每个新行都添加一个星号，以便在继续代码之前关闭块：

> // 这个注释
> 覆盖几行
> 而不需要添加更多斜杠 /*

幸运的是，Geany 会自动执行此操作，但在使用其他 IDE 时要小心。

> / 这个注释可以
> 覆盖几行
> 而不需要添加更多斜杠 /*

## 变量

与 Python 相比，C++ 中变量的使用略有不同。在 Python 中，你可以简单地声明 `a` 等于 10 并为变量赋值。然而，在 C++ 中，变量在使用之前必须先根据类型进行声明。

### 变量的声明

你可以通过代码中的语句来声明 C++ 变量。你可以声明几种不同类型的变量。以下是其工作原理。

- 第 1 步：打开一个新的空白 C++ 文件，并输入通常的代码头文件：

```cpp
#include <iostream>

using namespace std;

int main()
{}
```

- 第 2 步：从创建变量 `a` 和 `b` 开始，其中一个值为 10，另一个值为 15。使用数据类型 `int` 来声明这些变量。在大括号内：

```cpp
int a;
int b;
a = 10;
b = 5;
```

```cpp
int result;
result = a + b;
cout << result;
```

将上述内容按照截图所示插入到代码中。

| `Variables.cpp` |
| :--- |
| `#include <iostream>`<br>`using namespace std;`<br>`int main()`<br>`{`<br>`int a;`<br>`int b;`<br>`a = 10;`<br>`b = 5;`<br>`}`<br>`cout << a;`<br>`cout << "\n";`<br>`cout << b;` |

![](img/21ee864cf339a60c6b969b7bda291087_131_0.png)

- 第 3 步：构建并运行代码，但它不会做什么，除了将变量 10 和 5 存储在整数 `a` 和 `b` 中。忽略关于变量设置但未使用的警告，代码仍然可以运行。输出变量的内容，添加：

```cpp
cout << a;
cout << "\n";
cout << b;
```

`cout << "\n";` 部分在 10 和 5 的输出之间放置了一个新行。

- 第 5 步：一旦声明变量，就可以为变量赋值。你输入的代码可能看起来如下：

```cpp
int a = 10;
int b = 5;
int result = a + b;
```

```cpp
cout << result;
```

- 第 8 步：之前的步骤创建了变量 `StartLives`，这是一个全局变量。例如，在游戏中，玩家的生命值会根据表现的好坏增加或减少。当玩家重新开始游戏时，`StartLives` 回到它的默认状态 3。在这里我们赋值了 3 行，然后减去 2 点剩余生命：

`Variables.cpp`

```cpp
#include <iostream>

using namespace std;

int StartLives = 3;

int main() {
    int a = 10;
    int b = 5;
    int result = a + b;
    cout << "program exited with code: " << result << endl;
    return 0;
}
```

`Variables.cpp`

```cpp
#include <iostream>

using namespace std;

int StartLives = 3;

int main() {
    StartLives -= 1;
    cout << "program exited with code: " << result << endl;
    return 0;
}
```

- 第 6 步：C++ 特有的，你也可以使用以下方法在声明变量时立即为其赋值：

```cpp
int a (10);
int b (5);
```

然后，从 C++ 2011 开始，使用大括号：

```cpp
int result {a+b};
```

- 第 9 步：现代 C++ 编译器比你为它声明的大多数程序员都要智能得多。尽管如此，你实际上可以使用它的所有功能：

```cpp
#include <iostream>

using namespace std;

auto pi = 3.141593;

int main()
```

```cpp
double area, radius = 1.5;
area = pi * radius;
cout << area;
```

`Variables.cpp`

```cpp
#include <iostream>

using namespace std;

auto pi = 3.141593;

int main() {
    double area, radius = 1.5;
    area = pi * radius;
    cout << area;
}
```

- 第 7 步：你可以创建全局变量，它们在函数外部声明并在任何函数中使用。你到为止使用的都是在函数内部使用的局部变量。例如：

```cpp
#include <iostream>

using namespace std;

int StartLives = 3;

int main()
{
    StartLives -= 1;
    cout << StartLives;
```

```cpp
#include <iostream>

using namespace std;

int StartLives = 3;

int main() {
    StartLives -= 1;
    cout << StartLives;
}
```

- 第 10 步：尽管我们说忽略第 3 步中的警告，但警告和错误之间是有区别的。在这种情况下，只是一个新值。数据类型，双精度浮点值，代码可以产生的是结果。本质上，你可以处理 `double` 但不能处理错误。

`Variables.cpp`

```cpp
#include <iostream>

using namespace std;

auto pi = 3.141593;

int main() {
    double area, radius = 1.5;
    area = pi * radius;
    cout << area;
}
```
