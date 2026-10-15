
一个类也可以抛出其自身类类型的异常对象。通常，这是在异常类中由成员函数完成的，通常称为`Raise()`。例如，你可能会像这样设计异常类：

```
class Error {
public:
    void Raise() { throw Error(); }
};
```

该类还可能声明其他函数、构造函数、析构函数和数据成员。如果`e`是类型为`Error`的对象，则以下语句会抛出另一个`Error`类的对象：

```
e.Raise();  // Throws fresh Error object
```

根据`Error`类中的其他服务，这可能是抛出异常的一种好方法，即使它最初已被处理。这样做可以使异常保持活跃，导致 C++ 继续在函数调用链中向上搜索匹配的异常处理程序。在许多情况下，你可以通过抛出`catch`语句接收的相同对象来简单地做到这一点：

```
catch (Error e) {
    // initially handle this type of error
    throw e; // rethrow exception to this function's caller
}
```

## 异常与内存管理

如前几章所述，`operator new`在无法满足内存分配请求时会抛出异常。在 GNU C++ 中，该异常是`bad_alloc`类的对象。假设程序中有一个函数`f()`，它使用`new`创建类型为`TAnyClass`的动态对象：

```
T AnyClass * f()
{
    return new TAnyClass();
}
```

要捕获`new`在内存分配失败时抛出的异常，可使用如下`try`和`catch`语句：

```
try {
    TAnyClass * p = f();  // 可能抛出异常
}
catch (bad_alloc error) {
    cout << error.what() << endl;
    exit(1);
}
```

尽管上述代码可行，但在每次使用`new`时都捕获`bad_alloc`异常很不方便。因为内存不足通常表示严重问题，更常见的做法是在更高层捕获错误——例如在`main()`中，使用如下代码：

```
int main()
{
    for (;;) {
        try {
            run();  // 主程序循环
        }
        catch (bad_alloc error) {
            cout << "Out of memory" << endl;  // ???
            cout << error.what() << endl;  // ???
            exit(1);
        }
    }
}
```

基本思路是使用一个 Do-Forever `for`循环，反复调用一个函数——本例中为`run()`——你可以将其称为主程序引擎。`catch`语句捕获`run()`抛出的所有`bad_alloc`异常，或由`run()`调用的任何其他函数抛出的异常。然而，输出语句值得怀疑，因为如果系统内存不足，可能没有足够的空闲字节来执行输出语句本身。如果在输出语句期间发生异常，程序会调用`terminate()`并突然以核心转储结束。

一个有用的技巧可以缓解此类问题，即在程序开始时分配一块内存池，在内存分配失败时将其删除。例如，你可以预留 2,048 字节的块：

```
char *reserve = new char[2048];
```

这也可能放在`try`块中，但在程序开始运行时通常有一定内存可用。在发生`bad_alloc`异常时，删除预留的内存：

```
delete reserve;
reserve = NULL;
```

然后你可以重复导致错误的那个操作，希望`new`的使用能够成功。如果不行，会再次抛出`bad_alloc`异常，你可能不得不中止程序。一种做法是捕获并重新抛出异常：

```
catch (bad_alloc error) {
    if (reserve != NULL)
        throw (error);
}
```

这会导致异常对象在异常处理程序之外保持存活，除非在函数调用链中更高层有另一个处理程序，否则程序最终会调用当前未预期的异常处理程序。在该处理程序中，你可以执行有序关闭，关闭文件，并在结束程序前完成其他必要操作。

## 调试异常

GNU 调试器提供了一个用于捕获异常的命令，但在我使用的版本中似乎不起作用。不过，你可以尝试使用更新的编译器——也许对你有效。首先，编译本章中类似`unexpect.cpp`的程序（参见清单 16.4），并使用以下命令将其载入调试器：

```
$ g++ -g -o unexpect unexpect.cpp
$ gdb --silent unexpect
(gdb)
```

通过将函数名指定给`break`命令（简写为`b`）来在函数`main()`上设置断点，然后运行程序：

```
(gdb) b main
Breakpoint 1 at 0x80489ee: file unexpect.cpp, line 40.
(gdb) run
Starting program: /src/c16/unexpect
Breakpoint 1, main () at unexpect.cpp:40
40 set_unexpected( custom_unexpected );
```

## 总结

正如本章所述，C++ 异常是函数可以抛出的对象，用来报告异常情况。为了提供异常处理，程序在`try`块中调用函数，然后使用`catch`语句处理这些函数可能抛出的异常对象类型。任何未处理的异常都会调用低级的`unexpected()`和`terminate()`函数，你可以用自定义版本替换它们，以捕获所有可能的错误并防止程序意外关闭。本章还解释了相关主题，例如重新抛出异常、从标准异常类派生类，以及为 C++ `new`运算符报告的内存不足错误编写异常处理程序。

有关本章介绍主题的更多信息，请参阅以下章节：

- Chapter 22, “Mastering the Standard string Class”

- Chapter 25, “Applying Standard Algorithms”

# 第17章 创建类模板

正如类是一种构建对象的蓝图，模板就是构建函数和类的蓝图。也称为参数化类型，模板为通用类和函数提供规范，这些类和函数能够自动适应新的用途。

> 注意

> 有关使用模板的更多信息，请参阅第23章“使用标准模板库（STL）”。

## 介绍类模板

模板通常用于创建通用函数和类，这些函数和类不绑定到任何特定数据类型。例如，排序函数就是一个很好的模板，因为排序算法不直接依赖于其操作的数据类型。将函数实现为模板可将其简化为最一般的形式。在编译程序时，C++ 使用模板生成或实例化一个实际的函数，该函数适用于特定类型的数据。

模板类同样具有通用性。一个极佳的例子是容器类，它提供搜索和其他功能，但可以处理从最基本的整数到复杂类对象等任何数据类型。

## 模板函数

模板函数描述了函数的通用属性。最常见的是，你将模板函数声明在单独的头文件中，并在各个模块中包含它们。模板函数通常如下所示：

```
template <class T>
void f(T param)
{
    // ... function body
}
```

保留字`template`开始声明，并且始终后跟包含一个或多个表达式的尖括号。在此示例中只有一个表达式——以单词`class`开始，后跟你选择的任何标识符。在本例中，我使用`T`表示“类型”。这里的单词`class`不一定指 C++ 类，而是指任何“类”数据类型。

模板的前言之后是正在以模板形式声明的项目。在此示例中，它是一个名为`f()`的函数，返回`void`并接收一个类型为`T`的单个参数。实际数据类型在程序使用模板时稍后指定——在此，`T`只是指尚未定义类型的占位符。函数也可能返回占位符类型的值：

```
template <class FutureType>
FutureType AnyFunction(FutureType param)
{
    // ... function body
}
```

## 列表 17.1 MINMAX.H

```
#pragma interface

template <class T>
T max(T a, T b)
{
    if (a > b)
        return a;
    else
        return b;
}

template <class T>
T min(T a, T b)
{
    if (a < b)
        return a;
    else
        return b;
}
```

### 注意

`minmax.h`中的`#pragma interface`指令可能不再需要。某些版本的 GNU C++ 需要它来帮助链接器解析模板函数和类的使用。

仔细查看模板函数`max()`的声明：
