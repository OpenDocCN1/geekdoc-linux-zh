

## LISTING 21.8 CONTINUED

```
}
int GetCounter() const { return counter; }
};

int main()
{
TAnyClass v1(123);
cout << "v1 value == " << v1.GetValue() << endl;
cout << "v1 counter == " << v1.GetCounter() << endl;
return 0;
}
```

现在 counter 是可变的，GetValue() 可以被声明为 const，但仍然允许更改 counter 的值。这在需要将 const 类对象传递给另一个调用 GetValue() 的函数时可能很重要，例如拷贝构造函数。在这种情况下，声明 counter 为 mutable 即使对于 const 对象也能覆盖编译器的反对意见。然而，请务必理解，mutable 的滥用实际上违背了使用常量对象的初衷——即防止因函数调用而导致对象发生意外的更改。

## USING typename

在模板中使用 typename 保留字来为数据类型定义占位符。例如，Listing 21.9，typename.cpp，声明了一个模板函数，返回任意类型的两个值的最大值。

## LISTING 21.9 TYPENAME.CPP

```
#include <iostream.h>

//template <class T> T max(T a, T b)
template <typename T> T max(T a, T b)
{
    if (a > b)
        return a;
    else
        return b;
}

int main()
{
    int v1 = 123;
    int v2 = 321;
    cout << "max(123, 321) == " << max(v1, v2) << endl;
    return 0;
}
```

模板声明上方有一条注释，展示了创建数据类型占位符的更常见方式。通常，模板是这样声明的：

```
template <class T> T max(T a, T b)
```

如果你像许多程序员一样觉得这里使用 class 这个词令人不安，你可以使用 typename 代替：

```
template <typename T> T max(T a, T b)
```

然而，除了稍微更清晰之外，使用 typename 代替 class 好像并没有什么优势。使用

## POINTERS TO MEMBER FUNCTIONS

你可以用指针寻址类成员函数，但方式与常规函数不同。这是因为成员函数是相对于对象调用的，函数会接收一个 this 指针。因此，用指针寻址成员函数就需要新的技术。

> Note
> 静态函数是此规则的例外——它不引用其类的对象，因此不接收 this 指针。

由于成员函数绑定到其类名，声明指针需要使用函数类型和类名。例如，对于类 TAnyClass，你可以通过以下声明声明指向其成员函数之一的指针：

```
double (TAnyClass::*myfnptr)();
```

这表示 myfnptr 指向一个 TAnyClass 成员函数，该函数不声明参数并返回 double 类型的值。它没有指定确切是哪个函数，只要求函数具有这些特征。要声明 myfnptr 为指向返回 void 并声明一个 int 参数的类成员函数的指针，请使用如下声明：

```
void (TAnyClass::*myfnptr)(int);
```

## LISTING 21.10 MFNPTR.CPP

```
#include <iostream.h>
#include <iomanip.h> // Need output stream manipulators

class TAnyClass {
private:
    int value;
```

## LISTING 21.10 CONTINUED

```
public:
TAnyClass(): value(0) {}
int GetValue() { return ++value; }
};

// Declare pointer to member function

int (TAnyClass::*myfnptr)();

void main()
{
int i;
TAnyClass object;

cout << "Call GetValue the normal way:" << endl;
for (i = 0; i < 9; i++)
cout << setw(8) << dec << object.GetValue();
cout << endl;
cout << "Call GetValue using a pointer" << endl;
myfnptr = &TAnyClass::GetValue;
for (i = 0; i < 9; i++)
cout << setw(8) << dec << (object.*myfnptr)();
cout << endl;
cout << "Use dynamic instance and pointer" << endl;
TAnyClass *p = new TAnyClass(object);
for (i = 0; i < 9; i++)
cout << setw(8) << dec << (fp->*myfnptr)();
cout << endl;
}
```

TAnyClass 之后的那条单行声明指出 myfnptr 是一个指向 TAnyClass 成员函数的指针，该成员函数不返回任何值并声明一个 int 参数。程序可以将任何此类匹配函数的地址赋给该指针，然后使用它来调用该函数。例如，main() 中的测试程序构造了一个 TAnyClass 类型的对象，然后使用以下表达式调用 GetValue() 成员函数：

```
object.GetValue()
```

要使用指针调用同一个函数，程序将 myfnptr 赋值为 TAnyClass 中 GetValue() 成员函数的地址：

```
myfnptr = &TAnyClass::GetValue;
```

或者，你也可以使用如下单条语句声明并初始化成员函数指针：

```
int (TAnyClass::*myfnptr)() = &TAnyClass::GetValue;
```

