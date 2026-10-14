

这些示例展示了构造字符串对象的三种最常见方法。字符串 s1 使用括号中的字面量字符串创建。字符串 s2 使用赋值创建，但其他方式与之相同。字符串 s3 使用 s1 的副本创建。然而，由于字符串类使用引用计数，字符串对象 s1 和 s3 在内存中只存储一份字符串数据。清单 22.1，sdeclare.cpp，演示了构造字符串对象的其他一些方法。

```
```cpp
#include <iostream>
#include <string>
#include <vector>

void ShowString(const char* s, const string& sr)
{
    string sEmpty;
    string sFromLiteral("Stringing in the rain");
    string sFromString(sFromLiteral);
    string sFromAssign = "A string in time saves nine";
    string sFilled(40, '#');
    string sPartial(sFromAssign, 9, 7);
    char buffer[5] = { 'a', 'b', 'c', 'd', 'e' };
    string sFromPointers(buffer + 1, buffer + 5);

    vector<char> cVector(buffer, buffer + 5);
    string sFromIterators(cVector.begin(), cVector.end());
}

int main()
{
    ShowString("sEmpty", sEmpty);
    ShowString("sFromConst", sFromLiteral);
    ShowString("sFromString", sFromString);
    ShowString("sFromAssign", sFromAssign);
    ShowString("sFilled", sFilled);
    ShowString("sPartial", sPartial);
    ShowString("sFromPointers", sFromPointers);
    ShowString("sFromIterators", sFromIterators);
    return 0;
}

void ShowString(const char* s, const string& sr)
{
    cout << s << ": " << sr << endl;
    cout << " length:" << sr.length();
    cout << " size:" << sr.size();
    cout << " capacity:" << sr.capacity();
    cout << endl;
}
```
```

编译并运行测试程序以查看多个测试字符串的结果（为节省空间，我只在此处显示部分输出语句）：

```
```text
$ g++ sdeclare.cpp
$ ./a.out
sEmpty:
```
```

```
length:0 size:0 capacity:0
sFromConst : Stringing in the rain
length:21 size:21 capacity:32
...
sFilled : ################################
length:40 size:40 capacity:64
sPartial : in time
length:7 size:7 capacity:16
```

要使用特定字符填充字符串，请使用如下语句

```
string sFilled(40, '#');
```

这会创建一个由井号字符填充的 40 个字符的字符串。（有些人称之为磅符号。有见识的 Linux 大师知道它们是克林贡战舰。）字符串的容量为 64（参见前面的输出）。这是因为字符串类试图在不浪费的情况下高效地分配空间。在此示例中，结果字符串在需要新的内存分配之前还可以再增长 24 个字符。

要显式为字符串预留额外空间，您应该能够像以下语句中那样提供长度参数：

```
string sReserve("Short and Sweet", 64);
```

尽管这可行，但字符串中剩余的空间具有内存中该位置恰好存在的字节值。换句话说，前面的语句将字符串的长度、大小和容量都设置为 64。可能，这不是您想要的效果。作为变通方法，您可以将空字符赋给所需容量的字符串对象：

```
string sReserve(64, '\0');
```

您也可以指定要用于初始化新字符串对象的字符范围，例如以下语句：

```
string sFromAssign = "A string in time saves mine";
...
string sPartial(sFromAssign, 9, 7);
```

您还可以使用标准模板库容器类提供的迭代器函数。例如，以下使用字符向量构造字符串对象，该向量从前面的缓冲区初始化：
vector<char> cVector(buffer, buffer + 5);
string sFromIterators(cVector.begin(), cVector.end());

这是一种构造简单字符串对象的极其复杂的方法，但它展示了可用的各种方法。无论您的字符数据来源如何，您都可以将其传递给字符串类并获得一个正确构造的对象作为回报。（有关迭代器和标准模板容器类（如 vector）的信息，请参阅第 24 章“构建标准容器”。）

## READING AND WRITING string OBJECTS

大多数设计良好的 C++ 类提供输入和输出服务，字符串类也不例外。使用 I/O 流语句读写字符串对象。例如，以下语句将字符串写入标准输出：

```
string s("Write me right out");
cout << s << endl;
```

类似的语句提示用户输入字符串：

```
cout << "Enter a string: ";
cin >> s;
```

然而，第二条语句只读取输入的第一个单词，因为空白（例如空格和制表符）会终止输入。要读取包含空格和其他空白的整个字符串，请使用包含字符串头提供的 getline() 函数。直接调用该函数——它不是类成员函数。例如，以下语句从标准输入读取一个字符串到字符串对象中：

```
string s;
getline(cin, s, '\n');
```

为 getline() 指定三个参数：一个 istream 对象引用（本例中为 cin）、一个字符串对象如 s，以及应终止输入的字符（此处为换行控制）。清单 22.2，rstrings.cpp，展示了如何使用此技术通过字符串对象读取文本文件。

## LISTING 22.2 RSTRINGS.CPP

```
#include <iostream.h>
#include <fstream.h>
#include <string>

int main(int argc, char *argv[])
{
    string s; // String object

    if (argc <= 1) {
        cerr << "Error: filename missing" << endl;
```

