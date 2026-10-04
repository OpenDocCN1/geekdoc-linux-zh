
(1)Horse (2)Pegasus: 1
(1)Horse (2)Pegasus: 2
(1)Horse (2)Pegasus: 1
(1)Horse (2)Pegasus: 2
(1)Horse (2)Pegasus: 1

马不会飞。
我会飞！我会飞！我会飞！
马不会飞。
我会飞！我会飞！我会飞！
马不会飞。

这个程序可以正常工作，尽管代价是 `Horse` 类必须拥有一个 `Fly()` 方法。在第 10 行，为 `Horse` 提供了 `Fly()` 方法。在现实世界的类中，你可能会让它抛出一个错误，或者静默失败。在第 18 行，`Pegasus` 类重写了 `Fly()` 方法以“做正确的事”，在这里通过打印快乐信息来表示。

第 24 行的 `Horse` 指针数组用于证明，根据 `Horse` 或 `Pegasus` 对象的运行时绑定，调用了正确的 `Fly()` 方法。

> 注意：这些示例已精简到最核心的内容，以说明所考虑的重点。构造函数、虚析构函数等已删除移除，以保持代码简单。

# 向上渗透

将所需的函数放置在类层次结构中更高的位置是解决此问题的常见方案，这会导致许多函数“向上渗透”到基类中。这样，基类就面临着变成任何派生类可能使用的所有函数的全局命名空间的极大危险。这会严重破坏 C++ 的类类型系统，并创建一个巨大且笨重的基类。

通常情况下，你希望在整个类层次结构中向上渗透功能，而不迁移每个类的接口。这意味着如果两个类共享一个公共基类（例如，`Horse` 和 `Bird` 共享 `Animal`）并且有一个共同的函数（例如，鸟和马各自都有某种功能），你可能希望将该功能移动到基类中并创建一个虚函数。

然而，你想要避免的是将接口（如 `Fly`）向上渗透到它不属于的地方，仅仅为了只在某些派生类上调用函数。

# 向下转换

这种方法的另一种替代方案（仍在单继承范围内）是将 `Fly()` 方法保留在 `Pegasus` 中，并仅当指针实际上指向 `Pegasus` 对象时才调用它。为了使之工作，你将需要能够询问指针它实际上指向什么类型。这被称为运行时类型识别（RTTI）。使用 RTTI 直到最近才成为 C++ 的正式部分。

如果你的编译器不支持 RTTI，你可以通过在每个类中放置一个返回枚举类型的方法来模拟它。你可以在运行时测试该类型，如果它返回 `Pegasus`，则调用 `Fly()`。

早版本的 GNU 编译器（2.7.2 及更早版本）在所有平台上均不支持 RTTI。在光盘中包含的版本（2.9.5）默认支持它。

## 多态

> 警惕在程序中使用 RTTI。对它的使用可能是设计不良的迹象。请考虑改用虚函数、模板或多重继承。

然而，为了调用 `Fly()`，你必须对指针进行强制转换，告诉它所指向的对象是一个 `Pegasus` 对象，而不是 `Horse`。这被称为向下转换，因为你正在将 `Horse` 对象转换为更派生的类型。

C++ 现在正式地（尽管可能不情愿地）支持使用新的 `dynamic_cast` 运算符进行向下转换。它的工作原理如下：

如果你有一个指向基类 `Horse` 的指针，并将其赋值给一个指向派生类 `Pegasus` 的指针，你可以多态地使用该 `Horse` 指针。如果你随后需要获取 `Pegasus` 对象，你会创建一个 `Pegasus` 指针并使用 `dynamic_cast` 运算符进行转换。

在运行时，将检查基指针。如果转换正确，你的 `Pegasus` 指针将没有问题。如果转换不正确（即你实际上并没有 `Pegasus` 对象），你的新指针将为空。列表 13.2 阐释了这一点。

# 列表 13.2 向下转换

```
1: // Listing 13.2 Using dynamic_cast.
2: // Using rttis
3:
4: #include <iostream>
5: enum TYPE { HORSE, PEGASUS };
6:
7: class Horse
8: {
9: public:
10:    virtual void Gallop() { cout << "Galloping...\n"; }
11:
12: private:
13:     int Age;
14: };
15: class Pegasus : public Horse
16: {
17: public:
18:
19:     virtual void Fly() { cout << "I can fly! I can fly! I can fly!\n"; }
20: };
```

# 列表 13.2 续接

```
22:   const int NumberHorses = 5;
23:   int main()
24:   {
25:       Horse* Ranch[NumberHorses];
26:       Horse* pHorse;
27:       int choice,i;
28:       for (i=0; i<NumberHorses; i++)
29:       {
30:           cout << "(1)Horse (2)Pegasus: ";
31:           cin >> choice;
32:           if (choice == 2)
33:               pHorse = new Pegasus;
34:           else
35:               pHorse = new Horse;
36:           Ranch[i] = pHorse;
37:       }
38:       cout << "\n";
39:       for (i=0; i<NumberHorses; i++)
40:       {
41:           Pegasus *pPeg = dynamic_cast<Pegasus *>(Ranch[i]);
42:           if (pPeg)
43:               pPeg->Fly();
44:           else
45:               cout << "Just a horse\n";
46:           delete Ranch[i];
47:       }
48:       return 0;
49:   }
```

输出
(1)Horse (2)Pegasus: 1
(1)Horse (2)Pegasus: 2
(1)Horse (2)Pegasus: 1
(1)Horse (2)Pegasus: 2
(1)Horse (2)Pegasus: 1

马不会飞。
我会飞！我会飞！我会飞！
马不会飞。
我会飞！我会飞！我会飞！
马不会飞。

## 多态

# 常见问题

FAQ：在编译时，我从 GNU 编译器（2.7.2 及更早版本）得到一个错误：
1st3_02.cxx: In function 'main()'
1st3_02.cxx: 42: cannot take typeid object when -frtti is specified
1st3_02.cxx: 42: invalid type argument
1st3_02.cxx: 42: failed to build type descriptor of 'Pegasus',
1st3_02.cxx: maybe include typeinfo.h not included

FAQ：我该怎么办？
回答：这是 GNU 编译器最困惑的错误信息之一。不幸的是，你使用的版本可能不支持 RTTI，尽管它提供了规避方法。
如果你收到选项未识别警告，可以尝试使用 `-frtti` 选项重新编译，你的平台和特定版本不支持此功能。
2.9.5 版本默认支持 RTTI。

或者，你可以将方法留在原地，但将 `Horses`、`Birds` 和 `Pegasus` 对象向下强制转换，但这更糟了！

| 应该 (DO) | 不要 (DON'T) |
|---|---|
| 将功能向上继承层次结构中移动。 | 不要将指向基对象的指针向下强制转换为派生对象。 |
| 避免对对象的运行时类型进行 switch 切换——使用虚方法、模板和多重继承。 | 不要将接口向上继承层次结构中移动。 |

## 多重继承

可以从多个基类派生一个新类。这被称为多重继承。要派生自多个基类类，你需要在类定义中用逗号分隔每个基类。列表 13.3 展示了如何声明 `Pegasus` 使其同时派生自 `Horses` 和 `Birds`。该程序将 `Pegasus` 对象添加到两种类型的列表中。

输入列表 13.3 多重继承

```
1: // Listing 13.3. Multiple inheritance.
2: // Multiple Inheritance
3:
4: #include <iostream.h>
5:
6: class Horse
7: {
8: 
9: Horse() { cout << "Horse constructor... "; }
10: virtual ~Horse() { cout << "Horse destructor... "; }
11: virtual void Whinny() const { cout << "Whinnyl... "; }
12:
13: private:
14: int itsAge;
15: };
16:
17: class Bird
18: {
19: public:
20: Bird() { cout << "Bird constructor... "; }
21: virtual ~Bird() { cout << "Bird destructor... "; }
22: virtual void Chirp() const { cout << "Chirp... "; }
23: virtual void Fly() const
24:    cout << "I can fly! I can fly! I can fly! ";
25:  }
26:  private:
27:    int itsWeight;
28:  };
29: 
30:  class Pegasus : public Horse, public Bird
31:  public:
32:    void Chirp() const { Whinny(); }
33:    Pegasus() const { cout << "Pegasus constructor... "; }
34:    ~Pegasus() { cout << "Pegasus destructor... "; }
35:
36:  };
37:
38: 
39:    const int MagicNumber = 2;
40:    int main()
41:  {
42:      Horse* Ranch[MagicNumber];
43:      Bird* Aviary[MagicNumber];
44:      Horse * pHorse;
45:      Bird * pBird;
46:      int choice,i;
47:      for (i=0; i<MagicNumber; i++)
48:      {
49:          cout << "\n(1)Horse (2)Pegasus: ";
50:          cin >> choice;
51:          if (choice == 2)
52:              pHorse = new Pegasus;
53:          else
54:              pHorse = new Horse;
55:              Ranch[i] = pHorse;
56:      }
57:      for (i=0; i<MagicNumber; i++)
58:      {
59:          cout << "\n(1)Bird (2)Pegasus: ";
60:          cin >> choice;
61:          if (choice == 2)
62:              pBird = new Pegasus;
63:          else
64:              pBird = new Bird;
65:              Aviary[i] = pBird;
66:      }
67:      cout << "\n";
68:      for (i=0; i<MagicNumber; i++)
69:      {
70:          cout << "\nRanch[" << i << "]: ";
71:          Ranch[i]->Whinny();
72:          delete Ranch[i];
73:      }
74:  }
```

LISTING 13.3 续

```
75:   for (i=0; i<MagicNumber; i++)
76:   {
77:     cout << "\nAviary[" << i << "]: ";
78:     Aviary[i]->Chirp();
79:     Aviary[i]->Fly();
80:     delete Aviary[i];
81:   }
82:   return 0;
83:   }
```

(1)Horse (2)Pegasus: 1
Horse constructor...
(1)Horse (2)Pegasus: 2
Horse constructor... Bird constructor...
(1)Bird (2)Pegasus: 1
Bird constructor...
(1)Bird (2)Pegasus: 2
Horse constructor... Bird constructor...

Ranch[0]: Whinn!... Horse destructor...
Ranch[1]: Whinn!... Pegasus destructor... Bird destructor...
Horse destructor...
Aviary[0]: Chirp! I can fly! I can fly! I can fly! Bird destructor...
Aviary[1]: Whinn!... I can fly! I can fly! I can fly!
Pegasus destructor... Bird destructor... Horse destructor...

在第 6-14 行，声明了一个 `Horse` 类。构造函数和析构函数打印一条消息，`Whinny()` 方法打印单词 Whinn!。

在第 16-28 行，声明了一个 `Bird` 类。除了构造函数和析构函数外，该类有两个方法：`Chirp()` 和 `Fly()`，它们都是标识性的。在实际程序，它们可能会激活声器或生成图像。

最后，在第 30-36 行，声明了 `Pegasus` 类。它派生自 `Horse` 和 `Bird`。`Pegasus` 类覆盖了 `Chirp()` 方法以调用它继承自 `Horse` 的 `Whinny()` 方法。

创建了列表：第 41 行指向 `Horse` 的 `Ranch` 和第 42 行指向 `Bird` 的 `Aviary`。在第 46-55 行，`Horse` 和 `Pegasus` 对象添加到 `Ranch`。在第 56-65 行，`Bird` 和 `Pegasus` 对象添加到 `Aviary`。

对 `Bird` 和 `Horse` 指针调用虚方法会对 `Pegasus` 对象执行正确的操作。`Bird` 类将此声明为虚方法，因此对每个对象都会调用。每当创建一个 `Pegasus` 对象时，由于析构函数是虚的，输出反映出 `Bird` 部分和 `Horse` 部分都被创建。

### 声明多重继承
在类名后列出基类来声明继承自多个类。用逗号分隔基类。

示例 1
`class Pegasus : public Horse, public Bird`

示例 2
`class Schnoodle : public Schnauzer, public Poodle`

### 继承的对象
当在内存中创建 `Pegasus` 对象时，基类形成了 `Pegasus` 对象的一部分，如图 13.1 所示。

多个基类会出现一些问题。例如，如果两个基类具有相同的虚函数或数据怎么办？如果有多个构造函数怎么办？接下来的章节将回答这些问题并探索如何使用多重继承。

### 继承对象的构造函数
如果 `Pegasus` 派生自 `Horse` 和 `Bird`，且每个基类都有带参数的构造函数，`Pegasus` 类将依次初始化这些构造函数。列表 13.4 展示了做法。

输入列表 13.4 调用多个构造函数

```
1: // Listing 13.4
2: // Calling multiple constructors
3: #include <iostream.h>
4: typedef int HANDS;
5: enum COLOR { Red, Green, Yellow, Black, Brown };
6: {
7:   class Horse
8:   public:
9:      virtual ~Horse(COLOR color, HANDS height) { cout << "Horse destructor...\n"; }
10:      virtual void Whinny() const { cout << "Whinn... \n"; }
11:      virtual HANDS GetHeight() const { return itsHeight; }
```
