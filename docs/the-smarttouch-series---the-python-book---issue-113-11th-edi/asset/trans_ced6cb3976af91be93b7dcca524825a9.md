

## 在 C 语言中嵌入 Python

在这里，我们将学习如何在常规的 C 程序中调用 Python 代码，从而兼得两者之长。

在 C 程序中，有时你可能需要执行一段 Python 代码。例如，你可能希望程序能够运行用户代码，这样用户可以利用插件来扩展程序的功能。实现这一目标的方式就是将 Python 嵌入到 C 程序中。

我们将探讨如何嵌入 Python，如何运行你的 Python 代码，以及如何与你设置的 Python 解释器进行交互。这是 Python 本身内置的功能，因此除了 Python 开发包和 GCC 之外，你不需要在树莓派上安装任何额外的东西。你需要使用以下命令来安装它们：

```bash
sudo apt-get install python-dev gcc
```

现在，你应该已经拥有了编译代码所需的所有工具。

第一步是启动解释器。为了访问你需要的函数，你必须在 C 源代码文件的头部添加以下行：

```c
#include <Python.h>
```

现在你可以开始嵌入 Python 了。你需要第一个函数是 `void Py_Initialize()`。在初始化解释器之前，可以调用的其他函数只有 `Py_SetProgramName()`、`Py_SetPythonHome()`、`PyEval_InitThreads()`、`PyEval_ReleaseLock()` 和 `PyEval_AcquireLock()`。一旦该函数执行完毕，你就可以开始与此解释器交互了。这会启动解释器，并加载核心模块 `__builtin__`、`__main__` 和 `sys`。那么其他模块呢？你可以使用函数 `void Py_SetPythonHome(char *home)` 来设置搜索路径，解释器将在该路径下查找模块。如果你需要相关信息，可以使用函数 `char* Py_GetPythonHome()` 来获取当前的模块路径。

它不会设置 `sys.startup`，但你z需要使用函数 `void Py_Sys_SetArgv(int argc, char **argv, int updateargv)`。这样你就可以访问 Python 代码所需的任何命令行参数。你可以使用函数 `int Py_IsInitialized()` 来检查解释器是否已正确初始化。它返回一个整数，表示真（非零）或假（零）。

使用新解释器的最简单方法是使用函数 `int PyRun_SimpleString(const char *command)`。该函数接受一个包含任意代码片段的字符串。如果你有 multiple 行想要运行的代码，可以使用换行符来分隔这些行。例如，你可以打印某个角度的正弦值：

```c
PyRun_SimpleString("import math\na = math.sin(45)\nprint('The sine of 45 is ' + a)");
```

该函数是 `int PyRun_SimpleStringFlags(const char *command, PyObject*flags *flags)` 的简化版本。这不仅接受命令字符串，还接受 Python 编译器的编译器标志结构体。你需要查阅在线的开发文档以查看这些编译器标志的细节。假设你有一段更复杂的代码需要执行。处理 Python 脚本文件也有相应的函数。简化版本是 `int PyRun_SimpleFile(FILE *fp, const char *filename)`。你实际上需要提供两个对脚本的引用。第一个是通过 C 函数 `fopen()` 打开脚本文件得到的文件句柄，第二个是你刚打开的脚本名称。

你需要以读权限打开脚本文件。现在你还需要担心你的程序在文件系统上是否具有正确的文件权限来打开此脚本。规范的编程要求你应该检查对 `fopen()` 的调用，以验证其是否完成并返回了有效的文件句柄。这个简化版本不使用任何编译器标志，并在函数返回后关闭文件句柄。该函数的完整版本是 `int PyRun_SimpleStringFlags(FILE *fp, const char *filename, int closeit, Py_CompilerFlags *flags)`。如果 `closeit` 为真，则关闭文件句柄。如果脚本是你希望多次运行的一次，请将 `closeit` 设置为假，以便文件句柄保持打开状态。你可以在标志结构体中为 Python 解释器设置任何标志，类似于 `PyRun_SimpleStringFlags()` 函数调用。

如果这种简单的运行代码方式不够强大，还有更直接的方式与解释器交互。第一步是学习如何在 Python 解释器和 C 程序主体之间往返发送数据。基本工作流程是将你的 C 变量转换为它们的 Python 等价物，然后调用你想使用的 Python 函数，并将 Python 结果转换回 C 中的等价物。Python 是一种面向对象的语言，因此与解释器通信的核心在于 `Py_Object` 构造。它为你可以用来与 Python 通信的所有其他类型对象提供了基础。例如，创建一个 Python 字符串对象：

```c
PyObject *pName;
pName = PyString_FromString("print('Hello World')");
```

然后，你可以在使用 Python 函数时使用这个 Python 对象。你也可以从 C 代码中访问 Python 函数。你将函数存储在 `PyObject` 中作为引用，就像处理数据对象一样。第一步是通过以下代码获取相关模块的函数名字典：

```c
my_module = PyImport_ImportModule("__main__");
my_dict = PyModule_GetDict(my_module);
```

一旦你有了字典，你就可以通过以下方式获取特定函数的引用：

```c
my_func = PyDict_GetItemString(my_dict, func_name);
```

执行完此操作后，你会发现当 `func_name` 是包含你想要访问的函数的字符串时，你可以使用如下命令来运行该函数：

## Python 基础

### 扩展你的 Python

了解如何对发布 APK 进行数字签名并将其上传到你选择的应用商店。

使用 Python 解释器时，你并不局限于现有可用的功能；你可以在 C 代码中定义拥有自己方法和数据的 Python 对象来扩展可用功能。然后，这些新创建的对象可以从 Python 解释器内部调用。它们被定义为静态对象，代码如下：

```c
static PyObject* my_func(PyObject *self, PyObject *args) {
...
}
```

新的 `PyObject` 包含用于新对象的方法的可执行代码。你还需要创建一个方法定义，以便能够向 Python 解释器注册详细信息。你通过创建一个 `PyMethodDef` 数组来实现这一点：

```c
static PyMethodDef my_methods[] = {
  {"my_method", my_func, METH_VARARGS, "This is my method"},
  (NULL, NULL, 0, NULL)
};
```

完成这两部分后，你几乎就可以开始使用新的模块代码了。你需要使用以下函数对其进行初始化：

```c
Py_InitModule("my_module", my_methods);
```

现在，你可以像在系统中安装的其他任何模块一样，在 Python 代码中导入这个新模块。在你的 Python 代码中，你可以编写：

```python
import my_module
my_module.my_method()
```

需要注意的是，这种程度的控制也带来了巨大的责任。例如，你需要开始担心对象的引用计数等问题。解释器的垃圾收集器需要知道何时可以删除对象，每次有东西指向你新创建的对象时，你需要递增引用计数。每次移除一个引用时，你需要递减计数器。

你还可以在单个程序中创建多个子解释器。你可以使用函数 `Py_NewInterpreter()` 创建一个新的子解释器。这样，你可以让多个 Python 线程并发运行，并且基本上相互独立。完成后，你可以使用函数 `Py_EndInterpreter()` 关闭它们。利用所有这些功能，你能做的事情没有极限。

到目前为止，我们一直在具体查看与 Python 解释器交互的代码。但有时，你希望让最终用户能够访问解释器。在这些情况下，你可能希望给用户提供一个完整的 Python 控制台。你可以使用函数调用 `Py_Main(argc, argv)` 来做到这一点，其中你传递来自 C 程序部分的 `argc` 和 `argv`。这对于基于控制台的程序来说没问题，但对于 GUI 程序，你需要创建某种终端窗口以允许用户与 Python 解释器交互。这个控制台会自动继续运行，直到用户明确退出 Python。你需要做的最后一件事是清理解释器。你可以使用函数 `void Py_Finalize()` 来完成。该函数的主要问题是它以随机顺序销毁对象。如果它们依赖于其他对象，可能无法正确清理。如果你随后再次尝试重新初始化解释器，由于最终的清理步骤不干净，它可能会失败。

现在你已写好程序，你需要编译它。你需要包含标志以告诉编译器在哪里找到所有内容。幸运的是，你可以从 Python 本身获取这些标志。编译所需的标志可以通过命令 `python-config --cflags` 获取。你还需要知道在哪里找到要链接的库，这可以通过 `python-config --ldflags` 获取。完成所有这些之后，你将可以在任何地方访问 Python，即使是在另一个程序中。

## 代码列表

```c
/* A simple way to run Python code */
#include <Python.h>

int main(int argc, char *argv[])
{
    Py_SetProgramName(argv[0]);
    /* Initialize the Python interpreter */
    Py_Initialize();
    /* Run your SimpleString */
    PyRun_SimpleString("import time\nprint('Today is ',ctime(time()))\n");
    /* Don't forget to clean up */
    Py_Finalize();
    return 0;
}
```

```c
/* You can create an interactive Python console */
#include <Python.h>
int main(int argc, char *argv[])
{
    Py_Initialize();
    Py_Main(argc, argv);
    Py_Finalize();
}
```

```c
/* You can even run a script file */
#include <Python.h>
int main(int argc, char *argv[])
{
    FILE *fp;
    Py_Initialize();
    fp = fopen("my_script.py", "r");
    PyRun_SimpleFile(fp, "my_script.py");
    Py_Finalize();
    fclose(fp);
}
```

## 为什么选择 Python

它是树莓派的官方语言。请在 python.org/doc 阅读文档。

