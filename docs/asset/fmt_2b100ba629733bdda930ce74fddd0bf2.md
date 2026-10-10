
Version 7.10.3077

Copyright (C) Microsoft Corporation. All rights \
reserved.

```
cl -nologologo -DXP_PUTENV=putenv -DWIN32 \
-WIN32_LEAN_AND_MEAN -D_DLL -D_MT -D_STDC_ \
-D_X86_ /c main.cpp
main.cpp
cl -nologologo -DXP_PUTENV=putenv -DWIN32 \
-WIN32_LEAN_AND_MEAN -D_DLL -D_MT -D_STDC_ \
/c bar.cpp
bar.cpp
```

```
if exist bar.exe del bar.exe
cl -Febar.exe -0 -nologologo -G4 -W2 main.obj \
msvcrt.lib kernel32.lib wsock32.lib -link \
-nodefault:lib
```

处理 `putenv()` 不同形式的复杂性现在都在 Makefile 中，需要做的只是在代码中使用 `XP_PUTENV` 代替 `putenv()`。

## 使用特定平台的 putenv 实现

另一种在 Makefile 中不使用 `#ifdef` 管理此问题的方法是创建一个包含 `putenv()` 特定平台实现的源文件，如果我们处于需要它的平台，则将此源文件添加到构建中。以下是该文件的源代码 `compatibility.cpp`，它包含了我们 Win32 的 `putenv()` 定义：

```cpp
#if defined(WIN32)
#include <stdlib.h>

int putenv(const char *envstring)
{
    return _putenv(envstring);
}
#endif
```

## 第2 章 构建系统/工具链

要在 `bar.cpp` 中使用 `putenv()`，我们还需要一个头文件，我将其命名为 `compatibility.h`：

```cpp
#if defined(WIN32)
int putenv(const char *envstring);
#endif
```

Makefile 的更改与上述之前的类似。这次，如果 `HasPutenv` 为 `NO` 且定义了 `Win32Architecture`，我们将 `compatibility.cpp` 添加到 `SRCS` 变量，并将 `compatibility.o` 添加到 `OBJS` 变量，从而将其添加到构建中：

```
SRCS = main.cpp bar.cpp
OBJS = main.o bar.o
#if !HasPutenv
#if defined(Win32Architecture)
SRCS = $(SRCS) compatibility.cpp
OBJS = $(OBJS) compatibility.o
#endif
```

`ComplexProgramTarget(bar)`

最后，我们在 `bar.cpp` 中包含 `compatibility.h`，该文件已被重写为调用 `putenv()`：

```cpp
#include <stdlib.h>
#include <stdio.h>
#include "bar.h"
#include "compatibility.h"
```

```cpp
Bar::Bar() : m_bar(0)
{
}
```

```cpp
Bar::~Bar()
{
}
```

```cpp
void Bar::SetBar(int bar)
{
  m_bar = bar;
}
```

## 第10 项：使用跨平台 Make 系统

```cpp
int Bar::PutBar()
{
    char buf[16];
    sprintf(buf, "BAR=%d", m_bar);
    return putenv(buf);
}
```

最后执行一次 `xmkmf`、`nmake clean` 和 `nmake bar.exe`，我们看到 `compatibility.cpp` 已添加到构建中，并且我们将无错误地链接：

```
c:\nmake bar.exe
```

Microsoft (R) Program Maintenance Utility \
Version 7.10.3077

Copyright (C) Microsoft Corporation. All rights \
reserved.

```
cl -nologo -DXP_PUTENV=putenv -DWIN32 \
-WIN32_LEAN_AND_MEAN -D_DLL -D_MT -D_STDC_ \
-D_X86_ /c main.cpp
main.cpp

cl -nologo -DXP_PUTENV=putenv -DWIN32 \
-WIN32_LEAN_AND_MEAN -D_DLL -D_MT -D_STDC_ \
/c bar.cpp
bar.cpp

cl -nologo -DXP_PUTENV=putenv -DWIN32 \
-WIN32_LEAN_AND_MEAN -D_DLL -D_MT -D_STDC_ \
-D_X86_ /c compatibility.cpp
compatibility.cpp
```

```
if exist bar.exe del bar.exe
cl -Febar.exe -0 -nologologo -G4 -W2 main.obj \
bar.obj compatibility.obj msvcrt.lib kernel32.lib wsock32.lib -link \
-nodefault:lib
```

## 106 第 2 章 构建系统/工具链

```
OBJS = $(OBJS) compatibility.o
#endif
#endif
ComplexProgramTarget(bar)
```

另一种密切相关的方法是提供每个平台的兼容性文件（例如 `WinCompatibility.cpp`、`OSXCompatibility.cpp` 和 `LinuxCompatibility.cpp`）。通过这种方式，我们只需要提供缺失函数的实现，消除了（或显著减少了）源码中任何形式的 #ifdef 需求，最重要的是，通常情况下已经不再需要为 `Putenv` 或其他的 Imake #define 编写测试。以下是一个采用这种方法的 Makefile：

```
SRCS = main.cpp bar.cpp
OBJS = main.o bar.o
#if defined(Win32Architecture)
SRCS = $(SRC) WinCompatibility.cpp
OBJS = $(OBJS) WinCompatibility.o
#endif
#if defined(LinuxArchitecture)
SRCS = $(SRC) LinuxCompatibility.cpp
OBJS = $(OBJS) LinuxCompatibility.o
#endif
#if defined(DarwinArchitecture)
SRCS = $(SRC) OSXCompatibility.cpp
OBJS = $(OBJS) OSXCompatibility.o
#endif
ComplexProgramTarget(bar)
```

`OSXCompatibility.cpp` 和 `LinuxCompatibility.cpp` 目前都为空，因为这两个平台都都提供了 POSIX 版本的 `putenv()`。在 `WinCompatibility.cpp` 中不再需要使用 #ifdef 了：

```
#include <stdlib.h>

int putenv(const char *envstring)
{
    return _putenv(envstring);
}
```

### 事项 10：使用跨平台 Make 系统

#### Imake 使用的文件

现在你已经对 Imake 有了初步了解，让我们列出到目前为止讨论过的 Imake 文件（以及一些我们尚未讨论过的）：

- `Imake.tmpl`：该文件不应修改，定义了 Imake 的默认值。例如：

```
#ifndef HasPutenv
#define HasPutenv NO //* 假设没有 */
#endif
```

- `Imake.rules`：该文件不应修改，包含了大部分规则宏（如 `ComplexProgramTarget`），你将在 Makefile 中使用它们。

- `Win32.cf`、`linux.cf`、`darwin.cf`：这些文件包含了平台特定的定义，会覆盖 `Imake.tmpl` 中指定的定义。与 `Imake.tmpl` 一样，你不应该修改这些文件。使用 `grep(1)`，我们可以看到许多平台特定的配置文件都覆盖了 `Imake.tmpl` 中指定的 `HasPutenv` 定义：
