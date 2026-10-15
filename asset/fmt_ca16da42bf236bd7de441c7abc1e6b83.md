
`abs_main.o`: `abs_main.c`

`gcc -c abs_main.c`

第一行建立了 `abs_main.o` 和 `abs_main.c` 之间的依赖关系。如果 `abs_main.c` 比 `abs_main.o` 新，则执行第二行上的命令（重建 `abs_main.o`）。

第三行和第四行，以及第五行和第六行建立了类似的依赖和命令。

使用 Makefile 构建 `abs2` 程序的命令行输入是：

`make -f make_abs abs2`

`-f` 选项指示 `make` 读取 `make_abs` 文件而不是 `makefile`。在执行该命令后，你可以运行 `abs2` 程序。图 10-7 显示了 `make` 命令的输出和 `abs2` 程序的输出。

如果你忘记了自上次运行程序以来是否做过更改，可以使用 `make` 检查源文件的时间戳，并在必要时重建程序。如果程序是新的，`make` 工具不会重新编译，并显示 `make` 文件已更新的消息，如下方的代码所示：

```bash
[@localhost ~]$ make -f make_abs abs2
make: 'abs2' is up to date.
```

# 第 10 节课 A 使用 C 和 C++ 开发 UNIX 应用程序

![](img/b5f7722b7c2983a215c7726aaada19f9_405_0.png)

图 10-7 制作并运行 `abs2` 程序

`make` 工具遵循一组规则，包括默认规则和用户定义的规则。通常，`make` 规则包含：

- 目标（target）：你想要生成的文件名（在上面的示例中，目标是 `abs2`）
- 一个或多个依赖项（dependencies）：目标所依赖的文件
- 一个动作（action）：创建目标的 shell 命令。

现在你已经学习了 Makefile 的结构，可以创建一个简单的多模块 C 项目。

# 要创建一个简单的多模块 C 项目：

1. 使用你选择的编辑器创建文件 `square_func.c`。在文件中输入此代码：

```c
int square(int number)
{
    return (number * number);
}
```

2. 保存文件。

3. 接下来创建文件 `square_main.c`。输入此代码：

```c
#include <stdio.h>
int square(int number)
int main()
{
    int count, sq;
    for (count = 1; count < 11; count++)
{}
```

![](img/b5f7722b7c2983a215c7726aaada19f9_405_1.png)

# 介绍 C 编程 385

```c
sq = square(count);
printf("The square of %d is %d\n", count, sq);
}
```

4. 保存文件。

5. 接下来，创建一个名为 `make_square` 的 Makefile。输入以下文本：

> 在许多 UNIX 版本的 `make` 命令中（例如后期的 Red Hat Linux 版本），你必须在调用 `gcc` 编译器的每个命令行之前放置一个制表符。如果你不这样做，命令将返回错误。

```make
square_func.o: square_func.c
(按下 Tab)gcc -c square_func.c
square_main.o: -c square_main.c
(按下 Tab)gcc -c square_main.c
square: square_func.o square_main.o
(按下 Tab)gcc square_func.o square_main.o -o square
```

6. 保存文件并退出编辑器。

7. 输入 `make -f make_square square` 构建程序。按回车（如果你有错误，将错误的模块加载到编辑器中修正错误）。

8. 运行程序。你的屏幕应该像图 10-8。

![](img/b5f7722b7c2983a215c7726aaada19f9_406_0.png)

图 10-8 制作并运行 `abs2` 程序

如果你忘记了上次运行程序以来是否做过更改，可以使用 `make` 检查源文件的时间戳，并在必要时重建程序。如果程序是新的，`make` 工具不会重新编译，并显示 `make` 文件已更新。

# 调试你的程序

新程序员的典型错误包括：

- 忘记在语句结束加分号。
- 在 `scanf` 使用基本类型时忘记使用 `&` 运算符。
- 混淆 `printf` 和 `scanf` 中不同的格式符。
- 函数调用和参数的语法错误。

现在你已经理解了 `scanf` 的基础，可以输入数据了。

# 创建一个接受输入的程序

`scanf` 函数使用带有格式符的控制字符串，类似于 `printf`。这是一个示例：

```c
scanf("%d", &age);
```

`%d` 格式符的作用与 `printf` 一样。在这里它指示 `scanf()` 将输入解释为十进制整数。`&age` 运算符告诉 `scanf` 将输入存储在变量中。`&` 是地址运算符。当与变量配合使用时，它返回变量所在的内存地址。示例显示了如何使用 `scanf` 输入字符串：

```c
scanf("%s", city);
```

注意这个示例没有使用 `&` 运算符。每当你使用数组名称时，它都会解析为第一个元素的地址。在数组名称上使用 `&` 运算符将是错误的。

# 388 第10章 节课 A 在C和C++中开发 UNIX 应用程序

虽然 `scanf` 语句很少对程序的用户友好性有所贡献，但它接受多个输入。以下是一个示例：

```
scanf("%d %f %d", &x, &y, &z);
```

上述语句接受变量 `x`、`y` 和 `z` 中的值，它们分别是 `int`、`float` 和 `int`。在输入值时，用户必须使用空白字符将这三个值隔开。空白字符包括空格、制表符和换行符。

现在你来编写一个 C 程序来从键盘接受输入。

# 要使用 C 语言接受键盘输入：

1. 使用你选择的编辑器创建一个名为 `keyboard.c` 的文件，并输入以下行代码：

```
====================================================
程序名称: keyboard.c
目的: 使用键盘输入数据
====================================================
#include <stdio.h> /* 标准输入输出库 *
*/
int main() {
    char string[50]; /* 字符串字段 */
    float money; /* 浮点数字段 */
    int weight; /* 整数字段 */
    printf("\nenter your First Name: ");
    scanf("%s", string);
    printf("\nenter your Desired Monthly Income: ");
    scanf("%f", &money);
    printf("\nenter your friend's weight: ");
    scanf("%d", &weight);
    printf("\n\n Recap:\n");
    printf("\nI am %s and I wish to have $%.2f per month,", string, money);
    printf("\nI never would have guessed you weigh %d", weight);
    printf("\n\n");
}
n
```

2. 保存文件并退出编辑器。

3. 输入 `gcc keyboard.c -o keyboard` 并按回车键编译程序。

4. 输入 `./keyboard` 并按回车键执行程序。你的屏幕现在看起来应该类似于图 10-9。注意，你的屏幕显示会根据你的输入而不同。

![](img/b5f7722b7c2983a215c7726aaada19f9_409_0.png)

# 编码与解码程序 389

![](img/b5f7722b7c2983a215c7726aaada19f9_410_0.png)

图 10-9 `keyboard` 程序的输出

既然你已经创建了执行键盘和文件 IO 的 C 程序，你已经准备好编写安全演示程序了。

# 编码与解码程序

如果文件包含敏感信息，你可能希望对其加密，以便其他人无法读取其内容。当文件被加密时，其内容会被编码或修改，使得原始内容无法区分。使用一个公式进行加密，以便互补的解密算法可以将文件恢复到原始内容。

你为 Dominion Consulting 的编程人员编写的程序设计简单。它打开一个文件，从文件中读取一个字符，将字符值加 10，然后将字符写入第二个文件。此过程不断重复，直到文件中的所有字符都被读取、修改并写入第二个文件。第二个文件是第一个文件的编码版本。
