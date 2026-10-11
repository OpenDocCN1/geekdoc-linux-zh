
"The Great Trango Tower", "Karakoram", 6286

然而在某些情况下，你可能希望不显式地为对象赋值任何值。例如：

```
mountain steepestInWorld("The Great Trango Tower", "...", 6286);
```

在两个示例中，`mountain`类实例都由程序创建。尽管它们看起来没有使用构造函数，但会自动使用不接受参数的构造函数。该构造函数需要在代码的某处定义：

```cpp
mountain::mountain()
{
  // 不接受参数的构造函数
  // 为每个数据成员分配一个空白默认值。
  name = "";
  range = "";
  elevation = 0;
}
```

下一页的程序展示了如何实现这一点。山数组允许程序遍历这十个实例，而不是编写重复的代码。

### 示例 13.3 - class_array_of_objects.cpp

（由于原始文本在此处中断，未翻译后续内容）

当程序运行时，你应该会在屏幕上看到以下输出：

初始详细信息如下：

| 山峰编号 | 包含数据 |
|---|---|
| 山峰编号 0 包含这些数据: | (0m) |
| 山峰编号 1 包含这些数据: | (0m) |
| 山峰编号 2 包含这些数据: | (0m) |
| 山峰编号 3 包含这些数据: | (0m) |
| 山峰编号 4 包含这些数据: | (0m) |
| 山峰编号 5 包含这些数据: | (0m) |
| 山峰编号 6 包含这些数据: | (0m) |
| 山峰编号 7 包含这些数据: | (0m) |
| 山峰编号 8 包含这些数据: | (0m) |
| 山峰编号 9 包含这些数据: | (0m) |

设置值后，它们包含这些数据：

| 山峰编号 | 未知范围 |
|---|---|
| 山峰编号 0 包含这些数据: | 山峰 A，未知范围 (0m) |
| 山峰编号 1 包含这些数据: | 山峰 B，未知范围 (0m) |
| 山峰编号 2 包含这些数据: | 山峰 C，未知范围 (0m) |
| 山峰编号 3 包含这些数据: | 山峰 D，未知范围 (0m) |
| 山峰编号 4 包含这些数据: | 山峰 E，未知范围 (0m) |
| 山峰编号 5 包含这些数据: | 山峰 F，未知范围 (0m) |
| 山峰编号 6 包含这些数据: | 山峰 G，未知范围 (0m) |
| 山峰编号 7 包含这些数据: | 山峰 H，未知范围 (0m) |
| 山峰编号 8 包含这些数据: | 山峰 I，未知范围 (0m) |
| 山峰编号 9 包含这些数据: | 山峰 J，未知范围 (0m) |

## 在堆上动态创建

到目前为止，我们类的实例都是在`静态内存`中创建的。与简单数据类型和结构体一样，基于类的对象也可以被`动态`创建。我们可以将它们存储在堆内存中，并使用指针来定位和使用它们。此程序在堆上创建一个 `mountain`类的实例，而不是在静态内存中创建：

Example13.4-class_heap.cpp

```cpp
#include <iostream> // 程序将在屏幕上显示一些文本

using namespace std; // 将使用标准标识符 string, cout 和 endl

// -----------------------------------------------------------------------

class mountain
{
    private:
        string name;
        string range;
        int elevation;
    public:
        mountain(string name, string newRange, int newElevation);
        void displayDetails();
        void setName(string name);
        string getName();
};
```

```cpp
// -----------
mountain::mountain( string newName, string newRange, int newElevation )
{
    // 在创建该类的新实例时调用的构造函数函数
    name = newName;
    range = newRange;
    elevation = newElevation;
}
// -----------
void mountain::displayDetails()
{
    cout << name;
    cout << " , " << range;
    cout << " (" << elevation << "m)";
}
// -----------
void mountain::setName( string newName )
{
    name = newName;
}
// -----------
string mountain::getName()
{
    return name;
}
// ---------------------
```

```cpp
int main() {
  // 在堆上创建一个山峰对象并存储指向它的指针
  mountain* pMatterhorn = new mountain("Matterhorn", "Pennine Alps", 4478);
  cout << "This object is stored on the heap:" << endl;
  pMatterhorn->displayDetails();
  cout << endl << endl;
  // 通过附加备备名更新山峰名称
  pMatterhorn->setName(pMatterhorn->getName() + "/Monte Cervino");
  // 再次显示成员数据
  cout << "The object has been updated:" << endl;
  pMatterhorn->displayDetails();
  cout << endl << endl;
  // 销毁山峰对象
  delete pMatterhorn;
  pMatterhorn = NULL;
  cout << "The object has been destroyed." << endl;
  cout << endl << endl;
  return 0;
}
```

这是程序的运行情况：

注意，程序的最后部分使用 `delete` 来销毁山峰对象。直接包含在对象中的所有成员变量都被销毁了，释放了它们在堆上使用的内存。

然而，从堆上删除对象时存在一个潜在问题。如果一个对象包含一个或多个指向其他动态数据的指针，当使用 `delete` 运算符销毁对象时，这些指针值也将作为对象的一部分被销毁。它们所指向的动态数据仍然存在于堆上，不再有任何方法访问它来清理它。堆上的数据实际上被“孤立”了。请记住这被称为“内存泄漏”。

幸运的是，有一个解决方案。在尝试销毁对象时，可以自动调用一个特殊的“清理”函数。该函数可以在对象本身销毁之前清理之前使用的任何数据。这可以确保对象不再存在后内存不会被不占用。这样的函数被称为“析构函数”。

析构函数始终以波浪号 (`~`) 开头，后面跟着类名。例如，`mountain`的析构函数声明如下：

```cpp
public:
    ~mountain();
```

注意，析构函数需要在别处定义：

```cpp
mountain::~mountain()
{
    // 使用此函数销毁任何数据
    delete name;
    delete range;
    delete elevation;
}
```

## 运算符重载

虽然之前的类使用了 `displayDetails()` 函数

在通常情况下，除非你的代码定义了如何处理对象的成员变量，否则无法将对象的内容发送到流中，例如定义它们应该如何显示或保存到文件中：

```
cout << steepestInWorld;      // 这目前无法工作
outputStream << steepestInWorld;  // 这目前无法工作
```
