

调用 TContainer 成员函数 ShowAllObjects()，并通过调用 Sort() 按字母顺序对其进行排序。这些语句很容易理解：

```
container->ShowAllObjects("Before sorting");
container->Sort();
container->ShowAllObjects("After sorting");
```

最后，程序使用以下语句删除容器：

```
delete container;
```

这一行看似简单得令人难以置信，因为程序在运行时跟踪显示了这一点。不仅这一条语句删除了容器对象，它还通过调用虚 ~TMyObject() 析构函数删除了容器中保存的所有对象。为了验证确实如此，请使用 -D 选项编译 container.cpp 模块和 tcontain.cpp 程序，以指定名为 DEBUG 的符号。输入以下命令进行编译和运行测试：

```
$ g++ -c -DDEBUG container.cpp
$ g++ -DDEBUG tcontain.cpp container.o
$ ./a.out
```

DEBUG 符号启用了 TContainer 和 TMyObject 析构函数的跟踪，在屏幕上产生以下输出（为简洁起见，我删除了几行）。正如输出所示，删除容器也会删除存储在容器中的所有对象：

```
Before sorting
Number of objects == 9
Peach Mango Lime Banana Kiwi Grapefruit Orange Lemon Apple
After sorting
Number of objects == 9
Apple Banana Grapefruit Kiwi Lemon Lime Mango Orange Peach
Inside destructor for Apple
Inside destructor for Banana
...
Inside destructor for Orange
Inside destructor for Peach
Deleting container
```

> 注意
> 另请参阅第 17 章“创建类模板”，了解另一种可用于开发可存储各种类型对象的通用类（例如容器）的方法。

## 多重继承

如前所述，多重继承似乎是一个宏伟的想法，直到使用该技术时才显现问题。本章之所以涉及该主题，是因为在使用多重继承时会出现一种常见问题，其类似于由类在层次结构中多次出现而引起的递归。解决方案使用所谓的虚基类——但首先，让我们先看看多重继承的基础知识。

## 加载基类

从多个基类派生类很容易。如许多 C++ 书籍所示，只需使用如下声明继承两个或多个基类即可

```
class D: public A, public B, private C {
// ... class contents
};
```

在此示例中，新的派生类 D 继承了三个类 A、B 和 C。它指定 A 和 B 中的成员在新类中保留其私有、受保护和公共访问状态，但 C 的所有成员都将成为 D 的私有成员。

前述示例的问题在于，虽然在技术上是正确的，但它没有考虑到现实。很有可能，除非你很幸运，否则 A、B 和 C 中某些名称会冲突。例如，假设类 A 和 B 各有一个公共的 Display() 成员函数。要决定调用哪个函数，需要使用类名和 C++ 作用域解析运算符在如下语句中使用：

```
Display();  // ??? Ambiguous. Won't compile.
A::Display();  // Call A's Display() function
B::Display();  // Call B's Display() function
```

除非类 D 声明了自己的 Display() 函数，否则第一行无法编译。如图所示，为了解决多个 Display() 函数之间的名称冲突，你必须使用 A:: 和 B:: 等指定方式。这可行，但很混乱，并且它把调用正确函数的责任放在了程序员身上——而面向对象编程本应帮助你避免这种要求。

## 使用多个基类构造函数

继承多个基类时，必须小心创建初始化所有继承元素的构造函数。通常，你可以这样声明派生类及其构造函数：

```
class D: public A, public B, private C {
public:
  D(): A(), B(), C() { }
};
```

构造函数 D() 调用了三个继承类的构造函数，但在这种情况下，它没有执行其他操作，因此其语句块为空。再次，代码乍一看似乎足够简单。然而，C++ 规定构造函数按列出的顺序调用。如果一个类对象依赖于其中另一个对象，结果冲突可能导致难以理解的结果。当类声明自己为其他类的友元时尤其会发生这种情况，这是一个将在第 18 章“重载你的朋友”中讨论的话题，该章位于第四部分“高级 C++ 技术”。为避免此类麻烦，尽量创建尽可能独立运行的类——无论是否打算使用多重继承，这都是一个好建议。

