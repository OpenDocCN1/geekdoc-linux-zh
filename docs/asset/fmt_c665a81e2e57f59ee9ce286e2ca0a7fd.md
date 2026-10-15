
实现模块提供了 `TAnyClass` 模板中成员函数 `GetData()` 的内容。该成员函数仍然是模板形式——它使用占位类型 `T`——但其语句块提供了函数的功能——在本例中，只是返回对象的私有数据，无论它是什么。

同样，模板函数的语句使用 C++ `new` 运算符构造 `TAnyClass<T>` 类型的对象，并将指向该对象的指针作为函数的结果返回。同样，这仍然是一个模板。函数的实际实例化在为 `T` 提供数据类型时才会发生。

不幸的是，麻烦就从这里开始。清单 17.7，`usemtemplate.cpp`，尝试通过包含头文件来使用模板类和模板函数。然而，结果是一系列令人困惑的链接器错误。

```cpp
#include <iostream.h>
#include "string"
#include "template.h"

int main()
{
    TAnyClass<int> int_object(123);
    cout << "int_object  " << int_object.GetData() << endl;

    TAnyClass<double> double_object(3.14159);
    cout << "double_object  " << double_object.GetData() << endl;

    TAnyClass<string> string_object("String object");
    cout << "string_object  " << string_object.GetData() << endl;

    string s("Dynamic string object");
    TAnyClass<string> *p = MakeObject(s);
    cout << "*p = " << p->GetData() << endl;
    delete p;

    return 0;
}
```

要查看链接器找不到模板实例化时产生的错误，请注释掉或删除 `template.cpp` 文件（参见清单 17.6）中从注释“Cut Here”到末尾的行。然后输入以下命令：

```text
$ g++ -c template.cpp
$ g++ usemtemplate.cpp template.o
/tmp/cca011931.o: In function `main':
/tmp/cca011931.o(.text+0x1e): undefined reference to
`TAnyClass<int>::GetData(void) const'
```

模板模块（`template.cpp`）可以编译，但尝试链接主程序和模块时会产生未定义引用错误。虽然我在这里只展示了一个这样的错误，但如果你跟着操作，屏幕上会出现其他几个错误。问题在于 GNU C++ 不提供自动模板实例化，因此，尽管编译器对模板的使用感到满意，但它不会生成实际的类和函数。当链接器查找这些项目时，它找不到它们，编译在最后一步失败。

解决方案需要两个步骤：

1. 显式实例化你需要的每个模板实例。
2. 在使用模板的每个模块中声明每个函数的 `extern` 原型。

你之前从 `template.cpp` 中剪切的行执行了第一步。第二步可能不需要，但如果你仍然收到链接器错误，请尝试在任何使用模板类或函数的模块中添加如下 `extern` 声明：

```
extern template class TAnyClass<int>;
extern template class TAnyClass<double>;
extern template class TAnyClass<string>;
extern template class TAnyClass<string> * MakeObject(string param);
```

这些声明告诉链接器在链接到程序的所有模块中查找模板实例化。

## KNOWN TEMPLATE BUG

模板友元函数和内联成员函数可能无法正确编译。例如，模板类中的以下声明会产生“内部编译器错误 163”：

```
template <class T>
friend ostream & operator<< (ostream & ofs, const T &param) {
cout << data;
return ofs;
}
```

也许 GNU C++ 的后续版本会修复这个问题。在此之前，一个可行的变通方法是派生一个新类 from `ostream` 并重载 `operator<<( )` 作为成员函数而不是友元。 第 20 章，“自定义 I/O 流”，展示了这种方法的几个示例。

## DEBUGGING TEMPLATES

模板实例化在编译期间在幕后发生——当模板函数或类不能按预期工作时，这是一个巨大的劣势。找到程序中的错误已经够难了。当原因被隐藏起来时就更难了。幸运的是，GNU 调试器可以准确显示编译器如何实例化模板函数或类，并以此帮助你确定模板设计中的问题。

### 查看模板类实例化

要跟随并查看 C++ 模板类的实例化，请编译本章中的 `tdb.cpp` 程序并使用以下命令将其加载到 GNU 调试器中：

```
$ g++ -g -o tdb tdb.cpp
$ gdb --silent tdb
(gdb)
```

我们想要调查模板类对象的构造过程以及该对象的后续使用。因此，第一步任务是在代码中设置一些合适的断点位置。输入几个 `list` 命令直到找到构造 `TDatabase` 对象的语句（在我这里是第 31 行）。在该语句处设置断点然后运行程序：

```
(gdb) b 31
Breakpoint 1 at 0x80492a1: file tdb.cpp, line 31.
(gdb) run
Starting program: /src/c17/tdb
...
Breakpoint 1, main () at tdb.cpp:31
31 pDb = new TDatabase<TRecord*>(3);
```

此时，`pDb` 指针已被声明为类型 `TDatabase<TRecord>*`。这会促使编译器使用指定的 `TRecord` 数据类型实例化该类模板。要查看模板展开的结果，使用 `ptype` 命令：

```
(gdb) ptype pDb
type = class TDatabase<TRecord> {
private:
  TRecord *rp;
  int num;
public:
  TDatabase<TRecord> & operator=(TDatabase<TRecord> const &);
  TDatabase(TDatabase<TRecord> const &);
  TDatabase(int);
  ~TDatabase(void);
  TRecord & GetRecord(int);
} *
```

结果非常有趣，特别是与原始模板相比（请参阅清单 17.3，`db.h`）。实例化类的名称现在显示为 `TDatabase<TRecord>`。其指针数据成员 `rp` 被声明为类型 `TRecord *`，并且在类的 `public` 部分出现了一些新项目。前两个成员函数展示了 C++ 如何在未在类中显式提供时自动生成 `operator=()` 函数和拷贝构造函数。除了这些新增项之外，实例化类还完善了模板的析构函数和 `GetRecord()` 函数。调试器输出末尾的那个孤立星号表示 `pDb` 是指向所列类的指针。

### 跟踪模板类函数

要跟踪类的使用方式，可以在类模板成员函数中设置断点——即使这些函数实际上是在编译期间由 C++ 构造的。在某些情况下，你可能会遇到一些异常，因为调试器对 C++ 模板的支持尚未完全发挥作用。然而，必要的命令似乎工作得足够好，可以追踪大多数类型的模板错误。一种找到潜在断点位置的方法是列出模板的头文件。例如，如果你正在跟随操作，输入以下命令删除所有当前断点（如果退出调试器则重新加载 `tdb`）：

```
(gdb) delete
Delete all breakpoints? (y or n) y
```

接下来，输入一个 `list` 命令，后跟 `TDatabase` 模板类头文件的名称和行号。再次输入几次 `L` 直到找到此处显示的行（行号可能与你不同）：

```
(gdb) l db.h:1

26 TDatabase(int n): num(n)
```

在此行设置断点以在程序调用 `TDatabase` 构造函数时暂停程序，然后运行程序到断点（如果程序已在运行并被询问是否重启，回答 yes）：

```
(gdb) b 26
Breakpoint 2 at 0x804991c: file db.h, line 26.
(gdb) run
Starting program: /src/c17/tdb
Breakpoint 2, TDatabase<Record>::TDatabase (this=0x1,
n=1073743212)
at db.h:26
26 TDatabase(int n): num(n)
```
