
# 共享库的高级特性

## 42.1 使用 dlopen API

```bash
$ LD_LIBRARY_PATH=./dynload libdemo.so.1 x1
Called mod1-x1
```

在上述第一个命令中，`dlopen()` 注意到库路径包含一个斜杠，因此将其解释为相对路径（在这种情况下，为当前工作目录下的一个库）。在第二个命令中，我们在 `LD_LIBRARY_PATH` 中指定了库搜索路径。该搜索路径根据动态链接器的常规规则进行解释（在 particular 情况下，同样是在当前工作目录中查找库）。

### 列表 42-1：使用 dlopen API

```c
#include <dlfcn.h>

#include <tlpi_hdr.h>

int
main(int argc, char *argv[]) {
    void *libHandle;            /* 共享库句柄 */
    void (*funcp)(void);        /* 无参数函数指针 */
    const char *err;

    if (argc != 3 || strcmp(argv[1], "--help") == 0)
        usageErr("%s lib-path function-name\n", argv[0]);

    /* 加载共享库并获取句柄供以后使用 */
    libHandle = dlopen(argv[1], RTLD_LAZY);
    if (libHandle == NULL)
        fatal("dlopen: %s", dlerror());

    /* 在库中搜索 argv[2] 中指定的符号 */
    (void) dlerror();            /* 清除 dlerror */
    *(void (**)(&funcp) = dlsym(libHandle, argv[2]);
    err = dlerror();
    if (err != NULL)
        fatal("dlsym: %s", err);

    /* 如果 dlsym() 返回的地址非 NULL，则尝试将其作为无参数函数进行调用 */
    if (funcp == NULL)
        printf("%s is NULL\n", argv[2]);
    else
        funcp();

    dlclose(libHandle);         /* 关闭库 */
    exit(EXIT_SUCCESS);
}
```

`shlibs/dynload.c`

### 42.1.4 关闭共享库：dlclose()

`dlclose()` 函数用于关闭一个库。

```c
#include <dlfcn.h>

int dlclose(void *handle);
```

成功时返回 0，错误时返回 -1。

`dlclose()` 函数会减少系统对由 `handle` 指向的库的引用计数。如果该引用计数减到 0，且库中没有符号被其他库需要，则该库会被卸载。此过程也会（递归地）对该库依赖树中的库进行执行。在进程终止时，会对所有库执行隐式的 `dlclose()`。

> 从 glibc 2.2.3 开始，共享库中的函数可以在库被卸载时使用 `atexit()`

### 修正后的 42.1.5 获取关于加载符号的符号：dladdr()

给定一个地址（通常通过早期的 `dlsym()` 获取），`dladdr()` 返回一个关于该地址的结构。

```c
#define _GNU_SOURCE

#include <dlfcn.h>

int dladdr(const void *addr, Dl_info *info);
```

如果在共享库中找到 `addr` 则返回非零值，否则

`info` 参数是一个指向调用者分配的结构的指针，包含：

```c
typedef struct {
    const char *dli_name;   /* 包含 addr 的共享库路径 */
    void *dli_base;         /* 库加载的基地址 */
    const char *dli_sname;   /* 最近的符号名称 */
    void *dli_saddr;         /* 符号的实际值 */
} Dl_info;
```

提供了库的路径和运行地址。假设 `addr` 指向一个精确匹配的符号，则返回该符号。

SUSv3 未指定 `dladdr()`，且该函数在所有的 UNIX 实现中都可用。

### 42.1.6 访问程序中的符号

假设我们使用 `dlopen()` 加载库，通过 `dlsym()` 获取库中的函数地址，然后调用 `x()`。如果 `x()` 转而调用函数 `y(j)`，那么通常 `y(j)` 将在加载的共享库中查找。

有时，我们希望 `x()` 调用主程序中 `y(j)` 的实现（这类似于回调机制）。为了实现这一点，我们必须使全局作用域符号对动态链接器可见，链接程序时使用 `export-dynamic` 选项：

```bash
$ gcc -Wl,--export-dynamic main.c
```

（加上选项和参数）

等价地，我们可以写：

```bash
$ gcc -export-dynamic main.c
```

使用任一选项都允许动态加载的库访问程序的符号。

`gcc -dynamic` 选项和 `gcc -Wl,-E` 选项都是 `-Wl,--export-dynamic` 的同义词。

```c
void
__attribute__((visibility("hidden")))
func(void) {
    /* Code * */
}
```

`static` 关键字将符号的可见性限制在单个源文件内，而 `hidden` 属性则使符号在组成共享库的所有源文件中均可用，但防止其在库外部可见。

在配合 `static` 关键字使用时，`hidden` 属性还具有反向作用的效果，即防止在运行时发生符号覆盖（symbol interposition）。

- 版本脚本（Version scripts，第 42.3 节）可精确控制符号的可见性，并选择引用所绑定的符号版本。
- 当在动态加载共享库（第 42.1.1 节）时，可以使用 `dlopen()` 的 `RTLD_GLOBAL` 标志来指定库定义的符号应可供后续加载的库进行绑定，并可以使用 `--export-dynamic` 链接器选项（第 42.1.6 节）使主程序的全局符号对动态加载的库可见。

关于符号可见性主题的更多细节，请参阅 [Deeper, 2004 (b)]。

## 链接器脚本 (Linker Scripts)

版本脚本是一个包含链接器 `ld` 指令的文本文件。为了使用版本脚本，我们必须指定 `--version-script,myscriptfile` 链接器选项：

```bash
$ gcc -Wl,--version-script,myscriptfile.map ...
```

版本脚本通常（但并非总是）使用 `.map` 扩展名标识。以下章节描述了版本脚本的一些用途。

### 42.1 使用版本脚本控制符号可见性

版本脚本的用途之一是控制可能意外变成全局符号（即对链接该库的应用程序可见）的可见性。作为一个简单的例子，假设我们正从三个源文件 `vis.c`、`vis_f1.c` 和 `vis_f2.c` 构建一个共享库，它们分别定义了函数 `vis()`、`vis_f1()` 和 `vis_f2()`。`vis()` 函数被 `vis_f1()` 和 `vis_f2()` 调用，但并不打算供链接该库的应用程序直接使用。假设我们以通常方式使用该共享库：

```bash
$ gcc -g -fPIC -Wall vis.c vis_f1.c vis_f2.c
$ gcc -g -shared -o vis.so vis.o vis_f1.o vis_f2.o
```

如果我们使用以下 `readelf` 命令列出库导出的动态符号，我们将看到：

```bash
$ readelf --symbols --use-dynamic vis.so | grep vis
30: 00000790 59 FUNC DEFAULT 10 vis_f1
25: 000007d0 73 FUNC DEFAULT 10 vis_f2
27: 00000770 20 FUNC DEFAULT 10 vis
```

该共享库导出了三个符号：`vis()`、`vis_f1()` 和 `vis_f2()`。然而，我们需要确保库只导出 `vis_f1()` 和 `vis_f2()` 符号。我们可以使用以下版本脚本来实现这一结果：

```bash
$ cat vis.map
VER_1 {
  global: vis_f1;
  vis_f2;
  local: *
}
```
