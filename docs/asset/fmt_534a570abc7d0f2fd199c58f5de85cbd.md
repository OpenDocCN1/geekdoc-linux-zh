
```
/*
 * 作者 Doug Abbott
 *
 * 在 Eclipse 下构建和运行项目的简单演示。
 *
 * 用法：
 *   record_sort <filename> [1 |2]
 *
 * 按名称 (1) 或 ID (2) 对 <filename> 中的记录排序。
 * 默认按名称排序。输出到 stdout。
 */

#include <stdio.h>
#include <stdlib.h>

#include "record_sort.h"

int main (int argc, char **argv)
{
    int size, sort = 1;
    record_t *records;

    if (read_file(argv[1], &size, &records))
    {
        printf("Couldn't open file %s\n", argv[1]);
        exit(1);
    }
    if (argc > 2)
        sort = atoi(argv[2]);

    switch (sort)
    {
        case 1: sort_name (size, records);
            break;
        case 2: sort_ID (size, records);
            break;
        default:
            printf("*Invalid sort argument\n");
            return_records (size, records);
            exit(2);
    }
    write_sorted (size, records);
    return_records (size, records);
    return 0;
}
```

图 6.4

`record_sort.c`。

## 程序

在继续构建和运行项目之前，让我们仔细看看它实际上做了什么。`main()` 本身非常直观。它只是对在 `sort_utils.c` 中声明的函数的调用，这些函数执行实际工作。

## Eclipse 集成开发环境

`read_file()` 函数读取数据文件并将其组织为每行一条记录，其中每个记录包含一个文本名称和一个数字 ID。它为记录数组分配内存，并为每个名称字段单独分配内存。

## 构建项目

一旦你编译并保存了 `record_sort.c` 文件，下一步就是构建项目。在项目中创建或导入的所有文件都会自动成为项目的一部分，并被构建和链接到最终的可执行文件中。

在“项目资源管理器”`Project Explorer` 视图中，选择顶层的 `record_sort` 条目。然后执行 `Project>Build Project`，或者右键点击 `BuildConfigurations>Build>All`。在前一种情况下，将构建活动配置 `Active Configuration`。这是 `Debug` 配置的默认设置。可以通过执行 `Project>BuildConfigurations>SetActive` 来更改活动配置。

在后一种情况下，将构建 `Debug` 和 `Release` 配置。无论何种情况，“项目资源管理器”视图中的 `record_sort` 下都会出现一个或两个新条目。这些条目代表 `Debug/` 和 `Release/` 子目录，它们持有对应构建配置的对象文件和可执行文件。每个目录还包含一个 `Makefile` 和 Eclipse 特有的文件。

最初，构建将失败，因为 `sort_utils.c` 中已经包含了一些编译时错误和警告。打开“问题”`Problems` 视图，展开“错误”`Errors` 条目，右键点击显示“`record_t` has no member named ‘`Id`’”的项。选择“Go To”打开 `sort_utils.c`，并高亮显示错误的行。修正方法应该是显而易见的。

Eclipse CDT 以不同的方式识别构建问题。在“项目资源管理器”视图中，任何带有问题的项目和源文件都会标记一个红色的 X 表示错误，或者一个带有“!”的黄色盾牌图标表示警告。当在编辑器 `Editor` 中打开带有错误或警告的源文件时，标签页会显示相同的符号。“大纲”`Outline` 视图随后使用相同的图标来显示文件中的哪些函数存在错误或警告。

# 第 6 章

编辑器窗口使用相同的图标来识别发生错误或警告的行。你可以滚动源文件，在显示警告或错误图标的行上，“问题”窗口将跳转到相应的条目。如果你将光标悬停在标识为错误或警告的行上，就会弹出相应的错误消息。

修正问题并再次构建项目。顺便提一下，Eclipse 不会在构建前自动保存修改过的。你必须手动保存。该行为可以在“首选项”`Preferences` 中更改。保存 `sort_utils.c` 并再次运行构建。这次应该会成功，你将在 `Debug` 树中上方看到一个可执行文件。

在进行调试之前，你可能想在编辑器中开启行号显示，因为我们在操作过程中会引用行号。在编辑器中，右键点击左侧的垂直条，它被称为“标记器栏”`marker bar`。选项之一是“Show Line Numbers”。点击它。这是一个全局按钮。它适用于编辑器中当前打开的任何文件以及此后打开的任何文件。

## 使用 CDT 进行调试

CDT 与 GDB 集成得非常完美。像大多数工具一样，GDB 本身是面向命令行的。Eclipse 为原生接口提供了一个图形化封装器，这样你就不需要记住所有命令了。

在开始调试之前，我们必须创建一个 `debug launch configuration`。执行 `Run>Debug Configurations...`。选择 `C/C++ Application` 并点击左上角的 `New` 按钮。这将弹出如图 6.5 所示的调试配置对话框。所有内容都已填充。我们只需要添加一项。选择“Arguments”选项卡，并在“Program arguments”中输入“datfile”：`datafile` 是程序用于排序的数据记录样本。它与 `sort_utils.c` 和 `record_sort.h` 一起被导入到项目中。

点击 `Apply`，然后点击 `Debug`。系统会询问你是否要打开调试视图 `Debug perspective`。选择是。

图 6.6 显示了初始的调试视图。底部是“控制台”`Console` 窗口，在此进行终端 I/O。编辑器窗口显示 `record_sort.c`，并高亮了 `main()` 的第一行。右侧的“大纲”`Outline` 标签页列出了 `record_sort.c` 包含的所有头文件以及文件中声明的所有全局和外部符号，包括变量、常量和函数。

# Eclipse 集成开发环境 93

![](img/55fba0370caa0078213ac3714cffd0ec_88_0.png)

图 6.5

调试配置对话框。

右上角是一组标签页，提供了一系列调试信息，包括局部变量、断点和寄存器。初始时，所有局部变量都有随机值，因为它们被分配在栈上。在左上方 Debug 标签页正下方是一组执行图标。点击“Step Over”图标。编辑器窗口中的高亮移动到下一行，“视图”中的 `sort` 显示了其初始值 1。该值被黄色高亮显示，是因为它自上次调试器挂起以来发生了变化。你也可以通过简单地将光标悬停在任何变量上来查看其当前值。试一下。

现在，点击 Debug 视图工具栏中的“Resume”图标让程序运行。嗯，我们得到的结果并不完全符合预期 `datafile` 有两条记录，但只有一条记录输出到“控制台”视图。这是因为程序中内置了一些运行时错误，以便提供一些使用调试器的练习。

# 94 第 6 章

![](img/55fba0370caa0078213ac3714cffd0ec_89_0.png)

图 6.6

调试视图。

## 调试视图

在调试视图中，右键点击顶层项目并选择“Relaunch”以开始调试。如图 6.7 所示，调试视图以分级形式显示程序状态。层次结构的顶部是启动实例，即启动配置。然后是调试器实例。调试器下方是调试器控制的程序。对于 `record_sort` 只有一个线程。最后，在底层是线程的栈帧，通过函数名、源代码行号和程序计数器标识。目前，`main()` 的栈帧位于 `record_sort.c` 的第 22 行。

调试视图的工具栏有许多管理执行的按钮。将光标悬停在上面查看标签。

点击“Step Over”，然后点击“Step Into”进入 `read_file()` 函数。注意调试视图中出现了第二个栈帧，并且 `sort_utils.c` 在编辑器中打开。

# Eclipse 集成开发环境 95

![](img/55fba0370caa0078213ac3714cffd0ec_90_0.png)

图 6.7

调试视图。

此时我们应该仔细查看工作区右上角的四个标签视图。

## 变量视图
