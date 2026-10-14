

请确保不要在函数名后面加上括号。你只是想通过名称引用函数，而不是调用它。无论如何，要使用指针，请遵循以下两条规则：

+   1. 引用类的一个对象（除非该函数是静态的）。
+   2. 用括号包围函数调用。

如果 data 是一个 int 变量，且 object 是一个 TAnyClass 对象，则以下语句将使用成员函数指针把 GetValue() 返回的结果复制到 data 中：

```
int data = (object.*myfnptr)();
```

点号和星号是一个 C++ 符号，称为指针到成员运算符。它用于为类对象解引用成员函数指针。表达式 (object.*myfnptr) 中的括号是必要的，因为函数调用运算符——一组空括号——的优先级高于指针到成员运算符。前面语句等价于以下内容：

```
int data = object.GetValue();
```

你也可以通过使用指向对象的指针来调用成员函数。例如，在示例程序中，一个语句将 new 运算符创建的 TAnyClass 对象的地址赋给指针 fp：

```
TAnyClass *fp = new TAnyClass(object);
```

在此之后，下一个表达式使用成员函数指针调用 GetValue()：

```
(fp->*myfnptr)();
```

三字符符号 ->* 是指针到成员运算符的一个变体。同样，由于 () 的优先级高于 ->*，因此需要额外的括号。前面语句等价于以下内容：

```
fp->GetValue();
```

## 静态成员函数

第 14 章“投资继承”介绍了静态成员。简而言之，静态数据成员存在于类的所有对象中，而与之相比，非静态成员在每个类对象中都分配空间。成员函数也可以是静态的。与非静态成员函数不同，静态函数不是相对于对象调用，而是仅相对于类调用。这对于设计初始化值或执行影响所有随后构造对象的其他操作的函数非常有用。要声明静态成员函数，请在其原型前加上保留字 static：

```
class TAnyClass {
public:
    static void GlobalInit();
    ...
};
```

注意
静态成员函数可能不是虚函数。

实现静态成员函数的方式与其他函数相同，但不要重复 static 指定：

```
void TAnyClass::GlobalInit()
{
// ... statements to perform
}
```

静态成员函数可以执行任何操作，但由于它不是相对于类对象调用，因此函数中的语句可能不能引用非静态数据成员。此类成员仅存在于类对象中，因此它们根本不可用于静态函数。然而，该函数可以使用静态数据成员，事实上，静态成员函数通常用于初始化类的静态数据成员。列表 21.11，static.cpp，演示了使用静态数据和函数成员的一种常见方法。

### LISTING 21.11 STATIC.CPP

```
#include <iostream.h>
#include <iomanip.h>  // Need setw()

#define BUFSIZE 64

// A class with static data and function members
//
class TAnyClass {
private:
    static char buffer[BUFSIZE];
public:
    TAnyClass() { }
    static void InitBuffer();
    void DisplayBuffer(const char *msg);
    void FillBuffer(char byte);
};

// Actual buffer definition. This would usually appear
// in another module linked to the program.
//
char TAnyClass::buffer[BUFSIZE];

int main()
{
    TAnyClass objectA, objectB, objectC;
    TAnyClass::InitBuffer();
    objectA.DisplayBuffer("Object A buffer");
    objectA.FillBuffer(2);
    objectB.DisplayBuffer("Object B buffer");
    objectB.FillBuffer(3);
    objectC.DisplayBuffer("Object C buffer");
    return 0;
}
```

```
// Static function initializes the buffer
void TAnyClass::InitBuffer()
{
    for (int i = 0; i < BUFSIZE; i++)
        buffer[i] = i;
}

// Non static function called in reference to object
void TAnyClass::DisplayBuffer(const char *msg)
{
    cout << msg << endl;
    for (int i = 0; i < BUFSIZE; i++)
        cout << setw(4) << (int)buffer[i];
    cout << endl;
}

// Fill buffer with indicated value
void TAnyClass::FillBuffer(char byte)
{
    for (int i = 0; i < BUFSIZE; i++)
        buffer[i] = byte;
}
```

测试程序展示了如何为特定类的所有对象创建一个静态缓冲区。程序的类 TAnyClass 声明了两个静态成员：
static char buffer[BUFSIZE];
static void InitBuffer();

由于 buffer 对类是私有的，只有类成员函数可以引用它。函数 InitBuffer()，也声明为 static，用顺序值填充缓冲区。函数 FillBuffer() 用作为参数传递的值填充缓冲区。我们不希望大型缓冲区位于每个对象内部——相反，我们希望 TAnyClass 的所有对象都引用同一个缓冲区。这就是使用静态成员的主要目的。为了演示其工作原理，测试程序构造了三个 TAnyClass 对象：
AnyClass objectA, objectB, objectC;

接下来，调用静态 InitBuffer() 函数。由于它是静态的，它是相对于类调用的，而不是相对于类的任何特定对象：
TAnyClass::InitBuffer();

该语句可以出现在其他位置——它不必跟随三个对象的构造。为了证明所有三个对象都使用同一个缓冲区，程序显示缓冲区的初始内容，然后用值 2 填充它：
objectA.DisplayBuffer("Object A buffer");
objectA.FillBuffer(2);

即使 FillBuffer() 是相对于 objectA 调用的，对不同对象调用 DisplayBuffer() 也会显示全部为 2：
objectB.DisplayBuffer("Object B buffer");

