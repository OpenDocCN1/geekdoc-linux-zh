
在示例程序中，`operator<<( )`函数被声明为其类的友元，以便它可以访问私有数据成员`tc_x`和`tc_y`。该函数返回类型`ostream &`——一个`ostream`对象的引用。该函数还声明了两个参数：一个`ostream`引用对象`os`和一个对正在重载运算符的类的对象的`const`引用`TCoordinate`在此示例中。`TCoordinate`引用参数在GNU C++中必须是`const`，有些其他编译器不需要，但这也很好，因为在输出流语句中写入对象肯定不应该改变其值。

由于重载的运算符函数返回`ostream`引用，类的对象可以在级联输出语句中使用。例如，如果`p1`和`p2`是`TCoordinate`对象，此简单语句会显示它们的值：

```
cout << p1 << endl;
    << p2 << endl;
```

你可以为任何类提供相同的输出功能。在`operator<<( )`函数的实现中，按你想要的方式写入`os`参数，如示例程序在以下语句中所做的那样：

```
os << "x == " << t.tc_x << "; y == " << t.tc_y;
```

输出语句的目标是`os`，而不是你可能假设的`cout`。通过写入传递给重载函数的`ostream`引用对象`os`，`TCoordinate`对象可以写入任何目标，例如磁盘文件。更多内容将在第20章“自定义I/O流”中介绍。

清单19.7演示了重载输出运算符的工作方式。程序构造一个`TCoordinate`对象并使用以下语句将其写入`cout`：

```
TCoordinate p(10, 20);
cout << p << endl;
```

使用以下命令编译并运行程序以查看第二个语句产生的文本：

```
$ g++ pointout.cpp
$ ./a.out
x == 10; y == 20
```

## 重载输入流

重载输入流运算符`>>`实质上教会了C++如何输入一个类的对象。清单19.8，`pointin.cpp`，与`pointout.cpp`类似，但为`TCoordinate`对象添加了输入和输出运算符。

```cpp
#include <iostream.h>

class TCoordinate {
private:
    int tc_x, tc_y;
public:
    TCoordinate(): tc_x(0), tc_y(0) { }
    TCoordinate(int x, int y): tc_x(x), tc_y(y) { }
    void Setxy(int x, int y);
    int Getx() const;
    int Gety() const;
    friend ostream &
        operator<<(ostream & os, const TCoordinate &t);
    friend istream &
        operator>>(istream & is, TCoordinate &t);
};

int main()
{
    TCoordinate p;
    cout << "Before: " << p << endl;
    cout << "Enter x and y values (ex. 10 20): ";
    cin >> p;
    if (cin.good())
        cout << "Input error" << endl;
    else
        cout << "After: " << p << endl;
    return 0;
}

// Implement the overloaded << operator friend function
//
ostream &
operator<<(ostream & os, const TCoordinate &t)
{
    os << "x = " << t.tc_x << "; y = " << t.tc_y;
    return os;
}

// Implement the overloaded >> operator friend function
//
istream &
operator>>(istream & is, TCoordinate &t)
{
    is >> t.tc_x >> t.tc_y;
    return is;
}
```

重载的输入流运算符`>>`函数与输出函数类似声明为以下类的友元：

```
friend istream &
operator>>(istream & is, TCoordinate &t);
```

`operator>>() `函数返回一个`istream`输入流对象的引用，以便它可以在级联输入语句中使用。它声明了两个参数：一个名为`is`的`istream`引用和一个`TCoordinate`对象的引用。在这种情况下，输入对象不能是常量，因为输入运算符很可能以某种方式改变其值。在这种情况下，函数的实现只是使用以下语句从输入流参数`is`读取到`TCoordinate`对象的`tc_x`和`tc_y`私有数据成员中：

```
is >> t.tc_x >> t.tc_y;
```

在此之后，函数返回相同的输入流引用`is`。所有`operator>>() `函数都应以相同的方式结束。

`main()`程序演示了如何使用`TCoordinate`类的新输入功能。程序首先构造一个默认对象，然后提示你向其中输入值：

```
TCoordinate p;
cin >> p;
```

要尝试此操作，请输入以下命令编译并运行程序，然后键入两个整数值，用空白分隔，如下所示：

```
$ g++ pointin.cpp
$ ./a.out
Before: x == 0; y == 0
Enter x and y values (ex. 10 20): 45 62
After: x == 45; y == 62
```
