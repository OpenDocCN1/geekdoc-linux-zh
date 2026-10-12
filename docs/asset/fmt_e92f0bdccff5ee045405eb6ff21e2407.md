
# 使用 C/C++ 嵌入和扩展 Python

这里是我们将在第一个示例中使用的 Makefile：

```make
# 用于 ebdmo.c 的演示 Makefile

VERSION= 1.5

CC= gcc

OPT= -O2

LIBS=-ld -lpthread -lieee

installalldir=/usr

exec installalldir=/usr

DEFS=-DHAVE_CONFIG_H

INCLUDEDIR=$(installalldir)/include

INCLUDEPY=$(INCLUDEDIR)/python$(VERSION)

EXECINCLUSDEPEY=$(installalldir)/include/python$(VERSION)

LIBPY=$(installalldir)/lib/python$(VERSION)

LIBPL=$(LIBPY)/config

PYTHONBS=$(LIBPY)/libpython$(VERSION).a

CFLAGS= $(OPT) -I$(INCLUDEPY) -I$(EXECINCLUSDEPEY) $(DEFS)

default: ebdmo

ebdmo: ebdmo.o

	$(CC) -o ebdmo ebdmo.o $(PYTHONBS) $(LIBS)

ebdmo.o: ebdmo.c

	$(CC) $(CFLAGS) -c ebdmo.c
```

你可能需要对系统上使用的目录路径进行调整。

# 使用高级函数嵌入 Python

你可以在 Python 文档中找到一个简单的嵌入示例；我们将从一个类似的示例开始，该示例简单地克隆了 Python 程序的功能，将所有命令行参数和标准输入 `stdin` 传递给 Python 解释器进行评估。

典型的宿程序按照以下顺序与解释器交互：

- 初始化 Python 解释器
- 初始化静态链接的扩展模块
- 执行主程序的体
- 完成 Python 解释器

`ebdmo.c` 的初始版本非常简单：

```c
/* ebdmo.c - 嵌入 Python 演示 */
#include <stdio.h>
#include "Python.h"

int main(int argc, char **argv) {
	int rc;
	Py_Initialize();
	rc = PyRun_AnyFile(stdin,"*?");
	Py_Finalize();
	return rc;
}
```

# 第 17 章

主函数调用 `Py_Initialize` 来初始化 Python 解释器。然后我们调用 `PyRun_AnyFile`，将 `stdin` 的文件句柄作为输入文件传递，并将文件名设置为字符串 `"??"`。

Python 解释器识别出输入文件是 `stdin`，并在交互模式下运行——只要满足以下任何条件，它就会这样做：

- 在传递的文件句柄上 `isat` 返回真值
- 文件名为 `NULL`、`"<stdin>"` 或 `""`；强制 Python 解释器在交互模式下运行，即使 `stdin` 是文件而不是终端。

`PyRun_AnyFile` 返回后，我们通过调用 `Py_Finalize` 关闭 Python 解释器，并返回 `main` 的返回码。

现在制作并执行该文件，你将看到：

```
$ make
gcc -g02 -I/usr/include/python1.5 -I/usr/include/python1.5 -DHAVE_CONFIG_H -cbdemo.c
gcc -o ebdemo ebdemo.o /usr/lib/python1.5/config/libpython1.5.a -ldl -lpthread
$ ebdemo
>>> import sys.path
>>> print sys.path
['/usr/lib/python1.5/', '/usr/lib/python1.5/plat-linux-1386',
 '/usr/lib/python1.5/lib-tk', '/usr/lib/python1.5/lib-dynload',
 '/usr/lib/python1.5/site-packages']
>>> print sys.argv
Traceback (innermost last):
 File "???", line 1, in ?
AttributeError: name 'argv'
$ $
```

如所预期，Python 解释器在交互模式下运行。

从上述交互示例中有三个重要的点需要注意：

- 在解释器提示符处按 `D` `Ctrl-D` 会导致 Python 解释器退出并返回 `ebdemo` 程序。
- `sys.path` 的 Python 路径中不包含当前工作目录。当我们不带任何参数执行 Python 程序时，Python 会将执行程序的目录说明（如果有）插入 `sys.path` 中。在 `ebdemo` 示例中，我们没有告诉 Python 程序名称是什么，因此执行文件的路径没有包含在 `sys.path` 中。
- `sys.argv` 没有被设置，因为 `ebdemo` 示例没有设置它。

我们可以通过对 `ebdemo.c` 进行以下更改来修复这些问题：

```c
Py_SetProgramName(argv[0]);
Py_Initialize();
PySys_SetArgv(argc, argv);
rc = PyRunAnyfile(stdin, "???");
```

我们添加了对 `Py_SetProgramName` 的调用，将 `argv[0]` 作为程序名传递；这必须在调用 `Py_Initialize` 之前。我们还添加了对 `PySys_SetArgv` 的调用，传递当前的 `argc` 和 `argv` 变量。我们可以通过重新构建 `ebdemo.c` 并执行它来测试我们的更改：

```
$ ./ebdemo
>>> print sys.path
['', '/usr/lib/python1.5/', '/usr/lib/python1.5/plat-linux-i386', '/usr/lib/python1.5/lib-tk', '/usr/lib/python1.5/lib-dynload', '/usr/lib/python1.5/site-packages']
>>> print sys.argv
['ebdemo']
>>> D
```

有多个高级函数可用于执行、解析字符串或执行文件。请查看 Python 文档。

# 静态链接宿程序到扩展模块

高级 Python API 使嵌入快速且容易；但大多数宿应用程序需要对它们的脚本进行更多的控制。宿程序可以通过创建自己的模块并定义一组函数来实现扩展。使用这种功能，Python 脚本可以回调宿主机以获取或提供信息。

Python C API 还允许宿程序调用模块中的单个函数、调用实例方法并操作字典。这种功能提供了比高级函数更细致的执行控制。

# 使用低级调用嵌入 Python

我们将现在演示一些低级 C API 函数。

# 执行字符串

让我们修改 `ebdemo.c` 以增加更多功能：

```c
Py_SetProgramName(argv[0]);
Py_Initialize();
initsinfo();
if (argc < 2) {
    Py_SetArgv(argc, argv);
    rc = PyRun_AnyFile(stdin, "???");
} else {
    Py_SetArgv(argc-1, argv+1);
```
