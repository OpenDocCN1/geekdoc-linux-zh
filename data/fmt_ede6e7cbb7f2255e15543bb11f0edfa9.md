
在交互模式下运行解释器。

```c
void Py_Initialize()
```

初始化 Python 解释器。在使用 C API 中的任何函数之前都应该调用此函数，但 `Py_SetProgramName()`、`PyEval_InitThreads()`、`PyEval_ReleaseLock()` 和 `PyEval_AcquireLock()` 除外。

```c
int Py_Initialized()
```

如果解释器已初始化，则返回 1，否则返回 0。

```c
void Py_Finalize()
```

通过销毁自调用 `Py_Initialize()` 之后创建的所有子解释器和对象来清理解释器。通常，此函数会释放解释器分配的所有内存。然而，循环引用和扩展模块可能会引入此函数无法恢复的内存泄漏。

```c
void Py_SetProgramName(char *name)
```

设置通常位于模块 `argv[0]` 参数中的程序名。此函数应只在 `Py_Initialize()` 之前调用。

```c
char *Py_GetPrefix()
```

返回安装的平台无关文件的前缀。这与 `sys.prefix` 中的值相同。

```c
char *Py_GetExecPrefix()
```

返回安装的平台相关文件的可执行前缀。这与 `sys.exec_prefix` 中的值相同。

```c
char *Py_GetProgramPath()
```

返回 Python 可执行文件的完整路径。

```c
char *Py_GetPath()
```

返回默认模块搜索路径。路径作为字符串返回，由由平台分隔符分隔的目录名称组成（UNIX 上为 `:`；DOS/Windows 上为 `;`）。

```c
int PySys_SetArgv(int argc, char **argv)
```

设置命令行选项以填充 `sys.argv` 的值。此函数应只在 `Py_Initialize()` 之前调用。

# 从 C 访问 Python

虽然从 C 访问解释器有很多方法，但嵌入时最常用的有四个要素：

- 导入 Python 库模块（模拟 `import` 语句）
- 获取模块中定义对象的引用
- 调用 Python 函数、类和方法
- 访问对象的属性（数据、方法等）

所有这些操作都可以使用 Python C API 中定义的这些基本操作完成：

```c
PyObject *ImportModule(const char *modname)
```

导入 `modname` 并返回关联对象的引用。

```c
PyObject *GetAttr(PyObject *obj, char *name)
```

从对象中获取属性。

```c
int SetAttr(PyObject *obj, char *name, PyObject *value)
```

设置对象的属性。

```c
PyObject *CallWithKeywords(PyObject *func, PyObject *args, PyObject *kwargs)
```

带参数和关键字调用函数。

## 嵌入解释器 609

```c
#include "Python.h"

int main(int argc, char **argv) {
    PyObject *re;
    PyObject *re_compile;
    PyObject *pat;
    PyObject *pat_search;
    PyObject *args;
    char buffer[256];

    if (argc != 2) {
        fprintf(stderr,"Usage: %s pattern\n", argv[0]);
        exit(1);
    }

    Py_Initialize();

    /* import re */
    re = ImportModule("re");

    /* pat = re.compile(flags) */
    re_compile = PyGetAttr(re, "compile");
    args = PyValue("s", argv[1]);
    pat = PyCallObject(re_compile, args);
    Py_DECREF(args);

    /* pat_search = pat.search */
    pat_search = PyGetAttr(pat, "search");

    /* Read lines and perform matches */
    while (fgets(buffer, 255, stdin)) {
        args = PyValue("s", buffer);

        /* match = pat.search(buffer) */
        match = PyCallObject(pat_search, args);
        Py_DECREF(args);
        if (match != Py_None) {
            printf("%s", buffer);
            Py_DECREF(match);
        }
    }
    Py_DECREF(pat);
    Py_DECREF(re_compile);
    Py_DECREF(re);
    Py_Finalize();
    return 0;
}
```

在任何嵌入代码中，正确管理引用计数至关重要。特别是对于任何从 C 创建或作为评估结果返回给 C 的对象，都需要减少它们的引用计数。

### 转换为 C

使用解释器的一个大问题是将 Python 函数或方法调的结果转换为适当的 C 表示。根据一般规则，你需要确切知道某个操作将返回什么类型的数据。遗憾的是，没有像 `PyArg_ParseTuple` 那样的高级便利函数来转换单个值。然而，以下列了一些低级转换函数，只要你知道正在处理的是哪种 Python 对象，它们就可以将原始 Python 数据类型转换为适当的 C 表示：

#### Python 到 C 的转换函数

- `long PyInt_AsLong(PyObject *)`
- `long PyLong_AsLong(PyObject *)`
- `double PyFloat_AsDouble(PyObject *)`
- `char *PyString_AsString(PyObject *)` （仅限 Python 2）
- `char *PyBytes_AsString(PyObject *)` （仅限 Python 3）

对于任何比此复杂的类型，你需要查阅 C API 文档（`http://docs.python.org/c-api`）。

# ctypes

`ctypes` 模块提供了对 DLL 和共享库中定义的 C 函数的访问。尽管你需要了解一些关于底层 C 库的细节（名称、调用参数、类型等），但你可以使用 `ctypes` 来访问 C 代码，而无需编写 C 扩展封装器或使用 C 编译器编译任何内容。`ctypes` 是一个功能强大的模块，具有许多高级功能。在这里，我们将介绍使用它所需的核心部分。

## 加载共享库

以下类被用于加载 C 共享库并返回一个表示其内容的实例：

```
CDLL(name [, mode [, handle [, use_errno [, use_last_error]]]])
```

表示 C 共享库的类。`name` 是库的名称，例如 `'libc.so.6'` 或 `'msvcrt.dll'`。`mode` 提供了标志，决定在 Unix 上通过底层 `dlopen()` 函数如何加载和解析库。它可以通过 `RTLD_LOCAL`、`RTLD_GLOBAL` 或 `RTLD_DEFAULT`（默认值）的位或或来设置。在 Windows 上，会忽略 `mode`。`handle` 指定指向已加载库的句柄（如果可用）。默认情况下，`use_errno` 为 False。`use_last_error` 是一个布尔标志，为加载库中的 C 变量添加一层额外的安全性。该层会在调用任何函数之前保存线程本地的错误副本，并在之后恢复该值。默认情况下，`use_last_error` 为布尔标志，启用一对函数 `get_last_error()` 和 `set_last_error()`，它们可用于操作系统错误代码。这些函数在 Windows 上更常用。默认情况下，`use_last_error` 为 False。

```
WinDLL(name [, mode [, handle [, use_errno [, use_last_error]]]])
```

与 `CDLL()` 相同，但库中的函数假设遵循 Windows stdcall 调用约定（Windows）。

该实用函数可以用于在系统上定位共享库，并构建适用于前面类中 `name` 参数的模块。它定义在 `ctypes.submodule` 中：

```
find_library(name)
```
