
## 第 3 章：面向对象编程基础

### 构造函数与派生类

```cpp
person(string Nm) { Name = Nm; }

float height(void) { return Height; }

float weight(void) { return Weight; }

date birthDate(void) { return BirthDate; }
```

在这种情况下，`person` 类没有默认构造函数。当实例化 `person` 对象时，必须提供一个名称。例如：

```cpp
person Programmer("Chilly Willy");
```

如果我们创建一个名为 `employee` 的新类，它派自 `person`，例如：

```cpp
class employee : public person{
    protected:
        int EmployeeNumber;
        ...
};
```

在 `employee` 被正确构造之前，它的 `person` 组件必须被正确构造。这意味着当我们实例化一个 `employee` 对象时，我们需要一种方法将名称参数传递给 `person` 组件。为了做到这一点，我们声明 `employee` 的构造函数也接受一个表示名称的字符串参数，并在定义 `employee` 构造函数时调用 `person` 构造函数。例如：

```cpp
employee(int EmpNo, string Nm) : person(Nm) {
    EmployeeNumber = EmpNo;
}
```

这段代码会导致 `employee` 的 `person` 组件用 `Nm` 中存储的值进行初始化。现在要构造一个 `employee` 对象，我们可以使用：

```cpp
employee Mascot = new employee(202,"Chilly Willy");
```

或者：

```cpp
Mascot = new employee(202,"Chilly Willy");
```

`Qt` 和 `K` 类库中的许多类没有默认构造函数。因此，你派生的类必须向基类传递正确的信息。如果基类有默认构造函数，则你的派生类不需要实现任何特殊的构造函数。否则，你必须实现至少一个构造函数，将必要的参数传递给基类的至少一个构造函数。

### 析构函数与终结器

构造函数在对象最初创建（实例化）时被调用。析构函数在对象销毁时被调用。在 `C++` 中，这发生在对象超出作用域或使用 `delete` 语句显式销毁时。例如，

```cpp
delete Mascot;
```

会导致 `Mascot` 被销毁并调用 `Mascot` 的析构函数。你可以使用析构函数来释放内存、关闭文件、关闭设备或对象需要执行的任何其他最终清理工作。在 `C++` 中，析构函数的名称与类名相同。它们通过使用波浪号（`~`）与构造函数区分开来。例如：

```cpp
class employee {
    protected:
        int EmployeeNumber;
        string Status;
    public:
        employee(int EmployeeNumber = 1) {}
        ~employee(void) { Status = "fired"; }
};
```

像构造函数一样，析构函数通常会被自动调用。`Java` 没有析构函数。`Java` 最接近的是定义在基类 `Object` 中的 `finalize()` 方法。任何派生类都可以重写 `finalize()` 方法。`finalize()` 方法被称为终结器（finalizer），因为它是由 `Java` 垃圾回收器作为对象的“最后遗嘱”而调用的。一旦对象被确定要销毁，垃圾回收器就会收回其占用的资源。此时会调用 `finalize()` 方法。然而，无法保证 `finalize()` 方法一定会被调用，因为程序在需要垃圾回收之前可能已经正常终止。因此，`finalize()` 方法并不像 `C++` 析构函数。`finalize()` 方法可以被显式调用。

### 面向对象编程的基础

某些语言支持 `OOP` 的某些部分而不支持其他部分。例如，一种语言可能支持封装，但不支持继承和多态。像 `C` 这样的语言可能支持函数重载，但不支持继承。在 `C` 中，结构体（`struct`）可以提供某些类型的封装，但不能提供通过 `private` 和 `protected` 等访问修饰符所提供的完整封装。面向对象编程不仅仅是一种风格。它需要特殊的语法和语言支持。

> 企鹅原则 #3：封装、继承和多态是面向对象应用中的必要要素。

类层次结构是一组需要使用继承和多态的相关的类。此外，类层次结构被用于构建类库，而类库被用于构建面向对象的应用程序。类库，例如标准 `C++` 类库、`Java Foundation Classes (JFC)`、`Qt` 和 `K` 框架，为我们在线于 Linux 上的快速应用开发（RAD）提供了基础。在面向对象的 RAD 中获得最佳结果，需要对类库及其工作原理有深入的理解。

### 理解类库

类库之所以得这个名字，是因为它们包含了可重用类的集合。类库有源码形式（未编译或非解释）和二进制形式（对象代码）形式。源码形式将包含有类声明和类定义的文件。类库的二进制形式由类的编译后或解释后的版本组成。

#### C++ 中的源码类库

`C++` 中类的源码形式通常由两部分组成：通常存储在以 `.h` 结尾的文件中的声明，以及通常存储在以 `.cpp` 或 `.cc` 结尾的文件中的定义。以 `.h` 结尾的文件称为头文件。每个类通常有自己的头文件和自己的 `.cpp` 文件。例如：

```cpp
employee.h          // 包含类的声明
employee.cpp        // 包含类方法的定义
```

`employee.h` 文件将包含 `employee` 类的声明：

```cpp
// employee
class employee {
    protected:
        int EmployeeNumber;
        string Name;
    public:
        employee(void);
        employee(int X);
        string name(void);
};
```

`employee.cpp` 文件将包含该类方法的实现。`employee.cpp` 文件还将使用 `include` 语句来包含 `employee.h`。例如：

```cpp
// employee.cpp
#include "employee.h"

employee::employee(void) {
    EmployeeNumber = 1;
}

employee::employee(int X) {
    EmployeeNumber = X;
}

employee::name(void) {
    return Name;
}
```

#### #ifndef, #define 和 #endif 指令

在头文件的顶部包含 `#ifndef` 和 `#define` 预处理器指令通常是一个好习惯。`#ifndef` 表示“如果未定义”。`#define` 指令用于定义符号。我们使用 `#ifndef` 和 `#define` 预处理器指令来定义防止重复定义的符号。例如：

```cpp
#ifndef __EMPLOYEE_H
#define __EMPLOYEE_H

class employee {
    protected:
        int EmployeeNumber;
        string Name;
    public:
        employee(void);
        employee(int X);
        string name(void);
};

#endif
```

类的重复定义出现在文件嵌入其他头文件时。`payroll.h` 头文件可能包含 `employee.h`，而 `accounts_payable.h` 包含 `employee.h`。如果在同一个文件中包含了 `payroll.h` 和 `accounts_payable.h`，那么 `employee` 类将被包含两次。这会导致编译错误。`#ifndef`、`#define` 和 `#endif` 指令可以防止这种错误。

源码库将由所有根据目的或继承相关的头文件和 `.cpp` 文件组成。

#### C++ 中的对象代码（二进制）类库

对相关的源代码文件集合进行编译。对于将放入库中的代码，不会调用链接阶段。在 `GNU C++` 中，`-c` 选项指定只编译不链接代码。此过程将产生以 `.o` 结尾的文件。例如，

```
g++ -c employee.cpp
```
