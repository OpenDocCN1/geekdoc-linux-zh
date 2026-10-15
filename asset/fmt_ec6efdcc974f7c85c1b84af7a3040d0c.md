
```cpp
26:   SimpleCat::SimpleCat(SimpleCat& theCat)
27:   {
28:       cout << "Simple Cat Copy Constructor...\n";
29:   }
30: 
31:   SimpleCat::~SimpleCat()
32:   {
33:       cout << "Simple Cat Destructor...\n";
34:   }
35: 
36:   const SimpleCat & FunctionTwo(const SimpleCat & theCat)
37: int main()
38:   {
39:
40:       cout << "Making a cat...\n";
41:       SimpleCat Frisky;
42:       cout << "Frisky is " << Frisky.GetAge() << " years old\n";
43:       int age = 5;
44:       Frisky.SetAge(age);
45:       cout << "Frisky is " << Frisky.GetAge() << " years old\n";
46:       cout << "Calling FunctionTwo...\n";
47:       FunctionTwo(Frisky);
48:       cout << "Frisky is " << Frisky.GetAge() << " years old\n";
49:       return 0;
50:   }
51: 
52:   // functionTwo，传递指向常量对象的引用
53:   const SimpleCat & FunctionTwo(const SimpleCat & theCat)
54:   {
55:       cout << "Function Two. Returning...\n";
56:       cout << "Frisky is now " << theCat.GetAge();
57:       cout << " years old\n";
58:       // theCat.SetAge(8); const!
59:       return theCat;
60:   }
```

```
正在制作一只猫...
SimpleCat 构造函数...
Frisky is 1 year old
Frisky is 5 years old
Calling FunctionTwo...
FunctionTwo. Returning...
Frisky is now 5 years old
Frisky is 5 years old
Simple Cat 析构函数...
```

# 引用

由于参数和返回值仍然通过引用传递，因此没有产生拷贝，拷贝构造函数也没有被调用。然而，`FunctionTwo()` 中的指针现在是常量的，因此无法调用非 const 方法 `SetAge()`。如果第 64 行对 `SetAge()` 的调用没有被注释，程序将无法编译。

注意，在 `main()` 中创建的对象不是常量的，`Frisky` 可以调用 `SetAge()`。非常量对象的地址被传递给 `FunctionTwo()`，因为 `FunctionTwo()` 的声明将指针声明为指向常量对象的常量指针，对象被处理得就像常量一样！

# 引用作为指针的替代方案

列表 9.11 解决了创建额外拷贝的问题，并节省了拷贝构造函数和析构函数的调用。它使用了指向常量对象的指针，从而解决了函数修改对象的问题。然而，这有些繁琐，因为传递给函数的是指针。

由于你知道对象永远不会为空，如果传递引用而不是指针，在函数内部工作会更简单。列表 9.12 阐释这一点。

## 参考文献

对这一行进行粗略检查可能会让你认为 `rFriski` 和 `rBoots` 都是对 `CAT` 对象的引用，但其实你是错的。这句话实际上是说 `rFriski` 是一个 `CAT` 的引用，而 `rBoots`（尽管名字如此）并不是引用，而是一个普通的 `CAT` 变量。这应该重写为：

```
CAT &rFriski, rBoots; own
```

关于这个对象的答案是，引用和变量的声明不应该这样结合。正确的答案是：

```
CAT& rFriski;
CAT boots;
```

最后，许多程序员选择放弃参数，转而采用中间位置，即将 `&` 放在两个符号中间，如案例 2 所示。

当然，到目前为止关于引用运算符 (`&`) 的所有内容同样适用于间接引用运算符 (`*`)。重要的是意识到，理智的人对于“唯一正确方法”的认知存在差异。选择一种适合你自己的风格，并在任何程序中保持一致；清晰性是（且永远是）目标。

许多程序员喜欢以下声明引用和指针的惯例：

1. 将和符号和星号放在中间，两边各留空格。
2. 永远不要将引用、指针和变量全部声明在同一行。

## 不要返回一个不在作用域内的对象的引用！

当 C++ 程序员学习通过引用传递参数时，他们倾向于过度使用。这样做可能会过头。记住，引用始终是其他对象的别名。如果你将引用传入或传出函数，请务必问自己：“我正在别名哪个对象？它在每次使用时是否仍然存在？”

列表 9.13 展示了返回一个已不存在对象的引用的危险。

# 输入 列表 9.13 返回不存在对象的引用

```cpp
1: // Listing 9.13
2: // 返回一个对象的引用
```

# 列表 9.13 续

```cpp
3: // 已不再存在
4:
5: #include <iostream.h>
6:
7: class SimpleCat
8: {
9: public:
10: SimpleCat(int age, int weight);
11: ~SimpleCat();
12: int getAge() { return itsAge; }
13: int getWeight() { return itsWeight; }
14: private:
15: int itsAge;
16: int itsWeight;
17: };
18:
19: SimpleCat::SimpleCat(int age, int weight)
20: {
21: itsAge = age;
22: itsWeight = weight;
23: }
24:
25: SimpleCat &TheFunction();
26:
27: int main()
28: {
29: SimpleCat &rCat = TheFunction();
30: int age = rCat.getAge();
31: cout << "rCat is " << age << " years old!\n";
32: return 0;
33: }
34:
35: SimpleCat &TheFunction()
36: {
37: SimpleCat Frisky(5,9);
38: return Frisky;
39: }
```

```
./l079-13.cxx: In function `class SimpleCat &TheFunction()'
./l079-13.cxx:38: warning: reference to local variable `Frisky' returned
```

> GNU 编译器将无法编译此程序。它在 Borland 编译器上也无法编译，但在 Microsoft 编译器上可以通过。

返回局部变量的引用是一种糟糕的代码实践。

## 参考文献

在第 7–17 行，声明了 `SimpleCat`。在第 29 行，一个 `SimpleCat` 的引用通过调用 `TheFunction()` 的结果进行初始化，该函数在第 25 行声明返回一个 `SimpleCat`。

`TheFunction()` 的函数体声明了一个 `SimpleCat` 类型的局部对象，并初始化了它的年龄和重量。它通过引用返回该局部对象。GNU 编译器足够智能可以捕捉到这个错误并且不会让你运行程序。某些编译器会让你运行程序，但结果不可预期的。

当 `TheFunction()` 返回时，局部对象 `Frisky` 将被销毁（向你保证，这并不痛苦）。该函数返回的引用将是一个不存在对象的别名，这是一件坏事。

## 返回堆上对象的引用

你可能想通过让 `TheFunction()` 在堆上创建 `Frisky` 来解决列表 9.13 中的问题。这样，当你从 `TheFunction()` 返回时，`Frisky` 仍然存在。

这种方法的问题在于：当你用完 `Frisky` 后，该如何处理为 `Frisky` 分配的内存？列表 9.14 展示了这个问题。

```
列表 9.14 内存泄漏
1:    // Listing 9.14
2:    // 解决内存泄漏
3:    #include <iostream.h>
4:
5:    class SimpleCat
6:    {
7:    public:
8:        SimpleCat(int age, int weight);
9:        ~SimpleCat() {}
10:       int GetAge() { return itsAge; }
11:       int GetWeight() { return itsWeight; }
12:   private:
13:       int itsAge;
14:       int itsWeight;
15:   };
16:
17:   SimpleCat::SimpleCat(int age, int weight)
18:   {
19:       itsAge = age;
20:       itsWeight = weight;
21:   }
22:
23:   SimpleCat &TheFunction();
24:
25:   int main()
26:   {
27:       SimpleCat &rCat = TheFunction();
28:       int age = rCat.getAge();
29:       cout << "rCat is " << age << " years old!\n";
30:       return 0;
31:   }
32:
33:   SimpleCat &TheFunction()
34:   {
35:       SimpleCat Frisky(5,9);
36:       return Frisky;
37:   }
```

如果你正在编写一个需要创建内存并将其传回给调用函数，请考虑更改你的接口。让调用函数分配内存，并通过引用将其传递给你的函数。这将所有管理工作从你的程序中移出，交还给准备好删除它的函数。

| 应该 (Do) | 不应该 (DON'T) |
|---|---|
| 必须时，按值传递参数。 | 如果所引项可能会超出作用范围，请按引用传递。 |
| 必须时，按值返回。 | 不要使用指向空对象的引用。 |

## 总结

今天你学习了什么是引用，以及它们与指针的比较。你看到引用必须初始化为指向一个现有对象，并且不能重新赋值指向其他任何内容。对引用执行的任何操作实际上都是对引用的目标对象执行的。证明这一点是，取引用的地址返回的是目标对象的地址。

你看到通过引用传递对象可能比按值传递更高效。引用传递还允许被调用函数将参数中的值改回给调用函数。

你看到函数的参数和函数返回的值都可以按引用传递，这可以通过指针或引用来实现。

你看到如何使用指向常量对象的指针和常量引用在实现按引用传递效率的同时，安全地在函数之间传递值。

## 问答

- **既然指针可以做到引用能做的一切，为什么还需要引用？**
  - 引用更容易使用和理解。间接性被隐藏了，不需要反复对变量进行解引用。

- **既然引用更容易用，为什么还需要指针？**
  - 引用不能为空，且不能重新赋值。指针提供了更大的灵活性，但使用起来稍微困难。

# Q 为什么要从函数中按值返回？

A 如果返回的对象是局部的，你必须按值返回，否则你返回的是一个不存在对象的引用。

# Q 鉴于按引用返回的危险，为什么不总是按值返回？

A 按引用返回可以获得更高的效率。可以节省内存并让程序运行更快。

## 工作坊

工作坊包含测验题，帮助巩固你对所涵盖内容的理解，以及练习题提供使用所学知识的机会。在检查附录 D“练习题和测验题答案”之前，尝试回答测验和练习题，并确保在明天继续之前理解这些答案。

## 测验

1. 引用和指针之间的区别是什么？
2. 什么情况下必须使用指针而不是引用？
3. 如果内存不足以创建你的新对象，`new` 会返回什么？
4. 什么是常量引用？
5. 按引用传递和传递引用的区别是什么？

## 练习题

1. 写一个程序，声明一个 `int`、一个 `int` 的引用和一个指向 `int` 的指针。使用指针和引用来操作该 `int` 的值。
2. 写一个程序，声明一个指向常量整数的常量指针。将指针初始化为整数变量 `varOne`。使用指针为 `varOne` 赋值 7。创建第二个整数变量 `varTwo`。将指针重新赋值为 `varTwo`。先不要编译这个练习。
3. 现在编译练习 2 中的程序。什么产生了错误？什么产生了警告？
4. 写一个产生野指针（stray pointer）的程序。
5. 修复练习 4 中的程序。
6. 写一个产生内存泄漏的程序。
7. 修复练习 6 中的程序。

# 8. 漏洞排除：这个程序哪里有问题？

```cpp
1: #include <iostream>
2: 
3: class CAT
4: {
5: public:
6: CAT(int age) { itsAge = age; }
7: CAT(){}
8: int GetAge() const { return itsAge; }
9: private:
10: int itsAge;
11: };
12: 
13: CAT & MakeCat(int age);
14: int main()
15: {
16: int age = 7;
17: CAT Boots = MakeCat(age);
18: cout << "Boots is " << Boots.GetAge() << " years old\n";
19: return 0;
20: }
21: 
22: CAT & MakeCat(int age)
23: {
24: CAT * pCat = new CAT(age);
25: return *pCat;
26: }
```

9. 修复练习 8 中的程序。

# 第二周

# 第 10 天

# 高级函数

在第 5 天“函数”课程中，你学习了处理函数的基础知识。现在你知道了指针和引用是如何工作的，你就可以用函数做更多事情了。今天你将学习：

- 如何重载成员函数
- 如何重载运算符
- 如何编写支持带有动态分配变量类的函数

# 重载成员函数

在第 5 天，你学习了如何通过编写两个或多个同名但参数不同的函数来实现函数多态（或函数重载）。类成员函数也可以被重载，方式非常相似。

列表 10.1 所示的 `Rectangle` 类有两个 `DrawShape()` 函数。其中一个不接受参数，根据当前类的值绘制矩形。另一个接受两个值（宽度 `width` 和高度 `height`），并根据这些值绘制矩形，忽略当前类的类值。

# 输入 列表 10.1 重载成员函数

```cpp
1: //列表 10.1 重载成员函数
2: #include <iostream>
3: 
4: // Rectangle 类声明
5: class Rectangle
6: {
7: public:
8: // 构造函数
9: Rectangle(int width, int height);
10: Rectangle()
11: 
12: // 重载 DrawShape
13: void DrawShape() const;
14: void DrawShape(int aWidth, int height) const;
15: 
16: private:
17: int itsWidth;
18: int itsHeight;
19: };
20: 
21: // 构造函数实现
22: Rectangle::Rectangle(int width, int height):
23:     itsWidth(width), // 初始化
24:     itsHeight(height)
25:     {} // 空体
26: 
27: 
28: // 用于第三参数的默认值
29: void Rectangle::DrawShape(
30:     int width,
31:     int height,
32:     bool UseCurrentValue = false
33:  ) const
34:  {
35:     int printWidth;
36:     int printHeight;
37: 
38:     if (UseCurrentValue == true)
39:     {
40:         printWidth = itsWidth; // 使用当前类值
41:         printHeight = itsHeight;
```

# 高级函数

```cpp
50: }
51: 
52: // 演示函数的驱动程序
53: int main()
54: {
55:     // 初始化矩形为 30,5
56:     Rectangle theRect(30,5);
57:     cout << "DrawShape:\n";
58:     theRect.DrawShape();
59:     cout << "\nDrawShape(40,2):\n";
60:     theRect.DrawShape(40,2);
61:     return 0;
62: }
```

DrawShape():

列表 10.1 是第 1 周项目的简化版本。为了节省空间，删除了成员函数。主程序被简化为简单的驱动程序。
