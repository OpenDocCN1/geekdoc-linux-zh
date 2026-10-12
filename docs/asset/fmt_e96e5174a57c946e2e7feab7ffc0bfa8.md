
`int simple_math_ipow(int x, int y);`

在`mytest.c`顶部添加行`#include "simple_math.h"`：

```c
#include <stdlib.h>

#include <stdio.h>

#include "simple_math.h"
```

此项的添加消除了关于函数隐式声明的警告信息。通常会使用`#include <simple_math.h>`，但在这里，它是当前目录下的头文件——我们自己的头文件——因此我们在这里使用`"simple_math.h"`而不是`<simple_math.h>`。

如果你对其中一个文件做了微小的改动（因为你可能经常这样做）会怎样？你可能经常需要编译和链接，但脚本会构建所有内容，而不仅仅是更改的文件。我们真正需要的是一个只重新编译源文件的工具：`make`就是一个在当前目录查找`Makefile`并执行编译和链接的程序。`Makefile`包含了描述如何构建程序的规则和依赖关系。

### 22.4.1 完成我们的 Makefile

编译过程的第一个依赖项是`mytest`依赖于库`simple_math.a`和对象文件`mytest.o`。在`make`中我们创建：

```makefile
mytest: libsimple_math.a mytest.o

	gcc -Wall -o $@ -L. -lsimple_math
```

```makefile
libsimple_math.a: simple_math_sqrt.o simple_math_pow.o

	rm -f $@

	ar rc $@ $^

	ranlib $@

simple_math_sqrt.o simple_math_pow.o: %.c

	gcc -Wall -c $@ -o $<
```

```makefile
clean:

	rm -f *.o *.a mytest
```

### 22.4.2 整合

`Makefile`可以以任何顺序排列规则，但为了可读性，最好先说明明显的规则。还有一个你应该在开头说明的规则：

```makefile
# 注释以 # 字符开始，类似于脚本

# 构建 libsimplemath.a 和 mytest 程序的 Makefile

# Paul Sheer <psheer.co.za> 2000年3月19日星期日 15:56:08

OBJS = simple_math_sqrt.o simple_math_pow.o

LIBNAME = simple_math

CFLAGS = -Wall

all: lib$(LIBNAME).a mytest

mytest: lib$(LIBNAME).a mytest.o

	cc $(CFLAGS) -o $@ mytest.o -L. -l$(LIBNAME)

$(LIBNAME).a: $(OBJS)

	rm -f $@

	ar rc $@ $^

	ranlib $@

%.o: %.c

	cc $(CFLAGS) -c $@ -o $<

clean:

	rm -f *.o *.a mytest
```

现在我们可以在当前目录输入

```bash
make
```

导致所有内容被构建。你可以看到我们添加了一个额外的独立的目标`clean:`。目标可以这样显式地在命令行上运行：

```bash
make clean
```

这会删除所有构建的文件。

## 第 23 章 共享库

本章紧接我们在第 22 章中对静态`.a`库的构建。它讨论了动态链接库（DLL）的创建和安装。在这里，我将向你展示这两种方法，以便你对 DLL 在 UNIX 上的工作原理有一个良好的技术概述。随后，你可以迅速忘记下面讨论的`ldconfig`和`LD_LIBRARY_PATH`以外。

`.a`库文件适用于创建许多程序可以包含的函数。这种做法被称为代码复用。但请注意第 22 章中`.a`文件是如何链接（包含）到可执行文件`mytest`中的。`mytest`的体积由于`simple-math.a`的存在而增大。当数百个程序使用同一个`.a`文件时，这些代码实际上在整个文件系统中重复了。这种低效率在 LINUX 出现很久就被认为是不可接受的，因此发明了库文件，它们只在程序运行时与程序链接——这一过程被称为动态链接。而不是`.a`文件，`.so`（共享对象）文件存储在`/lib/`和`/usr/lib/`中，并在程序运行时自动链接到程序。

### 23.1 创建 DLL .so 文件

创建 DLL 需要对第 232 页的`Makefile`进行几处修改：

```makefile
OBJS = simple_math_sqrt.o simple_math_pow.o

LIBNAME = simple_math

SONAME = libsimple_math.so.1.0.0

SOVERSION = libsimple_math.so.1.0

CFLAGS = -Wall
```

```makefile
all: lib$(LIBNAME).so mytest
```

### 23.2 DLL 版本控制

```makefile
mytest: lib$(LIBNAME).so

	gcc $(CFLAGS) -o $@ mytest.o -L. -l$(LIBNAME)

lib$(LIBNAME).so: $(OBJS)

	gcc -shared $(CFLAGS) $(OBJS) -lc -Wl,-soname,$(SOVERSION) \
		-o $(SONAME) && \
		ln -sf $(SONAME) $(SOVERSION) && \
		ln -sf $(SONAME) lib$(LIBNAME).so

%.o: %.c

	gcc -fPIC -DPIC $(CFLAGS) -c -o $@ $<

clean:

	rm -f *.a *.so mytest
```

`gcc`的`-shared`选项构建了我们的共享库。`-W`选项是链接器选项，用于设置程序在运行时加载的库的版本号。`-fPIC -DPIC`意味着生成位置无关代码，即适用于动态链接。

运行后我们得到了：

```bash
lrwxrwxrwx 1 root root 23 Sep 17 22:02 libsimple_math.so.1 -> libsimple_math.so.1.0.0

lrwxrwxrwx 1 root root 23 Sep 17 22:02 libsimple_math.so.1.0 -> libsimple_math.so.1.0.0

-rwxr-xr-x 1 root root 6056 Sep 17 22:02 libsimple_math.so.1.0.0

-rwxr-xr-x 1 root root 1367 Sep 17 22:02 mytest
```

你可能会观察到，我们的三个`.so`文件与`/lib/`和`/usr/lib/`中的许多文件相似。这种复杂的链接和符号链接系统是库版本控制过程的一部分。虽然生成 DLL 超出了系统管理任务的范围，但理解库版本控制是非常重要的。

DLL 存在一个问题。考虑一个过时或有 Bug 的 DLL：仅用更新后的文件覆盖 DLL 文件将影响所有使用它的应用程序。如果这些应用程序依赖于 DLL 代码的某些行为，那么它们在使用新的 DLL 时可能会崩溃。UNIX 通过允许同时存在多个版本的 DLL 优雅地解决了这个问题。程序本身已经将它们所需的版本号构建在内部。

下列命令将显示`mytest`计划链接的 DLL 文件：

```bash
ldd mytest
```

```text
libsimple_math.so.1.0 => /lib/simple_math.so.1.0 (0x40018000)
```

```text
libc.so.6 => /lib/libc.so.6 (0x40022000)

lib/ld-linux.so.2 => /lib/ld-linux.so.2 (0x40000000)
```
