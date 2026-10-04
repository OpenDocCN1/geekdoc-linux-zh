
```cpp
28:    cout << "SimpleCat Frisky...\n";
29:    SimpleCat Frisky;
30:    cout << "pRags = new SimpleCat...\n";
31:    SimpleCat * pRags = new SimpleCat;
32:    cout << "delete pRags...\n";
33:    delete pRags;
34:    cout << "Exiting, watch Frisky go...\n";
35:    return 0;
36: }
```

SimpleCat Frisky...

构造函数调用。

SimpleCat *pRags = new SimpleCat...

构造函数调用。

delete pRags...

析构函数调用。

Exiting, watch Frisky go...

析构函数调用。

第 6-13 行声明了简化的 `SimpleCat` 类。第 9 行声明了 `SimpleCat` 的构造函数，第 15-19 行包含了它的定义。第 10 行声明了 `SimpleCat` 的析构函数，第 21–24 行包含了它的定义。

在第 29 行，在栈上创建了 `Frisky`，这导致了构造函数的调用。在第 31 行，在堆上创建了 `pRags` 指向的 `SimpleCat`；构造函数再次调用。在第 33 行，对 `pRags` 调用了 `delete`，析构函数被调用。当函数结束时，`Frisky` 离开作用域，析构函数被调用。

# 访问成员数据

你使用点 (`.`) 运算符访问本地创建的 `Cat` 对象的成员数据和函数。要访问自由存储上的 `Cat` 对象，你必须解引用指针，并在指针所指向的对象上调用点运算符。因此，要访问 `GetAge` 成员函数，你会写：

```cpp
(*pRags).GetAge();
```

使用括号是为了确保在访问 `GetAge()` 之前对 `pRags` 进行解引用。

由于这样做很繁琐，C++ 提供了一个间接访问的简写运算符：指向运算符 (`->`)，它通过输入连字符 (`-`) 后接大于号 (`>`) 创建。C++ 将其视为单个符号。列表 8.6 展示了如何访问在自由存储上创建对象的成员变量和函数。

# 列表 8.6 访问自由存储上对象的成员数据

```cpp
1: // Listing 8.6
2: // 访问堆上对象的成员数据
3: 
4: #include <iostream>
5: 
6: class SimpleCat
7: {
8: public:
9:     SimpleCat(){itsAge = 2; }
10:    ~SimpleCat() {}
11:    int getAge() const { return itsAge; }
12:    void setAge(int age) { itsAge = age; }
13: private:
14:    int itsAge;
15: };
16: 
17: int main()
18: {
19:    SimpleCat * Frisky = new SimpleCat;
20:    cout << "Frisky is " << Frisky->getAge() <<
21:         years old\n";
22:    Frisky->setAge(5);
23:    cout << "Frisky is " << Frisky->getAge() <<
24:         years old\n";
25:    delete Frisky;
26:    return 0;
27: }
```

输出: Frisky is 2 years old

Frisky is 5 years old

分析：在第 19 行，在自由存储上实例化了一个 `SimpleCat` 对象。默认构造函数将其年龄设置为 2，并在第 20 行调用了 `getAge()` 方法。因为这是一个指针，所以使用间接运算符 (`->`) 来访问成员数据和函数。在第 21 行，调用了 `setAge()` 方法，并在第 22 行访问了 `getAge()`。

# 自由存储上的成员数据

类的一个或多个成员数据可以是指指向自由存储上对象的指针。内存可以在类的构造函数或其任一方法中分配，并可以在析构函数中删除，如列表 8.7 所示。

# 列表 8.7 作为成员数据的指针

```cpp
1: // Listing 8.7
2: // 成员数据作为指针
3: 
4:  #include <iostream>
5: 
6:  class SimpleCat
7:  {
8:     public:
9:         SimpleCat();
10:        ~SimpleCat();
11:        int GetAge() const { return *itsAge; }
12:        void setAge(int age) { *itsAge = age; }
13: 
14: 
15:        int GetWeight() const { return *itsWeight; }
16:        void setWeight(int weight) { *itsWeight = weight; }
17: 
18:    private:
19:        int *itsAge;
20:        int *itsWeight;
21:    };
22: 
23: SimpleCat::SimpleCat()
24: {
25:     itsAge = new int(2);
26:     itsWeight = new int(5);
27: }
28: 
29: SimpleCat::~SimpleCat()
30: {
31:     delete itsAge;
32:     delete itsWeight;
33: }
34: 
35: int main()
36: {
37:     SimpleCat *Frisky = new SimpleCat();
38:     cout << "Frisky is " << Frisky->GetAge() << " years old\n";
39:     Frisky->SetAge(5);
40:     cout << "Frisky is " << Frisky->GetAge() << " years old\n";
41:     delete Frisky;
42:     return 0;
43: }
```

输出:

Frisky is 2 years old

Frisky is 5 years old

分析：`SimpleCat` 类在第 18 和 19 行声明了两个成员变量——都是指向整数的指针。内存在构造函数（24-26 行）中分配，并在析构函数（31-32 行）中释放。

# this 指针

每个成员函数都有一个隐藏参数：`this` 指针。`this` 指向具体的对象。因此，在调用 `GetAge()` 或 `SetAge()` 时，包含此隐藏参数。

可以显式地使用此指针，如列表 8.8 所示。

# 列表 8.8 使用 this 指针

```cpp
1:   // Listing 8.8
2:   // 使用指针
3: 
4:   #include <iostream>
5: 
6:   class Rectangle
7:   {
8:   public:
9:       Rectangle();
10:      Rectangle(int length)
11:      void SetLength(int length) { this->itsLength = length; }
12:      int GetLength() const { return this->itsLength; }
13: 
14:      void SetWidth(int width) { itsWidth = width; }
15:      int GetWidth() const { return itsWidth; }
16: 
17:  private:
18:      int itsLength;
19:      int itsWidth;
20:  };
21: 
22:  Rectangle::Rectangle()
23:  {
24:      itsWidth = 5;
25:      itsLength = 10;
26:  }
27:  Rectangle::~Rectangle()
28:  {}
29: 
30:  int main()
31:  {
32:      Rectangle theRect;
33:      cout << "theRect is " << theRect.GetLength()
34:      << << " feet long.";
35:      cout << "theRect is " << theRect.GetWidth()
36:      << << " feet wide.";
37:      theRect.SetLength(20);
38:      theRect.SetWidth(10);
39:      return 0;
40:  }
```

## 指针

```cpp
cout << " feet long.\n";
38: cout << "theRect is " << theRect.GetWidth();
cout << " feet wide.\n";
39: return 0;
40: }
```

theRect is 10 feet long.

theRect is 5 feet wide.

theRect is 20 feet long.

theRect is 10 feet wide.

`GetLength()` 和 `GetLength()` 访问函数显式地使用此指针来访问 `Rectangle` 对象的成员变量。而 `SetWidth` 和 `GetWidth` 访问器则没有使用。尽管语法易于理解，但它们的行为并没有区别。

如果这个指针仅仅止于此，那么费心去研究它也就意义了。然而，这个指针是一个指针；它存储了对象的内存地址。因此，它可以是一个强大的工具。

你将在第 10 天“高级函数”中讨论运算符重载时，看到这个指针的实际用途。现在，你的目标是了解这个指针并理解它是什么：一个指向对象本身的指针。

你不需要担心创建或删除这个指针。编译器会处理这些工作。

# 悬空指针、野指针或无效指针

一种糟糕且难以发现的错误来源之一是悬空指针。悬空指针（也称为野指针或无效指针）是在你对一个指针调用 `delete`——从而释放它所指向的内存——之后，在没有对其重新赋值或将其设置为 `NULL` 的情况下再次使用该指针时产生的。如果你尝试再次使用该指针，结果将是不可预测的，如果你运气好，你的程序将会崩溃。

这就像邮购公司搬走了，但你仍然按了手机上预设的按钮。可能什么都没有发生——空旷的仓库里电话铃响了。也许电话号码已经被重新分配给了一个军药工厂，你的电话触发了爆炸物并炸毁了你的整个城市！

简而言之，在对指针调用 `delete` 后不要再使用它。指针仍然指向旧的内存区域，但该内存已空可以存放其他数据；使用该指针会导致你的程序崩溃。更糟糕的是，程序可能会继续愉快地运行，并在几分钟后才出问题。这被称为定时弹，一点也不好玩。为了安全起见，在删除指针后，将其设置为 `NULL`。这会让指针失效。

> 悬空指针通常被称为野指针或无效指针。这仅仅是术语上的区别。

列表 8.9 展示了如何创建一个悬空指针。

> 此程序刻意创建了一个悬空指针。不要运行此程序——如果你运气好的话，它会崩溃。

# 列表 8.9 创建悬空指针

```cpp
// Listing 8.9
// 展示悬空指针
typedef unsigned short int USH;
#include <iostream.h>

int main() {
    USH *pInt = new USH;
    *pInt = 10;
    cout << "*pInt: " << *pInt << endl;
    delete pInt;

    long *pLong = new long;
    *pLong = 90000;
    cout << "*pLong: " << *pLong << endl;
    // 噢哦，这个被删除了！
    *pInt = 20;
    cout << "*pInt: " << *pInt << endl;
    cout << "*pLong: " << *pLong << endl;
    delete pLong;
    return 0;
}
```

```
*pInt: 10
*pLong: 90000
*pInt: 20
*pLong: 65556
```

（你的输出可能看起来不同。）

第 8 行将 `pInt` 声明为指向 `USH` 的指针，`pInt`指向新分配的内存。第 9 行将值 10 放入该内存，第 10 行打印它的值。在打印值之后，对指针调用了 `delete`。`pInt` 现在是一个悬空指针（或无效指针）。

第 13 行声明了一个新指针 `pLong`，它指向 `new` 分配的内存。第 14 行将值 90000 赋值给 `pLong`，第 15 行打印它的值。

第 17 行将值 20 赋值给 `pInt` 所指向的内存，而 `pInt` 不再指向任何有效区域。在 `delete` 之后，向内存赋值无疑将是一场灾难。

第 19 行打印 `pInt` 处的值。果真如此，它是 20。第 20 行打印 20，即 `pLong` 处的值；它突然变成了 65556。随之产生了两个问题：

1. 在 `pLong` 未被触动的情况下，它的值是如何变化的？

2. 当在第 17 行使用 `pInt` 时，20 去到哪里了？

正如你所猜的，这些是相关的问题。当第 7 行在 `pInt` 处放置值时，编译器将值 20 放在 `pInt` 之前指向的内存位置。但由于该内存已第 11 行释放，编译器可以重新分配它。当第 13 行创建 `pLong` 时，它被赋予了 `pInt` 旧的内存位置。（在某些计算机上这可能不会发生，取决于这些值存储在内存的什么。）当值 20 被赋值给 `pInt` 之前指向的位置时，它覆盖了 `pLong` 所指向的值。这被称为悬空指针错误。

# 常量指针

你可以将 `const` 关键字放在类型之前、类型之后或两处都用。例如：

```cpp
const int * p1; // 指向的 int 是常量
int * const p2; // p2 是常量，它不能指向其他地方
const int * const p3 两者都是常量
```

区分这些内容的技巧是看 `const` 右侧的内容以确定声明的是什么。如果类型在 `const` 右侧，则值是常量。如果变量在 `const` 右侧，则指针变量本身是常量。

# 常量指针与常量成员函数

在第 6 天“基础类”中，你学习了可以将 `const` 关键字应用于成员函数。当函数声明为 `const` 时，编译器会将任何从函数内部更改对象数据的尝试标记为错误。

如果你声明一个指向常量对象的指针，那么通过该指针调用的方法只能是 `const` 方法。列表 8.10 展示了这一点。

# 列表 8.10 续

```cpp
27:  Rectangle::Rectangle()
28:  {}
29: 
30:  int main()
31:  {
32:      Rectangle* pRect = new Rectangle;
33:      const Rectangle * pConstRect = new Rectangle;
34:      Rectangle * pConstRectPtr = new Rectangle;
35: 
36:      cout << "pRect width: " << pRect->GetWidth()
37:      << "\n";
38:      cout << "pConstRect width: " << pConstRect->
39:      GetWidth() << "\n";
40:      pRect->SetWidth(10);
41:      // pConstRect->SetWidth(10)
42:      pConstRectPtr->SetWidth(10);
43: 
44:      cout << "pRect width: " << pRect->GetWidth()
45:      << "\n";
46:      cout << "pConstRect width: "
47:      << pConstRect->GetWidth() << " "\n";
48:      cout << "pConstRectPtr width: "
49:      << pConstRectPtr->GetWidth() << " "\n";
50: }
```

pRect width: 5 feet pConstRect width: 5 feet pConstRectPtr width: 5 feet pRect width: 10 feet pConstRect width: 5 feet pConstRectPtr width: 10 feet

第 6–19 行声明了 `Rectangle`。第 14 行将 `GetWidth()` 成员方法声明为 `const`。第 32 行声明了一个指向 `Rectangle` 的指针。第 33 行声明了 `pConstRect`，它是一个指向常量 `Rectangle` 的指针。第 34 行声明了 `pConstRectPtr`，它是一个指向 `Rectangle` 的常量指针。

第 36–38 行打印了它们的值。
