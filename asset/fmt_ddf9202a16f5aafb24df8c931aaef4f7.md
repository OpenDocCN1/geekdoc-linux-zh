
`void setName(std::string newName);`

};

#endif

```
注意，不需要编译或构建上面的头文件。另一个文件使用 `mountain` 类的方法是添加该头文件的名称指令：

```cpp
#include "mountain.h"
```

成员函数的代码通常保存在单独的文件中。它也将以类命名，但以 ".cpp" 结尾。这意味着我们需要另一个文件来定义 `mountain` 类每个成员函数的代码：

### 示例 13.8b - mountain.cpp

```cpp
#include "mountain.h"           // 类在此文件中声明

#include <iostream>                    // 程序将在屏幕显示一些文本

using namespace std;                    // 将使用标准标识符 cout 和 endl

//--------------------------------------------------------------------------------

mountain::mountain()

{

    // 类必须有这个默认构造函数

    // 任何继承自 mountain 的类将尝试继承

    name = "Not assigned yet";

    range = "Not assigned yet";

    elevation = 0;

}

//--------------------------------------------------------------------------------

mountain::mountain(string newName, string newRange, int newElevation)

{

    // 在创建此类的新实例时调用的构造函数

    name = newName;

    range = newRange;

    elevation = newElevation;

}

//--------------------------------------------------------------------------------

void mountain::displayDetails()

{

    // 显示每个私有数据成员

    cout << " " << name << endl;

    cout << " " << range << endl;

    cout << " (" << elevation << "m)" << endl;

}

void mountain::setName(string setName)

{

  name = setName;

}
```

这是一个示例，它在包含可重用的 "mountain.cpp" 后，创建了 `mountain` 类的多个实例：

### 示例 13.8c - highest_mountains.cpp

```cpp
#include <iostream> // 程序将在屏幕上显示一些文本

#include "mountain.cpp" // mountain 类中包含的函数代码

using namespace std; // 将使用标准标识符 cout 和 endl

int main() {

    // 创建3 个不同的对象，每个对象都是 mountain 类的实例

    mountain highestInWales("Mt. Snowdon/Yr Wyddfa", "Snowdonia", 1085);

    mountain highestInAfrica("Kimanjaro", "Eastern Rift", 5895);

    mountain highestInSouthAmerica("Aconagua", "Andes", 6961);

    // 为 3 个对象中的每一个调用 displayDetails() 成员函数

    cout << "The highest mountain in Wales is ";

    highestInWales.displayDetails();

    cout << endl << endl;

    cout << "The highest mountain in Africa is ";

    highestInAfrica.displayDetails();

    cout << endl << endl;

    cout << "The highest mountain in South America is ";

    highestInSouthAmerica.displayDetails();

    cout << endl << endl;

    return 0;

}
```

注意，该程序包含一个包含 "mountain.cpp" 代码的指令：

```cpp
#include "mountain.cpp"
```
