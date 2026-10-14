

## 表 7.3 按位运算符

| 运算符 | 描述 | 示例 |
|---|---|---|
| & | 按位与 | C = A & B; |
| \| | 按位包含或 | C = A | B; |
| ^ | 按位异或 | C = A ^ B; |
| << | 左移位 | C = A << B; |
| >> | 右移位 | C = A >> B; |
| ~ | 按位取反 | C = ~A; |

在表达式中，表 7.3 中的前三个按位运算符根据逻辑与（&）、包含或（|）和异或（^）的规则组合两个操作数。接下来两个运算符 << 和 >> 将值中的位向左和向右移动。不要将其与 C++ I/O 流运算符混淆，它们看起来相同，但在上下文中用法不同。

最后一个运算符 ~ 翻转其操作数值中的位，将所有零位变为一，所有一位变为零，并生成一个称为按位取反的结果。运算符 ~ 是单目运算符，需要一个操作数。其他的是二元运算符，应用于两个操作数。

按位运算符的一个典型用途是掩码值，使用另一个值中的位对一个值中的位应用布尔运算。例如，使用异或运算符执行此操作可以加密文本，使其无法阅读但只需重复掩码操作即可轻松恢复。列表 7.2，encrypt.cpp，演示了这个基本思想。

## 列表 7.2 ENCRYPT.CPP

```
#include <iostream.h>
#include <string.h>

char input[128];   // String to encrypt
char mask;         // Exclusive-OR mask
unsigned int i;    // for-loop control variable

main()
{
cout << "Enter a string to encrypt: ";
cin.getline(input, sizeof(input));
cout << "Enter a single-character mask: ";
cin >> mask;
cout << "Original string == " << input << endl;
for (i = 0; i < strlen(input); i++)
input[i] = input[i] ^ mask;
cout << "Encrypted string == " << input << endl;
for (i = 0; i < strlen(input); i++)
input[i] = input[i] ^ mask;
cout << "Decrypted string == " << input << endl;
return 0;
}
```

使用以下命令编译程序：

```
$ g++ encrypt.cpp
$ ./a.out
```

提示时，输入要加密的字符串以及单个字符掩码，如本示例运行所示：

```
Enter a string to encrypt: Social Security #: 123-45-6789
Enter a single-character mask: @
Original string == Social Security #: 123-45-6789
Encrypted string == r/[@!], r*#52}49 cz qrsutmvwxy
Decrypted string == Social Security #: 123-45-6789
```

加密后的字符串是乱码，但正如输出的最后一行所示，原始文本很容易恢复。为了加密输入字符串，程序执行此 for 语句：

```
for (i = 0; i < strlen(input); i++)
    input[i] = input[i] ^ mask;
```

（你在第 9 章“控制程序流程”中会遇到 for 语句。）循环对输入字符串中的每个字符执行第二行的语句。每个字符都使用按位异或运算符（^）与掩码字符组合。因为异或运算符充当位切换器，使用相同的掩码重复此循环可以恢复原始数据。赋值可以用简写语句更简洁地写成：

```
input[i] ^= mask;
```

这执行的操作与前一个语句完全相同——它使用异或运算符将掩码应用于字符 input[i] 并将该操作的结果赋给 input[i]。然而，使用简写运算符，只需要对数组元素的引用一次。

### 警告
出于几个原因，本节中的 encrypt.cpp 程序并不是加密敏感数据的可靠方法。首先，只需编写一个程序将整个 ASCII 字符集应用于加密数据，就很容易发现单个字符掩码。另一个原因是，数据中的任何零字节都会被加密为掩码的值。然而，如果你只是想加密文本以防止好奇的眼睛窥视，简单的异或掩码可以是一种有效的加密技术。

## 运算符提示

以下各节包含一些使用本章介绍的 C 和 C++ 运算符的提示和简写表达式。

