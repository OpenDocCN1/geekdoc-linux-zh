
抛出一个异常，`exc` 是一个异常对象。异常的值取自 C 标准库中的 `errno` 变量。

```c
void PyErr_SetErrnoWithFilename(PyObject *exc, char *filename)
```

与 `PyErr_SetFromErrno()` 类似，但在异常值中包含文件名，如

```c
void PyErr_SetObject(PyObject *exc, PyObject *val)
```

抛出一个异常。`exc` 是一个异常对象，`val` 是一个包含异常值的对象。

```c
void PyErr_SetString(PyObject *exc, char *msg)
```

抛出一个异常。`exc` 是一个异常对象，`msg` 是描述发生了了什么的消息。

这些函数中的 `exc` 参数可以设置为以下之一：

| C 名称 | Python 异常 |
|---|---|
| `PyEx_ArithmeticError` | ArithmeticError |
| `PyEx_AssertionError` | AssertionError |
| `PyEx_AttributeError` | AttributeError |
| `PyEx_EnvironmentError` | EnvironmentError |
| `PyEx_EOFError` | EOFError |
| `PyEx_Exception` | Exception |
| `PyEx_FloatingPointError` | FloatingPointError |
| `PyEx_ImportError` | ImportError |
| `PyEx_IndexError` | IndexError |
| `PyEx_IOError` | IOError |
| `PyEx_KeyError` | KeyError |
| `PyEx_KeyboardInterrupt` | KeyboardInterrupt |
| `PyEx_LookupError` | LookupError |
| `PyEx_MemoryError` | MemoryError |
| `PyEx_NameError` | NameError |
| `PyEx_NotError` | NotImplementedError |
| 名称 | Python 异常 |
| --- | --- |
| `PyExc_OSError` | OSError |
| `PyExc_OverflowError` | OverflowError |
| `PyExc_ReferenceError` | ReferenceError |
| `PyExc_RuntimeError` | RuntimeError |
| `PyExc_StandardError` | StandardError |
| `PyExc_StopIteration` | StopIteration |
| `PyExc_SyntaxError` | SyntaxError |
| `PyExc_SystemError` | SystemError |
| `PyExc_SystemExit` | SystemExit |
| `PyExc_TypeError` | TypeError |
| `PyExc_UnicodeError` | UnicodeEncode |
| `PyExc_DecodeError` | UnicodeDecode |
| `PyExc_TranslateError` | UnicodeTranslate |
| `PyExc_ValueError` | ValueError |
| `PyExc_WindowsError` | WindowsError |
| `PyExc_ZeroDivisionError` | ZeroDivisionError |

# 引用计数

与用 编写的程序不同，C 扩展可能需要操作引用计数。这是通过以下宏完成的，所有宏都适用于 `PyObject` 类型。

| 宏 | 描述 |
| :--- | :--- |
| `Py_INCREF(obj)` | 增加 `obj` 的引用计数，`obj` 不能为空。 |
| `Py_DECREF(obj)` | 减少 `obj` 的引用计数，`obj` 不能为空。 |
| `Py_XINCREF(obj)` | 增加 `obj` 的引用计数，`obj` 可以为空。 |
| `Py_XDECREF(obj)` | 减少 `obj` 的引用计数，`obj` 可以为空。 |

作为一般规则，除非出现以下情况，否则不需要担心担心引用计数：

- 如果你保存了以后使用的 Python 对象的引用，则必须增加引用计数。
- 同样，为了释放之前保存的对象，必须减少其引用计数。
- 如果你从 C 操作 Python 容器（列表、字典等），你可能需要手动操作各个项的引用计数。例如，获取或设置容器中项的高级操作通常会增加引用计数。

如果你的扩展导致解释器崩溃（你忘记增加引用计数），或者在使用扩展函数时解释器发生内存泄漏（你忘记减少引用计数），你就知道存在引用计数问题。

# 线程

全局解释器锁用于防止多个线程同时在解释器中执行。如果扩展中编写的函数执行时间很长，它将阻塞其他线程的执行直到其完成。这是因为每当调用扩展时都会锁定。如果扩展是线程安全的，可以使用宏来释放并重新获取全局解释器锁：

```c
Py_BEGIN_ALLOW_THREADS
```

释放全局解释器锁并允许其他线程在解释器中运行。在锁释放期间，C 扩展不得调用任何 Python C API 的函数。

```c
Py_END_ALLOW_THREADS
```

重新获取全局解释器锁。在这种情况下，扩展将阻塞直到成功获取锁。

# 第 26 章 扩展与嵌入 Python

以下示例展示了这些宏的使用：

```c
PyObject *py_wrapper(PyObject *self, PyObject *args) {
    ...
    PyArg_ParseTuple(args, ...);
    Py_BEGIN_ALLOW_THREADS
    result = run_long_calculation(args);
    Py_END_ALLOW_THREADS
    return Py_BuildValue(fmt, result);
}
```

# 嵌入 Python 解释器

Python 解释器也可以被嵌入到 C 应用程序中。通过嵌入，Python 解释器作为一个编程库运行，C 程序可以初始化解释器、让解释器运行脚本和代码片段、加载库模块，并操作用 Python 实现的函数对象。

## 一个嵌入模板

使用嵌入设备时，你的程序负责管理解释器。这里有一个简单的 C 程序，展示了最基本的嵌入方式：

```c
#include <Python.h>

int main(int argc, char **argv) {
    Py_Initialize();
    Py_RunString("print('Hello World')");
    Py_Finalize();
    return 0;
}
```

在这个示例中，初始化了一个嵌入设备，以字符串形式执行了一个短脚本，并关闭了解释器。在继续之前，通常先让示例运行起来是个好主。

## 编译与链接

要在 UNIX 上编译嵌入式解释器，你的代码必须包含 `"Python.h"` 头文件，并链接如 `libpython2.6.a` 这样的解释器库。头文件通常位于 `/usr/local/include/python2.6`，库通常位于 `/usr/local/lib/python2`。对于 Windows，你需要在 Python 安装目录中找到这些文件。请注意解释器可能依赖于链接时需要包含的其他库。遗憾的是，这通常具有平台特定性，并且取决于 Python 在你机器上的配置方式——你可能需要花时间寻找。

## 基本解释器操作与设置

以下函数用于设置解释器和运行脚本：

`PyRun_AnyFile(FILE *fp, char *filename)`

如果 `fp` 是类似 UNIX 中的交互式设备，该函数将调用 `PyRun_InteractiveLoop()`。否则，调用 `PyRun_SimpleFile()`，`filename` 是一个为输入流命名的字符串。当解释器报告错误时，该名称将出现。如果 `filename` 为 NULL，则使用默认字符串 "???" 作为文件名。

```c
int PyRun_SimpleFile(FILE *fp, char *filename)
```

与 `PyRun_SimpleString(char)` 类似，区别是程序是从 `fp` 读取的。

```c
int PyRun_SimpleString(char *command)
```

在解释器的 `__main__` 模块中执行命令。成功时返回 0，发生异常时返回 -1。

```c
int PyRun_InteractiveOne(FILE *fp, char *filename)
```

执行单条交互命令。

```c
int PyRun_InteractiveLoop(FILE *fp, char *filename)
```
