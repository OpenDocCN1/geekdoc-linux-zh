

被替换为一个延长的声明，表明类 `string` 本身是一个复杂的嵌套模板。第 22 章“精通标准 string 类”涵盖了 C++ 字符串对象，因此我在这里不会深入介绍该声明。但很有趣的是，你可以使用 GNU 调试器准确地找出 C++ 在编译程序中如何实例化模板和其他类。

## 在模板类中设置断点

在模板类中设置断点的另一种有用方法是使用实例化类函数的名称而不是源代码行号。必要时重新加载 gdb 程序到调试器中，并输入以下命令在 `GetRecord()` 成员函数中设置断点（再次说明，行号可能与你不同）：

```
(gdb) b 'TDatabase<Record>::GetRecord()
Breakpoint 3 at 0x80496e4: file db.h, line 36.
(gdb)
```

实际上，你不必输入那么多。只需输入 `b 'T`（包括撇号），按 Tab，输入 `::Get`，再次按 Tab，就完成了。一般来说，你可以以这种方式使用命令行补全来输入冗长的标识符——毕竟，调试器知道程序中的所有符号，并且可以轻松地使用部分输入搜索匹配项。

> **注意**  
> 我不明白为什么其他调试器没有像命令行符号补全这样方便的功能。可能是因为你必须为这些产品付费！

设置完 `GetRecord()` 中的断点后，运行或继续程序直到它停止：

```
(gdb) cont
Continuing.
Breakpoint 3, TDatabase<Record>::GetRecord (this=0x804b680,
  recnum=0) at db.h:36
36 if (0 <= recnum && recnum < num)
```

这次，`GetRecord()` 的参数似乎是正确的。你现在可以继续逐步执行实例化函数并检查程序的异常处理。完成后输入 `q`。

> **提示**  
> 当程序在成员函数中暂停时，命令 `ptype this` 会显示调用该函数的对象的类型。

## 摘要

模板是创建实际函数和类的蓝图。模板指定一个或多个占位符类型，C++ 在编译期间用实际类型替换它们。这使得编写完全通用的函数和类成为可能，这些函数和类在编译时会根据实际数据类型进行塑形。模板通常写在包含到模块中的头文件中。模板的有用示例包括排序函数和容器类。

有关本章介绍主题的更多信息，请参阅以下章节：

- 第 15 章，“使用虚函数进行编程”
- 第 16 章，“处理异常”
- 第 22 章，“精通标准 string 类”
- 第 23 章，“使用标准模板库（STL）”

## 高级 C++ 技术

- 18 重载你的朋友 401
- 19 重载运算符 411
- 20 自定义 I/O 流 439
- 21  honing Your C++ Skills 473

## 第 18 章

## 重载你的朋友

```
AClass(double arg): value(arg) { }
};
```

类 AClass 声明了一个私有数据成员 value，类型为 double。类构造函数为该成员分配一个参数值。然而，按此写法，AClass 未提供对其私有数据的访问。在 value 初始化后，该私有数据成员就像熊妈妈身边的熊崽一样安全无虞。

接下来，假设你声明另一个类，其中包含 AClass 对象作为数据成员。这是朋友发挥作用的典型设计：

```
class BClass {
private:
    AClass anObject;  // AClass object data member
public:
    BClass(double arg): anObject(arg) { }
    double GetValue() { return anObject.value; } // ???
};
```

该类无法编译，因为其成员函数 GetValue() 试图访问 anObject 中的私有 value 数据成员。因为 value 对 AClass 是私有的，只有该类的成员才能访问该数据成员。

在这种情况下，程序员很容易被诱惑通过将 AClass 中原始的访问说明符从 private 改为 public 来“修复”问题。这可行，但就像用大锤拍苍蝇一样，因为它使 value 对 AClass 的所有用户都可用。所需的是从 BClass 内部对 AClass 私有数据的特殊访问。

解决方案是使 BClass 成为 AClass 的友元。这表示 BClass 对象有权在不使这些成员对任一类之外的语句可用的情况下访问 AClass 内部的私有和受保护成员。要进行此更改，请在需要访问的类内部使用 friend 保留字。在此示例中，BClass 需要使用 AClass 内部的私有 value 数据成员。因此，为了给予 BClass 这样做的权限，AClass 将 BClass 声明为友元。以下是新的 AClass 声明：

```
class AClass {
    friend class BClass;  // BClass is a friend of AClass
private:
    double value;  // AClass and BClass may use this member
    ...
};
```

与之前的 AClass 声明的唯一区别是在 AClass 的开头行之后添加了 friend class BClass。这告诉编译器授予 BClass 访问 AClass 的私有和受保护成员的权限。其他类和其他程序中的其他语句仍被阻止使用 AClass 的受限成员。你可以声明任意数量的类为友元。唯一的限制是 friend 保留字必须出现在类声明内部。关于友元还有一些其他事实值得记住：

- 一个类必须提前命名其所有友元。你不能在运行时创建友元。

