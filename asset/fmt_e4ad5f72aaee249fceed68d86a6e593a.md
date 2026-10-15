
在我们关于创建 C/C++ 项目的初步练习中，我们将创建一个相当简单的记录排序应用程序。待排序的记录由姓名和 ID 号组成。为了简化代码，我们将用下划线替换姓名字段中的空格。该程序将按升序排序一个记录文件，可以按照姓名或 ID 号排序，具体方式由命令行指定如下：

```
record_sort <datafile> [ 1 | 2 ]
```

其中 `1` 表示按姓名排序，`2` 表示按 ID 排序。如果未提供排序参数，则默认按姓名排序。

在 Eclipse C/C++ 视角中，选择 `File > New > C Project`。这将打开如图 5.4 所示的新项目向导。将其命名为 `record_sort`。项目类型为 `Executable > Empty Project`。工具链为 `Linux GCC`，我们将使用默认的工作区位置。点击 `Next` 会打开选择配置（Select Configurations）对话框，你可以在其中选择调试（`Debug`）和发布（`Release`）配置中的一种或两种。稍后你可以选择构建这些配置中的任意一个。它们之间的主要区别在于，`Debug` 配置在构建时开启了编译器的调试标志 `"-g"`，以便向 `GDB` 提供符号信息。而 `Release` 配置则不包含调试标志（图 5.4）。

![](img/f03d6fa2c5faefc793771df52bbb2ef9_86_0.png)

**图 5.3**

Eclipse 欢迎屏幕。

![](img/f03d6fa2c5faefc793771df52bbb2ef9_87_0.png)

**图 5.4**

新项目向导。

当你在“新项目向导”中点击 `Finish` 时，你会在“项目资源管理器”（`Project Explorer`）视图中找到一个条目。在 `record_sort` 项目下唯一的项是 `Includes`，它是一个用于搜索头文件的路径列表。

在此时，查看目录 `workspace/record_sort/` 会很有帮助。其中仅包含两个文件：`.cproject` 和 `.project`，这两个都是描述项目的 XML 代码。`.project` 为 Base Eclipse 平台提供配置信息，而内容更丰富的 `.cproject` 文件则为 `CDT` 提供信息。无需理解这些文件的内容，但了解它们的存在是有用的。

### 向项目添加源代码

基本上有两种方法可以向 C 项目添加源代码。当然，你可以在编辑器窗口中创建一个新文件，或者可以*导入现有文件*到项目中。执行 `File > Import...` 以打开导入选择对话框。展开 `General` 类别，并选择 `File System`。点击 `Next`，然后点击 `Browse`，导航至 `samples/record_sort` 并点击 `OK`。

这将打开导入对话框。选中全部三个文件并点击 `Finish`。这些文件现在会显示在“项目资源管理器”视图中。请注意，没有 `record_sort.c` 文件。这是因为你要自己输入它，以练习使用 `CDT` 编辑器。

点击工具栏左侧 New 图标旁边的向下箭头，并从下拉菜单中选择 `Source File`。将其命名为 `record_sort.c`。一个编辑器窗口将打开，其中包含一个初步的头注释。`record_sort.c` 的内容如图 5.5 所示，但在阅读下一节之前请勿开始输入。

### 内容辅助

`CDT` 编辑器具有多种功能，可以简化你的编码生活。这些功能统称为*内容辅助*（Content Assist）。内容辅助的基本思想是，基于当前上下文、作用域和前缀预测你可能输入的内容，从而减少你需要输入的按键次数。通过输入 `Ctrl + Space` 即可调用内容辅助，当你在 `struct` 或 `class` 名称后输入 `"."`、`"->"` 或 `":"` 时，它也会自动激活。

### 代码模板

*代码模板*是内容辅助的一个组成部分，它提供了常用代码段的起始点。当你输入字母组合后按 `Ctrl + Space` 时，将显示以该字母组合开头的代码模板列表。选择一个模板后，它会自动插入到文件当前光标所在的位置。

试一试：在输入完图 5.5 中的 `#include` 行后，输入 `"ma"` 然后按 `Ctrl + Space`。这将调出 `main()` 函数的模板。你可以在 `Window > Preferences > C/C++ > Editor > Templates` 中编辑模板。内容辅助的其他方面也可以在偏好设置（Preferences）中进行自定义。

```c
/**
 * author Doug Abbott
 *
 * Simple demonstration of building and running a project under
 * Eclipse.
 *
 * Usage:
 *     record_sort <filename> [1 | 2]
 *
 * Sorts records in <filename> either by name (1) or ID (2).
 * Default is name.  Outputs sorted file to stdout.
 */
#include <stdio.h>
#include <stdlib.h>

#include "record_sort.h"

int main (int argc, char **argv)
{
    int size, sort = 1;
    record_t *records;

    if (read_file (argv[1], &size, &records))
    {
        printf ("Couldn't open file %s\n", argv[1]);
        exit (1);
    }
    if (argc > 2)
        sort = atoi (argv[2]);

    switch (sort)
    {
        case 1: sort_name (size, records);
        break;

        case 2: sort_ID (size, records);
        break;

        default:
        printf ("Invalid sort argument\n");
        return_records (size, records);
        exit (2);
    }

    write_sorted (size, records);
    return_records (size, records);
    return 0;
}
```

**图 5.5**

`record_sort.c`.

### 自动闭合

当你输入时，请注意，每当你输入一个开引号（`''`）、括号（`()`）、方括号（`[]`）或尖括号（`<>`）、或大括号（`{}`），编辑器会自动添加对应的闭合字符，并将光标定位在两者之间。在括号内输入所需的内容，然后按 `Enter`。这将把光标定位在闭合字符之后。

但是，如果你将光标移出括号包围的空间，例如为了复制和粘贴一些文本，`Enter` 键将恢复其正常行为，即开始新行。

对于左大括号，右大括号的位置将根据当前选定的编码风格进行调整，并且光标会正确缩进。

最后，请注意，随着你的输入，大纲（Outline）视图中会出现相应的条目，标识头文件、函数以及（如果有的话）全局变量。

### 程序

在继续进行项目的构建和运行之前，让我们仔细看看程序实际上做了什么。`main()` 本身相当简单。它只是一组对声明在 `sort_utils.c` 中执行实际工作的函数的调用。

函数 `read_file()` 读取一个数据文件，假设该文件组织为每行一个记录，其中记录包含文本姓名和数字 ID。它为记录数组分配内存，并为每个姓名字段进行单独分配。

有两个排序函数——一个按姓名字段排序，另一个按 ID 字段排序。这两个都实现了 Shell 排序算法，该算法以其发明者 Donald Shell 命名。Shell 排序通过比较间隔几个位置的元素，相比简单的插入排序提高了性能。

在记录数组排序完成后，`write_sorted()` 将其写入 `stdout`。当然，这可以重定向到文件。

最后一步是在函数 `return_records()` 中释放所有已分配的内存。

该程序几乎没有任何“合理性检查”，如果你愿意，可以自行构建一些。此外，错误检查也非常少。

### 构建项目

一旦你完成并保存了 `record_sort.c` 文件，下一步就是构建项目。在项目内创建或导入的所有文件都自动成为其一部分，并会被构建和链接到最终的可执行文件中。
