

# 表 20.1 继续

| 常量 | 标准 | 效果 |
|---|---|---|
| nocreate | no | 如果文件尚不存在，则不创建新文件。用于检查文件是否存在。 |
| noreplace | no | 如果文件已存在，则不覆盖文件。 |
| out | yes | 打开文件以进行输出（写入）。 |
| trunc | no | 打开并截断现有文件。写入文件的新信息会替换文件当前内容。 |

不幸的是，表 20.1 中的常量在 ios 类的所有实现中并不相同。open_mode 枚举类型标识符甚至可能被命名为没有下划线的 openmode。GNU C++ 定义了表中列出的所有 open_mode 常量，大多数现代 ANSI C++ 编译器也是如此。然而，如果你编写代码以支持其他系统，不要对 open_mode（或 openmode）类型之间的差异感到惊讶。

> Tip
> GNU C++ 在文件 streambuf.h 中将 open_mode 定义为 ios 类的成员。

通过在逻辑或表达式中组合常量来指定多个选项。例如，你可以像这样定义一个符号常量 OFSMODE：

```
#define OFSMODE ios::out | ios::app
```

或者，更好的是，你可以使用如下语句定义一个类型为 open_mode 的 const 值

```
const ios::open_mode OFSMODE = ios::out | ios::app;
```

无论你选择哪种方法，都将 OFSMODE 常量传递给 ofstream 类构造函数的第二个参数，如本示例所示：

```
ofstream ofs("newfile.txt", OFSMODE);
```

当然，你也可以直接使用如下语句将多个选项传递给构造函数

```
ofstream ofs("newfile.txt", ios::out | ios::app);
```

在本章中，为简单起见，示例使用这种形式。然而，由于 open_mode 常量之间存在差异，为了更好的可移植性，最好定义一个列出你想要使用的模式的常量。

创建或覆盖文件后，始终检查 ofstream 对象是否准备好使用。你可以使用 if 语句执行此检查，如下所示：

```
#include <iostream.h>
#include <fstream.h>
#include <stdlib.h>
...
ofstream ofs("newfile.txt", ios::out);
if (!ofs) {
```

```
cerr << "Error: unable to create file" << endl;
    exit(1);
}
```

前三行包含了必要的库头文件。为了避免重复，本章后面的示例不再显示这些相同的行。构造 ofstream 对象 ofs（如果需要可以是另一个名称），为输出打开 newline.txt，如果文件尚不存在则创建该文件。if 语句测试文件是否已正确附加到 ofs 对象。如果没有，程序会向 cerr 写入错误消息并通过调用标准库的 exit() 函数退出。

## 对象有效性检查

许多程序员质疑 if 语句的表达式 (!ofs)。如果 ofs 是 ofstream 类的对象，你可能会想知道该表达式如何有意义。C 程序员尤其习惯于这种类型的表达式与指针一起使用，但 ofs 是一个变量——一个对象——而不是指针，那么 (!ofs) 如何检查其有效性呢？

答案隐藏在 ios 类中，该类使用以下内联声明重载了 C++ not 运算符 !() 函数：

```
int operator!() const { return fail(); }
```

由于运算符被重载，像以下这样的语句会调用 operator!() 函数，该函数返回 I/O 流 fail() 函数的值，如下所示：

```
if (!ofs) {
    ...
}
```

这是一个很好的例子，说明如何使用运算符重载使程序更易于理解。前面的是等价于稍微不太清晰的表达式

```
if (ofs.fail()) {
    ...
}
```

## 打开文本文件

打开文件以进行输入与创建或覆盖新文件类似。使用 ifstream 类，如以下示例代码所示，打开名为 oldfile.txt 的文件：

```
ifstream ifs("oldfile.txt", ios::in);
if (!ifs) {
    cerr << "Error: unable to open file" << endl;
    exit(1);
}
```

对象 ifs 由 ifstream 类构造并使用文件名和 open_mode 常量初始化。if 语句使用 ios 类的重载 operator!() 函数对对象进行操作，以测试操作是否成功。如果成功，对象——以及附加的文件——就可以进行读取；否则，程序会以错误消息停止。

