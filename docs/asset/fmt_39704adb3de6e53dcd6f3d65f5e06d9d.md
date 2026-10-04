
在这种形式下，`cin.get(a)` 值为 `cin`，所以第二个短语是 `>> b`。

# 应该 / 不该

- 当你需要跳过空白字符时，请使用提取运算符 (`>>`)。
- 当你需要检查每个字符（包括空白字符）时，请使用带字符参数的 `get()`。

# 从标准输入设备读取字符串

提取运算符 (`>>`) 可以用于填充字符数组，就像 `get()` 和 `getline()` 函数一样。

`get()` 的最终形式接受三个参数。第一个参数是字符数组的指针，第二个参数是读取的最大字符数加一，第三个参数是终止字符。这是函数重载的一个良好示例；根据函数调用传递的参数，选择合适的函数形式。

如果你在第二个参数输入 20，`get()` 将读取 19 个字符然后对字符串进行空终止，并存储在第一个参数中。第二个参数（终止字符）默认为换行符 (`'\n'`)。在读取到最大字符数之前遇到了终止字符，则会写入空字符并将剩余部分留在缓冲区中。

列表 16.6 展示了这种形式的 `get()` 的用法。

## 列表 16.6 使用字符数组使用 get()

```cpp
1:    // Listing 16.6 - Using get() with a character array
2:    #include <iostream>
3:
4:    int main() {
5:    {
6:        char stringOne[256];
7:        char stringTwo[256];
8:
9:        cout << "Enter string one: ";
10:       cin.get(stringOne,255);
11:       cout << "stringOne: " << stringOne << endl;
12:
13:       cout << "Enter string two: ";
14:       cin.get(stringTwo,255);
15:       cout << "stringTwo: " << stringTwo << endl;
16:       return 0;
17:  }
```

## 使用 cin.ignore() 清理输入

有时，你希望忽略行中剩余的字符，直到遇到行尾（EOL）或文件结束（EOF）为止。成员函数 `ignore()` 正是为了此目的。`ignore()` 接受两个参数：要忽略的最大字符数和终止字符。如果你编写 `ignore(80, '\n')`，在找到换行符之前，最多将忽略 80 个字符。随后换行符会被丢弃，`ignore()` 语句结束。列表 16.8 展示了 `ignore()` 的用法。

### 列表 16.8 使用 ignore()

```cpp
1: // Listing 16.8 - Using ignore()
2: #include <iostream.h>
3:
4: int main()
5: {
6:     char stringOne[255];
7:     char stringTwo[255];
8:
9:     cout << "Enter string one:";
10: cin.get(stringOne,255);
11: cout << "String one: " << stringOne << endl;
12:
13: cout << "Enter string two:";
14: cin.getline(stringTwo,255);
15: cout << "String two: " << stringTwo << endl;
16:
17: cout << "\n\nNow try again...\n";
18:
19: cout << "Enter string one:";
20: cin.get(stringOne,255);
21: cout << "String one: " << stringOne << endl;
22:
23: cin.ignore(255,'\n');
24:
25: cout << "Enter string two:";
26: cin.getline(stringTwo,255);
27: cout << "String Two: " << stringTwo << endl;
28: return 0;
29: }
```

```
Enter string one: once upon a time
String one: once upon a time
Enter string two: String two:
Now try again...
Enter string one: once upon a time
String one: once upon a time
Enter string two: there was a
String Two: there was a
```

在第 6 行和第 7 行，创建了两个字符数组。在第 9 行，提示用户输入，用户输入了 "once upon a time" 并回车。在第 10 行，使用 `get()` 读取此字符串。`get()` 填充 `stringOne` 并在换行符处终止，但将换行符留在了输入缓冲区。

在第 13 行，用户再次收到提示，但当 `getline()` 读取到缓冲区中已有的换行符时，它立即停止了，用户还没有输入任何内容。

在第 19 行，用户再次收到提示并输入了相同的第一行内容。这一次，在第 23 行，使用 `ignore()` 来“吃掉”换行符。因此，当执行第 26 行的 `getline()` 调用时，输入缓冲区是空的，用户可以输入故事的下一行。

## peek() 和 putback()

对象 `cin` 还有两个非常实用的方法：`peek()`，它查看但不提取下一个字符；以及 `putback()`，它将一个字符插入到输入流中。列表 16.9 展示了如何使用这些方法。

### 列表 16.9 使用 peek() 和 putback()

```cpp
1:    // Listing 16.9 - Using peek() and putback()
2:    #include <iostream>
3:
4:    int main()
5:    {
6:        char ch;
7:        cout << "enter a phrase: ";
8:        while (cin.get(ch))
9:        {
10:            if (ch == '!')
11:                cin.putback('$');
12:            else
13:                cout << ch;
14:                while (cin.peek() == '#')
15:                    cin.ignore(1,'#');
16:        }
17:       return 0;
18:   }
```

```
enter a phrase: Nowlis!thetime#forfun!
Now$istime$forfun$
```

在第 6 行，声明了一个字符变量 `ch`，在第 7 行，提示用户输入短语。该程序的目的是将任何叹号（！）转换为美元符号（$）并移除井号（#）。

只要获取到的不是文件结束结束（Linux 下为 Ctrl+D，其他操作系统为 Ctrl+C 或 Ctrl+D），程序就会继续循环。（记住 `cin.get()` 在文件结束时返回错误值）。如果当前字符是叹号，它会被丢弃，并将 $ 符号放回输入缓冲区；它将在下次时被读取。如果当前项不是叹号，则将其打印出来。会对下一个字符进行“窥视（peek）”，当发现井号时，它们会被移除。

这个示例并不是实现这两项操作最高效的方法（如果井号是第一个字符，它将无法找到），但它说明了这些方法的工作原理。这些方法相对冷门，所以不要花太多时间担心你何时会真正用到它们。把它们存入你的技巧箱吧；它们终会派上用场的。

## 列表 16.12 输出宽度

```cpp
// 列表 16.12 - 输出宽度
#include <iostream.h>
int main() {
    cout << "Start >>";
    cout.width(25);
    cout << 123 << " End\n";
    cout << "Start >>";
    cout.width(25);
    cout << 123 << " Next >>";
    cout << 456 << " End\n";
    cout << "Start >>";
    cout.width(4);
    cout << 123456 << " End\n";
    return 0;
}
```

```
Start >> 123 End
Start >> 123 << Next >>456 End
Start >>123456 << End
```

第一部分输出（第 6-8 行）在第 7 行设置宽度为 25 的字段内打印数字 123。这反映在输出的第一行中。

第二行输出首先在同样设置宽度为 25 的相同字段中打印值 123，然后打印值 456。注意，456 是在一个宽度被重置为仅足够大的字段中打印的；正如所述，`width()` 的效果仅持续到紧邻的输出。

最后的输出反映，设置一个比输出更小的宽度等同于设置一个仅足够大的宽度。

## 设置填充字符

通常，`cout` 用空格填充调用 `width()` 创建的空字段，如列表 16.12 所示。有时，你可能想用其他字符（如星号）填充该区域。要做到这一点，你需要调用 `fill()` 并将想要作为填充字符的字符作为参数传递。列表 16.13 展示了这一点。

## 列表 16.13 使用 fill()

```cpp
1:    // 列表 16.13 - fill()
2: 
3:    #include <iostream>
4: 
5:    int main()
6:    {
7:        cout << "Start >";
8:        cout.width(25);
9:        cout << 123 << "<End\n";
10:
11:
12:        cout << "Start >";
13:        cout.width(25);
14:        cout.fill('*');
15:        cout << 123 << "<End\n";
16:        return 0;
17:    }
```

```
Start > 123< End
Start *****************123< End
```

第 7–9 行重复了上一个示例的功能。第 12–15 行再次重复此，但这次在第 14 行，填充字符被设置为星号，这反映在输出中。

## 设置 iostream 标志

`iostream` 对象使用标志（flags）跟踪其状态。你可以通过调用 `setf()` 并传递一个预定义的枚举常量来设置这些标志。

当对象的某些或全部数据代表程序运行过程中可能改变的条件时，称该对象具有状态。

例如，你可以检查是否显示尾零（这样 20.00 就不会被截断为 20）。要开启尾零，调用 `setf(ios::showpoint)`。

枚举常量的作用域是 `iostream` 类（ios），因此使用全限定名 `ios::flagname` 进行调用，例如 `ios::showpoint`。

你可以使用 `ios::showpos` 在正数前加上加号 (+)。
你可以使用 `ios::left`、`ios::right` 或 `ios::internal` 来改变输出的对齐方式。

最后，你可以使用 `ios::dec`（十进制）、`ios::octal`（八进制—基八）和 `ios::hex`（十六进制）来设置数字的显示。这些标志也可以连接到插入操作符。列表 16.14 展示了这些设置。

作为额外奖励，列表 16.14 还引入了 `setw` 操纵符，它可以设置宽度，也可以与插入操作符连接。

## 列表 16.14 使用 setf

```
数字是 185
数字是 b9
数字是 \xb9
数字是 \xb9
数字是 \xb9
数字是: \xb9
```

分析：第 7 行，常量 `int number` 被初始化为值 185。这在第 8 行显示。

值在第 10 行再次显示，但这次连接了操纵符 `hex`，导致值以十六进制形式显示为 `b9`。（十进制形式的值 b 代表 11。11 乘以 16 等于 176；加上 9 总共 185。）

在第 12 行，设置了标志 `showbase`。这导致所有十六进制数前都加上前缀 0x，反映在输出中。

第 16 行，宽度设置为 10，值被推到最右侧。第 20 行，宽度再次设置为 10，但这次对齐方式设置为左侧，数字左对齐打印。

第 25 行，宽度设置为 10，但这次对齐方式是内部的。因此，0x 被左对齐打印，而值 b9 被右对齐打印。
最后，在第 29 行，宽度设置为 10。

## 流 与 printf()

大多数 C++ 实现都提供了 `printf()` 库。`printf()` 在某些方面比 `cout` 更容易使用，因为 `printf()` 不提供类型安全。`printf()` 不支持类，因此如果你想打印类的各种成员数据，你必须将每个访问器方法传递给 `printf()` 语句。

## 常用转换符

| 转换符 | 用于类型 |
| :--- | :--- |
| %s | 字符串 |
| %d | 整数 |
| %ld | 长整数 |
| %f | 浮点数 |
| %g | 浮点数 |
| %e | 科学计数法 |
| %o | 八进制 |
| %x | 十六进制 |
| %p | 指针 |

## 转换符说明

| 转换符 | 说明 |
| :--- | :--- |
| %s | 字符串 |
| %d | 整数 |
| %ld | 长整数 |
| %f | 浮点数 |
| %g | 浮点数 |
| %e | 科学计数法 |
| %o | 八进制 |
| %x | 十六进制 |
| %p | 指针 |

## 标志说明

| 标志 | 说明 |
| :--- | :--- |
| showpoint | 显示小数点点 |
| showpos | 在正数前显示加号 |
| left | 左对齐 |
| right | 右对齐 |
| internal | 内部对齐 |
| dec | 十进制 |
| octal | 八进制 |
| hex | 十六进制 |
| showbase | 显示进制前缀（如 0x） |

## 列表 16.15 使用 printf()

```cpp
1:    // 列表 16.15 - printf()
2: 
3:    #include <stdio.h>
4: 
5:    int main()
6:    {
7:        printf("hello world\n");
8: 
9:        char *phrase = "Hello again!\n";
10:    printf("%s",phrase);
11: 
12:        int x = 5;
13:        printf("%d\n",x);
14: 
15:        char *phraseTwo = "Here's some values: ";
16:        printf("%s",phraseTwo);
17: 
18:        int y = 7, z = 35;
19:        printf("%d %d\n",y,z);
20: 
21:        long longVar = 98456;
22:        printf("%ld\n",longVar);
23: 
24:        float floatVar = 8.8;
25:        printf("%f\n",floatVar);
26: 
27:        char *phraseThree = "Formatted: ";
28:        printf("%s%d %ld %f\n",phraseThree,y,z,floatVar);
29:        return 0;
30:    }
```
