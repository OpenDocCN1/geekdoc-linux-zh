
如前所述，多重继承似乎是一个宏伟的想法，直到使用该技术时才显现问题。本章之所以涉及该主题，是因为在使用多重继承时会出现一种常见问题，其类似于由类在层次结构中多次出现而引起的递归。解决方案使用所谓的虚基类——但首先，让我们先看看多重继承的基础知识。

# 多重继承的基础知识

## 加载基类

从多个基类派生类很容易。如许多 C++ 书籍所示，只需使用如下声明继承两个或多个基类即可

```
class D: public A, public B, private C {
// ... class contents
};
```

在此示例中，新的派生类 `D` 继承了三个类 `A`、`B` 和 `C`。它指定 `A` 和 `B` 中的成员在新类中保留其私有、受保护和公共访问状态，但 `C` 的所有成员都将成为 `D` 的私有成员。

前述示例的问题在于，虽然在技术上是正确的，但它没有考虑到现实。很有可能，除非你很幸运，否则 `A`、`B` 和 `C` 中某些名称会冲突。例如，假设类 `A` 和 `B` 各有一个公共的 `Display()` 成员函数。要决定调用哪个函数，需要使用类名和 C++ 作用域解析运算符在如下语句中使用：

```
Display();  // ??? Ambiguous. Won't compile.
A::Display();  // Call A's Display() function
B::Display();  // Call B's Display() function
```

除非类 `D` 声明了自己的 `Display()` 函数，否则第一行无法编译。如图所示，为了解决多个 `Display()` 函数之间的名称冲突，你必须使用 `A::` 和 `B::` 等指定方式。这可行，但很混乱，并且它把调用正确函数的责任放在了程序员身上——而面向对象编程本应帮助你避免这种要求。

## 使用多个基类构造函数

继承多个基类时，必须小心创建初始化所有继承元素的构造函数。通常，你可以这样声明派生类及其构造函数：

```
class D: public A, public B, private C {
public:
  D(): A(), B(), C() { }
};
```

构造函数 `D()` 调用了三个继承类的构造函数，但在这种情况下，它没有执行其他操作，因此其语句块为空。再次，代码乍一看似乎足够简单。然而，C++ 规定构造函数按列出的顺序调用。如果一个类对象依赖于其中另一个对象，结果冲突可能导致难以理解的结果。当类声明自己为其他类的友元时尤其会发生这种情况，这是一个将在第 18 章“重载你的朋友”中讨论的话题，该章位于第四部分“高级 C++ 技术”。为避免此类麻烦，尽量创建尽可能独立运行的类——无论是否打算使用多重继承，这都是一个好建议。

# 使用虚拟基类

派生类及其基类形成一个类层次结构，即使在相对简单的程序中也可能变得极其复杂。一个基类可以被一个或多个其他类继承，而这些类又可以成为更多类的基类。所有这些类因此通过单继承或多继承相互关联，就像圣经人物彼此繁衍一样，直到没人能分清谁与谁有关。

在如此复杂的类族谱中，尤其是在涉及多继承时，冲突很容易理解。最常见的冲突之一是当派生类继承了太多份特定的基类——就像彩票赢家一样，例如，他们突然拥有了比以前知道的更多的“表亲”。

为了演示派生类如何陷入继承困境，请检查以下程序中的类，见清单 15.8，`franch.cpp`。该程序使用了虚构公司与三个虚构加盟商 `Bob`、`Ted` 和 `Alice` 之间熟悉的关系。该程序可能看起来有点傻，但从现实世界借用熟悉的关系有助于解释多继承中一个典型且常常令人沮丧的问题。

```
// LISTING 15.8    FRANCH.CPP
#include <iostream.h>
#include <string.h>    // Need strlen(), strcpy()
#include <stdlib.h>    // Need free()

class Company {
private:
    char *name;
public:
    Company(const char *s) {
        name = new char[strlen(s) + 1];
        strcpy(name, s);
        cout << " In constructor for " << name;
        Display();
    }
    virtual ~Company() {
        cout << " In destructor for ";
        Display();
        delete[] name;
    }
    void Display() { cout << name << endl; }
};
```

## LISTING 15.8 CONTINUED

```
class Jennys: public Company {
public:
    Jennys(): Company("Jenny's") { }
};

class McDoughles: public Company {
public:
    McDoughles(): Company("McDoughles") { }
};

class BurgerQueen: public Company {
public:
    BurgerQueen(): Company("BurgerQueen") { }
};

class Bob:
    public Jennys,
    public McDoughles { 
};

class Ted:
    public McDoughles,
    public BurgerQueen { 
};

class Alice:
    public Jennys,
    public McDoughles,
    public BurgerQueen { 
};

int main()
{
    Bob *bobp;
    Ted *tedp;
    Alice *alicep;

    cout << endl << "Initializing Bob's restaurant" << endl;
    bobp = new Bob;
    cout << "Initializing Ted's restaurant" << endl;
    tedp = new Ted;
    cout << "Initializing Alice's restaurant" << endl;
    alicep = new Alice;

    cout << endl << "Deleting Bob's restaurant" << endl;
    delete bobp;
    cout << "Deleting Ted's restaurant" << endl;
    delete tedp;
    cout << "Deleting Alice's restaurant" << endl;
    delete alicep;
    return 0;
}
```

图 15.1 显示了 `Franch.cpp` 中类之间的关系。层次结构的根是 `Company` 类，它作为三个派生类 `Jennys`、`McDougles` 和 `BurgerQueen` 的基类。这些“公司”类都派生自 `Company`，每个类因此继承了 `name` 数据成员和 `display()` 成员函数。

## Figure 15.1

三个类 `Bob`、`Ted` 和 `Alice` 使用多继承派生而来。

![](img/6eab91cc30158075ed10d0cabbac9029_366_0.png)

我们三位冒险的投资者 `Bob`、`Ted` 和 `Alice` 使用多继承派生而来（参见清单 15.8）。类 `Bob` 将他的餐饮帝国派生自两个 `Company` 类 `Jennys` 和 `McDougles`。类 `Ted` 将他的财富派生自 `McDougles` 和 `BurgerQueen`。`Alice` 是该群体中最有进取心的灵魂，承担了三个 `Company` 类：`Jennys`、`McDougles` 和 `BurgerQueen`。当你使用以下命令编译并运行程序时，你会看到一份报告，表明为最高层类的对象创建时调用了构造函数和析构函数，`Bob`、`Ted` 和 `Alice`：

```
$ g++ franch.cpp
$ ./a.out
```

虽然我在这里没有展示程序冗长的输出，但在屏幕上你会看到使用如下语句创建对象的结果

```
bobp = new Bob;
...
delete Bob;
```

正如你在运行程序时屏幕上看到的那样，复杂类层次结构的所有正确构造函数和析构函数都被调用。到目前为止，一切顺利。但如果从公司和投资者组派生出另一个类，类关系中就会出现一个微妙的问题。假设一家公司收购了一些母公司和选定的加盟商。正如现实世界的公司金融中一样，公司和人员之间的复杂关系很容易失控。考虑一个 `Corporation` 类，它试图通过多继承继承 `McDougles` 公司以及加盟商 `Ted` 和 `Alice`：
