
`gcc infile.c -o outfile`

如果未指定输出文件名，`gcc` 将输出文件命名为 `a.out`。所有步骤都需要由 `gcc` 程序本身处理，因为 `gcc` 可以将链接等处理任务交给 `ld`（GNU 链接器）。

以下示例使用 `gcc` 从 `hello.c` 创建 `hello` 程序。首先是源码：

```c
/*
* hello.c - 标准 hello 世界程序
*/
#include <stdio.h>
int main(int argc, char *argv[]) {
    printf("Hello, Linux programming world!\n");
    return 0;
}
```

现在，编译并运行你的程序，请遵循以下操作：

```bash
$ gcc hello.c -o hello
```

如果一切顺利，`gcc` 静静地完成工作并返回 shell 提示符。它编译并链接源文件 `hello.c` (`gcc hello.c`)，创建一个名为 `hello` 的二进制文件。

如果你运行该程序，这是你的输出：

```bash
$ ./hello
Hello, Linux programming world!
```

> 注意：在当前目录专门执行 `hello` 程序的命令用 `.` 表示，因为在路径中包含当前目录存在安全风险。是，而不是一个类似于 `/bin:/usr/local/bin::` 的 `$PATH` 环境变量，应该是 `/bin:/usr/local/bin`，这样黑客就不会在你的当前目录下放置一个与你真正想要执行的良性命令同名的危险命令。

# 在 Linux 中编程

使用 `GCC`（以及任何其他编译器），预处理阶段会处理如 `#include <stdio.h>` 等构造以及 `#define` 宏。一旦处理完这些内容，就会开始常规处理。

`GCC` 依赖文件扩展名来确定它是哪种源代码文件——也就是说，使用哪种编程语言编写源代码。表 29-1 列出了最常见的扩展名以及 `GCC` 如何解释它们。

## 表 29-1

| 扩展名 | 类型 |
|---|---|
| `.a`, `.so` | 编译后的库代码 |
| `.c` | C 语言源代码 |
| `.C`, `.cc` | C++ 源代码（也可能使用 `.cpp`, `.cxx`, `.CPP`, `.cp`, 或 `.c++` 作为扩展名） |
| `.i` | 预处理过的 C 源代码 |
| `.ii` | 预处理过的 C++ 源代码 |
| `.m` | Objective-C 源代码 |
| `.o` | 编译后的对象代码 |
| `.S`, `.s` | 汇编语言源代码 |

## 编译多个源文件

复杂的程序由多个源文件组成，在最后一步之前，每个源文件都必须编译为对象代码。为此，请向 `gcc` 传递它需要编译的每个源文件的文件名。`GCC` 的调用可能如下：

```
$ gcc file1.c file2.o file3.c -o progame
```

`gcc` 会创建 `file1.o`、`file2.o` 和 `file3.o` 并将它们链接在一起以创建 `progame`。另一种方法是对每个文件单独单独使用 `gcc -c` 选项，为每个文件创建对象。然后在第二步中，将对象文件链接以创建可执行文件。因此，所示的单个命令变为：

```
$ gcc -c file1.c
$ gcc -c file2.c
$ gcc -c file3.c
$ gcc file1.o file2.o file3.o -o progame
```

这样做的原因之一是避免重新编译没有更改的文件。例如，如果你只更改了 `file3.c` 中的源代码，就不需要重新编译 `file1.c` 和 `file2.c` 来生成程序。在链接并创建可执行文件之前单独编译源文件的另一个原因是为了避免长时间的编译。如果其中一个源代码模块非常长，在单次 `gcc` 调用中编译多个文件可能会花费很长时间：

让我们来看一个从多个源文件创建一个单个二进制可执行文件的示例。示例程序 `newhello` 包含一个 C 源代码文件 `main.c`（见列表 29-1）、一个头文件 `msg.h`（见列表 29-2）以及另一个 C 源文件 `msg.c`。

### 列表 29-1
# newhello 的主程序

```
/*
 * main.c 驱动程序
 */
#include <stdio.h>
#include "msg.h"
int main(int argc, char *argv[])
{
    char msg_hi[] = "HI there, programmer! ";
    char msg_bye[] = "Goodbye, programmer! ";
    printf("%s\n", msg_hi);
    prmsg(msg_bye);
    return 0;
}
```

### 列表 29-2
# newhello 的辅助函数头文件

```
/*
 * msg.h - msg.c 的头文件
 */
#ifndef MSG_H_
#define MSG_H_
void prmsg(char *msg);
#endif /* MSG_H_ */
```

### 列表 29-3
# newhello 的辅助函数定义

```
/*
 * msg.c - msg.h 中声明的函数
 */
#include <stdio.h>
#include "msg.h"
void primsg(char *msg)
{
    printf("%s\n", msg);
}
```
