
```
cd lib
"making" all in ./lib...
namake -nologo -CDEBUGFLAGS="-O" all
cd compat
"making" all in ./lib/compat...
namake -nologo -CDEBUGFLAGS="-O" all
cd c1 nologo -DWIN32 -DWWIN32_LEAN_AND_MEAN \
-D_X86_ /c WinCompatibility.cpp
WinCompatibility.cpp
```

NMAKE: fatal error U1073: don't know how to make \

'COMPAT-def.cpp'

Stop.

NMAKE: fatal error U1077: \

"c:\Program Files\Microsoft Visual Studio .NET 2003 \

VC7\BIN\nmake.exe" : return code '0x2'

Stop.

NMAKE: fatal error U1077: \

"c:\Program Files\Microsoft Visual Studio .NET 2003

## 126 第 2 章 构建系统/工具链

```
VC7\nmake.exe'' : return code '0x2'
Stop.
MAKE : fatal error U1077: \
""c:\Program Files\Microsoft Visual Studio .NET 2003\
VC7\nmake.exe" : return code '0x2'
Stop.
MAKE : fatal error U1077: \
""c:\Program Files\Microsoft Visual Studio .NET 2003\
VC7\nmake.exe" : return code '0x2'
Stop.
```

上述输出的最后几行表示遇到了错误。为了更好地理解这个错误，让我们查看用于 `Win32.rules` 中创建共享库的规则部分：

```
#define SharedLibraryTarget(libname,rev,solist,def,up)
@@
AllTarget(libname.dll) @@@
@@
CppFileTarget(libname.def,libname-def.cpp,\n-LIBRARY_VERSION=rev,$(CONFIGFILES)) @@@
@@
XARdef0 = soloist@@@
@@
LibraryTargetName(libname): $(XVARuse0:o=.obj) \
libname.def($0) @@@
@@
RemoveFile($0,-def:libname.def) @@@
MakeLibrary($0,-def.def $(XVARuse0:o=.obj)) @@@
LinkBuildLibrary($0) @@@
```

如你所示，`CppFileTarget` 规则添加了一个目标，其名称通过连接 `LibName` 中指定的 `COMPAT` 和后缀 `.def` 形成。这是一个标准的 Windows def 文件，提供了关于库及其导出符号的信息，并在创建共享库时需要它。该目标的名称是 `def.cpp`。由于我们没有名为 `COMPAT-def` 的源文件，构建失败了。为了解决这个问题，我们需要在 `compat` 目录下提供一个如下内容的 `COMPAT-def` 文件：

```
LIBRARY COMPAT
VERSION 1.0
PORTS
```

该文件的结构非常简单。第一行提供库的名称，第二行提供库的版本。`PORTS` 行之后是共享库导出的函数列表。在创建此文件后，我们可以最后执行一次 `nmake`：

```
C:\src\nmake
```

Microsoft (R) Program Maintenance Utility \

Version 7.10.3077

Copyright (C) Microsoft Corporation. All rights \

reserved.

```
cd lib
"making" all in ./lib...
namake -nologo -CDEBUGFLAGS="-O" all
cd compat
"making" all in ./lib/compat...
namake -nologo -CDEBUGFLAGS="-O" all
cd c1 nologo -DWIN32 -DWWIN32_LEAN_AND_MEAN \
-D_X86_ /c WinCompatibility.cpp
WinCompatibility.cpp
```

## 事项 10：使用跨平台 Make 系统

-I./.././config/cf -DTOPDIR=../../ -DCDIR=

./lib/compat

Imakefile.c

```
nmake -nologo -L      Makefiles
cd
cd
cd app
if exist Makefile.bak del Makefile.bak
..\..\config\Imake -I..../config/cf \
-DTOPDIR=../.. -DCDIR=/app
```

Imakefile.c

```
nmake -nologo -L      Makefiles
cd bar
if exist Makefile.bak del Makefile.bak
..\..\config\Imake -I..../config/cf \
-DTOPDIR=../../.. -DCDIR=../bar
```

Imakefile.c

```
nmake -nologo -L      Makefiles
cd
cd
```

```
C:\src>nmake
```

Microsoft (R) Program Maintenance Utility \

Version 7.10.3077

Copyright (C) Microsoft Corporation. All rights \

reserved.

```
cd lib
"making" all in ./lib...
namake -nologo -CDEBUGFLAGS="-O" all
cd compat
"making" all in ./lib/compat...
namake -nologo -CDEBUGFLAGS="-O" all
cd c1 nologo -DWIN32 -DWWIN32_LEAN_AND_MEAN \
-D_X86_ /c WinCompatibility.cpp
WinCompatibility.cpp
```

NMAKE: fatal error U1073: don't know how to make \

'COMPAT-def.cpp'

Stop.

NMAKE: fatal error U1077: \

"c:\Program Files\Microsoft Visual Studio .NET 2003 \

VC7\BIN\nmake.exe" : return code '0x2'

Stop.

NMAKE: fatal error U1077: \

"c:\Program Files\Microsoft Visual Studio .NET 2003

## 126 第 2 章 构建系统/工具链

```
VC7\nmake.exe'' : return code '0x2'
Stop.
MAKE : fatal error U1077: \
""c:\Program Files\Microsoft Visual Studio .NET 2003\
VC7\nmake.exe" : return code '0x2'
Stop.
MAKE : fatal error U1077: \
""c:\Program Files\Microsoft Visual Studio .NET 2003\
VC7\nmake.exe" : return code '0x2'
Stop.
```

上述输出的最后几行表示遇到了错误。为了更好地理解这个错误，让我们查看用于 `Win32.rules` 中创建共享库的规则部分：
