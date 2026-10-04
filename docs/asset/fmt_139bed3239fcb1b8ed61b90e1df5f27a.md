
## 代码示例：前置递增运算符

```cpp
34:     Counter i;

35:     cout << "The value of i is " << i.GetItsVal() << endl;

36:     i.Increment();

37:     cout << "The value of i is " << i.GetItsVal() << endl;

38:     ++i;

39:     cout << "The value of i is " << i.GetItsVal() << endl;

40:     Counter a = ++i;

41:     cout << "The value of a: " << a.GetItsVal();

42:     cout << " and i: " << i.GetItsVal() << endl;

43:     return 0;

44: }
```

**输出**
```
The value of i is 0
The value of i is 1
The value of i is 2
The value of a: 3 and i: 3
```

## 分析

`operator++` 的实现（第 26-30 行）已更改为引用 `this` 指针并返回当前对象。这提供了一个赋值给 `a` 的 `Counter` 对象。正如之前讨论的，如果 `Counter` 对象分配了内存，那么覆盖拷贝构造将是非常重要的。在这种情况下，默认拷贝构造函数运行良好。

注意返回的值是一个 `Counter` 引用，从而避免了创建额外的临时对象。它是一个 `const` 引用，因为该值不应该被使用 `this` 的函数修改。

## 重载后置运算符

到目前位置，你已经重载了前置运算符。如果你想重载后置递增运算符呢？问题来了：如何区分前置和后置？按照惯例，在运算符声明中提供一个整数变量作为参数。该参数的值被忽略；它是这是一个后置运算符的信号。这在列表 10.12 中展示了这一点。

## 学习前置和后置的区别

在编写后置运算符之前，你必须理解它与前置运算符的区别。我们在第 4 天的“表达式和语句”中详细回顾过这一点（参见列表 4.3）。

### 高级函数

复习一下，前缀表示“先增，后取”，后置表示“先取，后增”。

因此，虽然前缀运算符可以简单地增加值并返回对象本身，但后置运算符必须返回增加之前存在的值。为了做到这一点，我们必须创建一个临时对象来保存原始值，增加原始对象的值，并返回该临时对象。

我们应该再次过一遍这一点。考虑以下行代码：

```cpp
a = x++;
```

如果 x 为 5，在执行该语句后 a 为 5，但 x 为 6。因此，我们返回了 x 的值并赋值给 a，然后增加了 x 的值。如果 x 是一个对象，它的后置运算符必须将原始值（5）存储在一个临时对象中，将 x 的值增加到 6，然后返回该临时对象以将其值赋值给 a。

注意，由于我们返回的是临时对象，我们必须按值返回而不是按引用返回，因为临时对象在函数返回时刻就会超出作用域。

列表 10.12 展示了前缀和后置运算符的使用。

## 列表 10.12 前缀和后置运算符

```cpp
1:    // Listing 10.12
2:    // Prefix and Postfix Operators
3:
4:
5:    #include <iostream.h>
6:
7:    class Counter
8:    {
9:        public:
10:           Counter();
11:           ~Counter()
12:           int GetItsVal()const { return itsVal; }
13:           void SetItsVal(int x) { itsVal = x; }
14:           const Counter& operator++ ();    // 前缀
15:
16:           const Counter operator++ (int); // 后置
17:
18:       private:
19:           int itsVal;
20:       };
21:
22:       Counter::Counter():
23:           itsVal(0)
24:       {}
```

## 列表 10.12 续

```cpp
25:   const Counter& Counter::operator++()
26:   {
27:       ++itsVal;
28:       return *this;
29:   }
30: 
31:   const Counter Counter::operator++(int x)
32:   {
33:       Counter temp(*this);
34:       ++itsVal;
35:       return temp;
36:   }
37: 
38:   int main() {
39:       Counter i;
40:       cout << "The value of i is " << i.GetItsVal() << endl;
41:       i++;
42:       cout << "The value of i is " << i.GetItsVal() << endl;
43:       i++;
44:       cout << "The value of a: " << i.GetItsVal() << endl;
45:       Counter a = i++;
46:       cout << "The value of a: " << a.GetItsVal() << endl;
47:       cout << "and i: " << i.GetItsVal() << endl;
48:       a = i++;
49:       cout << "The value of a: " << a.GetItsVal() << endl;
50:       cout << "and i: " << i.GetItsVal() << endl;
51:       return 0;
52:   }
```

**输出**
```
The value of i is 0
The value of i is 1
The value of i is 2
The value of a: 3 and i: 3
The value of a: 3 and i: 4
```

## 分析

后置运算符在第 16 行声明，在第 31–36 行实现。注意，第 14 行前缀运算符的原型不包含整数 (x)，这用于其正常语法。后置运算符使用一个标志位 (x) 来指示它是后置而非前缀。然而，标志位的值 (x) 从未被使用。

### 高级函数

## 运算符重载：一元运算符

声明一个重载运算符的方法与声明函数相同。使用关键字 `operator`，后跟要重载的运算符。一元运算符函数不接受参数，后置递增和递减除外，这些运算符接收一个整数作为标志位。

**示例 1**
```cpp
const Counter& Counter::operator++();
```

**示例 2**
```cpp
Counter Counter::operator--(int);
```

## 使用加法运算符

递增运算符是一元运算符。它只操作一个对象。加法运算符 (`+`) 是二元运算符，涉及两个对象。你如何为 `Counter` 实现 `+` 运算符重载？

目标是能够声明两个 `Counter` 变量并将它们相加，如下所示：

```cpp
Counter varOne, varTwo, varThree;
varThree = varOne + varTwo;
```

再次，你可以从编写一个函数 `Add()` 开始，该函数接受一个 `Counter` 作为参数，相加值，并返回一个带有结果的 `Counter`。列表 10.13 展示了这种方法。

## 列表 10.13 Add 函数

```cpp
// Listing 10.13
// Add 函数
#include <iostream>

class Counter {
public:
    Counter();
    Counter(int initialValue);
    ~Counter()
    int GetItsVal() const { return itsVal; }
    void SetItsVal(int x) { itsVal = x; }
    Counter Add(const Counter &);
private:
    int itsVal;
};

Counter::Counter(int initialValue):
    itsVal(initialValue)
{}

Counter::Counter():
    itsVal(0)
{}

Counter::Add(const Counter & rhs)
{
    return Counter(itsVal + rhs.GetItsVal());
}

int main()
{
    Counter varOne(2), varTwo(4), varThree;
    varThree = varOne.Add(varTwo);
    cout << "varOne: " << varOne.GetItsVal() << endl;
    cout << "varTwo: " << varTwo.GetItsVal() << endl;
    cout << "varThree: " << varThree.GetItsVal() << endl;
    return 0;
}
```

**输出**
```
varOne: 2
varTwo: 4
varThree: 6
```

## 分析

`Add()` 函数在第 15 行声明。它接收一个常量 `Counter` 引用作为要加对象的数值。它返回一个 `Counter` 对象，赋值给赋值语句的左侧，如第 37 行所示，`varOne` 是对象，`varTwo` 是 `Add` 函数的参数，结果赋值给 `varThree`。

为了在不初始化的情况下创建 `varThree`，需要一个默认构造函数。默认构造函数将 `itsVal` 初始化为 0，如第 26–28 行所示。由于 `varOne` 和 `varTwo` 需要初始化为非零值，创建了另一个构造函数，如第 22–24 行所示。为第 11 行的构造函数提供默认值 0。

## 重载 operator+

`Add()` 函数本身位于第 30–33 行。它可以工作，但使用起来不自然。重载 `+` 运算符会让 `Counter` 类的使用更加自然。列表 10.14 展示了这一点。

## 列表 10.14 operator+

```cpp
1:  // Listing 10.14
2:  // Overload operator (+)
3:
4:
5:
6:  #include <iostream>
7:
8:  class Counter
9:  {
10:     public:
11:         Counter();
12:         Counter(int initialValue);
13:         ~Counter()
14:         int GetItsVal() const { return itsVal; }
15:         void SetVal(int x) { itsVal = x; }
16:         Counter operator+(const Counter &);
17:     private:
18:         int itsVal;
19:     
20:
21:     Counter::Counter(int initialValue):
22:     itsVal(initialValue)
23:     }
24:
25:     Counter::Counter():
26:     itsVal(0)
27:     }
28:
29:     Counter::operator+(const Counter & rhs)
30:     {
31:         return Counter(itsVal + rhs.GetItsVal());
32:     }
33:
34:     int main()
35:     {
36:         Counter varOne(2), varTwo(4), varThree;
37:         varThree = varOne + varTwo;
38:         cout << "varOne: " << varOne.GetItsVal() << endl;
39:         cout << "varTwo: " << varTwo.GetItsVal() << endl;
40:         cout << "varThree: " << varThree.GetItsVal() << endl;
41:         return 0;
42:     }
```

**输出**
```
varOne: 2
varTwo: 4
varThree: 6
```

## 分析

`operator+` 在第 15 行声明，在第 28–31 行定义。将这些与上一个列表中 `Add()` 函数的声明和定义比较；它们几乎是相同的。然而，它们的使用语法完全不同。说这个：
`varThree = varOne + varTwo;`
比说：
`varThree = varOne.Add(varTwo);`
更自然。

变化并不大，但足以让程序更容易使用和理解。

> **注意**
> 用于重载 `operator++` 的技术可以应用于其他一元运算符，例如 `operator--`。

### 运算符重载：二元运算符

二元运算符的创建方式与一元运算符相同，但它们接收一个参数。该参数是相同类型对象的常量引用。

**示例 1**
```cpp
Counter::operator+(const Counter & rhs);
```

**示例 2**
```cpp
Counter::operator-(const Counter & rhs);
```

## 运算符重载中的额外问题

重载的运算符可以是成员函数（如本节所述），也可以是非成员函数。后者将在第 14 天“特殊类和函数”中在讨论友函数时进行描述。
必须是类成员的运算符只有：赋值 (`=`)、下标 (`[ ]`)、函数调用 (`()`) 和间接访问 (`->`) 运算符。
运算符 `[ ]` 将在第 11 天“继承”在介绍数组时讨论。

## 检查运算符重载的局限性

内置类型（如 `int`）上的运算符不能被重载。运算符的优先级顺序无法更改，运算符的元数（arity，即它是一元的还是二元的）无法更改。你不能发明新的运算符，因此不能将 `**` 声明为“幂”运算符。

元数是指运算符中使用的操作数数量。某些 C++ 运算符是单元的，只使用一个操作数（`myValue++`）。某些运算符是二元的，使用两个操作数（`a + b`）。只有一个运算符是三元的，它使用三个操作数。`?:` 运算符是三元运算符，因为它是 C++ 中唯一的三元运算符（`a > b ? x : y`）。

## 要重载的内容

运算符重载是新程序员最常用也最滥用的 C++ 特性之一。为某些较晦涩的运算符创建新的且有趣的用法是非常有吸引力的，但这些往往会导致代码变得混乱且难以阅读。

当然，让 `+` 运算符变为减法、让 `*` 运算符变为加法可能很有趣，但没有任何专业程序员会这样做。更大的危险在于出于善意但奇特的运算符用法——例如使用 `+` 表示连接一串字母，或表示分割字符串。考虑这些用法有理由，但谨慎行事有更好的理由。记住，重载运算符的目标是增加易用性和理解性。

| 应该 (Do) | 不要 (DON'T) |
|---|---|
| 当运算符重载能明确程序逻辑时，使用它。 | 不要创建违反直觉的运算符。 |
| 对于重载运算符，应该返回该类的对象。 | |

## 使用赋值运算符

如果你没有指定，编译器提供的第四个也是最后一个函数是赋值运算符（`operator=()`）。每当你向一个对象赋值时，该运算符就会被调用。例如：

```cpp
CAT catOne(5,7);
catTwo(3,4);
// ... 其他代码在此
catTwo = catOne;
```

## 第 10 天

在这里，创建了 `catOne` 并初始化其 `itsAge` 为 5，`itsWeight` 为 7。然后创建了 `catTwo` 并赋值为 3 和 4。

过了一会儿，`catTwo` 被赋予了 `catOne` 的值。这里有两个问题：如果 `itsAge` 是一个指针会怎样？`catTwo` 中的原始值会发生什么？

在之前检查拷贝构造函数时，讨论过处理在自由存储（free store）上存储值的成员变量。这里出现了相同的问题，正如你在图 10.1 和 10.2 中看到的那样。

C++ 程序员将浅拷贝（或成员级拷贝）与深拷贝区分开来。浅拷贝只是复制成员，两个对象最终指向自由存储器上的同一区域。深拷贝则会分配必要的内存。这在图 10.3 中所示。

然而，赋值运算符出现了一个额外的棘手问题：对象 `catTwo` 已经存在且已经分配了内存。如果你将 `catTwo` 赋值给自己，为了防止发生内存泄漏，这部分内存必须被删除吗？

```cpp
catTwo = catTwo;
```
