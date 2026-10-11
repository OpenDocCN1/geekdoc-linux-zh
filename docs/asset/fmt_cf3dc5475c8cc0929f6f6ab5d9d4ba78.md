
```cpp
int main() {
    // 创建一个新的二维点，在堆上存储其数据
    point2D* pFirstPoint = new point2D;

    // 顺指针设置结构体中的每个成员数据值
    pFirstPoint->xCoord = -10;
    pFirstPoint->yCoord = 5;
    pFirstPoint->textDescription = "坠毁的外星飞船";

    // 将指针传递给显示点的函数
    displayPoint(pFirstPoint);
    // -------------------------------------------------

    // 创建另一个二维点，在堆上存储其数据
    point2D* pSecondPoint = new point2D;

    // 顺着指针设置结构体中的每个成员数据值
    pSecondPoint->xCoord = 35;
    pSecondPoint->yCoord = 10;
    pSecondPoint->textDescription = "速取店";

    // 将指针传递给显示点的函数
    displayPoint(pSecondPoint);

    return 0;
}
```

正如前面提到的，该程序在堆上动态存储数据。每个 `point2D` 结构的地址都通过指针变量 `pFirstPoint` 和 `pSecondPoint` 存储：

### pFirstPoint

| 成员名称 | 值 |
| --- | --- |
| `xCoord` | -10 |
| `yCoord` | 5 |
| `textDescription` | 坠毁的外星飞船 |

### pSecondPoint

| 成员名称 | 值 |
| --- | --- |
| `xCoord` | 35 |
| `yCoord` | 10 |
| `textDescription` | 速取店 |

除了创建点并设置其坐标和文本描述的 `main()` 函数外，该程序还包含一个名为 `displayPoint()` 的函数。

`displayPoint()` 函数接收一个指向 `point2D` 结构的指针，并检查该指针是否可以安全引用。

如果指针不为 `NULL`，函数将在屏幕上显示 `point2D` 结构中的每个数据成员。

注意这里使用 `->` 指针-成员运算符来访问每个数据成员：

```cpp
cout << pPoint->textDescription;
```

`main()` 函数调用了两次 `displayPoint()`，针对存储在堆上的每个点各调用一次。

结果所示：

> 坠毁的外星飞船位于坐标 (-10, 5)

> 速取店位于坐标 (35, 10)

## 指针数组

此示例允许用户在运行时动态添加一个或多个人员的联系详情。

它创建了一个指针数组。当用户为每个人输入新详细信息时，程序会在堆上动态创建一个新的人员结构体以存储其数据。新创建的数据的地址将作为指针存储在一个名为 `pContact` 的数组中。

### 示例 12.9 - array_of_pointers.cpp

```cpp
#include <iostream>      // 程序将在屏幕上显示一些文本

using namespace std;              // 将使用标准标识符字符串，cout 和 endl
const char TAB = '\t';

//----------------------------------------------------
// 创建新结构体。程序稍后将使用其中的几个变量。
struct person {
    string firstName;
    string emailAddress;
    bool sendNewsletter;
};

//----------------------------------------------------
int main() {
    const int MAX_PEOPLE = 100;
    person* pContact[MAX_PEOPLE];

    int numberOfPeopleEntered = 0;

    person* pNewPerson;
    string newName, newEmail, wantNewsletter;
    //----------------------------------------------------
    // 输入人员详细信息，直到指针数组达到最大尺寸
    // 或者你选择退出
    do {
        cout << "输入新人的姓名，完成后输入 'quit' 退出：" << endl;
        getline(cin, newName);
```

```cpp
if ( newName != "quit" )
{
    cout << "输入他们的邮箱地址：" << endl;
    getline(cin, newEmail);

    cout << "他们想接收每月通讯？y 或 n：" << endl;
    getline(cin, wantNewsletter);

    // 在堆上创建新人员
    pPerson = new person;

    // 设置他们的详细信息
    pPerson->firstName = newName;
    pPerson->emailAddress = newEmail;
    pPerson->sendNewsletter = ( wantNewsletter == "y" );

    // 将指针存储在数组中，以便稍后显示邮件列表时使用
    pContact[numberOfPeopleEntered] = pPerson;

    numberOfPeopleEntered++;

} // 结束 if 判定

cout << endl; // 在再次提示前显示空行
while ( newName != "quit" and numberOfPeopleEntered < MAX_PEOPLE ) {
//
//
// 显示所有订阅了邮件列表的人员
if ( numberOfPeopleEntered > 0 ) {
    cout << "邮件列表：" << endl;
    cout << "--------------------------" << endl;

    // 使用数组中的每个指针来访问人员的详细信息
    for ( int index = 0; index < numberOfPeopleEntered; index++) {
        pCurrentPerson = pContact[index];
        // 如果指针不为 NULL，判断是否在邮件列表中
        if ( pCurrentPerson != NULL && pCurrentPerson->sendNewsletter ) {
            cout << pCurrentPerson->firstName << endl;
        }
    } // 结束 for
} // 结束 if 判定
} // 结束 while
} // 结束 do

return 0;
}
```
