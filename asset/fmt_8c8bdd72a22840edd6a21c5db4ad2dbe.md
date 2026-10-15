
你可以定义某个特定运算符与你创建的任何新类是如何相互作用的。这被称为“运算符重载”。你可以精确地定义每个运算符如何被用于处理类中的数据成员。这可以使类变得更易使用，因为你可以使用如 `+` 或 `=` 等熟悉的运算符符号，而不是调用函数。

该程序展示了如何重载 `<<` 运算符，使得 `mountain` 类的实例可以发送到流，例如 `cout`（屏幕）或 `ofstream`（输出文件）。随后，就可以像对待简单数据类型一样对 `mountain` 对象使用 `<<` 运算符，而不是调用 `displayDetails()` 函数。

示例 `13.6-class_overloaded_operator.cpp`

```cpp
#include <iostream>      // 程序将在屏幕上显示一些文本

using namespace std;      // 将使用标准标识符 string, cout 和 endl

// -----------------------------------------------------------------

class mountain

{

private:

    // 数据成员

    string name;

    string range;

    int elevation;

public:

    // 成员函数和运算符

    mountain(string newName, string newCountry, int newElevation);

    void displayDetails();

    friend ostream& operator<<(ostream &ostream, mountain &objectToShow);

// -----------------------------------------------------------------

mountain::mountain(string newName, string newRange, int newElevation)

{

    // 在创建此类的新实例时调用的构造函数

    name = newName;

    range = newRange;

    elevation = newElevation;

}

// ------------------------------------------

void mountain::displayDetails() {

    // 手动在屏幕上显示每个数据成员的值

    cout << ", " << range;

    cout << " (" << elevation << "m)";

}

// ------------------------------------------

ostream& operator<< (ostream &outStream, mountain &objectToDisplay) {

    // 重载运算符以允许 mountain 对象的数据成员

    // 发送到流，例如 cout (the) 或输出文件流

    outStream << objectToDisplay.name << ", " << objectToDisplay.range

               << " (" << objectToDisplay.elevation << "m")";

    return outStream;

}

// ------------------------------------------

int main() {

    // 创建一个 mountain 类的实例对象

    mountain steepestInWorld("The Great Trango Tower", "Karakoram", 6286);

    // 显示对象的数据成员

    cout << "这两种方法将在屏幕上产生相同的结果：" << endl;

    cout << steepestInWorld << endl;

    steepestInWorld.displayDetails();

    cout << endl;

    return 0;

}
```

当程序执行时，两种方法的结果都会在屏幕上显示相同的文本：

> 这两种方法将在屏幕上产生相同的结果：
> The Great Trango Tower, Karakoram (6286m)
> The Great Trango Tower, Karakoram (6286m)

注意，程序使用了 `friend` 关键字，以允许输出流访问 `mountain` 类的 `name`、`range` 和 `elevation` 数据成员。这是必要的，因为这些数据成员是私有的 `private`，意味着它们只能通过 `mountain` 的成员函数访问。通过将该运算符声明为 `mountain` 类的友元，当 `<<` 运算符尝试访问数据成员时，它将获得权限，从而使它们能够被显示。

## 继承——基于其他类创建新类

有时，你的程序可能需要创建一个与现有对象相似但并不完全相同的对象：例如，你可能想创建一个一种新种的对象，它与现有对象非常相似，但又拥有一个或多个额外的数据成员或函数。

在这种情况下，可以定义一种基于某些其他现有类的新类型类。你可以指定新类包含的额外成员，例如新的数据成员、成员函数或新类将要使用的重载运算符。

基于另一个现有类创建新类被称为“继承”。新类将自动生成其所基于的现有类中定义的任何数据成员、运算符或函数。

例如，我们已经在几个程序中创建并使用了 `mountain` 类。如果我们想创建一个新的 `volcano`（火山）类，我们可以创建一个新类，并指定它所使用的每一个数据成员、函数和运算符。

除了 `mountain` 类包含的 `name`、`range` 和 `elevation` 数据成员外，我们可能想给 `volcano` 类添加两个数据成员：`extinct`（灭绝）和 `lastErupted`（最后喷发）。这些指示了现实中的火山是否仍然活跃。

| 对象类: mountain |
| :--- | :--- |
| string | name |
| string | range |
| int | elevation |

| 对象类: volcano |
| :--- | :--- |
| string | name |
| string | range |
| int | elevation |
| bool | extinct |
| string | lastErupted |

## 继承时对成员访问的控制

在本章的开头，我们已经简要描述了类的 `public`（公有）、`private`（私有）和 `protected`（保护）成员之间的区别。

我们已经看到，特定类的 `private` 成员不能被不属于该类的代码直接访问。任何 `private` 数据成员只能由该类的成员函数访问，而 `private` 成员函数只能由同类函数调用。

当一个类继承另一个类的的数据成员或函数时会发生什么？

任何指定为 `private` 的成员对于继承类来说都是不可见的。为了允许继承类访问成员，有必要使用 `protected` 访问说明符对其进行声明。类的任何 `protected` 成员都可以被该类访问，也可以被任何继承自它的类访问。

在下一个程序中，你将看到 `mountain` 类的数据成员已变为 `protected`，以便继承的 `volcano` 类可以使用它们：

```cpp
class mountain

{

protected:

    // 受保护的数据成员可以直接被该类访问

    // 也可以被继承它的类访问，例如 volcano 类

    string name;

    string range;

    int elevation;

    mountain(); // 不会被使用，但 volcano 会尝试继承它

public:

    mountain(string newName, string newCountry, int newElevation);

    void displayDetails();

    void setName(string newName);

};
```

要指定我们正在从现有的 `mountain` 类继承 `volcano` 类，我们如下所示开始新类的声明：

```cpp
class volcano : public mountain
```

新 `volcano` 类的完整声明所示：

```cpp
class volcano : public mountain {
  private:
    bool extinct;
    string lastErupted;
  public:
    volcano();
```
