
# 数组、C 字符串和链表

```cpp
57:     for (unsigned short i = 0; i < itsLen; i++)
58:         itsString[i] = cString[i];
59:     itsString[itsLen] = '\0';
60: }
```

## 列表 12.12 续

```cpp
100:     return itsString[itsLen - 1];
101: else
102:     return itsString[offset];
103: }

// 用于 const 对象的常量偏移操作符
//（参见拷贝构造函数！）
char String::operator[](unsigned short offset) const
{
    if (offset > itsLen)
        return itsString[itsLen - 1];
    else
        return itsString[offset];
}

// 通过将当前字符串
// 加到右操作侧创建一个新字符串
String String::operator+(const String& rhs)
{
    unsigned short totalLen = itsLen + rhs.GetLen();
    String temp(totalLen);
    unsigned short i;
    for (i = 0; i < itsLen; i++)
        temp[i] = itsString[i];
    for (unsigned short j = 0; j < rhs.GetLen(); j++, i++)
        temp[i] = rhs[j];
    temp[totalLen] = '\0';
    return temp;
}

// 修改当前字符串，无返回值
void String::operator+=(const String& rhs)
{
    unsigned short rhsLen = rhs.GetLen();
    unsigned short totalLen = itsLen + rhsLen;
    String temp(totalLen);
    unsigned short i;
    for (i = 0; i < itsLen; i++)
        temp[i] = itsString[i];
    for (unsigned short j = 0; j < rhs.GetLen(); j++, i++)
        temp[i] = rhs[i - itsLen];
    temp[totalLen] = '\0';
    *this = temp;
}

int main()
{
    String s1("initial test");
    cout << "S1\t" << s1.GetString() << endl;

    char *temp = "Hello World";
    s1 = temp;
    cout << "S1\t" << s1.GetString() << endl;

    char tempTwo[20];
    strcpy(tempTwo, "nice to be here");
    s1 += tempTwo;
    cout << "tempTwo\t" << tempTwo << endl;
    cout << "S1\t" << s1.GetString() << endl;

    cout << "S[4]\t" << s1[4] << endl;
    s1[4] = 'x';

    cout << "S1\t" << s1.GetString() << endl;
    cout << "S1[999]\t" << s1[999] << endl;

    String s2("Another string");
    String s3;
    s3 = s1 + s2;
    cout << "S3\t" << s3.GetString() << endl;

    String s4;
    s4 = "Why does this work?";
    cout << "S4\t" << s4.GetString() << endl;
    return 0;
}
```

| S1: | initial test |
| :--- | :--- |
| S1: | Hello World; nice to be here |
| tempTwo: | nice to be here |
| S1: | Hello World; nice to be here |
| S1[4]: | o |
| S1: | Hellx World; nice to be here |
| S1[999]: | e |
| S3: | Hellx World; nice to be hereAnother string |
| S4: | Why does this work? |

第 7–31 行是 `String` 类的声明。第 11–13 行包含了三个构造函数：默认构造函数、拷贝构造函数、一个加法构造函数，以及一个接受现有空终止（C 风格）字符串的构造函数。

该 `String` 类重载了偏移操作符 (`[]`)、加操作符 (`+`) 和加赋值操作符 (`+=`)。偏移操作符被重载了两次：一次返回 `char`，另一次返回 `char` 引用的非常量函数。

非常量版本用于如下语句：

`SomeString[4] = 'x';`

如第 161 行所示。这允许直接访问字符串中的每个字符。返回的是字符的引用，因此调用函数可以对其进行操作。

常量版本用于访问常量 `String` 对象时，例如在拷贝构造函数的实现中（第 63 行）。注意 `rhs[i]` 被访问时，`rhs` 被声明为 `const String`。通过非常量成员函数访问该对象是不合法的。因此，偏移操作符必须重载一个常量访问器。

如果返回的对象，你可能希望将其声明为常量引用。但由于是 `char`，这样做没有意义。

默认构造函数实现在第 33–39 行。它创建了一个长度为 0 的字符串。`String` 类的约定是不计算终止符的长度。

拷贝构造函数实现在第 63–70 行。它将新字符串的长度设置为现有字符串的长度加上 1（终止符）。它将现有字符串的每个字符拷贝到新字符串，并终止新字符串。

第 53–60 行实现了接受现有 C 风格字符串的构造函数。该构造函数与拷贝构造函数相似。现有字符串的长度通过调用 `strlen` 确定。

偏移操作符在第 107 行重载了两次：返回 `char` 和返回 `char` 引用的非常量函数。

## 链表和其他结构

数组非常像保鲜盒。它们是极佳的容器，但它们的尺寸是固定的。如果你选择一个太大的容器，就会浪费存储区域的空间。如果你选择一个太小的容器，它的内容就会溢出来，导致你陷入一团糟。

解决这个问题的方法之一是使用链表。链表是一种由小容器组成的数据结构，这些容器被设计为适应大小并根据需要链接在一起。其思想是编写一个类，持有你的数据的一个对象——例如一个 `CAT` 或一个 `Rectangle`——并且它可以指向下一个对象。你为需要存储的每个对象创建一个容器，并根据需要将它们链在一起。

这些容器被称为节点。列表中的第一个节点称为头节点，列表中的最后一个节点称为尾节点。

列表有三种基本形式。从简单到复杂，它们是：

- 单向链表
- 双向链表
- 树

在单向链表中，每个节点都向前指向下一个节点，但不向后指向。要找到特定节点，从顶部开始从一个节点移动到另一个节点，就像玩寻宝一样（“下一个节点在沙发下”）。双向链表允许你在链中向前和向后移动。树是由节点构建的复杂结构，其中每个节点都可以指向两个或三个方向。图 12.5 显示了这三个基本...

### 图 12.5 单向链表

![](img/a66ce94ee9cc26e5c70f5604bcd3600c_430_0.png)

## 链表案例研究

在本节中，我们将详细研究链表的案例，包括你如何创建复杂结构，更重要的是，你如何使用继承、多态和封装来管理大型项目。

## 职责委托

面向对象编程的一个基本前提是：每个对象都非常出色地完成*一个*事情，并将任何不是其核心使命的任务委托给其他对象。

汽车是硬件中这一理念的完美示例：引擎的工作是产生动力。动力的分配不是引擎的任务；那是传动器的任务。转向既不是引擎也不是传动器的任务；它被委托给了轮子。

一个设计良好的机器有很多许多小的、易于理解的部件，每个部分各司其职并协作完成更大的目标。一个设计良好的程序也是如此：每个类都只专注于自己的分内，但它们合在一起就创造出了一件极其了不起的毯子。

## 链表的组成部分

链表由节点组成。节点类本身将是抽象的；我们将使用三个子类型来完成工作。有一个头节点，其工作是管理列表的头部；一个尾节点（猜猜它的工作是什么！），以及零或多个内部节点。内部节点将跟踪列表中要持有的实际数据。

注意，数据和列表是完全不同的。在理论上，你可以在列表里保存任何你喜欢类型的数据。链接在一起的不是数据，而是*持有*数据的节点。

驱动程序并不知道节点；它与列表交互。然而，列表做的工作很少；它只是将任务委托给节点。

### 列表 12.13

```cpp
0:  //*******************************************
1:  // FILE: Listing 12.13
2:  //
3:  // PURPOSE: 演示链表
4:  // NOTES:
5:  //
6:  //
7:  //
8:  //
9:  // 演示一种面向对象的方法来实现
10: // 链表。列表将任务委托给节点。
11: // 节点是一个抽象数据类型。使用了三种类型的
12: // 节点：头节点、尾节点和内部
13: // 节点。只有内部节点持有数据。
14: //
15: // 创建该类是为了作为一个对象
16: // 放在链表中。
17: //
18: // ************************************
21: #include <iostream.h>
23: enum { kSmaller, kLarger, kSame };

// 放入链表中的数据类
// 此链表中的任何类必须支持两个方法：
// Show（显示值）和 Compare（返回相对
// 位置）
class Data
{
public:
    Data(int val) : myValue(val) {}
    ~Data(int) {}
    int Compare(const Data &);
    void Show();
private:
    int myValue;
};

// Compare 用于决定对象在列表
// 中的位置。
int Data::Compare(const Data &otherData)
{
    if (myValue < otherData.myValue)
        return kSmaller;
    if (myValue > otherData.myValue)
        return kLarger;
    else
        return kSame;
}

// 前向声明
class Node;
class HeadNode;
class TailNode;

// 表示列表节点的 ADT
// 每个类必须重写 Insert 和 Show
class Node
{
public:
    Node();
    virtual ~Node();
    virtual Node * Insert(Data *theData) = 0;
    virtual void Show() = 0;
private:
};

// 这是持有实际数据的节点
// 在这种情况下对象的类型是
class InternalNode : public Node
{
public:
    InternalNode(Data * theData, Node * next);
    ~InternalNode() { delete myNext; delete myData; }
    Node * Insert(Data * theData);
    void Show() { myData->Show(); myNext->Show(); }

private:
    Data * myData; // 数据本身
    Node * myNext; // 指向列表中的下一个节点
};

// 构造函数的作用是初始化
InternalNode::InternalNode(Data * theData, Node * next) :
    myData(theData), myNext(next)
{
}

// 列表的核心部分
// 当我们将一个新对象放入列表时
// 它被传递给节点，由节点找出
// 它去哪里并将其插入列表
Node * InternalNode::Insert(Data * theData)
{
    // 新家伙比我大还是小？
    int result = myData->Compare(*theData);

    switch (result)
    {
        // 根据惯例，如果是相同的则排前面
        case kSame: // 穿
        case kLarger: // 新数据在在我前面
        {
            InternalNode * dataNode = new InternalNode(theData, this);
            return dataNode;
        }

        // 它比我大，所以把它传递给下一个
        // 节点并让他来处理。
        case kSmaller:
            myNext = myNext->Insert(theData);
            return this;
    }
    return this; // 取悦编译器
}

// 尾节点只是一个哨兵
class TailNode : public Node
{
```

```cpp
120: }
121:
122:
123: // 尾节点只是一个哨兵
124:
125: class TailNode : public Node
126: {
```
