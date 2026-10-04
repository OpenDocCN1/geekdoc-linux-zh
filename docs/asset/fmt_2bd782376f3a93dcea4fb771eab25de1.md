
代码列表 9.10 创建了 `SimpleCat` 对象并调用了两个函数。第一个函数按值接收 `Cat` 并按值返回它。第二个函数接收对象的指针而不是对象本身，并返回对象的指针。

# 代码列表 9.10 使用指针通过引用传递对象

```cpp
1: //Listing 9.10
2: // 对象的指针
3:
4: #include <iostream.h>
5:
6: class SimpleCat
7: {
8: public:
9:     SimpleCat(); // 构造函数
10:    SimpleCat(const SimpleCat&); // 拷贝构造函数
11:    ~SimpleCat(); // 析构函数
12: };
13:
14: SimpleCat::SimpleCat()
15: {
16:     cout << "Simple Cat Constructor...\n";
17: }
18:
19: SimpleCat::SimpleCat(const SimpleCat&)
20: {
21:     cout << "Simple Cat Copy Constructor...\n";
22: }
23:
24: SimpleCat::~SimpleCat()
25: {
26:     cout << "Simple Cat Destructor...\n";
27: }
28:
29: SimpleCat FunctionOne(SimpleCat theCat);
30: SimpleCat* FunctionTwo(SimpleCat *theCat);
31:
32: int main()
33: {
34:   cout << "Making a cat...\n";
35:   SimpleCat Frisky;
36:   cout << "Calling FunctionOne...\n";
37:   FunctionOne(Frisky);
38:   cout << "Calling FunctionTwo...\n";
39:   FunctionTwo(&Frisky);
40:   return 0;
41:   }
42:
43:   // FunctionOne,按值传递
44:   SimpleCat FunctionOne(SimpleCat theCat)
45:   {
46:       cout << "Function One. Returning...\n";
47:       return theCat;
48:   }
49:
50:   // FunctionTwo,按引用传递
51:   SimpleCat* FunctionTwo(SimpleCat *theCat)
52:   {
53:       cout << "Function Two. Returning...\n";
54:       return theCat;
55:   }
```

## 输出

```
1: Making a cat...
2: Simple Cat Constructor...
3: Calling FunctionOne...
4: Simple Cat Copy Constructor...
5: Function One. Returning...
6: Simple Cat Copy Constructor...
7: Simple Cat Destructor...
8: Simple Cat Destructor...
9: Calling FunctionTwo...
10: Function Two. Returning...
11: Simple Cat Destructor...
```

> 行号在上面的输出有助于分析。

非常简化的 `SimpleCat` 类定义在 6 到 12 行。构造函数、拷贝构造函数和析构函数都会打印输出信息。

在第 34 行，`main()` 打印“Making a cat...”。在第 35 行，`SimpleCat Frisky` 被实例化。

在第 36 行，`main()` 打印“Calling FunctionOne...”。因为 `FunctionOne()` 按值传递，这在栈上创建了对象的拷贝。

在第 37 行，`FunctionOne()` 被调用。

在第 38 行，`main()` 打印“Calling FunctionTwo...”。在第 39 行，`FunctionTwo(&Frisky)` 被调用。

# 常量指针

虽然通过指针传递效率更高，但它是危险的。`FunctionTwo()` 并没有意图要修改 `SimpleCat`，但它接收了 `SimpleCat` 的地址。这使得对象暴露在修改风险之下。

解决方案是传递指向常量 `SimpleCat` 的指针。这样做可以防止调用任何非 `const` 的 `SimpleCat` 成员函数，从而保护对象不被修改。代码列表 9.11 展示了这一观点。

# 代码列表 9.11 传递指针

```cpp
1: //Listing 9.11
2: // 对象的指针
3:
4: #include <iostream.h>
5:
6: class SimpleCat
7: {
8: public:
9:     SimpleCat();
10:    SimpleCat(SimpleCat&);
11:    ~SimpleCat();
12:
13:    int getAge() const { return itsAge; }
14:    void setAge(int age) { itsAge = age; }
15:
16:    private:
17:    int itsAge;
18:    };
19:
20: SimpleCat::SimpleCat()
21: {
22:     cout << "Simple Cat Constructor...\n";
23:     itsAge = 1;
24: }
25:
26: SimpleCat::SimpleCat(const SimpleCat&)
27: {
28:     cout << "Simple Cat Copy Constructor...\n";
29: }
30:
31: SimpleCat::~SimpleCat()
32: {
33:     cout << "Simple Cat Destructor...\n";
34: }
35:
36: const SimpleCat * const FunctionTwo(const SimpleCat * const theCat);
37:
38: int main()
39: {
40:     cout << "Making a cat...\n";
41:     SimpleCat Frisky;
42:     cout << "Frisky is ";
43:     cout << Frisky.getAge();
44:     cout << " years old\n";
45:     int age = 5;
46:     Frisky.setAge(age);
47:     cout << "Frisky is ";
48:     cout << Frisky.getAge();
49:     cout << " years old\n";
50:     cout << "Calling FunctionTwo...\n";
51:     FunctionTwo(&Frisky);
52:     cout << "Frisky is now ";
53:     cout << Frisky.getAge();
54:     cout << " years old\n";
55:     return 0;
56: }
57: 
58: // functionTwo，传递一个 const指针
59: const SimpleCat * const FunctionTwo(const SimpleCat * const theCat)
60: {
61:     cout << "Function Two. Returning...\n";
62:     cout << "Frisky is now " << theCat->getAge();
63:     cout << " years old\n";
64:     // theCat->setAge(8); const!
65:     return theCat;
66: }
```

## 输出

```
Making a cat...
Simple Cat Constructor...
Frisky is 1 years old
Frisky is 5 years old
Calling FunctionTwo...
Function Two. Returning...
Frisky is now 5 years old
Frisky is 5 years old
Simple Cat Destructor...
```

## 分析

`SimpleCat` 添加了两个访问函数：第 13 行的 `getAge()`（这是一个 `const` 函数）和第 14 行的 `setAge()`（它不是 `const` 函数）。它在第 17 行添加了成员变量 `itsAge`。

构造函数、拷贝构造函数和析构函数仍然被定义以打印它们的消息。然而，拷贝构造函数从未被调用，因为对象是通过引用传递的，没有产生拷贝。在第 41 行创建了一个对象，并从第 42 行开始打印默认年龄。

在第 46 行，使用 `setAge` 设置了 `itsAge`，并在第 47 行打印了结果。程序中没有使用 `FunctionOne`，但调用了 `FunctionTwo()`。`FunctionTwo()` 发生了微变化，在第 36 行声明了参数和返回值，以接收一个指向常量对象的常量指针，并返回一个指向常量对象的常量指针。

## 引用

由于参数和返回值仍然通过引用传递，因此没有产生拷贝，拷贝构造函数也没有被调用。然而，`FunctionTwo()` 中的指针现在是常量的，因此无法调用非 `const` 方法 `setAge()`。如果第 64 行对 `setAge()` 的调用没有被注释，程序将无法编译。

注意，在 `main()` 中创建的对象不是常量的，`Frisky` 可以调用 `setAge()`。非常量对象的地址被传递给 `FunctionTwo()`，因为 `FunctionTwo()` 的声明将指针声明为指向常量对象的常量指针，对象被处理得就像常量一样！

# 引用作为指针的替代方案

列表 9.11 解决了创建额外拷贝的问题，并节省了拷贝构造函数和析构函数的调用。它使用了指向常量对象的指针，从而解决了函数修改对象的问题。然而，这有些繁琐，因为传递给函数的是指针。

由于你知道对象永远不会为空，如果传递引用而不是指针，在函数内部工作会更简单。列表 9.12 阐释这一点。

# 代码列表 9.12 传递对象的引用

```cpp
1: //Listing 9.12
2: // 传递对象的引用
3:
4: #include <iostream.h>
5:
6: class SimpleCat
7: {
8:   public:
9:     SimpleCat();
10:    SimpleCat(SimpleCat&);
11:    ~SimpleCat();
12:
13:
14:    int getAge() const { return itsAge; }
15:    void setAge(int age) { itsAge = age; }
16:
17:  private:
18:    int itsAge;
19:  };
20:
21: SimpleCat::SimpleCat()
22: {
23:
24:     cout << "Simple Cat Constructor...\n";
25:     itsAge = 1;
26: }
27:
28: SimpleCat::SimpleCat(const SimpleCat& theCat)
29: {
30:     cout << "Simple Cat Copy Constructor...\n";
31: }
32:
33: SimpleCat::~SimpleCat()
34: {
35:     cout << "Simple Cat Destructor...\n";
36: }
37:
38: const SimpleCat & FunctionTwo(const SimpleCat & theCat);
39:
40: int main()
41: {
42:     cout << "Making a cat...\n";
43:     SimpleCat Frisky;
44:     cout << "Frisky is " << Frisky.getAge() << " years old\n";
45:     int age = 5;
46:     Frisky.setAge(age);
47:     cout << "Frisky is " << Frisky.getAge() << " years old\n";
48:     cout << "Calling FunctionTwo...\n";
49:     FunctionTwo(Frisky);
50:     cout << "Frisky is " << Frisky.getAge() << " years old\n";
51:     return 0;
52: }
53:
54: // functionTwo，传递指向常量对象的引用
55: const SimpleCat & FunctionTwo(const SimpleCat & theCat)
56: {
57:     cout << "Function Two. Returning...\n";
58:     cout << "Frisky is now " << theCat.getAge();
59:     cout << " years old\n";
60:     // theCat.setAge(8); const!
61:     return theCat;
62: }
```

## 输出

```
Making a cat...
Simple Cat Constructor...
Frisky is 1 years old
Frisky is 5 years old
Calling FunctionTwo...
Function Two. Returning...
Frisky is now 5 years old
Frisky is 5 years old
Simple Cat Destructor...
```

## 引用

由于参数和返回值仍然通过引用传递，没有产生拷贝，拷贝构造函数也没有被调用。然而，`FunctionTwo()` 中的引用现在是常量的，因此无法调用非 `const` 方法 `setAge()`。如果第 60 行对 `setAge()` 的调用没有被注释，程序将无法编译。

注意，在 `main()` 中创建的对象不是常量的，`Frisky` 可以调用 `setAge()`。非常量对象被传递给 `FunctionTwo()`，因为 `FunctionTwo()` 的声明将参数声明为指向常量对象的引用，对象被处理得就像常量一样！
