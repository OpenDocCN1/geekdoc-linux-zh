
```c
char my_string[] = "hello there";

my_print (my_string);
my_print2 (my_string);
}

my_print (char *string)
{
    printf ("The string is %s\n", string);
}

my_print2 (char *string)
{
    char *string2;
    int size, size2, i;

    size = strlen (string);
    size2 = size - 1;
    string2 = (char *) malloc (size + 1);
    for (i = 0; i < size; i++)
        string2[size2 - i] = string[i];
    string2[size] = '\0';
    printf ("The string printed backward is %s\n", string2);
}
```

## 其他 C 语言编程工具

Slackware Linux 发行版包含许多尚未介绍的 C 语言开发工具。本节将描述其中许多额外工具及其典型用法。

### xxgdb

xxgdb 是基于 X 窗口系统的 gdb 图形用户界面。gdb 命令行版本中存在的所有功能在 xxgdb 中也都有提供。xxgdb 允许你通过按下按钮而不是输入命令来执行许多最常用的 gdb 命令。它还图形化地表示断点设置的位置。

通过在 Xterm 窗口中输入以下内容来启动 xxgdb。

```
xxgdb
```

启动 xxgdb 时，可以指定 gdb 可用的任何命令行选项。xxgdb 还有一些自己的命令行选项。这些选项在表 26.2 中有说明。

**表 26.2. xgdb 的命令行选项。**

| 选项 | 描述 |
|---|---|
| db_name | 指定要使用的调试器名称。默认值为 `gdb`。 |
| db_prompt | 指定调试器提示符。默认值为 `gdb`。 |
| gdbinit | 指定初始 `gdb` 命令文件的文件名。默认值为 `.gdbinit`。 |
| nx | 告诉 `xgdb` 不执行 `.gdbinit` 文件。 |
| bigicon | 使用较大的图标大小作为 `xgdb` 图标。 |

当启动 xgdb 时，屏幕上会打开一个窗口。此窗口如图 26.1 所示。

![](img/e8e6b47ac20475e23d48b4c476f5d891_512_0.png)

xgdb 主窗口包含一条消息，类似于启动 gdb 命令行版本时屏幕上显示的内容。在 xgdb 主窗口的底部附近有四个按钮。Source Listing（源列表）、Command Buttons（命令按钮）和 Display Window（显示窗口）按钮在激活时各自会弹出一个附加窗口。Quit（退出）按钮终止 xgdb 程序。

Source Listing 按钮会弹出一个显示正在调试的程序源代码的窗口。此窗口如图 26.2 所示。

![](img/e8e6b47ac20475e23d48b4c476f5d891_512_1.png)

Command Buttons 按钮会弹出一个包含另外 26 个按钮的窗口。这些按钮各自执行一个 gdb 命令。gdb 命令按钮窗口如图 26.3 所示。

![](img/e8e6b47ac20475e23d48b4c476f5d891_513_0.png)

Display Window 按钮会弹出一个用于显示任何 display 命令结果的窗口。你可以通过从源列表中选择一个变量或表达式，然后单击命令按钮窗口中的 Display 按钮，来告诉 xxgdb 显示哪个变量或表达式。显示窗口如图 26.4 所示。

![](img/e8e6b47ac20475e23d48b4c476f5d891_513_1.png)

有关使用 xxgdb 的更多信息，请参考 **xxgdb** 手册页和 **gdb** 手册页。

### calls

calls 是一个程序，未包含在随本书提供的 Linux CD-ROM 中，但你可以在 sunsite FTP 站点的 `/pub/Linux/devel/lang/c/calls.tar.z` 目录下获取副本。一些较旧的 Linux CD-ROM 发行版包含此文件。由于它是一个有用的工具，我们将在这里介绍它。如果你认为它对你有用，请从 FTP 或 BBS 站点或另一个 CD-ROM 获取副本。calls 在命令行传递给它的文件上运行 GCC 预处理器，并显示这些文件中函数的函数调用树。

**提示**

要在系统上安装 calls，请以 root 身份登录并执行以下步骤：

1. 解压并解包该文件。
2. cd 到解包命令创建的 calls 子目录。
3. 将名为 calls 的文件移动到 /usr/bin 目录。
4. 将名为 calls.1 的文件移动到 /usr/man/man1 目录。
5. 删除 /tmp/calls 目录。

这将在系统上安装 calls 程序和手册页。

当 calls 打印调用跟踪时，它会在函数名称后的括号中包含找到该函数的文件名。

```
main [test.c]
```

如果函数不在传递给 calls 的文件中，它不知道该函数位于何处，因此只打印函数名称。

```
printf
```

calls 还在其输出中注明递归函数和静态函数。递归函数以以下方式表示：

```
fact <<< recursive in factorial.c >>>
```

静态函数的表示如下：

```
total [static in calculate.c]
```

作为示例，假设使用以下程序作为输入执行 calls：

```c
#include <stdio.h>
main ()
{
    char my_string[] = "hello there";
    my_print (my_string);
    my_print2(my_string);
}

my_print (char *string)
{
    printf ("The string is %s\n", string);
}

my_print2 (char *string)
{
    char *string2;
    int size, size2, i;

    size = strlen (string);
    size2 = size - 1;
    string2 = (char *) malloc (size + 1);
    for (i = 0; i < size; i++)
        string2[size2 - i] = string[i];
    string2[size] = '\0';
    printf ("The string printed backward is %s\n", string2);
}
```

这会产生以下输出：

![](img/e8e6b47ac20475e23d48b4c476f5d891_515_0.png)

calls 识别许多命令行选项，使你能够指定输出的外观以及显示哪些函数调用。有关这些命令行选项的更多信息，请参考 calls 手册页或在命令行输入 `calls -h`。

### cproto

cproto 是另一个未包含在此 Linux CD-ROM 中但可从 FTP 和 BBS 站点轻松获取的程序。cproto 读取 C 源文件并自动为所有函数生成函数原型。使用 cproto 可以省去为程序中编写的所有函数输入函数定义的工作。

**提示**

要在系统上安装 cproto，请以 root 身份登录并执行以下步骤：

1. 解压并解包该文件。
2. cd 到解包命令结果创建的 cproto 子目录。
3. 将名为 cproto 的文件移动到 /usr/bin 目录。
4. 将名为 cproto.1 的文件移动到 /usr/man/man1 目录。
5. 删除 /tmp/cproto 目录。

这将在系统上安装 cproto 程序和手册页。

通过 cproto 程序运行以下代码：

```c
#include <stdio.h>

main ()
{
    char my_string[] = "hello there";
    my_print (my_string);
    my_print2(my_string);
}

my_print (char *string)
{
    printf ("The string is %s\n", string);
}

my_print2 (char *string)
{
    char *string2;
    int size, size2, i;

    size = strlen (string);
    size2 = size - 1;
    string2 = (char *) malloc (size + 1);
    for (i = 0; i < size; i++)
        string2[size2 - i] = string[i];
    string2[size] = '\0';
    printf ("The string printed backward is %s\n", string2);
}
```

以下输出显示为：

```c
/* test.c */
int main(void);
int my_print(char *string);
int my_print2(char *string);
```

此输出可以重定向到包含文件，并用于定义所有函数的原型。

### indent

indent 工具是另一个随 Linux 提供的编程工具。此程序以最简单的形式重新格式化或美化打印你的 C 代码，使其具有一致的缩进，并且所有开始和结束括号都具有一致的表示。有许多选项可以指定你希望 indent 如何格式化你的代码。有关这些选项的信息，请参考 indent 手册页或在命令行输入 `indent -h`。

以下示例显示了 indent 程序的默认输出。

运行 indent 前的 C 代码：

```c
#include <stdio.h>

main() {
    char my_string[] = "hello there";
    my_print(my_string);
    my_print2(my_string); }

my_print (char *string)
{
    printf ("The string is %s\n", string);
}

my_print2         (char *string) {
    char *string2;
    int size, size2, i;

    size = strlen (string);
    size2 = size - 1;
    string2 = (char *) malloc (size + 1);
    for (i = 0; i < size; i++)
        string2[size2 - i] = string[i];
    string2[size] = '\0';
    printf ("The string printed backward is %s\n", string2);
}
```

运行 indent 后的 C 代码：

```c
#include <stdio.h>

main()
{
    char my_string[] = "hello there";
    my_print (my_string);
    my_print2(my_string);
}

my_print (char *string)
{
    printf ("The string is %s\n", string);
}

my_print2 (char *string)
{
    char *string2;
    int size, size2, i;

    size = strlen (string);
    size2 = size - 1;
    string2 = (char *) malloc (size + 1);
    for (i = 0; i < size; i++)
        string2[size2 - i] = string[i];
    string2[size] = '\0';
    printf ("The string printed backward is %s\n", string2);
}
```

