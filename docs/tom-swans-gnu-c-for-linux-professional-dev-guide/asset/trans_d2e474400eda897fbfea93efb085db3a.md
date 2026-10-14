

```cpp
// Explicit template instantiation for function MakeObject()
//
template TAnyClass<string> * MakeObject(const string param);
```

实现模块提供了 TAnyClass 模板中成员函数 GetData() 的内容。该成员函数仍然是模板形式——它使用占位类型 T——但其语句块提供了函数的功能——在本例中，只是返回对象的私有数据，无论它是什么。

同样，模板函数的语句使用 C++ new 运算符构造 TAnyClass<T> 类型的对象，并将指向该对象的指针作为函数的结果返回。同样，这仍然是一个模板。函数的实际实例化在为 T 提供数据类型时才会发生。

不幸的是，麻烦就从这里开始。清单 17.7，usemtemplate.cpp，尝试通过包含头文件来使用模板类和模板函数。然而，结果是一系列令人困惑的链接器错误。

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

要查看链接器找不到模板实例化时产生的错误，请注释掉或删除 template.cpp 文件（参见清单 17.6）中从注释“Cut Here”到末尾的行。然后输入以下命令：

```text
$ g++ -c template.cpp
$ g++ usemtemplate.cpp template.o
/tmp/cca011931.o: In function `main':
/tmp/cca011931.o(.text+0x1e): undefined reference to
`TAnyClass<int>::GetData(void) const'
```

模板模块（template.cpp）可以编译，但尝试链接主程序和模块时会产生未定义引用错误。虽然我在这里只展示了一个这样的错误，但如果你跟着操作，屏幕上会出现其他几个错误。问题在于 GNU C++ 不提供自动模板实例化，因此，尽管编译器对模板的使用感到满意，但它不会生成实际的类和函数。当链接器查找这些项目时，它找不到它们，编译在最后一步失败。

解决方案需要两个步骤：

- 1. 显式实例化你需要的每个模板实例。
- 2. 在使用模板的每个模块中声明每个函数的 extern 原型。

你之前从 template.cpp 中剪切的行执行了第一步。第二步可能不需要，但如果你仍然收到链接器错误，请尝试在任何使用模板类或函数的模块中添加如下 extern 声明：

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

也许 GNU C++ 的后续版本会修复这个问题。在此之前，一个可行的变通方法是派生一个新类 from ostream 并重载 operator<<( ) 作为成员函数而不是友元。 第 20 章，“自定义 I/O 流”，展示了这种方法的几个示例。

## DEBUGGING TEMPLATES

模板实例化在编译期间在幕后发生——当模板函数或类不能按预期工作时，这是一个巨大的劣势。找到程序中的错误已经够难了。当原因被隐藏起来时就更难了。幸运的是，GNU 调试器可以准确显示编译器如何实例化模板函数或类，并以此帮助你确定模板设计中的问题。

