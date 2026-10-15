
a.out。下面的会话说明了这两种选项。请注意，对搜索路径的更改仅对当前会话有效；要永久更改搜索路径，需要在 ~/.login 或 ~/.cshrc 文件中更改 path 变量的值（详见第 2 章）。

```
% a.out
a.out: Command not found.
% ./a.out
UNIX Rules the Networking World!
% set path = ($path ~)
% a.out
UNIX Rules the Networking World!
%
```

在 Bash 下，搜索路径可使用 PATH=$PATH:. 命令进行更改。要永久更改，需要在 ~/.profile 或 ~/.bash_profile 文件中更改 PATH 变量的值。

## 17.5.3.1 处理多个源文件

你可以使用 gcc 命令在单条命令行中编译和链接多个 C 源文件并创建可执行文件。例如，你可以使用以下命令行为 C 源文件 driver.c、stack.c 和 misc.c 创建名为 polish 的可执行文件。

```
% gcc driver.c stack.c misc.c -o polish
%
```

如果三个源文件之一被修改，你需要重新输入整条命令行，这会产生两个问题。首先，三个文件都会被编译成各自的目标模块，尽管只有其中一个需要重新编译。这会导致编译时间变长，特别是文件较大时。其次，当处理三个文件时，重新输入整行可能不是大问题，但当文件数量多得多时，你肯定不会喜欢这样做。为避免这些问题，你应该为所有源文件创建目标模块，然后只重新编译已更新的模块。所有目标模块随后被链接在一起以创建单个可执行文件。

你可以使用带 -c 选项的 gcc 命令为 C 源文件创建目标模块。当使用 -c 选项编译程序时，编译器会在当前目录中留下目标文件。目标文件的名称为源文件名并带 .o 扩展名。你可以使用另一条 gcc 命令链接多个目标文件。在下面的会话中，我们分别编译三个源模块——driver.c、stack.c 和 misc.c——以创建它们的目标文件，然后使用另一条 gcc 命令将它们链接并创建单个可执行文件 polish。

```
% gcc -c driver.c
% gcc -c stack.c
% gcc -c misc.c
% gcc misc.o stack.o driver.o -o polish
% polish
[output of the program]
%
```

你也可以使用 -c 选项同时编译多个文件。在下面的第一条命令行中，我们使用一条命令编译全部三个源文件以生成目标文件。编译器在编译时会显示文件名称。命令行中列出文件的顺序并不重要。第二条命令行链接三个目标文件并生成一个可执行文件 polish。

```
% gcc -c driver.c stack.c misc.c
% gcc misc.o stack.o driver.o -o polish
%
```

现在如果更新了其中一个源文件，你只需使用 gcc -c 命令生成该源文件对应的目标文件。然后使用第二条 gcc 命令行再次链接所有目标文件以生成可执行文件。

## 17.5.3.2 链接库

UNIX 系统上的 C 编译器在编译时会自动为你的程序链接适当的库。然而，有时你必须显式地告诉编译器链接所需的库。你可以通过使用带 -l 选项的 gcc 命令来实现，其后紧跟库名称中在字符串 lib 之后且在扩展名之前的字母。大多数库位于 /lib 目录中。你需要为每个需要链接的库使用单独的 -l 选项。在下面的会话中，我们将数学库 (/lib/libm.a) 链接到 power.c 文件中程序的目标代码。我们使用第一条 gcc 命令行来显示如果未链接数学库时编译器产生的错误消息。该消息说符号 pow 在 power.o 文件中未找到，而该文件正是使用它的地方。数学库的名称为 libm.a，因此我们在 -l 选项后使用字母 m，该字母位于字符串 lib 之后并在扩展名之前。

```
% cat power.c
#include <stdio.h>
#include <math.h>

int main()
{
    float x,y;
    printf ("The program takes x and y from stdin and displays x^y.\n");
    printf ("Enter integer x: ");
    scanf ("%f", &x);
    printf ("Enter integer y: ");
```

