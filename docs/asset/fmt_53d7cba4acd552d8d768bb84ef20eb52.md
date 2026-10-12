
```cpp
// 列表 16-3
// 一个演示使用
// ostream_iterator 将输出发送到
// 显示器的程序

#include <iostream>
#include <string>
#include <set>
#include <iterator>
#include <algorithm>

int main(int argc, char argv[]) {
    set<string, less<string> > Out(cout,"\n");
    PenguinPrinciples.insert("The more objects you have");
    PenguinPrinciples.insert("the better off you are");
    PenguinPrinciples.insert("if at first you don't succeed");
    PenguinPrinciples.insert("type --help");
    copy(PenguinPrinciples.begin(),PenguinPrinciples.end(),Out);
}
```

内容显示在屏幕上，是因为`copy()`算法将`Out`作为其目标。注意`Out`在构造函数中通过声明连接到了`cout`：

```cpp
ostream_iterator<string> Out(cout,"\n");
```

此外注意`\n`换行符被传递给构造函数。这意味着在容器项发送到显示器时，将使用新行来分隔每一项。

这是列表 16-3 程序的输出：

* If at first you don't succeed

The objects you

the better off you are

type --help

脑筋急转弯：尝试找出为什么列表 16-3 程序中的字符串是以这种奇怪的顺序发送的。

## 与 `cout` 使用转义字符 `\n`, `\b`, `\t`

字符`"\n"`、`"\b"`和`"\t"`在插入`ostream`时具有特殊含义。`"\n"`字符会导致插入一个新行。因此，代码

```cpp
cout << "Penguin Principle" << "\n";
```

会导致打印"Penguin Principle"然后将光标移动到下一行的开头。`"\b"`导致光标向后移动一个字符。例如，代码

```cpp
cout << "Penguin Principle" << "\b" << "E";
```

会导致小写的`e`被大写的`E`替换，短语：

Penguin Principle

将出现在显示器上。`'\t'`字符导致在流中插入一个制表符。`'\t'`字符可以帮助你格式化输出列。字符`"\f"`也可以插入`ostream`，导致分页。然而，当与显示器一起时，`"\f"`没有这种效果。这当`ostream`连接到打印机或任何具有分页功能的设备时非常有用。

## 使用 `istream` 获取输入

`cout`的对应项是`istream`。`istream`类用于从输入流读取数据。读取数据的常用方法是使用提取运算符`>>`。然而，还有其他读取数据的方法，例如使用`get()`、`getline()`和`read()`方法。提取运算符用于读取整数、浮点数和字符等基本类型。它一直直到遇到空白。这意味着如果你想读取带空格的字符串，提取运算符只会读取第一个单词。读取带空格的字符串，应该使用`getline()`方法。`get()`方法用于从输入流读取单个字符。当你想要读取包括空白在内的字符时，这非常有用。`read()`方法用于从输入流读取指定数量的字符。当需要读取大块数据时非常有用。

## 读取字符

字符字符串和字符串对象可以使用提取运算符`>>`从输入流读取。如果字符串不包含空格，这非常简单。例如，如果输入流包含单词`open`，我们执行提取操作如下：

```cpp
string Input;
cin >> Input;
cout << Input;
```

单词`open`将被输出。这是因为`>>`运算符将空白视为分隔符。当读取字符串`open`时，它会在紧随其后的第一个空格停止。

## 读取包含空格的字符串

读取嵌入空格的字符串对象或空终止字符数组的方法是使用`get()`、`getline()`或`read()`方法。例如，如果我们的输入流包含字符串`open`，我们可以写：

```cpp
string Input;
getline(cin, Input);
cout << Input;
```

## 读取整数和浮点数

键盘处理的优选技术是避免直接读取数字。从字符或字符串读取信息通常更好。如果需要数字，将数字读取为字符串并使用库函数之一将其转换为相应的类型。例如：

```cpp
string NumBuffer;
float Number;
cin >> NumBuffer // 将数字读取为字符串

Number = atof(NumBuffer.c_str);
```

通过这种处理，如果用户输入字符或短语，`cin`不会进入错误状态。此外，一旦你有了`NumBuffer`的内容，就可以检查它是否包含有效数字的字符。然后你可以使用`atof()`和`atoi()`等函数将这些字符转换为数字。读取`int`、`float`或`double`需要的编程非常繁琐。

## 读取不带空格的字符串

（上面已涵盖）

## 第 16 章 开发字符模式应用程序 521

这段代码会将字符串"open source software"发送到显示器。我们也可以通过使用`getline`方法将其获取到空终止字符数组中。

例如：

```cpp
char Input[80];
cin.getline(Input,79,'\n');
cout << Input;
```

语句`cin.getline(Input,79,'\n');`的意思是开始提取字符到数组`Input`中，直到遇到新行或读取`79`个字符（以先者为准）。`ist`类的`get()`和`getline()`方法可读取空白字符。

## 使用 `istream_iterator` 将键盘信息读入容器

`istream_iterator`类可以直接将键盘输入获取到标准`C++`容器类中。`istream_iterator`通过连接`cin`来构造。

例如：

```cpp
istream_iterator<string> Input(cin);
```

这把`istream_iterator Input`连接到`cin`对象。为了使`istream_iterator`工作，你还需声明一个表示键盘输入结束的`istream_iterator`。

例如：

```cpp
istream_iterator<string> EofKeyboard;
```

使用`copy()`算法将键盘输入读入标准`C++`容器中。

例如：

```cpp
vector<string> PenguinPrinciples;
istream_iterator<string> Input(cin);
istream_iterator<string> EofKeyboard;
copy(Input,EofKeyboard,back_inserter(PenguinPrinciples));
```

这段代码允许你在控制台输入任意数量的字符串。这些字符串将被插入到名为`PenguinPrinciples`的`vector`末尾。当没有更多字符串需要输入时，`back_inserter()`函数允许用户继续输入；用户可以输入`Ctrl-D`序列来表示输入结束或文件结束。一旦字符串存储在`vector`中，应用程序就对其完全访问权限。列表 16-4 中的程序简单地从键盘获取字符串列表，将其存储在`vector`容器中，然后将这些字符串发送到显示器。

## 列表 16-4：演示如何使用 `istream_iterator` 的程序
