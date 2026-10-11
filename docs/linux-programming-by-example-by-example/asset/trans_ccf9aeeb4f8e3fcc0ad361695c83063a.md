

当你针对静态库进行链接时，生成的二进制文件比使用共享库时要大得多。那么，为什么要使用静态库呢？一个常见的原因是保证用户能够运行你的程序——在共享库的情况下，你的程序运行所需的代码是在运行时动态链接的，而不是在编译时静态链接的。如果你的程序所需的共享库没有安装在用户的系统上，她将遇到错误，无法运行你的程序。

Netscape 浏览器就是这个问题一个完美的例子。Netscape 严重依赖于 Motif，这是一种昂贵的 X 编程语言工具包。大多数 Linux 用户无法负担在系统上安装 Motif，因为它花费太多钱，所以 Netscape 实际上在你的系统上安装了浏览器的两个版本；一个是针对共享库链接的，`netscape-dynMotif`，另一个是静态链接的，`netscape-statMotif`。`netscape` 可执行文件本身实际上是一个 shell 脚本，它确定你是否安装了 Motif 共享库，并必要的话启动其中一个二进制文件。

## 示例

![](img/be588b36b489136ce784030a08a1d3d4_47_0.png)

### 示例

1. 这个示例创建一个静态库，`libmsg.a`。执行此操作所需的命令是

```
$ gcc -c msg.c -o libmsg.o
$ ar rcs libmsg.a libmsg.o
```

回想本章前文，`-c` 告诉 `gcc` 创建一个名为对象文件，在本例中为 `libmsg.o`。第二行使用 `ar` 命令从对象模块 `libmsg.o` 创建名为 `libmsg.a` 的静态库。下一个示例使用此库。

- 要了解有关 `ar` 命令的更多信息，请参见第 299 页的“ar 命令”。

![](img/be588b36b489136ce784030a08a1d3d4_47_1.png)

### 示例

2. 现在你有一个库可以针对其进行链接。你需要告诉 `gcc` 在哪里找到包含文件（使用 `-I`），在哪里找到库（使用 `-L`），以及库的名称（使用 `-l`），如下所示：

```
$ gcc showit.c -o newhello-lib -I. -L. -lmsg
```

之前的示例通过一起编译 `showit.c` 和 `msg.c` 创建了 `newhello`。这一次，我们通过针对静态库 `libmsg.a` 进行链接来创建 `newhello-lib`。该示例通过链接位于当前工作目录（`-L.`）中的 `libmsg.a`（`-lmsg`）创建了一个名为 `newhello-lib` 的二进制文件（选择此名称是为了将其与其他示例区分开）。`.` 指的是当前目录。此程序的输出如下所列：

![](img/be588b36b489136ce784030a08a1d3d4_48_0.png)

**输出**

```
$ ./newhello-lib
Hi there, programmer!
Goodbye, programmer!
```

## 错误检查和警告

`gcc` 拥有一整套错误检查、生成警告的命令行选项。这些包括 `-ansi`、`-pedantic`、`-pedantic-errors` 和 `-Wall`。首先，`-pedantic` 告诉 `gcc` 发出严格 ANSI/ISO 标准 C 要求的所有警告。任何使用被禁止的扩展（如 `gcc` 支持的扩展）的程序都将被拒绝。`-pedantic-errors` 行为类似，只是它发出的是错误而不是警告。`-ansi` 关闭不符合标准的 GNU 扩展。然而，这些选项没有一个能保证你的代码即使在使用这些选项中的一个或全部进行编译时无错，也是 100% 符合 ANSI/ISO 标准的。

`-Wall` 选项指示 `gcc` 显示与正在编译的代码相关的所有通常相关的警告。`-Wall` 会对大多数程序员认为可疑和/或易于修改以防止生成的警告的代码发出警告。一个不良编程习惯的例子是声明一个变量但未在其他地方使用它。另一个例子是声明变量时未明确指定其类型。

## 示例

考虑以下示例，它展示了非常糟糕的编程形式。它将 `main` 声明为返回 `void`，而实际上 `main` 返回 `int`，并且它使用 GNU 扩展 `long long int` 来声明一个 64 位整数。

```
pedant.c
/*
 * pedant.c - use -ansi, -pedantic or -pedantic-errors
 */
#include <stdio.h>

void main(void)
{
 long long int i = 01;
 puts("This is a non-conforming C program");
}
```

### 示例

1. 首先，尝试使用无一致性检查进行编译：

**输出**

```
$ gcc pedant.c -o pedant
pedant.c: In function 'main':
pedant.c:8: warning: return type of 'main' is not 'int'
```

2. 接下来，使用 `-ansi` 开关进行编译：

**输出**

```
$ gcc -ansi pedant.c -o pedant
pedant.c: In function 'main':
pedant.c:8: warning: return type of 'main' is not 'int'
```

这里的教训是，`-ansi` 强制 `gcc` 发出标准要求的诊断消息。它并不确保你的代码符合 ANSI C。尽管 `main` 的声明不正确，但程序仍然编译通过了。

3. 现在，使用 `-pedantic`：

**输出**

```
$ gcc -pedantic pedant.c -o pedant
pedant.c: In function 'main':
pedant.c:9: warning: ANSI C does not support 'long long'
pedant.c:8: warning: return type of 'main' is not 'int'
```

同样，尽管发出了警告，代码仍然编译通过。

4. 最后，使用 `-pedantic-errors`：

**输出**

```
$ gcc -pedantic-errors pedant.c -o pedant
pedant.c: In function 'main':
pedant.c:9: ANSI C does not support 'long long'
pedant.c:8: return type of 'main' is not 'int'
```

程序编译失败。`gcc` 在显示所需的错误诊断后停止。

重申一下，`-ansi`、`-pedantic` 和 `-pedantic-errors` 编译器选项并不能确保符合 ANSI/ISO 标准的代码。它们只是帮你走在这条路上。指出 `gcc` 文档中关于使用 `-pedantic` 的备注是有启发性的：

> “该选项并不旨在实用；它存在的唯一目的是取悦那些声称 GNU CC 不支持 ANSI 标准的挑剔者。一些用户试图使用 `-pedantic` 来检查程序是否严格符合 ANSI C。他们很快发现，它并没有完全做到他们想要的；它发现了一些非 ANSI 的做法，但不是所有——只有那些 ANSI C 要求进行诊断的做法。”

## 优化选项

代码优化旨在提高性能。其权衡是更长的编译时间、编译期间增加的内存使用量，以及或许更大的代码大小。

目前，`gcc` 有三个优化级别。单纯的 `-O0` 选项告诉 `gcc` 同时减小代码大小和执行时间。它等同于 `-O1`。此级别执行的优化类型取决于目标处理器，但总是至少包括线程跳转和延迟栈弹出。*线程跳转优化*旨在减少跳转操作的数量。*延迟栈弹出发生在编译器允许参数在函数返回时在栈上累积，然后同时弹出，而不是在每个被调用函数返回时逐个弹出参数时。*

`-O2` 级别的优化包括所有第一级优化以及涉及处理器指令调度的额外调整。在此级别，编译器试图确保处理器在等待其他指令结果时有指令可以执行。编译器还试图补偿*数据延迟*，即从缓存或主存获取数据造成的延迟。实现高度依赖于特定的处理器。`-O3` 选项包括所有 `-O2` 优化、循环展开和其他特定于处理器的功能。

根据你对特定 CPU 系列的低级知识的多少，你可以使用 `-fflag` 选项请求你希望执行的具体优化。这三个标志值得考虑：`-ffastmath`、`-finline-functions` 和 `-funroll-loops`。`-ffastmath` 生成增加速度但违反 IEEE 和/或 ANSI 标准的浮点数学优化，`-finline-functions` 就地展开所有“简单”函数，很像预处理器宏替换。不过，编译器决定什么构成简单函数。

`-funroll-loops` 指示 `gcc` 展开所有具有固定迭代次数的循环，前提是迭代次数可以在编译时确定。*循环展开*意味着循环的每次迭代将变成单独的语句。因此，一个具有例如 100 次迭代的循环变成了 100 个顺序代码块，每个块执行相同的语句。图 1.2 以图形方式说明了循环展开。

注意，该图只是说明循环展开的一般原理。`gcc` 使用的实际方法可能差异很大。

`-finline-functions` 和 `-funroll-loops` 启用的优化可以极大地提高程序的执行速度，因为它们避免了函数调用和变量查找的开销，但代价通常是巨大的

