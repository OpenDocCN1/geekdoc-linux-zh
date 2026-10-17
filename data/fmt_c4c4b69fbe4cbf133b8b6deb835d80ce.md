
在第 40 行中，使用 `pRect` 将矩形的宽度设置为 10。在第 41 行中，本应使用 `pRect`，但它被声明指向一个常量 Rectangle。因此，它无法合法地调用非 `const` 成员函数；该行被注释掉了。在第 42 行中，`pConstRectPtr` 调用了 `SetWidth()`；`pConstRectPtr` 被声明为指向矩形的常量指针。换句话说，指针是常量，不能指向其他任何地方，但矩形不是常量。

# const this 指针

当你将一个对象声明为 `const` 时，你实际上是在声明该指针是一个 `const` 对象的指针。`const this` 指针只能用于 `const` 成员函数。

常量对象和常量指针将在明天再次讨论，常量对象的引用已在讨论中。

![](img/a66ce94ee9cc26e5c70f5604bcd3600c_284_0.png)

| 应该 (DO) | 不要 (DON'T) |
|---|---|
| 如果通过引用传递的对象不应改变，请用 `const` 保护。 | |
| 当对象可以改变时，通过引用传递。 | |
| 当小对象不应改变时，通过值进行传递。 | |

# 指针算术

指针可以与另一个指针相减。一种强大的技术是让两个指针指向数组中不同的元素，并取它们的差，以显示这两个成员之间隔了多少个元素。这在解析字符数组时非常有用，如列表 8.11 所示。

# 列表 8.11 演示如何从字符字符串解析单词

```cpp
1: #include <iostream.h>
2: #include <ctype.h>
3: #include <string.h>
4: bool GetWord(char* string, char* word, int& wordOffset);
5: // 驱动程序
6: int main(
7: {
8:   const int bufferSize = 255;
9:   char buffer[bufferSize+1]; // 存放整个字符串
10:  char word[bufferSize+1];
11:    int wordOffset = 0;           // 从开始开始
12:    cout << "Enter a string: ";
13:    cin.getline(buffer,bufferSize);
14:
15:
16:    while (GetWord(buffer,word,wordOffset))
17:    {
18:        cout << "Got this word: " << word << endl;
19:    }
20:
21:    return 0;
22:
23:    }
24:
25:
26:    // 从字符串中解析单词的函数
27:    bool GetWord(char* string, char* word, int&wordOffset)
28:    {
29:
30:        if (!string[wordOffset]) // 字符串结束？
31:            return false;
32:
33:
34:        char *p1, *p2;
35:        p1 = p2 = string - wordOffset; // 指向下一个单词
36:
37:        // 跳过空格
38:        for (int i = 0; i<(int)strlen(p1) && !isalnum(p1[i]); i++)
39:            p1++;
40:
41:        // 检查是否有一个单词
42:        if (!isalnum(p1[0]))
43:            return false;
44:
45:        // p1 现在指向单词的开头
46:        // p2 也指向这里
47:        p2 = p1;
48:
49:        // 将 p2 移动到单词末尾
50:        while (isalnum(p2[0]))
51:            p2++;
52:
53:        // p2 现在在单词末尾
54:        // p1 在单词开头
55:        // 单词的长度是差值
56:        int len = int (p2 - p1);
57:
58:
59:        // 将单词拷贝到缓冲区
60:        strncpy(word,p1,len);
61:        // 用空字符终止
62:        word[len] = '\0';
63:
64:        // 现在寻找下一个单词的开头
65:        for (int i = int(p2-string); i < (int)strlen(string) && !isalnum(string[i]); i++)
65:            p2++;
66:        wordOffset = int(p2-string);
67:        return true;
68: }
```

## 指针

Q 为什么我应该将一个对象声明为 const，即使这会限制了我对它的操作？

A 作为一名程序员，你希望让编译器帮助你发现 bug。一种很难发现的严重 bug 是函数以对调用函数不明显的方式改变了对象。将对象声明为 `const` 可以防止此类更改。

![](img/a66ce94ee9cc26e5c70f5604bcd3600c_288_0.png)

## 工作坊 (Workshop)

工作坊提供了测验题帮助你巩固对所涵盖内容的理解，并提供了练习让你获得使用所学知识经验。在查看附录 D 中的“练习和测验答案”之前，尝试回答测验和练习题，并在继续第二天的内容之前确保理解答案。

## 测验 (Quiz)

- 1. 使用什么运算符来确定变量的地址？
- 2. 使用什么运算符来查找指针所持地址存储的值？
- 3. 什么是指针？
- 4. 指针中存储的地址与该地址的值之间有什么区别？
- 5. 间接运算符（indirection operator）和地址运算符（address operator）之间有什么区别？
- 6. `const int * ptrOne` 和 `int * const ptrTwo` 之间有什么区别？

## 练习 (Exercises)

- 1. 这些声明的作用分别是什么？
  - a. `int * pOne;`
  - b. `int vTwo;`
  - c. `int * pThree = &vAge;`
- 2. 如果你有一个名为 `yourAge` 的无符号短整数变量，你会如何声明一个指针来操作 `yourAge`？
- 3. 使用指针和指向整数的指针将值 50 赋值给变量 `yourAge`（所示）。
- 4. 编写一个小型程序，声明一个整数和一个指向整数的指针。将整数的地址赋给指针。使用指针为整数变量设置值。

## 5. BUG 排除 (BUG BUSTER): 这段代码哪里错了？

```cpp
#include <iostream.h>
int main() {
    int *pInt;
    *pInt = 9;
    cout << "The value at pInt: " << *pInt;
    return 0;
}
```

## 6. BUG 排除 (BUG BUSTER): 这段代码哪里错了？

```cpp
int main() {
    int SomeVariable = 5;
    cout << "SomeVariable: " << SomeVariable << "\n";
    int *pVar = &SomeVariable;
    *pVar = 9;
    cout << "SomeVariable: " << *pVar << "\n";
    return 0;
}
```

## 第二周

## 第 9 天

## 参考文献

昨天你学习了如何使用指针操作自由存储（free store）上的对象，以及如何间接引用这些对象。引用（References）是今天课程的主题，它们带给你几乎所有所有的指针功能，但语法简单得多。今天你将学习：

- 什么是引用
- 引用与指针的区别
- 如何创建和使用引用
- 引用的局限性是什么
- 如何通过引用将值和对象传入或传出函数

## 什么是引用？

*引用*（reference）是一个别名或同义词；当你创建一个引用时，你用另一个对象的名称（即目标对象）来初始化它。从那一刻起，该引用充当目标的替代名称，你对引用进行的任何操作实际上都是作用在目标上的。

你通过编写目标对象的类型，后跟引用运算符 `&`，最后是引用的名称来创建一个引用 (`&`)。引用可以使用任何合法的变量名，但许多程序员倾向于在所有引用前缀加上 "r"。因此，如果你有一个名为 `someInt` 的整数变量，你可以通过编写以下代码为该变量创建一个引用：

```cpp
int &someRef = someInt;
```

这读作 `rSomeRef`，是一个指向整数的引用，并初始化为指向 `someInt`。列表 9.1 显示了如何创建和使用引用。

> 注意，引用运算符 `&` 与用于地址运算符的符号相同。然而，它们并不是同一个运算符，尽管它们显然有联系。

## 列表 9.1 创建和使用引用

```cpp
1: //Listing 9.1
2: // 展示引用的使用
3: 
4: #include <iostream.h>
5: 
6: int main()
7: {
8:     int intOne;
9:     int &rSomeRef = intOne;
10: 
11:    intOne = 5;
12:    cout << "intOne: * " << intOne << endl;
13:    cout << "rSomeRef: * " << rSomeRef << endl;
14: 
15:    rSomeRef = 7;
16:    cout << "intOne: * " << intOne << endl;
17:    cout << "rSomeRef: * " << rSomeRef << endl;
18:    return 0;
19: }
```

```
intOne: 5
rSomeRef: 5
intOne: 7
rSomeRef: 7
```

## 引用

在第 8 行，声明了一个局部 `int` 变量 `intOne`。在第 9 行，声明了一个 `int` 引用 `rSomeRef` 并将其初始化为指向 `intOne`。如果你声明了引用但不初始化它，将得到编译错误。

在第 11 行，`intOne` 被赋值为 5。在第 12 行和 13 行，`intOne` 和 `rSomeRef` 的值被打印出来，它们是相同的。

在第 15 行，`rSomeRef` 被赋值为 7。在第 16 行和 17 行，`intOne` 的值发生了变化，因为引用是目标的别名，如图像所示![](img/a66ce94ee9cc26e5c70f5604bcd3600c_288_0.png)。

## 在引用上使用地址运算符

如果你对引用使用地址运算符 `&`，它返回的是目标的地址。这就是引用的本质。列表 9.2 展示了这一点。

### 列表 9.2 获取引用的地址

```cpp
1: //Listing 9.2
2: // 展示引用的使用
3:
4: #include <iostream.h>
5: 
6: int main()
7: {
8:     int intOne;
9:     int &rSomeRef = intOne;
10: 
11:    intOne = 5;
12:    cout << "intOne: * " << intOne << endl;
13:    cout << "rSomeRef: * " << rSomeRef << endl;
14: 
15:    rSomeRef = 7;
16:    cout << "intOne: * " << intOne << endl;
17:    cout << "rSomeRef: * " << rSomeRef << endl;
18:    return 0;
19: }
```

```
intOne: 5
rSomeRef: 5
intOne: 7
rSomeRef: 7
```

如果你对引用使用地址运算符 `&`，它返回的是目标的地址。如果你对引用使用地址运算符 `&`，它返回的是目标的地址。这就是引用的本质。列表 9.2 展示了这一点。

## 引用不能重新赋值

即使是经验丰富的 C++ 程序员，知道规则——引用不能重新赋值——在尝试重新赋值引用时也会感到困惑。看起来看起来是重新赋值，实际上是给目标赋值。列表 9.3 展示了这一事实。

## 列表 9.3 给引用赋值

```cpp
1: //Listing 9.3
2: // 给引用赋值
3: 
4: #include <iostream>
5: 
6: int main()
7: {
8:     int intOne;
9:     int &rSomeRef = intOne;
10: 
11:    intOne = 5;
12:    cout << "intOne: * " << intOne << endl;
13:    cout << "rSomeRef: * " << rSomeRef << endl;
14:    cout << "&intOne: " << &intOne << endl;
15:    cout << "&rSomeRef: " << &rSomeRef << endl;
16: 
17:    int intTwo = 8;
18:    rSomeRef = intTwo;
19:    cout << "intOne: * " << intOne << endl;
20:    cout << "&intTwo: " << &intTwo << endl;
21:    cout << "rSomeRef: * " << rSomeRef << endl;
22:    cout << "&intOne: " << &intOne << endl;
23:    cout << "&intTwo: " << &intTwo << endl;
24:    cout << "&rSomeRef: " << &rSomeRef << endl;
25:    return 0;
26: }
```

但事实并非如此。实际发生的情况是 `someRef` 继续作为 `intOne` 的别名，因此这次赋值等同于以下操作：

```cpp
intOne = intTwo;
```

确实，当打印 `intOne` 和 `someRef` 的值时（第 19–21 行），它们与 `intTwo` 相同。事实上，当在第 22–24 行打印地址时，你会发现 `someRef` 继续指向 `intOne` 而不是 `intTwo`。

## 做 (Do) / 不要做 (DON'T)

| 做 | 不要做 |
|---|---|
| 使用引用创建对象的别名。 | 不要尝试对引用重新赋值。 |
| 初始化所有的引用。 | 不要将地址运算符与引用运算符混淆。 |

## 什么可以被引用？

任何对象都可以被引用，包括用户定义的对象。注意，你创建的是对对象的引用，而不是对类的引用。你不应该写这样的代码：

```cpp
int &rIntRef = int; // 错误
```

你必须将 `rIntRef` 初始化为一个特定的整数，例如：

```cpp
int howBig = 200;
int &rIntRef = howBig;
```

同样，你不能初始化对 CAT 的引用：

```cpp
CAT &rCatRef = CAT; // 错误
```

你必须将 `rCatRef` 初始化为一个特定的 CAT 对象：

```cpp
CAT frisky;
CAT &rCatRef = frisky;
```

对对象的引用使用方法与对象本身完全相同。成员数据和方法通过普通的类成员运算符（.`）来访问，就像对于内置类型一样，引用充当了对象的别名。列表 9.4 说明了这一点。

## 列表 9.4 对象的引用

```cpp
1: // Listing 9.4
2: // 类对象的引用
3:
4: #include <iostream.h>
5:  class SimpleCat
{
  public:
    SimpleCat(int age, int weight);
    SimpleCat() {}
    int GetAge() { return itsAge; }
    int GetWeight() { return itsWeight; }
  private:
    int itsAge;
    int itsWeight;
};

SimpleCat::SimpleCat(int age, int weight)
{
    itsAge = age;
    itsWeight = weight;
}

int main()
{
    SimpleCat Frisky(5,8);
    SimpleCat &rCat = Frisky;

    cout << "Frisky is: " << Frisky.GetAge() << " years old.\n";
    cout << "Frisky weighs: " << rCat.GetWeight() << " pounds.\n";
    return 0;
}
```

OUTPUT Frisky is 5 years old. And Frisky weighs: 8 pounds.
