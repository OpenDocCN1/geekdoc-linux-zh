
## 代码示例

```cpp
12:      virtual COLOR GetColor() const { return itsColor; }

13:   private:

14:      HANDS itsHeight;

15:      COLOR itsColor;

16:  };

17:

18:

19:  Horse::Horse(COLOR color, HANDS height):
20:    itsColor(color), itsHeight(height)
21:  {
22:    cout << "Horse constructor...\n";
23:  }

24:

25:  class Bird
26:  {
27:    public:
28:      Bird(COLOR color, bool migrates) { cout << "Bird destructor...\n"; }
29:      virtual ~Bird() {}
30:      virtual void Chirp() const { cout << "Chirp... \n"; } 
31:      virtual void Fly() const 
32:      {
33:        cout << "I can fly! I can fly! I can fly! \n";
34:      }
35:      virtual COLOR GetColor() const { return itsColor; }
36:      virtual bool GetMigration() const { return itsMigration; }
37:    private:
38:      COLOR itsColor;
39:      bool itsMigration;
40:  };
```

## 多态

```cpp
42:  };

43: 
44: Bird::Bird(COLOR color, bool migrates):
45:     itsColor(color), itsMigration(migrates)
46:     {
47:     cout << "Bird constructor...\n";
48: }
49: 
50:     class Pegasus : public Horse, public Bird
51:     {
52:     public:
53:         void Chirp() const { Whinny(); }
54:         Pegasus(COLOR, HANDS, bool, long);
55:         ~Pegasus() const { cout << "Pegasus destructor...\n"; }
56:         virtual long GetNumberBelievers() const
57:         {
58:             return itsNumberBelievers;
58:         }
59:     private:
60:         long itsNumberBelievers;
61:     };
62: 
63:     Pegasus::Pegasus(
64:         COLOR a,
65:         HANDS height,
66:         bool migrates,
67:         long NumBelieve):
68:         Horse(a, height),
69:         Bird(a, migrates),
70:         itsNumberBelievers(NumBelieve)
71:     {
72:         cout << "Pegasus constructor...\n";
73:     }
74: 
75:     int main()
76:     {
77:         Pegasus *ppeg = new Pegasus(Red, 5, true, 10);
78:         ppeg->Fly();
79:         ppeg->Whinny();
80:         cout << "\nY Pegasus is " << ppeg->GetHeight();
81:         cout << " hands tail and ";
82:         if (ppeg->GetMigration())
83:             cout << " it does migrate.";
84:         else
85:             cout << " it does not migrate.";
86:         cout << "\nA total of " << ppeg->GetNumberBelievers();
87:         cout << " people believe it exists.\n";
88:         delete ppeg;
89:         return 0;
90:     }
```

## 输出

马的构造函数...
鸟的构造函数...
天马的构造函数...
我可以飞！我可以飞！嘶嘶！...
你的天马高 5 手手，而且它会迁徙。
总共有 8 个人相信它的存在。

天马的析构函数...
鸟的析构函数...
马的析构函数...

## 分析

在第 7–18 行，声明了 `Horse` 类。构造函数接受两个参数：一个是在第 5 行定义的枚举，另一个在第 4 行定义。第 20–24 行构造函数的实现简单地初始化了成员变量并打印了一条消息。

在第 26–42 行，声明了 `Bird` 类，构造函数的实现位于第 45–49 行。同样，`Bird` 类接受两个参数。有趣的是，`Horse` 构造函数接受颜色（以便你可以检测不同颜色的马），而 `Bird` 构造函数接受羽毛的颜色（同一根羽毛可能会粘在一起）。当你想要询问天马的颜色时，这会导致一个问题，你将在下一个示例中看到。

`Pegasus` 类本身声明在第 50–63 行，其构造函数在第 65–74 行。`Pegasus` 对象的初始化包含三个语句。首先，初始化带有颜色和高度的 `Horse`。然后，初始化带有颜色和布尔值的 `Bird`。最后，初始化了 `Pegasus` 成员变量 `itsNumberBelievers`。在完成所有操作后，调用 `Pegasus` 构造函数体。

在 `main()` 函数中，创建了一个 `Pegasus` 指针并使用它访问基对象的成员函数。

## 解析歧义

在列表 13.4 中，`Horse` 类和 `Bird` 类都有方法 `GetColor()`。你可能需要要求 `Pegasus` 对象返回它的颜色，但你遇到了一个问题：`Pegasus` 类同时继承自 `Bird` 和 `Horse`。它们都有颜色，且获取该颜色的方法具有相同的名称和签名。这为编译器产生了歧义，你必须解决它。

如果你直接写：

```cpp
COLOR currentColor = pPeg->GetColor();
```

`g++` 将给出编译错误：

```text
request for method `GetColor` is ambiguous
```

你可以通过显式调用你想要调用的函数来解决歧义：

```cpp
COLOR currentColor = pPeg->Horse::GetColor();
```

每当你需要解决成员函数或成员数据继承自哪个类时，你可以通过在基类或函数前加上类名来完全限定调用。

请注意，如果 `Pegasus` 重写了此函数，问题将像预期的那样移动到 `Pegasus` 成员函数中：

```cpp
virtual COLOR GetColor() const { return Horse::GetColor(); }
```

这向 `Pegasus` 类的客户端隐藏了问题，并在 `Pegasus` 内部封装了它想要从哪个基类继承颜色的知识。客户端仍然可以通过编写以下代码来强制执行：

```cpp
COLOR currentColor = pPeg->Bird::GetColor();
```

## 继承自共享基类

如果 `Bird` 和 `Horse` 都继承自一个共同基类（例如 `Animal`）会发生什么？图 13.2 显示了它的样子。

**图 13.2 共同基类。**

![](img/a66ce94ee9cc26e5c70f5604bcd3600c_458_0.png)

如图 13.2 所示，存在两个基类对象。当在共享基类中调用函数或数据成员时，存在另一个歧义。例如，如果 `Animal` 将 `itsAge` 声明为成员变量并将 `GetAge()` 声明为成员函数，而你调用 `pPeg->GetAge()`，你是通过 `Horse` 调用继承自 `Animal` 的 `GetAge()` 函数，还是通过 `Bird` 调用？你也必须解决这个歧义，正如列表 13.5 所示。

### 列表 13.5 共同基类

（注：代码部分由于重复性保持原样，此处仅翻译注释）

```cpp
1: // 列表 13.5
2: // 共同基类
3: #include <iostream>
4: 
5: typedef int HANDS;
6: enum COLOR { Red, Green, Yellow, Black, Brown };
7: 
8: class Animal // horse 和 bird 的共同基类
9: {
10:    public:
11:        Animal(int);
12:        virtual ~Animal() { cout << "Animal destructor..."; }
13:        virtual int GetAge() const { return itsAge; }
14:        virtual void SetAge(int age) { itsAge = age; }
15:    private:
16:        int itsAge;
17: };
18: 
19: Animal::Animal(int age)
20:     : itsAge(age)
21:     {
22:         cout << "Animal constructor...";
23:     }
```

（此处省略重复的 `Horse` 和 `Bird` 类定义，逻辑与原文一致）

## 多态

链式调用有两个原因：要么在当前情况下区分要调用哪一个基类，要么是为了执行某些工作，然后让基类中的函数继续执行其他工作。有时，你可能想执行某些工作然后链式调用，或者先链式调用，然后在基类返回时执行某些工作。

`Pegasus` 构造函数接受五个参数：生物的颜色、高度（以手为单位）、是否迁徙、有多少人相信它以及它的年龄。构造函数在第 87 行使用颜色、高度和年龄初始化 `Pegasus` 的 `Horse` 部分。在第 88 行使用颜色、是否迁徙和年龄初始化 `Bird` 部分。最后，它在第 89 行初始化 `itsNumberBelievers`。

第 87 行对 `Horse` 构造函数的调用引入了第 38 行所示的实现。`Horse` 构造函数使用 `age` 参数来初始化 `Pegasus` 中 `Horse` 部分的 `Animal` 部分。接着它初始化 `Horse` 的两个成员变量——`itsColor` 和 `itsHeight`。

第 88 行对 `Bird` 构造函数的调用引入了第 60 行所示的实现。在这里，`age` 参数也被用于初始化 `Bird` 的 `Animal` 部分。

注意，用于 `Pegasus` 的 `color` 参数用于初始化 `Bird` 和 `Horse` 中的成员变量。同样注意，`age` 被用于初始化 `Horse` 的 `Animal` 以及 `Bird` 的基类 `Animal` 中的 `itsAge`。

## 虚拟继承

在列表 13.5 中，`Pegasus` 类费了很大功夫来区分它想要调用哪一个 `Animal` 基类。大多数情况下，使用哪一个类的决定是随机的——毕竟，`Horse` 和 `Bird` 具有相同的基类。

在 C++ 中，你可能不想要两个共享基类的副本（如图 13.2 所示），而是更希望有一个单一的共享基类（如图 13.3 所示）。

你通过将 `Horse` 和 `Bird` 均设为虚拟基类来实现这一点。`Animal` 类完全没有变化。`Horse` 和 `Bird` 类的变化仅在于声明中使用 `virtual` 关键字。然而，`Pegasus` 发生了巨大的变化。

通常，类的构造函数只初始化它自己的变量及其基类。然而，虚拟继承的基类是一个例外。它们由其最派生类初始化。因此，`Animal` 不是由 `Horse` 和 `Bird` 初始化，而是由 `Pegasus` 初始化。`Horse` 和 `Bird` 必须在它们的构造函数中初始化 `Animal`，但在创建 `Pegasus` 对象时，这些初始化将被忽略。

**图 13.3 菱形继承。**

![](img/a66ce94ee9cc26e5c70f5604bcd3600c_462_0.png)
![](img/a66ce94ee9cc26e5c70f5604bcd3600c_463_0.png)

列表 13.6 重写了列表 13.5，以利用虚拟派生。

### 输入列表 13.6 虚拟继承的使用示例

```cpp
1: // Listing 13.6
2: // Virtual inheritance
3: #include <iostream.h>
4: 
5: typedef int HANDS;
6: enum COLOR { Red, Green, Blue, Yellow, White, Black, Brown };
7: 
8: class Animal             // common base to both horse and bird
9: {
10:    public:
11:        Animal(int);
12:        virtual ~Animal() { cout << "Animal destructor...\n"; }
13:        virtual int GetAge() const { return itsAge; }
14:        virtual void SetAge(int age) { itsAge = age; }
15:    private:
16:        int itsAge;
17: };
18: 
19: Animal::Animal(int age):
20:    itsAge(age)
21: {
22:    cout << "Animal constructor...\n";
23: }
24: 
25: class Horse : virtual public Animal
26: {
27: public:
28:    Horse(COLOR color, HANDS height, int age);
29:    virtual ~Horse() { cout << "Horse destructor...\n"; }
30:    virtual void Whinny() const { cout << "Whinny...\n"; }
31:    virtual HANDS GetHeight() const { return itsHeight; }
32:    virtual COLOR GetColor() const { return itsColor; }
33: protected:
34:    HANDS itsHeight;
35:    COLOR itsColor;
36: };
37:
38: Horse::Horse(COLOR color, HANDS height, int age):
39:    Animal(age),
40:    itsColor(color), itsHeight(height)
41: {
42:    cout << "Horse constructor...\n";
43: }
44: 
45: class Bird : virtual public Animal
46: {
47:   public:
48:      Bird(COLOR color, bool migrates, int age);
49:      virtual ~Bird() { cout << "Bird destructor...\n"; }
50:      virtual void Chirp() const { cout << "Chirp...\n"; }
51:      virtual void Fly() const {
52:        cout << "I can fly!\n"; }
53:      virtual COLOR GetColor() const { return itsColor; }
54:      virtual void GetMigration() const { return itsMigration; }
55: protected:
56:    COLOR itsColor;
57:    bool itsMigration;
58: };
59: 
60: Bird::Bird(COLOR color, bool migrates, int age):
61:    Animal(age),
62:    itsColor(color), itsMigration(migrates)
63: {
```
