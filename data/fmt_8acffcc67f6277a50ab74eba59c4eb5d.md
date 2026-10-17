
注意，`make` 只重新构建了 `main.o` 和 `bar` 目标，这是预期结果，因为这些是受 `main.cpp` 变化影响的目标。

# 项目 10：使用跨平台 Make 系统

然而，仍然存在两个问题：编译器和命令行参数仍然是硬编码的。这些问题可以通过示例中的宏来解决：

```
OBJS = bar.o main.o
CXXFLAGS = -g
```

```
bar: $(OBJS)
$(CXX) $(CXXFLAGS) -o $$ $(OBJS)
```

```
bar.o: main.cpp bar.h
$(CXX) $(CXXFLAGS) -c bar.cpp
```

```
main.o: main.cpp bar.h
$(CXX) $(CXXFLAGS) -c main.cpp
```

通过注意到 `.o` 文件的唯一依赖是其对应的 `.cpp` 文件和 `bar.h`，并使用额外的 `make` 功能（如模式规则），我们可以进一步简化 `Makefile` 并改进此文件：

```
OBJS = bar.o main.o
CXXFLAGS = -g
```

```
bar: $(OBJS)
$(CXX) $(CXXFLAGS) -o $$ $(OBJS)
```

```
%.o : %.cpp
$(CXX) $(CXXFLAGS) -c $$
```

```
$(OBJS) : bar.h
```

我们改进了一些事情，但仍然存在一些问题。将 `-g` 从命令中提取并将其放入名为 `CXXFLAGS` 的宏中是一个巨大的改进，但它仍然硬编码在 `Makefile` 中，更糟糕的是，它与编译器解耦了：如果 `make` 将 `CXX` 设置为 `g++` 的其他值，`-g` 标志的含义可能与传递给 `g++` 时完全不同，或者可能没有任何意义。

# 在 Windows 上构建

让我们看看将 `Makefile` 和源代码移动到 Windows 然后尝试构建程序会发生什么。为了便于讨论，我们假设 Windows 系统上没有安装 Cygwin。

首先，尝试输入 `make` 看看会发生什么：

```
C:\make
'make' is not recognized as an internal or external command.
```

这显然告诉我们 `make` 不可用，这并不意外，因为 `make` 不是 Windows 原生的，且没有安装 Cygwin。在这一点上，我们可以做两件事来克服这个障碍。安装 Cygwin 将为我们提供 GNU `make` 的副本，有了 GNU `make`，我们将获得在 Mac OS X 或 Linux 上看到的相同结果。然而，让我们尝试第二个选项，调用微软的 `nmake` 实用看看会发生什么：

```
C:\nmake -f Makefile
Microsoft (R) Program Maintenance Utility \
Version 6.00.8168.0
Copyright (C) Microsoft Corp 1988-1998. \
All rights reserved.
```

```
cl -g -o bar bar main.o
Microsoft (R) 32-bit C/C++ Optimizing Compiler \
Version 12.00.8804 for 80x86
Copyright (C) Microsoft Corp 1984-1998. \
All rights reserved.
```

```
Command line warning D4002 : \
ignoring unknown option '-g'
Command line warning D4024 : \
unrecognized source file type 'bar.o', object file
```

```
Command line warning D4024 : unrecognized source \
file type 'main.o', object file
```

```
Microsoft (R) Incremental Linker Version 6.00.8447
Copyright (C) Microsoft Corp 1992-1998. \
All rights reserved.
```

```
/out:bar.exe
/out:bar.exe
bar.o
main.o
LINK : fatal error LNK1181: \
cannot open input file "bar.o"
MAKE : fatal error U1077: 'cl' : return code '1'
Stop.
```

如你所见，微软 `make` 不识别 `.o` 文件，也不识别 `-g` 标志。然而它确实为 `CXX` 宏提供了一个合理的值。让我们重写 `Makefile` 以更好地适应 `nmake` 和 Windows 平台：

```
OBJS = bar.obj main.obj
CXXFLAGS = /Zi

bar: $(OBJS)
$(CXX) $(CXXFLAGS) $(OBJS)

%.obj : %.cpp
$(CXX) $(CXXFLAGS) -c $<

$(OBJS) : bar.h
```

在这里，我更改了 `OBJS` 的值以反映 Microsoft C++ 使用的不同后缀，并将 `CXXFLAGS` 宏更改为 `/Zi`，这是 Microsoft C++ 对 `-g` 标志的版本。输入 `nmake`，我们得到了如下输出：

```
C:\dev\make -f Makefile
Microsoft (R) Program Maintenance Utility \
Version 6.00.8168.0
Copyright (C) Microsoft Corp 1988-1998. \
All rights reserved.
```

```
cl /c bar.cpp
Microsoft (R) 32-bit C/C++ Optimizing Compiler \
Version 12.00.8804 for 80x86
Copyright (C) Microsoft Corp 1984-1998. \
All rights reserved.
```

```
bar.cpp(22) : error C265: 'setenv' undeclared identifier
MAKE : fatal error U1077: 'cl' : return code '1'
Stop.
```

如你所见，微软 `make` 不识别 `.o` 文件，也不识别 `-g` 标志。然而它确实为 `CXX` 宏提供了一个合理的值。为了解决这些问题，让我们重写 `Makefile` 以更好地适应 `nmake` 和 Windows 平台：

```
OBJS = bar.obj main.obj
CXXFLAGS = /Zi

bar: $(OBJS)
$(CXX) $(CXXFLAGS) $(OBJS)

%.obj : %.cpp
$(CXX) $(CXXFLAGS) -c $<

$(OBJS) : bar.h
```

在这里，我更改了 `OBJS` 的值以反映 Microsoft C++ 使用的不同后缀，并将 `CXXFLAGS` 宏更改为 `/Zi`，这是 Microsoft C++ 对 `-g` 标志的版本。输入 `nmake`，我们得到了如下输出：

```
C:\dev\make -f Makefile
Microsoft (R) Program Maintenance Utility \
Version 6.00.8168.0
Copyright (C) Microsoft Corp 1988-1998. \
All rights reserved.
```

```
cl /c bar.cpp
Microsoft (R) 32-bit C/C++ Optimizing Compiler \
Version 12.00.8804 for 80x86
Copyright (C) Microsoft Corp 1984-1998. \
All rights reserved.
```

```
bar.cpp(22) : error C265: 'setenv' undeclared identifier
MAKE : fatal error U1077: 'cl' : return code '1'
Stop.
```

如你所见，微软 `make` 不识别 `.o` 文件，也不识别 `-g` 标志。然而它确实为 `CXX` 宏提供了一个合理的值。为了解决这些问题，让我们重写 `Makefile` 以更好地适应 `nmake` 和 Windows 平台：

```
OBJS = bar.obj main.obj
CXXFLAGS = /Zi

bar: $(OBJS)
$(CXX) $(CXXFLAGS) $(OBJS)

%.obj : %.cpp
$(CXX) $(CXXFLAGS) -c $<

$(OBJS) : bar.h
```
