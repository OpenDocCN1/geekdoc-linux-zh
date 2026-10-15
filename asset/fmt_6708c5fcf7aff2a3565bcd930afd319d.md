
```cpp
bc = new NewCar();

bc->Helmholtz();

delete bc;

return EXIT_SUCCESS;

}
```

## 模板

模板是 C++ 语言中一个非常强大的特性，但经常被忽视。通过模板的概念，可以创建类定义的模式以处理任何数据类型，即使该类型在编译时尚未定义。同样，函数模板也是可以创建以处理不同类型的模式。如果没有模板，当我们尝试编译 C++ 程序时，它不会无错误编译。然而，当声明模板类和模板函数时，这个问题就不会出现，因为模板是参数化类型，而参数可以是任何（存在的或不存在的）数据类型。

## 212 企业级 Linux 应用开发

模板避免了为不同数据类型编写重复（相同）代码的情况。因此，它们可以用于创建一组对不同数据类型使用相同逻辑的函数。模板还有另一个使用场景，即在我们无法使用特定数据类型时使用 `void` 指针的情况。在这些情况下，我们无法编写需要对类型数据操作的代码，因为 `void` 指针没有指向特定类型。然而，当使用模板时，它们会取代 `void` 指针，可以在模板上执行任何特定类型的操作。列表 5.13 提供了一个示例，以演示模板类的定义和使用。从程序列表中可以注意到，尽管在实现模板类时使用了泛型参数类型 `<class T>`，但类模板可以与任何类型（包括 C++ 通常支持的内置数据类型）结合使用。该列表位于附带的 CD 中。

![](img/1c052d580a194876cd94f43b32c39cf4_227_0.png)

## 列表 5.13 TemplateClass.cpp

```cpp
// 此示例旨在演示实现泛型栈类的

// 模板类的使用。

#include <cl.h>

#include <iostream>

#include <cstring>

using std::cout;

using std::endl;

template <class T> class tmplStack

{

    T* StBuffer;

    int availPos;

    int maxSize;

public:

    tmplStack(int n); // 构造函数

    ~tmplStack(); // 析构函数

    void push(T item); // 将元素推入栈顶

    T pop(void); // 从栈顶弹出元素

    int getSize(); // 返回栈的大小

};

template <class T> tmplStack::tmplStack(int n)

{

    availPos = n;

    maxSize = n;

    StBuffer = new T[n];

}

template <class T> tmplStack::tmplStack()

{

    delete[] StBuffer;

}

template <class T> void tmplStack::push(T item) {

  if (availPos < maxSize) {

    StBuffer[maxSize - availPos] = item;

    --availPos;

    return;

  }

}

template <class T> T tmplStack::pop( void ) {

  if (availPos < maxSize) {

    T Obj = StBuffer[maxSize - (availPos+1)];

    ++availPos;

    return Obj;

  } else

    return NULL;

  }

template <class T> int tmplStack::getSize() {

  return (maxSize - availPos);

}

int main() {

  tmplStack<char*> chptrStack(10);

  char myStr[6][25];

  strcpy(myStr[0],"Borland Kylix");

  chptrStack.push(myStr[0]);

  strcpy(myStr[1],"Borland Delphi");

  chptrStack.push(myStr[1]);

  strcpy(myStr[2],"Borland Builder");

  chptrStack.push(myStr[2]);

  strcpy(myStr[3],"Borland C++Builder");

  chptrStack.push(myStr[3]);

  strcpy(myStr[4],"Borland OptimizeIt Suite");

  chptrStack.push(myStr[4]);

  strcpy(myStr[5],"Borland Together");

  chptrStack.push(myStr[5]);

  int stackSize = chptrStack.getSize();

  cout << "Items on the char string = " << stackSize << endl;

  cout << "Stack items are listed top to bottom " << endl;

  for (int j=0; j < stackSize; ++j) {

    cout << chptrStack.pop() << endl;

  }

214 企业级 Linux 应用开发
```

```cpp
tmplStack<int> intStack(5);
intStack.push(100);
intStack.push(50);
intStack.push(25);
intStack.push(15);

int stackSize = intStack.getSize();
cout << "Items on the int stack = " << stackSize << endl;
cout << "Int stack items are listed from top to bottom " << endl;
for (int j=0; j < stackSize; ++j) {
    cout << intStack.pop() << endl;
}

return EXIT_SUCCESS;
}
```

如前所述，使用以下命令编译程序：

```bash
$ bc++ TemplateClass.cpp
```

程序的成功编译将创建一个与源程序同名的默认执行文件，但没有扩展名。当程序执行时，命令行提示符处的输出如图 5.3 所示。

![](img/1c052d580a194876cd94f43b32c39cf4_229_0.png)

图 5.3 模板类的应用程序输出

## C++ 中的命名空间

C++ 中的命名空间通过定义一个新的作用域允许使用重复名称（如变量、类和函数），这意味着不同命名空间中定义的同名标识符可以共存。然而，单个命名空间内的标识符名称必须是唯一的。我们经常遇到多个团队独立开发不同模块并具有相同标识符名称的场景。通过为每个团队/模块分配不同的命名空间，团队可以自由地使用自己的名称而不必担心命名冲突。命名空间引入了新的声明区域，区域内声明的所有标识符都可以通过命名空间名前在区域外部访问。这里显示了一个使用相同标识符名称的典型命名空间声明，以便更好地理解该概念。

```cpp
namespace first {
    class myClass {
    };
}
namespace second {
    class myClass {
    };
}
namespace outer {
    namespace inner {
        class myClass {
    };
    }
}
```

示例中的第三个命名空间展示了命名空间如何嵌套。命名空间中声明标识符可以通过不同的方式访问。这些方法并非相互替代，而是在本节所述，在不同情况下提供了不同级别的便利性。在一种样式中，标识符名称使用 `::` 运算符开头，如下：

```cpp
first::myClass object1;
second::myClass object2;
outer::inner::myClass object3;
```

然而，如果这种这种表示法，标识符的每次出现都应该以此方式前缀。这种限定标识符名称方法的优点是应用程序可以使用任意数量的命名空间而不会引入冲突。但如果命名空间名称多次出现，则值得考虑第二种样式，即使用 `namespace <name>` 指令提到一次命名空间，然后在不限定标识符的情况下访问命名空间内的标识符。

```cpp
using namespace first;
myClass object;
```
