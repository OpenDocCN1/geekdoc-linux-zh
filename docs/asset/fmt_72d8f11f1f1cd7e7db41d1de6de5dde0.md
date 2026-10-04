
# C++ 代码示例：Employee 类与 String 类的包含关系

```cpp
17:    long GetSalary() const { return itsSalary; }

18:

19:    void SetFirstName(const String & fName)
20:      { itsFirstName = fName; }
```

```cpp
21:    void SetLastName(const String & lName)
22:    { itsLastName = lName; }
23:    void SetAddress(const String & address)
24:    { itsAddress = address; }
25:    void SetSalary(long salary) { itsSalary = salary; }
26:    private:
27:        String  itsFirstName;
28:        String  itsLastName;
29:        String  itsAddress;
30:        long    itsSalary;
31:    };

33: Employee::Employee():
34:    itsFirstName(""),
35:    itsLastName(""),
36:    itsAddress(""),
37:    itsSalary(0)
39:    }

40: Employee::Employee(char * firstName, char * lastName,
41:    char * address, long salary):
42:    itsFirstName(firstName),
43:    itsLastName(lastName),
44:    itsAddress(address),
45:    itsSalary(salary)
46:    }

48: Employee::Employee(const Employee & rhs):
49:    itsFirstName(rhs.GetFirstName()),
50:    itsLastName(rhs.GetLastName()),
51:    itsAddress(rhs.GetAddress()),
52:    itsSalary(rhs.GetSalary())
53:    }

55: Employee::~Employee() {}

57: Employee & Employee::operator=(const Employee & rhs)
58:    {
59:        if (this == &rhs)
60:            return *this;
62:        itsFirstName = rhs.GetFirstName();
63:        itsLastName = rhs.GetLastName();
64:        itsAddress = rhs.GetAddress();
65:        itsSalary = rhs.GetSalary();
67:        return *this;
69:    }
```

# 高级继承

```cpp
int main() {
    Employee Edie("Jane", "Doe", "1461 Shore Parkway", 20000);
    Edie.SetSalary(50000);
    String LastName = "Levine";
    Edie.SetLastName(LastName);
    Edie.SetFirstName("Edythe");
    cout << "Name: " << Edie.GetFirstName().GetString() << "\n";
    cout << " " << Edie.GetLastName().GetString() << "\n";
    cout << "Address: " << Edie.GetAddress().GetString() << "\n";
    cout << "Salary: " << Edie.GetSalary() << "\n";
    return 0;
}
```

> 将列表 15.1 中的代码保存到名为 `String.hpp` 的文件中。然后，每当你需要 `String` 类时，都可以使用 `#include "String.hpp"` 来包含列表 15.1，如列表 15.2 所示。

为了书中演示方便，我将实现与类的声明放在了一起。在实际程序中，你会将类声明保存在 `String.hpp` 中，将实现保存在 `String.cpp` 中。然后你将 `String.cpp`（使用 makefile）添加到你的程序中，并让 `String.cpp` `#include "String.hpp"`。

输出结果：
```text
Name: Edythe Levine
Address: 1461 Shore Parkway
Salary: 50000
```

在第 72 行，创建了一个 `Employee` 对象，并传入四个值来初始化该 `Employee` 对象。在第 73 行，调用了 `Employee` 访问函数 `SetSalary()`，传入常量值 50000。注意，在实际程序中，这将是一个动态值（在运行时设置）或一个常量。

在第 74 行，创建了一个字符串并初始化为 C++ 字符串常量。该对象随后被用作第 75 行 `SetLastName()` 的参数。

在第 76 行，调用了 `Employee` 函数 `SetFirstName()` 并传入了另一个字符串常量。然而，如果你足够关注细节，你会发现 `Employee` 并没有一个接受字符字符串作为参数的 `SetFirstName()` 函数；`SetFirstName()` 需要的是一个常量字符串引用。

编译器解决了这个问题，因为它知道如何从常量 char 字符字符串创建一个字符串。它之所以知道这一点，是因为你已经在列表 15.1 的第 9 行告诉了它如何做。

## 访问被包含类的成员

`Employee` 对象对 `String` 的成员变量没有特有的访问权限。如果 `Employee` 对象 `Edie` 尝试访问其自身 `itsFirstName` 成员变量的成员变量 `itsLen`，它将得到编译时错误。这并不是什么负担，访问器函数为 `String` 类提供了一个接口，`Employee` 类不需要担心实现细节，正如它不需要担心整数变量 `itsSalary` 是如何存储其信息的。

## 过滤对包含成员的访问

注意，`String` 类提供了 `operator+`。`Employee` 类的设计者通过声明所有字符串访问器（如 `GetFirstName()`）返回常量引用，从而阻止了在 `Employee` 对象上调用 `operator+`。因为 `operator+` 不（也无法）成为一个 `const` 函数（它会改变被调用的对象），尝试编写以下内容将导致编译时错误：

```cpp
String buffer = Edie.GetFirstName() + Edie.GetLastName();
```

`GetFirstName()` 返回一个常量 `String` 对象（注：此处应为常量引用），而你不能在常量对象上调用 `operator+`。

要修复此问题，将 `GetFirstName()` 重载为非 const：

```cpp
const String & GetFirstName() const { return itsFirstName; }
String & GetFirstName() { return itsFirstName; }
```

注意，返回值不再是 `const`，且成员函数本身不再是 `const`。仅更改返回值不足以重载该函数；你必须更改函数的 `const` 属性。

## 包含的代价

重要的是，每当构造或创建 `Employee` 副本时，`Employee` 的用户都要为这些字符串付出代价。取消列表 15.1 中第 38, 51, 63, 75, 84 行的 `cout` 语句，可以看到这些被调用的频率。列表 15.3 重写了驱动程序以打印对象创建和销毁的位置。

# 高级继承（部分 2）

要编译此内容，请取消列表 15.1 中第 38, 51, 63, 75, 84 和 99 行的注释。

## 列表 15.3 包含类

```cpp
1: #include "String.hpp"
2: class Employee
3: {
4: public:
5: Employee();
6: Employee(char *, char *, long);
7: Employee(const Employee&);
8: Employee& operator=(const Employee&);
9: const String& GetFirstName() const
10: { return itsFirstName(); }
11: const String& GetLastName() const
12: { return itsLastName(); }
13: const String& GetAddress() const
14: { return itsAddress(); }
15: long GetSalary() const
16: { return itsSalary; }
17: void SetFirstName(const String& fName)
18: { itsFirstName = fName; }
19: void SetLastName(const String& lName)
20: { itsLastName = lName; }
21: void SetAddress(const String& address)
22: { itsAddress = address; }
23: void SetSalary(long salary)
24: { itsSalary = salary; }
25: private:
26: String itsFirstName;
27: String itsLastName;
28: String itsAddress;
29: long itsSalary;
30: };
31: Employee::Employee():
32: itsFirstName(""),
33: itsLastName(""),
34: itsAddress(""),
35: itsSalary(0)
36: }
37: Employee::Employee(char * firstName, char * lastName,
38: char * address, long salary):
39: itsFirstName(firstName),
40: itsLastName(lastName),
41: itsAddress(address),
42: itsSalary(salary)
43: }
44: Employee::Employee(const Employee & rhs):
45: itsFirstName(rhs.GetFirstName()),
46: itsLastName(rhs.GetLastName()),
47: itsAddress(rhs.GetAddress()),
48: itsSalary(rhs.GetSalary())
49: }
50: Employee::~Employee() {}
51: Employee & Employee::operator=(const Employee & rhs)
52: {
53: if (this == &rhs)
54: return *this;
55: itsFirstName = rhs.GetFirstName();
56: itsLastName = rhs.GetLastName();
57: itsAddress = rhs.GetAddress();
58: itsSalary = rhs.GetSalary();
59: return *this;
60: }
61: int main()
62: {
63: cout << "Creating Edie...\n";
64: Employee Edie("Jane", "Doe", "1461 Shore Parkway", 20000);
65: Edie.SetSalary(50000);
66: cout << "Calling SetFirstName with char *...\n";
67: Edie.SetFirstName("Edythe");
68: cout << "Creating temporary LastName...\n";
69: String LastName("Levine");
70: Edie.SetLastName(LastName);
71: cout << "Name: ";
```

```text
1: Creating Edie...
2: String(char*) constructor
3: String(char*) constructor
4: String(char*) constructor
5: Calling SetFirstName with char "..."
6: String(char*) constructor
7: String destructor
8: Creating temporary LastName...
9: String(char*) constructor
10: Name: Edythe Levine
11: Address: 1461 Shore Parkway
12: Salary: 20000
13: String destructor
14: String destructor
15: String destructor
16: String destructor
```

列表 15.3 使用与列表 15.1 和 15.2 相同的类声明。然而，`cout` 语句已经取消了注释。列表 15.3 的输出进行了编号，以便分析。

在列表 15.3 的第 63 行，打印了 `Creating Edie...` 语句，如输出的第 1 行所示。在第 64 行，创建了一个带有四个参数的员工对象 `Edie`。输出显示 `String` 的构造函数被调用了三次，正如预期那样。

第 66 行打印了一条信息语句，第 67 行是 `Edie.SetFirstName("Edythe")` 语句。该语句导致从字符 `"Edythe"` 创建了一个临时字符串，如输出的第 6 和 7 行所示。注意，临时字符串在赋值语句中使用后立即被销毁。

在第 69 行，在程序体中创建了一个 `String` 对象。程序员正在显式地执行之前在语句中隐式执行的操作。这次你在输出的第 9 行看到了构造函数，但没有析构函数。该对象直到函数结束离开作用域时才会被销毁。

在第 82-88 行（推测行号），当 `Employee` 对象离开作用域时，其内部的字符串会被销毁，第 78 行创建的字符串 `LastName` 在离开作用域时也会被销毁。

## 按值拷贝

列表 15.3 说明了创建一个 `Employee` 对象导致了五次 `String` 构造函数调用。列表 15.4 再次重写了驱动程序。这次静态成员变量 `ConstructorCount` 被取消了注释并被使用。

对列表 15.1 的分析表明，每当调用字符串构造函数时，`ConstructorCount` 都会增加。列表 15.4 中的驱动程序调用了打印函数，并传入了 `Employee` 对象，首先通过引用传递，然后通过值传递。`ConstructorCount` 记录了当员工作为参数传递时创建了多少字符串对象。

> 注意：要编译此列表，请保留你在列表 15.1 中取消注释的那些行以运行列表 15.3，此外，还需要取消列表 15.1 中的第 23、39、52、64、76 和 153 行。

## 列表 15.4 值传递

```cpp
1: #include "String.hpp"
2:
3: class Employee
4: {
5:
6: public:
7:     Employee();
8:     Employee(char *, char *, char *, long);
9:     Employee(const Employee&);
10:    Employee(const Employee&);
11:    Employee &operator=(const Employee&);
12:
13:    String &FirstName() const
14:    { return firstName; }
15:    String & GetLastName() const { return lastName; }
16:    String & GetAddress() const { return itsAddress; }
17:    long GetSalary() const { return itsSalary; }
18:
19:    void SetFirstName(const String &fName)
20:    { itsFirstName = fName; }
21:    void SetLastName(const String &lName)
22:    { itsLastName = lName; }
23:    void SetAddress(const String & address)
24:    { itsAddress = address; }
25:    void SetSalary(long salary) { itsSalary = salary; }
26:
27: private:
28:    String itsFirstName;
29:    String itsLastName;
30:    String itsAddress;
```
