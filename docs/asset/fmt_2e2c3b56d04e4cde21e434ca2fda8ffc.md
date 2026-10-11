
当小部件需要绘制时，就会调用第 56 行的 `paintEvent()` 方法。第 60 行的 `orientation()` 方法根据面板的的方向返回垂直（Vertical）或水平（Horizontal）。在本示例中，文本会选择相应的方向，并计算文本的位置，使其出现在小程序窗口的中心。

此示例实现了第 72 行的 `mouseEvent()` 方法，并通过启动 `kmail` 应用程序来响应任何鼠标点击。

## 总结

在复杂到需要运行多个程序的系统中，应用程序之间的通信易易性可能非常重要。此外，使用标准方法可以与作为其他项目编写的应用程序进行通信。本章探讨了以下内容：

- KDE 通过名为 `dcservice` 的后台进程发送和接收进程间消息。
- 使用 `KCCommandLineArgs` 类来读取和处理命令行参数可以简化命令行解析的编程任务，并为所有 KDE 应用程序标准化参数格式。
- 使用 `KUniqueApplication` 替代 `QApplication` 可以确保你的程序在任何时候只有一个副本在运行。

下一章将描述一些实用类，你可以利用这些类来处理如读写文件、操作数据和时间信息等任务。

# 一些通用实用类

用于创建 GUI 界面的类在处理某些其他任务时也大大用用场。特别是快速、高效地处理字符字符串的能力可能非常重要。在显示和检索数据时涉及大量的字符串操作，如果没有一些让工作变得更容易的设施，编写字符串处理将非常耗时。

编写应用程序时经常出现的另一个问题是处理日历和时钟算术的能力。虽然总会有操作系统以某种形式返回时间，但对时间值执行复杂操作需要大量的编程工作——例如，如果你有两个日期，你能确定它们之间有多少天吗？

大多数大型数据文件被交给数据库包进行存储和检索，但任何大小的程序都会使用字符串文件来包含特殊数据。尽管 C 和 C++ 标准使用非常简单的方法来读写这些文件，但仍然存在对其包含的数据进行格式化和反格式化的问题。

本章涵盖了一些非常有用的类，它们在解决这些问题方面大有用。虽然这绝不是 Qt 中可用类的完整列表，但它涵盖了一些核心类——其中一些是最明显的类。

## 字符串类

许多编程涉及字符串操作。这对于所有编程都是如此，但对于用户界面的编程尤为如此。数据被转换为字符串以便显示，用户输入的数据从字符字符串转换为某些内部数据格式。一些特殊的字符串处理类使这一切处理起来变得更加容易。

# 第 16 章

## 本章内容

- 使用字符串类操作字符串
- 运行一个定时器，在到期时通知你的程序
- 标记当前时间并在稍后检查已通过
- 执行日期和日历算术
- 从文件读取文本
- 向文件写入文本

# 检查 QString

`QString` 可能是最基本的字符串类，也是你应该使用的类。`QString` 类拥有许多可以用于字符串操作的方法，并在内部将数据存储为 Unicode。

Unicode 与 ASCII 字符集之间没有兼容性问题，Unicode 包含更多字符。标准的 7 位 ASCII 字符集限于 127 个字符，包括拉丁字母、数字、标点符号和一些控制字符（如回车和退出）。Unicode 使用 16 位字符，因此可以包含高达 65,536 个唯一字符。然而，Unicode 字符集的前 127 个字符（数值 0 到 127）与 ASCII 字符集相同，因此将 ASCII 转换为 Unicode 是轻而易举的。将拉丁字符转换为 ASCII 也同样简单。

关于 Unicode 的更多信息，请参见第 17 章。

以下示例展示了用于定位和提取字符串部分的一些方法：

```
1 /* stringexamine.cpp */
2 #include <QString.h>
3 #include <iostream>
4
5 int main(int argc,char **argv)
6 (
7 QString string;
8 Qchar qchar;
9
10 string =
11 "There is much more to KDE than just a pretty face.";
12
13 cout << string << endl;
14 cout << "The string length is " << endl
15 << string.length() << " characters." << endl;
16 qchar = string[4];
17 cout << "The 5th character is " << (char)qchar.unicode() << "." << endl;
18 cout << "The first 'u' is at " << endl
19 << string.find('u') << "." << endl;
20 cout << "The last 'u' is at " << endl
21 << string.find('u') << "." << endl;
}
```

该程序的输出看起来如下：

There is much more to KDE than just a pretty face.

The string length is 40 characters.

The 5th character is h.

The first 'u' is at 2.

The last 'u' is at 35.

# 374 第二部分 ♦ 逐步进阶

`left()` 和 `right()` 方法返回包含从开头或结尾指定数量字符的 `QString`。`mid` 方法返回包含从索引点开始的指定数量字符的 `QString`。（在本示例中，索引为 22，字符数量为 8。）

## 第 16 章 ♦一些通用工具类

```cpp
35 cout << "Replace init) : "
36 << init(qstring).replace(15,10,"ABC") << endl;
37 
38 return(0);
39 )
```

未更改 (Un-nganged): There is more to KDE than a pretty face.

大写: THERE IS MORE TO KDE THAN A PRETTY FACE.

小写: There is more to kde than a pretty face.

插入 'X': There is mxOre to KDE than a pretty face.

插入 'ABC': There is mABCore to KDE than a pretty face.

前置 'X': Xtere is more to KDE than a pretty face.

前置 'ABC': ABCThere is more to KDE than a pretty face.X

追加 'X': There is more to KDE than a pretty face.ABC

追加 'ABC': There is more tABC than a pretty face.

删除 10: There is more tABC a pretty face.

替换 10: There is more tABC a pretty face.

此示例使用了第 5 行的 `init()` 函数来初始化字符串，因为 `QString` 的每个方法都会修改 `QString` 对象的内容。

第 18 行和第 20 行的 `upper()` 和 `lower()` 方法将字符串中的每个字母转换为大写或小写。对于非字母字符或与方法大小相反的字符，不会发生任何变化。

第 22 行和第 24 行的 `insert()` 方法通过移动字符串部分长度以待插入字符的数量来增加字符串长度。作为参数传递的字符或多个字符会被插入到字符串留下的空隙中。

第 26 行和第 28 行的 `prepend()` 方法通过移动所有字符以待插入字符的数量来增加字符串长度。作为参数传递的字符或多个字符会被插入到字符串前端留下的空隙中。

第 30 行和第 32 行的 `append()` 方法增加字符串的字符长度，并将字符存储在字符串右侧留下的空隙中。

第 34 行的 `remove()` 方法根据指定的字符数量缩短字符串的右侧。这会覆盖中间的一组字符，有效地将它们从字符串中删除。在本示例中，索引为 15，删除的字符数量为 10。

第 36 行的 `replace()` 方法可用于延长字符串、缩短字符串或保持长度不变。在任何情况下，字符串中的某些字符都会被替换。该过程在功能上等同于执行 `remove()` 后执行 `insert()`。索引点（在本示例中为 15）右侧的字符根据插入和删除字符的数量向右或向左移动（在本示例中，向左移动了 7 个字符并插入了 3 个字符）。然后使用指定的字符串覆盖索引处的行。

## CString 数字转换

`CString` 类的一部分包含了一些在数字与数值的字符表示之间的直接转换方法。下面的示例演示了它们的工作原理：
