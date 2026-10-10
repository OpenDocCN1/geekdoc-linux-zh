
## 手动编译

示例项目的简单性使得手动编译变得非常容易。在项目根目录下执行以下命令，通过单条命令即可生成名为 `appexp` 的应用程序。

```
gcc -o appexp src/main.c src/app.o src/bar.c src/lib.c
```

该命令运行 `GCC` 包装程序，调用预处理器、编译器和链接器将这四个 c 文件转换为可执行文件。单条命令的方法对于这种简单的项目是可以接受的，但对于较大的项目来说将是不切实际的。接下来的命令 set 将编译分解为更复杂的构建过程中常见的增量步骤。

```
gcc -c -o main.o src/main.c
gcc -c -o app.o src/app.c
gcc -c -o bar.o src/bar.c
gcc -c -o lib.o src/lib.c
gcc -o appexpp main.o app.o bar.o lib.o
```

该系列中的前四条命令将 `src` 目录下的 c 文件转换为根目录下的目标文件。最后一条命令调用链接器将生成的四个目标文件组合成一个可执行文件。

## 构建脚本

如果每次需要重新构建应用程序时都要输入上一节描述的任何命令，将非常繁琐。下一个显而易见的步骤是将这些命令放入脚本中，以便通过单条命令执行构建应用程序所需的所有步骤。列表 6.1 显示了为了自动化构建过程可能编写的构建脚本内容。

### 列表 6.1 构建脚本（位于 CD-ROM 的 `./source/ch6/buildit`）

```
#!/bin/sh

# 构建第 6 章示例项目

gcc -c -o main.o src/main.c
gcc -c -o app.o src/app.c
gcc -c -o bar.o src/bar.c
gcc -c -o lib.o src/lib.c
gcc -o appexpp main.o app.o bar.o lib.o
```

该脚本将上一节概述的命令收集到一起。它允许源代码的开发者和用户通过简单的 `./build` 命令行来构建应用程序。此外，它可以进行版本控制并随源代码一起分发，以于那些尝试构建应用程序的人进行理解。

构建脚本的缺点之一是它每次调用时都会重新构建整个项目。对于本章中的小型示例，这不会导致开发周期的显著增加，但随着文件数量的增加，运行整个构建过程将变成沉重的负担。`make` 工具相比 shell 脚本解决方案的一个主要增强是它能够理解项目依赖关系的能力。理解依赖关系允许 `make` 工具仅重新因源文件更改而需要更新的项目部分。

### 简单的 Makefile

`make` 工具使用开发者创建的输入文件来描述要构建的项目。GNU make 使用 `Makefile` 作为其输入文件的默认名称。因此，当输入 `make` 命令调用 `make` 工具时，它会在当前目录下查找名为 `Makefile` 的文件来告诉它如何构建项目。列表 6.2 展示了用于构建示例项目的基础 Makefile。

### 列表 6.2 简单的 Makefile（位于 CD-ROM 的 `./source/ch6/buildit`）

```
appexp: main.o app.o bar.o lib.o
	gcc -o appexp main.o app.o bar.o lib.o

main.o: src/main.c
	gcc -c -o main.o src/main.c

app.o: src/app.c
	gcc -c -o app.o src/app.c

bar.o: src/bar.c
	gcc -c -o bar.o src/bar.c

lib.o: src/lib.c
	gcc -c -o lib.o src/lib.c
```

### 64 GNU/Linux 应用程序编程

```bash
gcc -c -o app.o src/app.c
gcc -o appexp main.o app.o bar.o lib.o
```

`make` 是如何消除对其他命令的需求的？因为 GNU make 理解创建可执行文件过程中的每一个步骤，它通过检查文件的日期来确定 `main.o`、`bar.o` 和 `lib.o` 的依赖树中没有任何内容发生变化，因此这些对象文件不需要重新创建。相反，它会检查 `app.o` 是否发生变化，从而它意识到其中一个依赖项（即 `app.c`）发生了变化，因此它需要重新构建。如果你理解了 Makefile 语法中表示的依赖树，你就理解了 `make` 优于简单构建脚本的威力。Makefile 语法还提供了本节讨论之外的其他功能；本章的其余部分将考虑 GNU make 的一些更有用的功能。

## Makefile 变量

GNU make 提供了对一种变量的支持，这种形式与标准 UNIX Shell 中提供的变量非常相似。这些变量允许将名称与任意长度的文本字符串关联。为变量赋值的 Basic 语法如下：

```makefile
MY_VAR = A text string
```

这会导致创建一个名为 `MY_VAR` 的变量，其值为 `A text string`。在 Makefile 的后续部分，通过使用以下语法 `${var-name}` 获取变量值，其中 `var-name` 被替换为要获取的变量名称。列表 6.3 提供了一个示例 Makefile，用来说明变量在 Makefile 中的基本用法。

### 列表 6.3 简单变量 Makefile（位于光盘 `/source/ch8/Makefile.simvar`）

```makefile
MY_VAR=file1.c file2.c

all:
    echo ${MY_VAR}
```

第 2 行将值 `file1.c file2.c` 赋值给变量 `MY_VAR`。当调用 `make` 程序时，它会尝试构建在第 4 行定义的 `all` 目标。第 5 行的命令被执行，输出如列表 6.4 所示。

### 第 6 章 使用 GNU make 构建软件 65

### 列表 6.4 简单变量 Makefile 输出

```bash
$ make
echo file1.c file2.c
file1.c file2.c
```

第 2 行是调用 `make` 程序。第 3 行是 `make` 程序在运行列表 6.3 第 5 行命令时的输出。注意，在执行到此点时，变量替换已经发生。第 4 行是 `make` 调用的 `echo` 命令的实际输出。

GNU make 允许通过提供将字符串连接到变量现有值的能力，来增量地构建变量值。GNU make 语法使用 `+=` 符号表示连接操作。列表 6.5 展示了在列表 6.3 的简单 Makefile 中，如何在创建 `MY_VAR` 变量值时使用连接操作。

### 列表 6.5 变量连接 Makefile（位于光盘 `/source/ch6/Makefile.varconcat`）

```makefile
MY_VAR=file1.c
MY_VAR+=file2.c

all:
echo ${MY_VAR}
```

针对列表 6.5 中的 Makefile 运行 `make` 应该生成与列表 6.4（即列表 6.3 中的 Makefile）完全相同的输出。

GNU make 提供了广泛的内置功能来操作变量。提供了一些用于通用字符串处理操作的函数，如替换、剥离和分词。Makefile 中变量的一个常见用途是存储和管理涉及的文件名和路径。为了方便这种变量用法，GNU make 提供了专门的函数，可以将变量的内容作为路径或文件名来执行操作。列表 6.6 中的 Makefile 展示了 GNU make 提供的一些函数的使用。列表 6.7 展示了在列表 6.6 的 Makefile 上运行 `make` 程序的预期输出。

### 66 GNU/Linux 应用程序编程

### 列表 6.6 变量操作 Makefile（位于光盘 `../source/ch6/Makefile.varmanipulation`）
