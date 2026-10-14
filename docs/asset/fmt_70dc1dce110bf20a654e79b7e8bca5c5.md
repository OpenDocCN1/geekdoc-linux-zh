
`if ((ret_str = malloc(sizeof(char)*new_length))==NULL)`

(gdb) s

`45 sprintf(digit_str, "%d", new_length);`

(gdb)

值得注意的是，`gdb` 指出了传递给函数的参数。
细心的读者可能已经发现了第 35 行的错误。它分配了一个大小为一个字符的内存区域，但这个区域被赋值给了一个由多得多的字符组成的字符字符串。要纠正这个问题，只需要修改源代码并重新启动编译。

此外，还可以根据指针找到变量的值、结构体的内容以及字符串的内容。这些操作可以通过 `print` 命令以非常简单的方式完成：

```
(gdb) print new_length

$1 = 68

(gdb) print str

$2 = 0xffffff947 "ThisIsProgrammeThatDoesNotWork"

(gdb) print *str

$3 = 67 'C'

(gdb)
```

最后，关于调试器的最后一个操作是在调用列表中找到函数调用所在的位置。该操作通过 `where` 命令或 `backtrace` 命令完成：

```
(gdb) where

#0 doublestr (str=0xbfff947 "ThisIsAProgrammeDoesNotWork")
    at coreumped.c:46
#1 0x80485bf in main (argc=2, argv=0xbfff828) at coreumped.c:17
#2 0x8048544 in _crt_dummy__ ()

(gdb) backtrace

#0 doublestr (str=0xbfff947 "ThisIsAProgrammeDoesNotWork")
    at coreumped.c:46
#1 0x80485bf in main (argc=2, argv=0xbfff828) at coreumped.c:17
#2 0x8048544 in _crt_dummy__ ()
```

该命令提供了调试期间执行的不同调用列表，对于每一个调用，都列出了函数所在的文件、行号以及不同的参数列表。

# 附录 3

# make 的使用

## make 的原理
启动时，`make` 会使用当前目录下的 `datafile` 文件或 `Makefile`。它分析其内容并启动指示的命令。这个工具非常有用，因为它能够避免重新编译除必要代码以外的所有代码。

## 编写 Makefile
本节说明的示例在附录 4 中也会提到。它使用了几个文件：

- `complex.c`: 实现复数计算的模块；
- `complex.h`: `complex.c` 模块原型的接口；
- `draw.c`: 以图形形式表示复数的模块；
- `draw.h`: `draw.c` 模块原型的接口；
- `main.c`: 主文件。

关联的 `Makefile` 如下：

```
Makefile

# 用于复数的 Makefile

CC=gcc

RM=/bin/rm

# 编译标志

CFLAGS=-g

# 文件
```

# 附录 3：make 的使用：

```Makefile
SRC=complex.c draw.c main.c

OBJ=$(SRC:.c=.o)

PROG=complex

LIB=-lm

# 生成规则

$(PROG) : $(OBJ)
$(CC) $(CFLAGS) $(OBJ) -o $(PROG) $(LIB)

# 保持整洁！

clean:
$(RM) -f $(OBJ) $(PROG)

# 依赖关系

complex.o : complex.c draw.h
draw.o : draw.c draw.h complex.h
main.o : main.c draw.h complex.h
```

该文件的第一部分由各种声明组成，在某些情况下（例如需要更改编译器）提供了一定的使用灵活性。在这里定义了编译时将使用的选项。在这里，涉及到 `-g` 选项，它可以对可能出现的错误进行调试。

接下来是要编译的不同文件的列表。变量 `OBJ` 基于一种规则，避免了手动列出对象集，该规则假设它们除了扩展名外与源文件名相同。

最后部分是创建可执行文件的规则。只有当所有对象文件都生成时，该规则才会满足。文件末尾是依赖关系，这将能够编译被修改的文件。

例如，假设所有对象文件已生成，但自上次编译以来，开发者修改了 `draw.h` 文件。在下一次编译时，只有某些文件会被重新编译：

```
make
gcc -c draw.c -o draw.o
gcc -c main.c -o main.o
gcc complex.o main.o -o complex -lm
```

根据依赖关系的定义，`complex.c` 文件不会被重新编译。要找到程序的依赖关系，只需启动 `-MM` 命令。这将产生该模块使用的头文件列表。

# 附录 4 库的管理

## 符号的创建与处理
符号的创建和处理可以根据指针找到变量的值、结构体的内容以及字符串的内容。这些操作可以通过 `print` 命令以非常简单的方式完成：
（此处省略重复示例代码块翻译，保持逻辑一致）

最后，关于调试器的最后一个操作是在调用列表中找到函数调用所在的位置。该操作通过 `where` 命令或 `backtrace` 命令完成：
（此处省略重复示例代码块翻译，保持逻辑一致）

# 附录 4：库的管理

当程序运行时。最后，需要为新版本创建一个链接库 `libcomplex.so`。

当开发者纠正库中的错误时，或者他添加了新函数时（对于任何不影响现有程序执行的修改），都有必要重新构建库。只需增加次版本号（minor number）即可。当开发者进行更改现有程序运行轨迹的修改时，必须增加 `libcomplex.so.1.0` 的主版本号（major number），并且必须赋予正确的名称 `libcomplex.so.2`。最后，他必须为新版本重新创建链接库 `libcomplex.so`。

## 库的动态加载

ELF 格式带来的优势之一是能够指定库的动态加载，并在操作终止时卸载它们。许多程序如 `perl` 和 `Java` 都使用了这些特性。

此功能需要使用库 `libld` 以及头文件 `<dlfcn.h>`。动态加载的整个原理详见于 [Lu, 1995]。下面的示例说明了这一特性：

```c
dltest.c

#include <dlfcn.h>
#include <stdio.h>

#ifdef PI
#define PI 3.1415926535897932386
#endif

typedef double (*fun_t) (double);

void main(int argc, char **argv) {
    void *ptr = NULL;
    char *nombib = "libm.so";
    char *function = "cos";
    fun_t fun = NULL;
    double result = 0;
    /* 动态加载库 */
    if ((ptr = dlopen(nombib, RTLD_LAZY)) == NULL) {
        fprintf(stderr, "dlopen(%s) -> %s \n", nombib, dlerror());
        exit(1);
    }
    /* 获取函数地址 */
    if ((fun = (fun_t) dlsym(ptr, function)) == NULL) {
        fprintf(stderr, "dlsym(%s) -> %s \n", function, dlerror());
        exit(1);
    }
    printf("Call of %s in %s \n", function, nombib);
    result = (*fun) ((double) PI / 4);
    dlclose(ptr);
    printf("Result : %f \n", result);
}
```

`dltest.c`

该程序的编译目的仅是执行 `cos` $\pi$ 操作，其结果如下：

```bash
gandalf# gcc -c -g -Wall dltest.c -o dltest.o
gandalf# gcc -g dltest.o -o dltest -ldl
gandalf# ldd dltest
  libdl.so.1 => /lib/libdl.so.1.7.14
  libc.so.5 => /lib/libc.so.5.3.9
gandalf# ./dltest
Call Cos in libm.so
Result : 0.707107
```

该程序没有链接到数学库，但调用的是数学库中的 `cos` 函数。
这些函数的原型如下：

```c
#include <dlfcn.h>
```
