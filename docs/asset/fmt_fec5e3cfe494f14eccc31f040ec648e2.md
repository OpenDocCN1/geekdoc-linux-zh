
# errtest.c - Test program for error-handling library

```c
/*
 * errtest.c - Test program for error-handling library
 */
#include <stdio.h>
#include <stdlib.h>
#include "liberr.h"

#define ERR_QUIT_SKIP 1
#define LOG_QUIT_SKIP 1

int main(void)
{
    FILE *pf;

    fputs("Testing err_ret . . . \n", stdout);
    if((pf = fopen("foo", "r")) == NULL)
        err_ret("%s %s", "err_ret", "failed to open foo");

    fputs("Testing log_ret . . . \n", stdout);
    if((pf = fopen("foo", "r")) == NULL)
        log_ret("errtest.log", "%s %s", "log_ret", "failed to open foo");

#ifdef ERR_QUIT_SKIP
    fputs("Testing err_quit . . . \n", stdout);
    if((pf = fopen("foo", "r")) == NULL)
        err_quit("%s %s", "err_quit", "failed to open foo");
#endif /* ERR_QUIT_SKIP */

#ifdef LOG_QUIT_SKIP
    fputs("Testing log_quit . . . \n", stdout);
    if((pf = fopen("foo", "r")) == NULL)
        log_quit("errtest.log", "%s %s", "log_quit", "failed to open foo");
#endif /* LOG_QUIT_SKIP */

    exit(EXIT_SUCCESS);
}
```

编译并运行 `errtest` 将产生以下输出：

![](img/be588b36b489136ce784030a08a1d3d4_346_0.png)

### 输出

```
$ gcc -g errtest.c -o errtest -L . -lerr
$ ./errtest
Testing err_ret . . .
  err_ret failed to open foo: No such file or directory
Testing log_ret . . .
$ cat errtest.log
  log_ret failed to open foo: No such file or directory
```

两个 `#ifdef` `#endif` 结构阻止了 `*_quit` 函数的执行。为了测试它们，注释掉其中一个宏并重新编译，然后注释掉另一个宏并重新编译。尝试将测试 `*_quit` 函数作为一项练习。

## 共享库

共享库比静态库有几个优势。首先，它们需要更少的系统资源。它们使用更少的磁盘空间，因为共享库代码没有被编译到每个二进制文件中，而是在运行时从单个位置动态链接和加载。它们使用更少的系统内存，因为内核将库占用的内存分配给使用该库的所有程序共享。

共享库的另一个优势是它们稍快，因为它们只需加载到内存中一次。最后，共享库简化了代码和系统维护。随着 `bug` 被修复或功能被添加，用户只需获取更新的库并安装即可。使用静态库时，每个使用该库的程序都必须重新编译。

如前所述，动态链接器/加载器 `ld.so` 在运行时将符号名称链接到定义它们的相应共享库。共享库有一个特殊的名称，即 `soname`，由库名和主版本号组成。例如，我的一个系统上 C 库的全名是 `libc.so.5.4.46`。库名是 `libc.so`；主版本号是 5；次版本号是 4；46 是发布或补丁级别。因此，C 库的 `soname` 是 `libc.so.5`。

新 C 库 `libc6` 的 `soname` 是 `libc.so.6`——主版本号的变更表明发生了重大变化，以至于这两个库在（很大程度上！）是不兼容的。次版本号和补丁级别编号会随着 `bug` 的修复而变化，但 `soname` 保持不变，因此新版本通常与旧版本兼容。

了解 `soname` 很重要，因为应用程序是链接到 `soname` 的。它是如何工作的？`ldconfig` 实用程序从实际库（例如 `libc.so.5.4.46`）创建到 `soname`（`libc.so.5`）的符号链接，并将此信息存储在 `/etc/ld.so.cache` 中。在运行时，`ld.so` 扫描缓存文件，找到所需的 `soname`，并由于符号链接的存在，将实际库加载到内存中，并将应用程序函数调用链接到已加载库中的适当符号。

在以下情况下，库版本变得不兼容：

- 导出的函数接口发生变化
- 添加了新的函数接口
- 函数行为偏离了原始规范
- 导出的数据结构发生变化
- 导出的数据结构已添加

为了维护库的兼容性，请遵循以下准则：

- 使用新名称向您的库中添加函数，而不是修改现有函数或更改其行为。
- 仅将项目添加到现有数据结构的末尾，并使它们可选或在库内部初始化它们。
- 不要扩展数组中使用的数据结构。

## 构建共享库

构建共享库的过程与构建静态库的过程略有不同。以下列表概述了构建共享库所需的步骤：

1. 在编译对象文件时，使用 `gcc` 的 `-fPIC` 选项，该选项生成位置无关代码（PIC），可以在任何地址链接和加载。
2. 不要使用 `gcc` 的 `-fomit-frame-pointer` 选项——这样做可能会使调试变得不可能。
3. 使用 `gcc` 的 `-shared` 和 `-soname` 选项。
4. 使用 `gcc` 的 `-Wl` 选项向链接器 `ld` 传递参数。
5. 通过使用 `gcc` 的 `-l` 选项显式链接 C 库。这确保如果您的程序缺少正确版本的 C 库，程序将无法编译，因为对新函数或修改后函数的引用会导致编译器错误。

## 示例

![](img/be588b36b489136ce784030a08a1d3d4_348_0.png)

此示例将错误处理库构建为共享库。它首先构建对象文件，然后链接该库。然后它从完整的库名称到 `soname` 创建符号链接，并从完整的库名称到共享库的名称（仅以 `.so` 结尾）创建符号链接。

```bash
$ gcc -fPIC -g -c librerr.c -o librerr.o
$ gcc -g -shared -Wl,-soname,liberr.so -o librerr.so.1.0.0 librerr.o -lc
$ ln -s librerr.so.1.0.0 librerr.so.1
$ ln -s librerr.so.1.0.0 librerr.so
```

由于您不会将此库作为系统库安装在 `/usr` 或 `/usr/lib` 中，因此必须创建两个链接：一个用于 `soname`，另一个用于共享库。链接器在链接 `librerr` 时会使用共享库名称；也就是说，当使用 `-lerr` 时。

## 使用共享库

现在，为了使用新的共享库，重新查看上一节中介绍的测试程序 `errtest.c`。同样，您需要告诉链接器使用哪个库以及在哪里找到它，因此请使用 `-l` 和 `-L` 选项。最后，为了执行程序，您需要告诉动态链接器/加载器 `ld.so` 在哪里找到共享库，因此请使用 `$LD_LIBRARY_PATH` 变量。

## 示例

![](img/be588b36b489136ce784030a08a1d3d4_349_0.png)

此示例将 `errtest` 链接到 `liberr` 的共享库版本，然后运行 `errtest`。

```bash
$ gcc -g errtest.c -o errtest -L. -lerr
$ LD_LIBRARY_PATH=.$(pwd) ./errtest
```

![](img/be588b36b489136ce784030a08a1d3d4_349_1.png)

### 输出

```text
Testing err_ret . . .
err_ret failed to open foo: No such file or directory
Testing log_ret . . .
```

正如前面所指出的，环境变量 `$LD_LIBRARY_PATH` 将其中包含的路径添加到受信任的库目录 `/lib` 和 `/usr/lib` 中。`ld.so` 将首先搜索环境变量中指定的路径，并确保找到您的库。使用笨拙的命令行的一种替代方法是，将您的库的路径名添加到 `/etc/ld.so.conf` 中，并通过运行（以 root 身份）`ldconfig` 更新缓存（`/etc/ld.so.cache`）。
