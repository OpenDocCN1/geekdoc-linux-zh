
```cpp
if ( 2 * num < 40 ) {
    myFile << ",";
}
} // 循环结束
// 在数字序列后换行
myFile << endl;
cout << "The file has been created." << endl;
return 0;
}
```

下面的语句使用了特殊字符，允许在显示的字面量字符串中包含引号：

```cpp
cout << "Making file \"even-numbers\" in your directory." << endl;
```

如果没有这个特殊字符，你将无法在文件名 `even-numbers` 周显示引号

## 将用户输入保存到文件

程序经常需要保存用户在运行时输入的数据。在某些情况下，输入的数据量是可预测的，但在另一些情况下，程序不知道会期待多少数据，也不知道需要保存多少数据。

我们将从一个请求少量固定数据的简单程序开始。

下一页的示例将要求用户输入三个单词，并将每个单词存储在独立的变量中。程序将在你的计算机上创建一个名为 `"veryisafed"` 的新文件。然后将这三个变量的每个值分别写入文件中作为单独的文本。最后，程序关闭新创建的数据文件。

## 示例 11.2 - save_text.cpp

```cpp
#include <iostream>    // 程序将在屏幕上显示一些文本
#include <fstream>      // 程序将使用文件
using namespace std;               // 将使用标准标识符 string, cin, endl,
int main() {
    // 在 SD 卡上创建一个文件
    ofstream myFile;
    myFile.open("verysafedata");
    // 输入三个单词并使用变量存储在内存中
    string firstWord, secondWord, thirdWord;
    cin >> firstWord;
    cin >> secondWord;
    cin >> thirdWord;
    // 将这些单词存储在卡上的文件中
    myFile << "First I typed this... ";
    myFile << firstWord << endl;
    myFile << "Then I typed this... ";
    myFile << secondWord << endl;
    myFile << "Finally I typed this... ";
    myFile << thirdWord << endl;
    // 通知电脑你已完成对文件的使用
    myFile.close();
    return 0;
}
```

一旦你运行程序并输入文本，你就可以从 Linux 命令行检查你的 Pi 是否成功创建了存储数据的文件。

下面的截图显示了使用 `cat` 命令检查文本是否已成功存储在 `"verysafedata"` 文件中：

```
$pi@Desktop $ ls verysafedata
verysafedata
$ cat verysafedata
First I typed this... Albatross
Then I typed this... Squirrel
Finally I typed this... Vampire
$pi@Desktop $
```

这个程序是非常可预测的。它总是保存每三个值，尽管你可以更改这三个值。遗憾的是，我们并不总是知道计算机想要向文件中写入多少数据。要保存的数据量可能要不可预测得多。

394 | 在树莓派上使用 C++ 编程

## 示例 11.3 - save_inputs.cpp

当然，这假设一切进展顺利：即你的 Pi 上有足够的空空间，并且你有权限在当前工作目录中创建文件。你将在后面的程序中学习如何在尝试创建文件时防止发生任何错误。

警告：当你运行程序时，如果你的 Pi 的当前目录下已经有一个名为 `"my-data"` 的文件，它将被新文件覆盖，其中的任何数据也将丢失。

为了测试程序运行，请输入几个单词，后面跟一个空行：

```
请输入几行文本。
完成后请按回车输入空行。
one
two
big
GNU
Thank you - text saved to "my-data".
```

你可以看到数据文件已经创建，并且它包含了你输入的值：

```
pi@~/Desktop $ ls -1 my-data
4 -rw-r--r-- 1 pi pi 37 Dec 4 01:11 my-data
pi@~/Desktop $ cat my-data
one
two
big
GNU
*** End of file! ***
pi@~/Desktop$
```

`ls` 命令显示 `"my-data"` 文件包含 37 字节的数据。`cat` 显示该文件中包含的文本数据。如上面所示，我输入的每行都已保存到文件中。

另外注意，我完成输入数据时最后的那个空行并没有实际保存到文件中。程序没有将此发送到 `myfile` 流以进行保存。

## 向现有文件末尾追加数据

到目前为止，我们的程序使用简单的 `open()` 函数调用来创建输出文件流，并传入了要写入的文件名：

```cpp
myFile.open("my-data");
```

记住，用这种方式打开文件流时，任何同名的现有文件都将被覆盖，其包含的任何数据也将丢失。

如果你的程序需要将数据添加到现有文件的末尾而不是覆盖它，你可以在打开输出文件流时指定一个额外选项来追加数据。

程序可以通过识别额外的参数来使用文件追加模式 `ios::app` 来创建一个输出文件流：

```cpp
myFile.open("my-data", ios::app);
```

这意味着写入文件流的数据将位于文件中任何现有数据之后。新的数据行将被添加到末尾。

如果文件不存在会发生什么？你的程序如何能向一个不存在的文件追加数据呢？如果之前不存在该文件，且这是第一次向名为此名的文件写入数据，那么通过 `open()` 调用将自动创建该文件，以便向其中添加数据。

下面的程序在打开输出文件时使用了文件追加模式：

## 示例 11.4 - append_inputs.cpp

```cpp
#include <iostream>    // 程序将在屏幕上显示一些文本
#include <fstream>       // 程序将使用文件
using namespace std;               // 将使用标准标识符 string, cout and endl
int main() {
    // 通知用户需要做什么
    cout << "请输入几行文本。" << endl;
    cout << "完成后请按回车输入空行。" << endl;
    // 以追加模式打开文件或写入 "my-data"
    ofstream myFile;
    myFile.open("my-data", ios::app);
    // 通知用户需要做什么
    string lineText;
    do {
        // 从键盘获取一行
        getline(cin, lineText);
        // 如果行为空，则退出循环
        if (lineText.empty()) {
            break;
        }
        // 将行写入文件
        myFile << lineText << endl;
    } while (true);
    // 通知电脑你已完成对文件的使用
    myFile.close();
    // 通知用户发生了什么
    cout << "Thank you - text saved to \"my-data\"." << endl;
    return 0;
}
```

下面的程序在打开输出文件时使用了文件追加模式：

## 示例 11.4 - append_inputs.cpp

```cpp
#include <iostream>    // 程序将在屏幕上显示一些文本
#include <fstream>       // 程序将使用文件
using namespace std;               // 将使用标准标识符 string, cout and endl
int main() {
    // 通知用户需要做什么
    cout << "请输入几行文本。" << endl;
```
