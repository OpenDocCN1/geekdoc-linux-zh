

该语句构造了一个 Overflow 类的对象，并将其抛回给函数的调用者。在该函数中，程序可以用如下代码捕获异常

```
catch (Overflow) {
    cout << "Overflow detected" << endl;
}
```

## 标准异常类

通常，异常类派生自一个提供问题信息的基类。为了使你的异常处理与 C++ 默认处理器兼容，最佳做法是基于标准 C++ 异常类来构建你自己的异常处理器，该类声明如下

```
class exception {
public:
    exception() { }
    virtual ~exception() { }
    virtual const char* what() const;
};
```

要使该类在你的程序中可用，请包含标准异常头文件，在本例中，该文件不以 .h 结尾。同时包含标准字符串头文件，以便在异常对象中存储描述性消息：

```
#include <exception>
#include <string>
```

exception 类声明了三个公共成员：一个什么都不做的默认构造函数、一个虚析构函数，以及一个返回类型为 const char* 的虚函数 what()，并且由于 const 后缀，表明调用该函数不会对对象进行任何更改。要使用 exception 类，可以派生另一个类，如下所示：

```
class TMyException: public exception {
private:
    string what_str;
public:
    TMyException(const string &what_arg):
        what_str(what_arg) { }
    virtual const char* what() const {
        return what_str.c_str();
    }
};
```

派生类公有继承标准 exception 类，并添加了一个名为 what_str 的私有字符串对象。新类的构造函数指定了一个对 C++ 字符串对象的引用参数，并使用初始化表达式将 what_arg 赋给 what_str。构造函数没有其他职责要执行，因此其语句块为空。虚函数 what() 通过调用 what_str 对象的 c_str() 函数返回一个指向 C 风格字符串的 const char *。函数 what() 在异常对象中是传统的，用于获取导致抛出异常的问题描述。

要使用派生类，函数语句会抛出派生类的对象，并将字符串描述作为参数。函数可能写成如下形式：

```
int AnyFunction()
{
    if (errorCondition)
        throw TMyException("Underflow");
    else
        return aValue;
}
```

如果检测到错误条件，函数会抛出 TMyException 类的对象；否则，它会正常返回一个值。

> **Note**
> 
> 有关 C++ 字符串对象的更多信息，请参阅第 22 章，“精通标准字符串类。”

## 介绍 try 块

现在是时候加入另一个复杂因素——try 块，它们在第一次使用时似乎让每个人都感到困惑。为了在 catch 语句中捕获异常，使用前一节中的 TMyException 类和示例 AnyFunction()，程序可以用如下代码启用异常处理：

```
int x;
try {
    x = AnyFunction();  // Might throw an exception
    cout << "x = " << x << endl;  // May not execute
}
catch (TMyException except) {
    cout << except.what() << endl;
    exit(1);
}
```

try 块执行一个或多个语句，其中一些可能会抛出异常。在本例中，示例 AnyFunction() 如果检测到错误就会抛出 TMyException 类型的异常。如果发生这种情况，x 不会被赋值，并且输出语句不会执行。相反，程序会立即跳转到第一个与异常类型匹配的 catch 语句。在本例中，示例 catch 语句捕获异常对象，通过调用 what() 显示其消息，然后通过调用 exit() 结束程序。

一个或多个 catch 语句必须跟随在 try 块之后。你不能将 try 块放在一个地方，而将它的 catch 语句放在另一个地方。那就像棒球比赛中投手在投手丘上，而捕手却在停车场里。在所有情况下，你必须在 try 块后跟随一个或多个 catch 语句，以捕获被尝试语句抛出的任何异常。

