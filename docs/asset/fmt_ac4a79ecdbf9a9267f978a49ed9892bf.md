
```c
void __attribute__ ((destructor)) some_name_unload(void)

{

    /* 结束化代码 */

}
```

函数名 `some_name_load()` 和 `some_name_unload()` 可以替换为你所需的名称。

也可以在主程序中使用 gcc 的 `constructor` 和 `destructor` 属性来创建初始化和结束化函数。

## __init__() 和 __fini__() 函数

一种旧的共享库初始化和结束化技术是在库中创建两个函数：`__init__()` 和 `__fini__()`。`void __init(void)` 函数包含在库被进程加载时要执行的代码。`void __fini(void)` 函数包含在库被卸载时执行的代码。

如果我们创建了 `__init__()` 和 `__fini__()` 函数，那么在构建共享库时必须指定 `gcc -nostartfiles` 选项，以防止链接器包含这些函数的默认版本。（使用 `-Wl` 和 `-Wl,-fini` 链接器选项，我们可以根据需要为这两个函数选择替代名称）。

使用 `__init__()` 和 `__fini__()` 被认为是过时的，取而代之的是 gcc `constructor` 和 `destructor` 属性，后者等属性允许我们定义多个初始化和结束化函数。

## 4.5 预加载共享库

出于测试目的，有时选择性地覆盖动态链接器通常通过第 41.11 节规则找到的函数（或其他符号）是有用的。要做到这一点，我们可以定义环境变量 `LD_PRELOAD`，它是一个由空格或冒号分隔的共享库名称组成的字符串，这些库将在最先加载；如果可执行文件需要它们定义的任何函数，这些函数将被自动使用，从而覆盖动态链接器本会搜索的其他同名函数。例如

假设我们有一个程序调用了定义在 `libdemo` 库中的函数 `x1()` 和 `x2()`。当我们运行该程序时，我们看到如下输出：

```
$ ./prog

Called mod1-x1 DEMO

Called mod2-x2 DEMO
```

（在本例中，我们假设共享库位于标准目录之一，因此我们不需要使用 `LD_LIBRARY_PATH`）。我们可以通过创建另一个共享库 `libalt.so` 来选择性地覆盖 `x1()`。预加载这个库将导致：

```
$ LD_PRELOAD=./libalt.so ./prog

Called mod1-x1 DEMO

Called mod2-x2 DEMO
```

在这里，我们看到 `libalt.so` 中的 `x1()` 函数被调用，但对于 `x2()` 未提供定义。`LD_PRELOAD` 环境变量按进程控制。或者，`/etc/ld.so.preload` 文件（以空格分隔库列表）则可以在系统范围内执行相同的任务。

## 4.6 监控动态链接器

有时，监控动态链接器的操作以知道它在哪里搜索是有用的。我们可以使用 `LD_DEBUG` 变量来实现。通过设置一个（或多个）关键字，我们可以获取各种类型的跟踪。例如，设置 `LD_DEBUG=help`：

`LD_DEBUG` 的有效选项：

- `all`
- `bindings`
- `commands`
- `dependencies`
- `exit`
- `help`
- `info`
- `libs`
- `linker`
- `relocation`
- `statistics`
- `symbols`
- `unused`
- `versions`

每行开头显示的 LD_DEBUG 值是被跟踪进程的 PID。如果我们正在监控多个进程（父进程和子进程），这非常有用。

默认情况下，`LD_DEBUG` 输出被写入标准错误（error），但我们可以通过为 `LD_DEBUG_OUTPUT` 环境变量分配路径将其重定向到其他地方。下面的示例显示了请求跟踪符号时提供的简略输出：

```
$ LD_DEBUG=symbols ./prog

10687: find=librt.so [0] searching

10687: cache=/etc/ld.so

10687: trying file=librt.so

10687: find=libc.so [0] searching

10687: cache=/etc/ld.so

10687: trying file=libc.so

10687: find=libpthread.so [0] searching

10687: cache=/etc/ld.so

10687: trying file=libpthread.so
```
