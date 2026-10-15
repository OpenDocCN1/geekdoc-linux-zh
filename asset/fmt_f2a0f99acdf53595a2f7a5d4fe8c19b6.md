
```
#include <iostream.h>
#include <fstream.h>
#include <stdlib.h>
#include <string.h>
#include <string>

#define STR "2: Another literal string"

int main(int argc, char *argv[])
{
    if (argc <= 1) {
        cerr << "Error: filename missing" << endl;
        exit(1);
    }
    ifstream ifs(argv[1], ios::in);
    if (!ifs) {
        cerr << "Error: " << argv[1] << " already exists" << endl;
        cerr << "        Specify a different filename" << endl;
        exit(2);
    }
    ofstream ofs(argv[1], ios::out);
    if (!ofs) {
        cerr << "Error: unable to write to " << argv[1] << endl;
        exit(3);
    }

    ofs << "1: A literal string" << endl;
    ofs.write(STR, strlen(STR));
    ofs << endl;
    char *c = "String addressed by pointer";
    ofs << "3: " << c << endl;
    string string_object("4: A string object");
    ofs << string_object << endl;
    return 0;
}
```

使用以下命令编译并运行程序：

```
$ g++ -o wine wine.cpp
$ ./wine wine.txt
```

通过输入以下命令检查新文件的内容：

```
$ cat newfile.txt
1: A literal string
2: Another literal string
3: String addressed by pointer
4: A string object
```

与 `wchar.cpp` 中一样，如果指定的文件已存在，程序会显示错误信息并退出。可以通过再次输入相同的文件名来测试：

```
$ ./wline newfile.txt
Error: newfile.txt already exists
Specify a different filename
```

检测已存在文件并打开文件进行输出的代码与 `wchar.cpp` 中的相同。程序的不同之处在于它如何将文本行写入输出。基本上，有两种选择。你可以使用输出流语句来写入字符串，例如：

```
ofs << "Write me to disk!" << endl;
```

或者，你可以调用 `write()` 成员函数并传入两个参数：指向字符串的指针和要写入的字符数。例如，这会写入由 `char` 指针 `s` 寻址的字符串，并使用标准 `string.h` 头文件中声明的 `strlen()` 函数：

```
#include <string.h>
...
ofs.write(s, strlen(s));
```

不过这样不会写入换行字符，因此通常仅在写入字符串的一部分时才有用。

`wline.cpp` 程序中的最后两个语句演示了如何构造并将 C++ 字符串对象写入输出文件：

```
string string_object("4: A string object");
ofs << string_object << endl;
```

> 注意

> 第 22 章“精通标准 `string` 类”更详细地解释了如何使用字符串对象。

## 二进制文件流

不要在 GNU C++ 文件流库中寻找二进制文件操作。没有。尽管你可以为二进制访问打开文件——这是大多数磁盘操作系统，包括 Linux 所提供的功能——但以其原生形式读写二进制数据，例如浮点值，则是留给程序员征服的高峰。

所需步骤很少在 C++ 编程书籍中涉及，为完成此任务，我在本节中开发了三个新类。这些类为所有原生 C++ 数据类型提供二进制文件 I/O——并且你可以轻松添加新类型，例如你自己的类。以下各节中的示例程序解释了如何使用这些类。我们需要四种基本功能：

- 将任何对象的一个或多个字节写入文件。
- 从文件读取一个或多个字节到对象中。
- 将任意大小的对象转换为字节。
- 将一组字节转换为任意对象。

### 介绍二进制文件流

以几乎与构造其他文件对象相同的方式构造二进制文件流对象——例如文本文件。然而，指定 `ios::binary` `open_mode` 常量。例如，要创建一个新的二进制文件，使用如下代码构造一个 `ofstream` 对象：

```
ofstream ofs("newfile.dat", ios::out | ios::binary);
if (!ofs) {
  cerr << "Error: unable to create or write file" << endl;
  exit(1);
}
```

> 注意

> 旧的 C++ 编译器可能使用 `ios::bin` 替代较新的 ANSI C++ 和 GNU C++ 常量 `ios::binary`。

要打开现有二进制文件进行读取，使用类似的编程构造一个 `ifstream` 对象：

```
ifstream ifs("oldfile.dat", ios::in | ios::binary);
if (!ifs) {
  cerr << "Error: unable to open file" << endl;
  exit(1);
}
```

不幸的是，尽管上述代码打开了用于二进制输入和输出的文件，但 `ofs` 和 `ifs` 对象没有用于读写二进制数据的规定。为了检查这个问题，并理解本节中描述的解决方案，先看看错误的做法会很有帮助。

### 错误的解决方案

> 注意

> 本节中的编程在 CD-ROM 的 `src/c20/wrong.cpp` 文件中。由于该程序演示了不正确的技术，因此此处未列出。但是，你可以使用命令 `g++ wrong.cpp` 然后 `./a.out` 运行它。

按前一节中所述构造输入和输出文件流似乎可行——直到你尝试使用文件对象在文件中读写二进制值时为止。例如，考虑如果像这样创建一个新文件会发生什么：

```
ofstream ofs("test.dat", ios::out | ios::binary);
```

认为这创建了一个新的文件 `test.dat`，准备以二进制格式写入数据，然后你尝试使用如下语句输出一些 `double` 浮点值：

```
if (ofs) {
  double d = 3.14159;
  ofs << d;  // ???
  ofs << d * d;  // ???
}
ofs.close();
```

关闭输入文件之后，你尝试读取文件的内容，方法是构造一个输入流对象并使用如下语句：

```
ifstream ifs("test.dat", ios::in | ios::binary);
if (ifs) {
    double d;
    ifs >> d;  // ???
    cout << "d == " << d << endl;
    ifs >> d;  // ???
    cout << "d * d == " << d << endl;
}
```

程序看起来运行得很顺利，但报告的结果明显是错误的。程序显示的内容如下：

```
$ ./a.out
d == 3.1416
d * d == 0.86959
```

哪里出了问题？第一个值看起来没问题，但π的平方几乎不可能是0.86959。使用Linux的 `hexdump` 工具检查文件数据，为解开这个神秘的bug提供了线索。如果你已经编译并运行了 `wrong.cpp` 程序，请输入以下命令来检查 `test.dat` 的内容：

```
$ hexdump -bc test.dat
0000000 063 035 056 061 064 061 065 071 071 056 071 070 066 071 065 071
0000020 3   . 1 4 1 5 9 9 . 8 6 9 5 9
```

文件的内容表明，尽管文件是以二进制I/O方式打开的，但数据却以文本形式存储。这是因为C++ I/O流的设计目标是将二进制值转换为文本，并且它们不会根据文件的打开方式以任何方式改变这一行为。

当程序读取文件时，标准输入语句执行相反的任务：在这种情况下，读取的第一个值为3.141599，第二个值为0.86959。由于这两个值是一个接一个写入的，文件中没有任何迹象表明第二个值实际上应该是9.86959，于是输入流错误地“假定”小数点分隔了两个值。

这是一个有趣的问题，不过幸运的是，正如下一节所解释的，解决起来并不太难。

### 正确的解决方案
