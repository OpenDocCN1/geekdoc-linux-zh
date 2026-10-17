
## 多态

Pegasus 不再需要区分对 `GetAge()` 的调用，它可以自由地从 `Animal` 继承此函数。注意，Pegasus 仍然必须区分对 `GetColor()` 的调用，因为该函数位于它的两个基类中而不在 `Animal` 中。

### 为虚拟继承声明类

为了确保派生类只有一个公共基类的实例，请让中间类虚拟继承基类。

- 示例 1
```
class Horse : virtual public Animal
class Bird : virtual public Animal
class Pegasus : public Horse, public Bird
```
- 示例 2
```
class Schnauzer : virtual public Dog
class Poodle : virtual public Dog
class Schnnoodle : public Schnauzer, public Poodle
```

## 多继承的问题

虽然多继承相比单继承具有若干优势，但许多 C++ 程序员并不愿意使用它。他们提出的问题是许多编译器不支持它，它使得调试变得困难，并且几乎所有可以通过多继承完成的工作都可以不使用它的情况下完成。

这些都是合理的担忧，你可能会警惕在程序中引入不必要的复杂度。某些调试器在处理多继承时会有困难，某些设计在不需要的情况下使用多继承会变得异常复杂。

| 应该 | 不要 |
| :--- | :--- |
| 当新类需要来自多个一个基类的函数和功能时，使用多继承。当最派生类必须只有一个共享基类的实例时，使用虚拟继承。当使用虚拟基类时，从最派生类初始化共享基类。 | 当使用单继承就能完成时，不要使用多继承。 |

## 混入与能力类

在多重继承和单继承之间取得折中方案的方法是使用所谓的“混入”（mixins）。因此，你可能会让你的 `Horse` 类同时继承自 `Animal` 和 `Displayable`。`Displayable` 仅会添加几个用于在屏幕上显示任何对象的方法。

混入，或能力类（capability class），是一种不添加许多或任何数据而添加功能的类。

能力类像任何其他类一样被混入派生类中，通过声明派生类公地继承这些类来实现。能力类与任何其他类的唯一区别在于，能力类几乎很少或没有数据。当然，这是一种任意的区分，仅仅是一种简写标记方式，表示有时你想要做的只是混入一些额外的能力，而不会使派生类复杂化。

对于某些调试器来说，这使得处理混入比处理复杂的复合对象更容易。此外，访问另一个主要基类中的数据时产生歧义的概率也较低。

例如，如果 `Horse` 继承自 `Animal` 和 `Displayable`，那么 `Displayable` 将一如既往，因此 `Horse` 中的所有数据将派生自 `Animal`，但 `Horse` 中的函数将派生自两者。

“混入”一词源于马萨诸塞州萨默维尔的一家冰淇淋店，那里糖果和蛋糕被混合在基础冰淇淋口味中。对于那些在那里度过暑假的面向对象编程程序员来说，这似乎是一个很好的比喻，特别是在使用面向对象编程语言 SCOOPS 时。

## 抽象数据类型

通常，你会一起创建一个类层次结构。例如，你可能会创建一个 `Shape` 类，并在此基础上派生 `Rectangle` 和 `Circle`。从 `Rectangle`，你可能会派生出 `Square` 作为 `Rectangle` 的一个特例。

每个派生类都将重写 `Draw()` 方法、`GetArea()` 方法等。列表 13.7 展示了 `Shape` 类及其派生类 `Circle` 和 `Rectangle` 类的骨架实现。

### 列表 13.7 Shape 类

```cpp
//Listing 13.7. Shape classes.

#include <iostream.h>

class Shape {

public:

    Shape(){}

    virtual ~Shape(){}

    virtual long GetArea() { return -1; }

    virtual long GetPerim() { return -1; }

    virtual void Draw() { }

private:

};

class Circle : public Shape {

public:

    Circle(int radius):itsRadius(radius){}

    virtual ~Circle(){}

    long GetArea() { return 3 * itsRadius * itsRadius; }

    long GetPerim() { return 6 * itsRadius; }

    void Draw() { }

private:

    int itsRadius;

    int itsCircumference;

};

void Circle::Draw() {

    cout << "Circle drawing routine here!\n";

}

class Rectangle : public Shape {

public:

    Rectangle(int len, int width):
    itsLength(len), itsWidth(width) {}

    virtual ~Rectangle(){}

    virtual long GetArea() { return itsLength * itsWidth; }

    virtual long GetPerim() { return 2*itsLength + 2*itsWidth; }

    virtual int GetLength() { return itsLength; }

    virtual int GetWidth() { return itsWidth; }

    virtual void Draw() { }

private:

    int itsWidth;
    int itsLength;

};

void Rectangle::Draw() {

    for (int i = 0; i<itsLength; i++)
    {
        for (int j = 0; j<itsWidth; j++)
            cout << "x ";
        cout << "\n";
    }
}

class Square : public Rectangle
{
public:
    Square(int len);
    Square(int len, int width);
    virtual ~Square(){}
    long GetPerim() {return 4 * GetLength();}
};

Square::Square(int len):
Rectangle(len,len)
{}

Square::Square(int len, int width):
Rectangle(len,width)
{
    if (GetLength() != GetWidth())
        cout << "Error, not a Rectangle??\n";
}

int main()
{
    int choice;
    bool fquit = false;
    Shape * sp;

    while (!fquit)
    {
        cout << "(1)Circle (2)Rectangle (3)Square()Quit: \n";
        cin >> choice;

        switch (choice)
        {
            case 0: fQuit = true; break;
            case 1: sp = new Circle(5); break;
            case 2: sp = new Rectangle(4,6); break;
            case 3: sp = new Square(5); break;
            default: cout << "Please enter a number between 0 and 3*" << endl; continue; break;
        }
        if (fQuit)
            break;
        sp->Draw();
        delete sp;
        cout << "\n";
    }
    return 0;
}
```

在这个示例中，额外的功能仅仅是打印了一条额外的消息，但可以想象为基类提供了一个共享的绘制机制，例如设置一个所有派生类都会使用的窗口。

## 列表 13.9 实现纯虚函数

```cpp
//实现纯虚函数

#include <iostream.h>

class Shape
{
public:
    Shape(){}
    virtual long GetArea() = 0;
    virtual long GetPerim() = 0;
    virtual void Draw() = 0;
private:
};

void Shape::Draw()
{
    cout << "Abstract drawing mechanism!\n";
}

class Circle : public Shape
{
public:
    Circle(int radius):itsRadius(radius){}
    virtual ~Circle(){}
    long GetArea() { return 3 * itsRadius * itsRadius; }
    long GetPerim() { return 9 * itsRadius; }
    void Draw();

private:
    int itsRadius;
    int itsCircumference;
};

void Circle::Draw()
{
    cout << "Circle drawing routine here!\n";
    Shape::Draw();
}

class Rectangle : public Shape
{
public:
    Rectangle(int len, int width):
        itsLength(len), itsWidth(width){}
    virtual ~Rectangle(){}
    long GetArea() { return itsLength * itsWidth; }
    long GetPerim() { return itsLength + 2*itsWidth; }
    virtual int GetLength() { return itsLength; }
    virtual int GetWidth() { return itsWidth; }
    void Draw();
private:
    int itsWidth;
    int itsLength;
};

void Rectangle::Draw()
{
    for (int i = 0; i<itsLength; i++)
    {
        for (int j = 0; j<itsWidth; j++)
            cout << "*";
    }
    cout << "\n";
    Shape::Draw();
}

class Square : public Rectangle
{
public:
    Square(int len);
    Square(int len, int width);
    virtual ~Square(){}
    long GetPerim() { return 4 * GetLength(); }
};

Square::Square(int len):
    Rectangle(len,len)
{}

Square::Square(int len, int width):
    Rectangle(len,width)
{}

{
    if (GetLength() != GetWidth())
        cout << "Error, not a square... a Rectangle??\n";
}

int main()
{
    int choice;
    bool fQuit = false;
    Shape * sp;

    while (1)
    {
        cout << "(1)Circle (2)Rectangle (3)Square (0)Quit: ";
        cin >> choice;

        switch (choice)
        {
            case 1: sp = new Circle(5); break;
            case 2: sp = new Rectangle(4,6); break;
            case 3: sp = new Square(5); break;
            default: fQuit = true; break;
        }

        if (fQuit)
            break;

        sp->Draw();
        delete sp;
        cout << "\n";
    }
    return 0;
}
```
