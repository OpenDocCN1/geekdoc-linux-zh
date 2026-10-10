
## F.2 在 DBX 内部运行程序

在 dbx 内部运行一个程序似乎并没有太大用处——毕竟，直接运行程序而不先调用调试器来完成任务要容易得多。dbx 允许你做的是逐行执行该程序，并在变量和表达式的值发生变化时检查它们。

### F.3 列出源代码

list 命令会向你展示源代码。试一试：

```
(dbx) list 1, 15 Return
```

这告诉 dbx 你希望查看从第 1 行到第 15 行的源代码。dbx 会显示该文件，并在显示时为行号编号。（实际上这些行号并没有被添加到源文件中。）

### F.4 设置断点

断点是程序中你希望执行暂停的位置。可以使用 stop 命令来设置断点。让我们在 第 8 行设置一个断点：

```
(dbx) stop at 8 Return
```

dbx 会告诉你断点已设置：

```
stop at "recip.c":8
```

现在使用 run 命令开始执行：

```
(dbx) run Return
```

程序将运行直到到达第 8 行，然后在此停止。dbx 随后将显示第 8 行：

```
Running: a.out
stopped in main at line 8 in file "recip.c"
8 printf("This program calculates reciprocals.\n");
(dbx)
```

### F.5 单步执行程序

此时，你可以使用 cont（"continue"）命令恢复程序的执行，但更富教学意义的做法是逐行单步执行程序。step 命令允许你这样做：

```
(dbx) step Return
```

你应该看到类似以下内容：

```
This program computes reciprocals.
stopped in main at line 9 in file "recip.c"
9 printf("Enter a number:");
(dbx)
```

请注意，你首先看到的是由上一条语句打印出的那行内容。再次单步执行，但这次单步执行两行：

```
(dbx) step 2 Return
```

由第 9 行产生的提示符现在出现了：

```
Enter a number:
```

输入 1 并按下 Return 键。

```
Enter a number: 1 Return
```

程序像往常一样读取该数字。然后它继续执行程序的下一行并停止：

```
stopped in main at line 11 in file "recip.c"
11 recip = 1/n;
(dbx)
```

### F.6 打印表达式

print 命令允许你检查变量的值。例如，要查看 n 的值，你可以输入：

```
(dbx) print n Return
```

dbx 将响应 n 的当前值：

```
n = 1
(dbx)
```

再次单步执行：

```
(dbx) step
stopped in main at line 12 in file "recip.c"
12 printf("The reciprocal of %d is %d.\n", n, recip);
```

使用 print 检查 n 和 recip 两者的值：

```
(dbx) print n, recip Return
n = 1
recip = 1
(dbx)
```

使用 cont 命令继续程序的执行；这将运行完剩余的行而不停顿：

```
(dbx) cont Return
```

你应该看到类似以下内容：

```
The reciprocal of 1 is 1.
execution completed, exit code is 1
(dbx)
```

程序现在已经运行完毕，但你仍然在 dbx 内部。使用 quit 命令退出 dbx：

```
(dbx) quit Return
```

### F.7 跟踪变量和函数

trace 命令会在变量值发生变化时打印它们的值，并显示程序中函数的调用。启动 dbx：

```
$ dbx a.out
```

dbx 提示符告诉你你在 dbx 中：

```
Reading symbolic information...
(dbx)
```

我们想要跟踪 main() 函数中 n 的值：

```
(dbx) trace n in main
```

dbx 将确认跟踪已设置：

```
(2) trace n
(dbx)
```

我们还希望跟踪 recip 的值：

```
(dbx) trace recip in main
(3) trace recip
(dbx)
```

让我们也跟踪对 main() 函数的调用：

```
(dbx) trace main
(4) trace main
```

现在运行程序：

```
(dbx) run Return
```

dbx 将运行程序，显示变量的值并显示对函数的调用：

```
Running: a.out
(process id 3558)
main called from function _start
initially (at line "recip.c":8): recip = -26843620
initially (at line "recip.c":8): n = 0
This program computes reciprocals.
Enter a number:
```

在提示符处输入数字 1，并注意变量值的变化是如何被打印出来的：

```
Enter a number: 1 Return
after line "recip.c":10: n = 1
after line "recip.c":11: recip = 1
The reciprocal of 1 is 1.
main returns 1
execution completed, exit code is 1
```

输入 rerun 命令：

```
(dbx) rerun Return
```

dbx 将再次运行程序：

```
Running: a.out
(process id 3565)
main called from function _start
initially (at line "recip.c":8): recip = -26843620
initially (at line "recip.c":8): n = 0
This program computes reciprocals.
Enter a number:
Enter zero to cause an error:
```

```
Enter a number: 0 Return
terminating signal 8 SIGFPE
```

退出 dbx：

```
(dbx) quit Return
```

使用 ls 命令查看是否创建了一个 core 文件：

```
$ ls Return
```

### F.8 使用 where

你无法直接读取 core 文件，但 dbx 可以。具体来说，dbx 中的 where 命令允许你查明错误发生在程序的哪里。针对 a.out 和 core 文件启动 dbx：

```
$ dbx a.out core Return
```

你可能会看到在 dbx 提示符出现之前有几次警告信息：

```
Reading symbolic information...
core header file read successfully.
Reading symbolic information...
Reading symbolic information...
Reading symbolic information...
program terminated by signal FPE (integer divide by zero)
Current function is main
  11        recip = 1/n;
(dbx)
```

这告诉你已经知道的事实，即 core 文件是由除零错误生成的。它还表明这发生在 main() 函数的第 11 行。某些版本的 dbx 要求你使用 where 命令来确定错误发生的位置：

```
(dbx) where Return
[1] .div(0x1, 0x0, 0x4, ...
[2] main(), line 11 in "recip.c"
(dbx)
```

dbx 提示符前的最后一行告诉你，错误发生在 main() 函数的第 11 行。

### F.9 在 dbx 中运行 Shell 命令

sh 命令允许你在仍然位于 dbx 内部时运行 shell 命令。使用此命令配合 rm 来删除 core 文件：

```
(dbx) sh rm core Return
```

现在使用 sh 和 ls 检查 core 文件是否确实已被移除：

```
(dbx) sh ls Return
```

## G 附录：使用 MAKE 维护程序

UNIX 的 **make** 程序旨在通过跟踪源文件中所做的任何更改来管理大型多文件项目。它允许你修改并重编译一个源文件，而无需重编译整个程序。

### G.1 makefile

**make** 程序会在名为 **makefile** 或 **Makefile** 的文件中查找其指令。对于 **Trip** 目录中的程序，创建一个名为 **makefile** 的文件，并输入清单 G–1 中所示的行。

```
# Makefile for the Trip program

trip: main.o chicago.o indiana.o indy.o
	cc -o trip main.o chicago.o indiana.o indy.o

main.o: main.c
	cc -c main.c

chicago.o: chicago.c
	cc -c chicago.c

indiana.o: indiana.c
	cc -c indiana.c

indy.o: indy.c
	cc -c indy.c

clean:
	rm *.o
```

清单 G–1
Trip 程序的 Makefile。

让我们考虑一下这个文件的一些有趣特性：

-   `# Makefile for the Trip program`
    这是一行*注释*。*make* 会忽略井号（#）之后的所有内容。

-   `trip: main.o chicago.o indiana.o indy.o`
    这被称为一条*依赖行*。它表明文件 **trip** 依赖于目标文件 **main.o**、**chicago.o**、**indiana.o** 和 **indy.o**。注意，依赖行必须从第一列开始。

-   `(TAB)cc -o trip main.o chicago.o indiana.o indy.o`
    这是一条*动作行*。它跟在依赖行之后，显示了文件 **trip** 如何由文件 **main.o**、**chicago.o**、**indiana.o** 和 **indy.o** 创建。在这种情况下，**cc** 链接目标文件并将可执行文件放入 **trip**。动作行必须以制表符（Tab）开头。

-   `chicago.o: chicago.c`
    这是另一条依赖行，表明 **chicago.o** 依赖于源文件 **chicago.c**。

-   `(TAB)cc -c chicago.c`
    这是一条*动作行*，表明 **chicago.o** 是通过使用 **cc** 的 **-c** 选项编译 **chicago.c** 而生成的。

-   `clean:`
    这条依赖行表明“clean”不依赖于任何文件。这是一个*空依赖*的例子。在这种情况下，“clean”不是一个文件的名称，而是一个命令，你可以通过键入以下内容来运行它：
    ```
    $ make clean Return
    ```
    然后 *make* 会浏览 *makefile*，找到空依赖“clean”，并执行下一动作行上的命令。

-   `(TAB)rm *.o`
    这条动作行将删除任何以 .o 结尾的文件——换句话说，就是目标文件。这是 *make* 在你键入以下内容时将执行的操作：
    ```
    $ make clean Return
    ```

