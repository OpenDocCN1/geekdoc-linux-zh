
`delete myComputerPtr;` // 删除数组的错误方法

`delete[] myComputerPtr;` // 删除数组的正确方法

通常，对象包含其他对象。此类对象应该设计为在内部处理它们所包含对象的生命周期。当该类的对象被显式销毁（使用 `delete` 运算符）或超出作用范围时（对象在栈上创建时），该类的析构函数会被调用。析构函数是释放从堆获取内存的方便的地方；但它并不一定是释放内存的地方，因为在对象指针超出作用范围之前就有释放内存的机会，如前。

# 对象引用

对象的引用是对象的别名，并包含对象的地址。对象引用不应与指针对象混淆。指针是

# 面向对象编程 207

对象本身具有独立的存在性，而引用没有。在程序的特定实例中，尽管指针通常不指向其所声明类型的任何特定对象，但指针本身是存在的并占用四个字节的内存。指针对象的地址存在于物理 RAM 中，并且与它所指向的对象的地址不同。然而，对象的引用与其所引用的对象之间没有独立的独立性。如果对象不存在，它的引用也不存在；或者当对象超出作用域时，对象引用也随之消失。这意味着对象引用不能为 NULL，而指针可以被设置为 NULL。对象引用看起来比物理上更具概念性，并且是相对于对象指针的一种更高级层次的抽象。当程序被编译时，编译器会将所有标识符信息存储在符号表中。在符号表中，对象引用作为指向真实编译对象的条目形式存储的，而不是作为独立的实体。对象引用是对象的地址，它通过在对象名称前加上取地址符 `&` 来标识。例如，如果对象的标识名称为 `myobject`，那么它的引用被标识为 `&myobject`。

引用在向函数传递参数时非常有用。使用时，调用函数可以以类似于对象指针的方式处理它们；使用 `->` 运算符访问对象成员。当调用函数接收对象引用作为参数时，它不需要检查对象是否为 NULL，因为如上述所述，只有在对象存在时，对象引用才存在。然而，当函数接收对象指针作为参数时，在尝试访问对象的成员之前确保指针不为 NULL 是明智的，因为对象指针具有独立的存在性并且可以为 NULL。列表 5.11 提供了一个示例程序，展示了传递函数参数的所有不同方式：按值传递、按引用传递和按指针传递。从示例中可以看出，当原始对象按值传递给函数时，原始对象的私有变量的值不会改变。这是因为调用函数是在对象的副本上进行操作，而不是原始对象。该列表可在附带的 CD-ROM 中找到。

![](img/1c052d580a194876cd94f43b32c39cf_222_0.png)

## Listing 5.11 FunctionArguments.cpp

```cpp
#include <class.h>
#include <iostream>
#pragma hdrstop
using std::cout;
using std::endl;
#pragma argsused
```

## 208 企业级 Linux 应用程序开发

```cpp
class MyClass {
    private:
        int intVar;
    public:
        // 类实现
        MyClass() { };
        int getVar() { return intVar; }
        void setIntVar(int value) { intVar = value; }
}
```

```cpp
void ObjectByValue(MyClass myObj) {
    myObj.setIntVar(10);
}
```

```cpp
void ObjectByReference(MyClass& myObj) {
    // 当传递引用时，不需要
    // 像我们处理对象指针那样进行 NULL 检查。
    myObj.setIntVar(25);
}
```

```cpp
void ObjectByPointer(MyClass* myObj) {
    // 当传递指针时，要求确保在
    // 我们通过指针访问对象之前
    // 指针不为 NULL
    if (myObj != NULL) {
        myObj->setIntVar(30);
    }
}
```

```cpp
int main() {
    MyClass myObj;
    myObj.setIntVar(20);
    cout << "Initial value of intVar = " << myObj.getIntVar() << endl;
    // 按值传递对象
    ObjectByValue(myObj);
    cout << "Value after passing (by value) to function = " << myObj.getIntVar() << endl;
    // 按引用传递对象
    ObjectByReference(myObj);
    cout << "Value after passing (by reference) to function = " << myObj.getIntVar() << endl;
    // 按指针传递对象
    ObjectByPointer(&myObj);
    cout << "Value after passing (by pointer) to function = " << myObj.getIntVar() << endl;
    return EXIT_SUCCESS;
}
```

### 面向对象编程 209

此程序应使用 Borland C++ 编译器 `bc++` 进行编译，该编译器由 Kylix 提供。编译器位于 `/usr/local/kylix3/bin` 目录。如果该目录包含在 PATH 环境变量中，则可以在 shell 命令中调用编译器而无需加完整路径，如下所示。

```
$ bc++ FunctionArguments.cpp
```

程序的成功编译将创建一个与源程序同名但无扩展名的默认输出文件。当程序执行时，在命令行提示符处显示的输出如图 5.2 所示。

![](img/1c052d580a194876cd94f43b32c39cf_224_0.png)

**图 5.2** 展示对象引用的控制台应用程序输出。

## 虚函数与多态

如本章所述，多态是一个核心原则。

### 210 企业级 Linux 应用程序开发

多态是不同对象以自己的方式响应相同消息的能力。这通过虚函数实现。当在基类中声明虚函数时，编译器为该类创建一个虚函数表（`vtable`）。虚函数表包含虚函数的指针。该类的每个对象都有一个指向虚函数表的指针（`vptr`）。

当调用虚函数时，程序使用 `vptr` 来查找要执行的函数。这被称为动态绑定。列表 5.12 提供了一个示例，展示了虚函数的工作原理。该列表可在附带的 CD-ROM 中找到。

![](img/1c052d580a194876cd94f43b32c39cf_225_0.png)

## Listing 5.12 VirtualFunctions.cpp

```cpp
#include <class.h>
#include <iostream>
#pragma hdrstop
using std::cout;
using std::endl;
#pragma argsused
class Car {
public:
    Car() { };
    virtual void Helmholtz() {
        cout << "Hello from an object of Car" << endl;
    }
};
class MyCar : public Car {
public:
    MyCar() { };
    void Helmholtz() override {
        cout << "Hello from an object of MyCar" << endl;
    }
};
class YourCar : public Car {
public:
    YourCar() { };
    void Helmholtz() override {
        cout << "Hello from an object of YourCar" << endl;
    }
};
class NewCar : public Car {
public:
    NewCar() { };
};
int main() {
    Car* bc;
    bc = new Car();
    bc->Helmholtz();
    delete bc;
    bc = new MyCar();
    bc->Helmholtz();
    delete bc;
    bc = new YourCar();
    bc->Helmholtz();
    delete bc;
```
