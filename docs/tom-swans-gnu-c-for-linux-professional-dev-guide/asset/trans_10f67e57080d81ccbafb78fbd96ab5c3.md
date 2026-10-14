

Listing 20.6, rdouble.cpp, 通过读取 wdouble.cpp 写入到 test.dat 中的二进制 double 值完成了整个说明。该程序展示了如何从 ifstream 派生一个新类，以便以二进制形式读取特定类型的值。

## LISTING 20.6 RDOUBLE.CPP

```
#include <iostream.h>
#include <fstream.h>
#include <stdlib.h>

#define FILENAME "test.dat"

class bifstream: public ifstream {
public:
    bifstream(const char *fn)
        : ifstream(fn, ios::in | ios::binary) { }
    void readBytes(void *p, int len);
    bifstream & operator>> (double &);
};

bifstream & bifstream::operator>> (double &d)
{
    readBytes(&d, sizeof(d));
    return *this;
}

int main()
{
    bifstream bifs(FILENAME);
    if (!bifs) {
        cerr << "Error: unable to open " << FILENAME << endl;
        cerr << " compile wdouble.cpp and run first\n";
        exit(1);
    }
    double d;
    long count = 0;
    cout.precision(8);
    bifs >> d;
    while (!bifs.eof()) {
        cout << ++count << ": " << d << endl;
        bifs >> d;
    }
    return 0;
}

void bifstream::readBytes(void *p, int len)
{
    if (!p) return;
    if (len <= 0) return;
    read((char *)p, len);
}
```

要运行完整测试，请编译 `wdouble.cpp` 和 `rdouble.cpp`，然后一起运行这两个程序。以下是完整的命令和输出行：

```
$text
$ g++ -o wdouble wdouble.cpp
$ g++ -o rdouble rdouble.cpp
$ ./dwouble
Writing to test.dat
$ ./rdouble
1: 3.14159
2: 9.869587
3: 9.999999
4: 4.7e-08
```
```

将 `rdouble.cpp` 的输出与 `wdouble.cpp` 中写入磁盘二进制值的语句进行比较。它们与预期结果一致。这表明，与其以文本形式读写数据，现在派生的 `bifstream` 和 `bofstream` 类以原生二进制格式处理数据。新的 `bifstream`（binary-input-file-stream）类派生自 `ifstream`。其构造函数按如下方式声明并内联实现：

```
bifstream(const char *fn):
  ifstream(fn, ios::in | ios::binary) { }
```

与 `bofstream` 构造函数一样，这段代码只是调用其祖先类构造函数，传递一个文件名字符串和两个打开常量以将文件打开为二进制输入。`bifstream` 类还声明了如下函数 `readBytes()`：

```
void readBytes(void *, int);
```

这是 `bofstream::writeBytes()` 函数的对应物，并且声明了相同的参数——指向要写入的数据对象的指针及其以字节为单位的大小。`readBytes()` 函数执行三条语句以二进制形式读取值：

```
if (!p) return;
if (len <= 0) return;
read((char *)p, len);
```

如果指针为 NULL，或请求的大小小于或等于零，则函数不执行任何操作。否则，它调用继承的 `read()` 函数，从打开的文件中输入 `len` 字节到指针 `p` 指定的地址。

最后，`bifstream` 类重载了 C++ 输入流运算符 `>>`，声明如下：

```
bifstream & operator>> (double &);
```

由于此声明，任何将 double 变量写入 `bifstream` 对象的语句都会调用重载函数。其实现调用 `readBytes()` 函数来执行实际的输入任务：

```
readBytes(&d, sizeof(d));
return *this;
```

与之前一样，d 是要从文件中加载的 double 对象。首先，readBytes() 将 sizeof(d) 字节读入 d 的地址所在的内存中。然后，函数返回其自身的 bifstream 对象，以便级联输入语句例如以下语句能正常工作：

bifs >> d1 >> d2 >> d3;

## CLASSES FOR BINARY FILE I/O

扩展前两节中的概念可得到 bofstream 和 bifstream 类的多功能版本。借助下面修订后的类，你可以以二进制形式读写所有原生 C++ 数据类型。Listing 20.7, bstream.h，声明了这两个类。

## LISTING 20.7 BSTREAM.H

```
#include <iostream.h>
#include <fstream.h>

// Binary output file stream

class bofstream: public ofstream {
public:
    bofstream(const char *fn)
        : ofstream(fn, ios::out | ios::binary) { }
    void writeBytes(const void *, int);
    template <class T>
    bofstream & operator<< (const T & data);
};

template <class T>
bofstream & bofstream::operator<< (const T & data)
{
    writeBytes(&data, sizeof(data));
    return *this;
}

// Binary input file stream

class bifstream: public ifstream {
public:
    bifstream(const char *fn)
        : ifstream(fn, ios::in | ios::binary) { }
    void readBytes(void *, int);
    template <class T>
    bifstream & operator>> (T & data);
};

template <class T>
bifstream & bifstream::operator>> (T & data)
{
    readBytes(&data, sizeof(data));
    return *this;
}
```

