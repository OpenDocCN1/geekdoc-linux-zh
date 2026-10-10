
```cpp
class Television {
private:
    int channelNumber;
    bool on;

public:
    void powerOn() { on = true; }
    void powerOff() { on = false; }
    void changeChannel(int x) { channelNumber = x; }
};

void main() {
  Television derekTV;
  Television johnTV;
  derekTV.powerOn();
  derekTV.changeChannel(52);
  johnTV.powerOn();
  johnTV.changeChannel(1);
}
```

# 第5章 在树莓派上进行编程 201

## 封装

封装用于隐藏对象的内部机制。在物理电视的类比中，封装是由保护内部电子系统的外壳提供的。然而，你仍然拥有遥控器，它会直接影响内部工作方式。

在面向对象编程 `OOP` 中，你使用访问修饰符 `private` 决定哪些工作需要隐藏（例如电视电子设备），并使用访问修饰符 `public` 决定哪些是接口的一部分（例如电视遥控器）。

```cpp
class Television{
private:
    int channelNumber;
    bool on;
    void remodulate_tuner();
public:
    powerOn() { on = true; }
    powerOff() { on = false; }
    changeChannel(int x) {
        channelNumber = x;
        remodulate_tuner();
    }
};
```

现在 `Television` 类拥有了私有状态数据（`on`, `channelNumber`），这些数据只受公共接口方法（`powerOn()`, `powerOff()`, `changeChannel()`）的影响，并且有一个私有的实现方法 `remodulate_tuner`，它无法从类外部调用。

这种方法有许多优点：首先，该类的用户（另一个程序员）不需要理解 `Television` 类的内部原理；他们只需要理解公共接口。其次，`Television` 类的作者可以修改和/或完善类的内部原理，而不会影响其他程序员的代码。

## 继承

继承是面向对象编程（`OOP`）的一种特性，它允许从其他类的描述中构建类描述。人类经常这样做；例如，如果你问“什么是鸭子？”，你可能会回答：“它是一种会游泳的鸟，它有嘴而不是喙。”这个描述是准确的，但它假设鸭子的概念也是被所理解的。重要的是，该描述说明了鸭子具有游泳的额外行为，而且它具有用嘴代替喙的替换行为。你可以用伪代码粗略地对此建模：

```cpp
class Bird{
public:
    void fly();
    void describe() { cout << "Has a bill and can fly"; }
};
```

```cpp
class Duck: public Bird{ // 鸭子是 一只鸟
    Bill bill;
public:
    void swim();
    void describe() { cout << "Has a bill and can fly and swim"; }
};
```

在这种情况下，你可以创建一个 `Duck` 类的对象：

```cpp
int main(){
    Duck d; // 创建 Duck 实例对象
    d.swim();      // Duck 类特有
    d.fly();       // 继承自父类 Bird
    d.describe(); // describe 被继承并被 Duck 重写
    // 所以，会显示 "A bill and can fly and swim"
}
```

这里的示例说明了继承有多重要。你可以通过继承并向类描述添加内容（例如 `d.swim()`）来构建代码，或者通过继承父类并替换行为（例如 `describe()`）来提供更具体的实现；这被称为方法重写（`overriding`），它是多态（多种形式）的一种类型。另一种多态形式被称为重载（`overloading`），意味着多个方法在同一个类中可以拥有相同的名称，编译器通过不同的参数类型来消除歧。

你可以通过“是……的”（`is-a`）测试来检查你是否具有继承关系；例如，“鸭子是鸟”是有效的，但“鸟是鸭子”是无效的，因为并不是所有的鸟都是鸭子。这与“是……的一部分”（`is-a-part-of`）关系形成对比；例如，“嘴是鸭子的一部分”。`is-a-part-of` 关系表示嘴是类的成员/状态。当类关系变得复杂时，使用这种简单的检查非常有用。

你也可以使用类对象的指针；例如，在 C++ 中，使用以下代码为两个 `Duck` 对象动态分配内存：

```cpp
int main() {
    Duck *a = new Duck();
    Bird *b = new Duck(); // 父类指针可以指向子对象
    b->describe(); // 实际上会描述鸭子（如果是虚函数）
    b->swim(); // 不允许！Bird 不“知道” swim()
}
```

有趣的是，`Bird` 指针 `b` 被允许指向 `Duck` 对象。`Duck` 是 `Bird` 的子类，`Bird` 指针可以调用的所有方法 `Duck` 对象都“知道”。因此可以调用 `describe()` 方法。箭头符号（`b->describe()`）只是 C++ 中编写 `(*b).describe()` 的新写法。在这种情况下，`Bird` 指针 `b` 的静态类型是 `Bird`。

最后一点是，在 C++ 继承可以使用访问访问符 `protected`。如果你想在父类中创建一个方法或状态，使其对子类可用，但又不想将其设置为公共：

> 注意：我在 `ee402.eng.dcu.ie` 上提供了关于这些主题的笔记。特别是第 3 章和第 4 章详细地描述了这个主题，包括关于抽象类、析构函数、多重继承、友元函数和标准模板库（`STL`）的材料。

# 第5章 在树莓派上进行编程 203

## 使用 C++ 进行面向对象的 LED 控制

现在，可以通过将功能导向的 C++ 代码重构为包含状态和方法的 `LED` 类，将 OOP 概念应用于 RPi 上的真实 C++ 程序。这段代码稍微冗长一些。然而，主要区别列表 5-16 所示的代码可以同时使用同一类的多个对象来控制 GPIO。为此，示例还显示了图 5-1 中 `GPIO4`（引脚 7）的电路也被复制到了 `GPIO17`（引脚 11）。

列表 5-16：`chap05/makeLEDOOP/makeLEDOps`
