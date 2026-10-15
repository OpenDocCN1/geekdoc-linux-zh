
使用以下两个命令编译并运行 `rchar.cpp`。该程序可以读取并显示任何文本文件，但这里第二个命令告诉它读取并显示其自己的源代码：

```
$ g++ -o rchar rchar.cpp
$ ./rchar rchar.cpp
```

## 注意

由于本章中的一些程序相互依赖，所有编译命令都使用 `-o` 选项为编译后的代码文件指定一个不同于通常的 `a.out` 的名称。

`rchar.cpp` 中的 `main()` 函数首先检查你在命令行上是否提供了文件名。如果没有（`argc` 小于或等于 1），程序会显示错误消息并退出。以下语句尝试打开指定的文件：

```
ifstream ifs(argv[1], ios::in);
```

如果成功，`ifs` 对象就可以作为输入流语句的源使用。例如，一个简单的 `while` 循环从文件中读取所有字符并使用输出流语句显示它们：

```
while (ifs.get(c))
    cout.put(c);
```

# 一次写入一个字符的文本

创建和写入文本文件同样简单，如清单 20.2，`wchar.cpp` 所演示。

## LISTING 20.2 WCHAR.CPP

```
#include <iostream.h>
#include <fstream.h>
#include <stdlib.h>

int main(int argc, char *argv[])
{
    if (argc <= 1) {
        cerr << "Error: filename missing" << endl;
        exit(1);
    }

    ifstream ifs(argv[1], ios::in);
    if (ifs) {
        cerr << "Error: " << argv[1] << " already exists" << endl;
        cerr << "  Specify a different filename" << endl;
        exit(2);
    }

    ofstream ofs(argv[1], ios::out);
    if (!ofs) {
        cerr << "Error: unable to write to " << argv[1] << endl;
        exit(3);
    }

    ofs << "1: A string" << endl;
    ofs.put('2');
    ofs.put(':');
    ofs.put(' ');
    ofs.put('C').put('h').put('a').put('r').put('s');
    ofs << endl;

    return 0;
}
```

通过发出以下命令编译并运行该程序。该程序不会覆盖现有文件：

```
$ g++ -o wchar wchar.cpp
$ ./wchar test.txt
```

假设 `test.txt` 之前不存在，`wchar.cpp` 会向文件写入文本。使用以下命令检查文件的内容：

```
$ cat test.txt
1: A string
2: Chars
```

如果你再次尝试运行该程序，它会检测到 `test.txt` 的存在并以错误消息退出：

```
$ ./wchar test.txt
Error: test.txt already exists
  Specify a different filename
```

如果指定的文件不存在，该程序会使用 `ofstream` 类的对象创建一个新文件：

```
ofstream ofs(argv[1], ios::out);

if (!ofs) {
    ...
}
```

如果表达式 `(!ofs)` 为真，则发生错误，程序退出。否则，程序继续使用输出语句向文件写入文本。以下语句向文件写入字符串和换行字符：

```
ofs << "1: A string" << endl;
```

And this writes a single character:

```
ofs.put('2');
```

Or, you could use the following statement to do the same:

```
ofs << '2'; // Same as preceding
```

顺便说一下，因为 `put()` 成员函数返回 `ostream &`（`ostream` 类对象的引用，`ios` 的一个祖先类），你可以把多个 `put()` 函数调用串联起来，形成一种看起来很奇怪的构造，比如这样：

```
ofs.put('A').put('B').put('C');
```

我不喜欢这种晦涩难懂且 `tricky` 的语句，但我在这里提到它是因为我在 C++ 程序中见过这种技术。以下写法更清晰，产生相同的结果，而且看起来也不那么奇怪：

```
cout << 'A' << 'B' << 'C';
```

## 按行读取文本

许多如果不是大多数的话，文本文件都是按可变长度的行组织的，以换行控制字符分隔。使用本节中的技术可以一次按行读取文本文件。额外好处是，这通常比一次读一个字符快得多，虽然缺点是需要从一开始就假设一个最大行长度。清单 20.3，`rline.cpp`，与 `rchar.cpp` 类似，但它一次按行读取指定的文本文件并报告文件中的字符数和行数：

## LISTING 20.3 RLINE.CPP

```
#include <iostream.h>
#include <fstream.h>
#include <stdlib.h>
#include <string.h>
#define BUFLEN 128
int main(int argc, char *argv[])
{
    if (argc <= 1) {
        cerr << "Error: filename missing" << endl;
        exit(1);
    }
    ifstream ifs(argv[1], ios::in);
    if (!ifs) {
        cerr << "Error: unable to open " << argv[1] << endl;
        exit(2);
    }
    char buffer[BUFLEN];
    long nc = 0, nl = 0;
    while (!ifs.eof()) {
ifs.getline(buffer, sizeof(buffer), '\n');
if (!ifs.eof() && strlen(buffer) == 0) {
    nc += strlen(buffer);
    nl++;
    cout << buffer << endl;
}
cout << endl << endl << "Total characters: " << nc;
cout << endl << "Number of lines: " << nl << endl;
return 0;
}
```

使用以下命令编译并运行程序。你可以指定任何要读取和显示的文本文件名——这里第二个命令显示程序自身的源代码文件：

```
$ g++ -o rline rline.cpp
$ ./rline rline.cpp
```

程序使用与逐字符读取文本相同的方式打开文件。要读取文本行，程序调用 `getline()` 成员函数，使用以下语句：

```
ifs.getline(buffer, sizeof(buffer), '\n');
```

`buffer` 是一个 `char` 数组。调用 `getline()` 并指定目标、缓冲区大小和行结束字符可确保整行被读取。以下语句只读取下一个单词（由空白分隔的文本）：

```
ifs >> buffer; // ???
```

与其这样，最好预先用 `setw()` 操纵符设置缓冲区大小。例如，要一次按单词读取文件，包含 `iomanip.h` 头文件并使用如下片段中的语句：

```
#include <iomanip.h>
...
ifs >> setw(BUFLEN) >> buffer;
```

这也能确保语句不会覆盖缓冲区的末尾，尽管 GNU C++ 似乎无论如何都不会这样做。

示例 `rline.cpp` 程序还演示了一种通过调用 `eof()` 成员函数来检测文件结束的方法，该函数参考文件流对象。此函数使得编写一个简单的 `while` 循环变得容易，该循环在处理完文件中的每一丝数据后结束：

```
while (!ifs.eof()) {
    ifs.getline(buffer, sizeof(buffer), '\n');
    // Process line in buffer
}
```

## 按行写入文本

本节中四种基本文本文件技术中的最后一种解释了如何一次按行写入文本文件。清单 20.4，`wine.cpp`，演示了该方法。
