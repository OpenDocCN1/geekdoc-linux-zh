

## 列表 28-2B

`recip.p` 程序的 Pascal 代码。

```pascal
{ Compute reciprocals }
program reciprocal(input, output);
var n, recip: integer;
begin
writeln('This program computes reciprocals.');
write('Enter a number: '); 
readln(n);
recip := 1 div n;
writeln('The reciprocal of ', n, ' is ', recip);
end.
```

该程序引入了前一个程序中未涉及的几个特性：

-   `{ Compute reciprocals }`
    写注释的一种替代方式是使用花括号 `{...}` 包围注释。

-   `var n, recip: integer;`
    这是一个**声明**。它指示编译器创建两个变量 (var) 来存储整数，并将它们命名为 `n` 和 `recip`。Pascal 要求在使用所有变量之前必须先声明它们。该行末尾放置一个分号，以将其与后续行分隔开。

-   `write('Enter a number: ');`
    `write` 是一个标准的 Pascal 过程，用于在标准输出上写入数据。与 `writeln` 不同，`write` 在打印完成后不会另起一行。

-   `readln(n);`
    该 `readln` 语句从标准输入获取用户输入，并将其存储在变量 `n` 中。

-   `recip := 1 div n;`
    该行计算倒数。计算机首先将整数 `1` 除以变量 `n` 的内容，然后将结果赋值给变量 `recip`。在 Pascal 中，`div` 用于两个整数的除法。符号对 `:=` 被视为一个运算符，称为*赋值运算符*。它将表达式 `1 div n` 的值赋值给变量 `recip`。

-   `writeln('The reciprocal of ', n, ' is ', recip)`
    这是一个带有四个参数的 `writeln`。它将打印字符串 `"The reciprocal of "`，接着是变量 `n` 的值，字符串 `" is "`，最后是变量 `recip` 的值。

## 28.5 创建并运行 recip.p

1.  **创建源文件。** 使用 *vi* 编辑器创建一个名为 `recip.p` 的文件：

    ```bash
    $ vi recip.p Return
    ```

    按照列表 28-2B 所示准确输入程序，然后写入文件并退出编辑器。

2.  **编译源代码。** 可执行文件的默认名称是 `a.out`。您可以使用 *pc* 的 *-o* 选项指定其他名称。对于可执行文件，让我们使用名称 *recip*（不带 *.p* 后缀）：

    ```bash
    $ pc -o recip recip.p Return
    ```

    这指示 *pc* 编译 `recip.p` 并将可执行代码放入文件 `recip` 中。

3.  **如有必要，纠正任何语法错误并重复步骤 2。**

4.  **运行程序。** 要运行程序，请输入可执行文件的名称：

    ```bash
    $ recip Return
    ```

    您应该会看到一条消息和一个提示符：

    > 本程序计算倒数。
    > 请输入一个数字：

5.  **在提示符后输入一个数字。** 尝试数字 2：

    > 请输入一个数字：2 Return

    程序的响应将是：

    > 2 的倒数是 0
    > $

    这显然是错误的：2 的倒数是 1/2，而不是 0。事实上，只有当输入为 `-1` 或 1 时，`recip.p` 才会给出正确答案。其原因与计算机存储和使用整数的方式有关。要修复此缺陷，您应修改程序，使其使用*实数*类型变量而不是*整数*类型变量。（我们将其作为练习留给读者。）

## 28.6 算术异常与核心转储

`recip.p` 程序如何处理除以零的情况？

1.  **运行程序。**

    ```bash
    $ recip Return
    ```

    程序将打印一条消息和一个提示符：

    > 本程序计算倒数。
    > 请输入一个数字：

2.  **在提示符后输入零。**
    请输入一个数字：0 (Return)
    您应该会收到一条错误消息，内容如下：

    > 算术异常（核心转储）

    发生了什么事？这并不难理解。除以零是一个未定义的操作，导致程序崩溃。

3.  **检查核心文件。** 如果您列出目录中的文件，您应该会看到一个名为 `core` 的文件：
    `$ ls (Return)`
    由于您无法读取*核心*文件，并且它占用了大量空间，因此应该删除它。

4.  **删除核心文件。**
    `$ rm core (Return)`

## 28.7 为 recip.p 设置调试

虽然您不能像读取普通 UNIX 文本文件那样读取核心文件，但您可以使用诸如 `dbx` 之类的调试器检查该文件并确定导致程序崩溃的原因。

-   **使用调试选项编译程序。** 对于大多数编译器，`-g` 选项表示“调试”：
    `$ pc -g recip.p (Return)`
    这会使编译器在编译后的代码中包含额外信息，供 `dbx` 使用。如果您想了解如何使用 `dbx`，请参阅附录 F。

## 28.8 命令摘要

以下每个命令都在 shell 提示符处输入，并以 `(Return)` 结束。

| 命令 | 描述 |
| :--- | :--- |
| `pc file.p` | 编译并链接 `file.p` 中的源代码 |
| `pc -g file.p` | 编译 `file.p`；为调试器设置 |
| `pc -o file file.p` | 编译 `file.p`；将可执行代码放入 `file` |
| `pc file.p -o file` | 同上 |

## 28.9 练习

1.  大多数系统上的 `pc` 编译器接受多个选项。参考 UNIX 手册以确定您的 Pascal 编译器接受的选项。
2.  重写 `recip.p` 以使用 `real` 变量。确保使用实数除法运算符 `/` 而不是整数除法运算符 `div`。
3.  即使您已重写 `recip.p` 以使用 `real` 变量，它可能仍无法正确处理零输入。阅读您的 Pascal 书籍关于 `if-then` 语句的内容，然后重写 `recip.p` 程序，使得当用户输入零时，打印消息“0 的倒数未定义”。
4.  由于数字前有很大的空格，`recip.p` 的输出并不如可能的那样美观。参考您的 Pascal 书籍了解如何格式化输出，然后修改 `recip.p` 以控制输出行的间距。
5.  `time` 实用程序测量执行程序或 shell 脚本所需的时间。您可以使用命令行 `time a.out (Return)` 对 `a.out` 的执行进行计时。使用 `man` 命令了解 `time` 的工作原理。然后在该实用程序上试用您的一个源文件。
6.  编写一个 Pascal 程序 `sroot.p`，以计算用户在键盘上输入的数字的平方根。（参考您的 Pascal 书籍了解如何计算平方根。）

# 附录

# 附录 A：驯服您的终端

*stty*（"set terminal"）命令允许您设置影响终端操作的参数。在本附录中，您将看到如何使用 *stty* 执行以下任务：

-   设置终端以处理小写输入。
-   定义删除键。
-   确保终端正确回显您的输入。

## A.1 纠正仅大写输出

有时系统可能会表现您的终端只能处理大写字母。（如果在登录前不小心按下了 "Caps Lock" 键，可能会出现这种情况。）以下命令将修正该问题：

```bash
$ stty -lcase Return
```

## A.2 定义删除键

大多数用户期望 `Backspace` 键删除命令行中的字符。（其他人更喜欢使用 `Delete` 或 `(Control)-(H)`。）以下命令将 `Backspace` 设置为字符删除键：

```bash
$ stty erase <Backspace> Return
```

以下命令将 `Delete` 设置为字符删除键：

```bash
$ stty erase <Delete> Return
```

要将 `(Control)-(H)` 键组合设置为字符删除键，请使用命令行：

```bash
$ stty erase ^h Return
```

注意，脱字符 (^) 用于表示 Control 键。

## A.3 设置终端回显

当您在键盘上输入字符时，系统应将它们回显到终端屏幕上（除非您正在输入密码）。如果您输入的内容没有出现在屏幕上，您可以使用以下命令开启回显：

```bash
$ stty echo Return
```

另一方面，如果每个字符都被回显两次，您应该关闭回显：

```bash
$ stty -echo Return
```

