
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

如你所示，`CppFileTarget`规则添加了一个目标，其名称通过连接`LibName`中指定的`COMPAT`和后缀`.def`形成。这是一个标准的 Windows def 文件，提供了关于库及其导出符号的信息，并在创建共享库时需要它。该目标的名称是`def.cpp`。由于我们没有名为`COMPAT-def`的源文件，构建失败了。为了解决这个问题，我们需要在`compat`目录下提供一个如下内容的`COMPAT-def`文件：

```
LIBRARY COMPAT
VERSION 1.0
PORTS
```

该文件的结构非常简单。第一行提供库的名称，第二行提供库的版本。`PORTS`行之后是共享库导出的函数列表。在创建此文件后，我们可以最后执行一次`nmake`：

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

## 第 2 章 构建系统/工具链

`if exist COMPAT.dll del COMPAT.dll`

`link @C:\DOCUME-1\PREFER-1\Temp\nm429C.tmp`

Microsoft (R) Incremental Linker \

Version 7.10.3077

Copyright (C) Microsoft Corporation. All rights \

reserved.

```
-dll -out:COMPAT.dll del WinCompatibility.obj \
msvcrit.lib kernel32.lib wsock32.lib -link \
-nodefaultlib:libc
LINK : warning NLK4044: unrecognized option '/link'; \
ignored
..\..\config\mkdir ..\..\bin
if exist ....\dist\bin\COMPAT.dll del
..\..\dist\bin\COMPAT.dll
cd ....\dist\bin && copy ....\lib\ncompat.dll
1 file(s) copied.
cd
cd
cd app
"making" all in ..app/...
make -nologo - CDEBUGFLAGS="-O" all
cd bar
"making" all in ..app/bar/...
make -nologo -L CDEBUFLAGS="-O" all
cl -nologo -I../../../include -0 -DWIN32 \
WIN32_LEAN_AND_MEAN -D_X86_ /c main.cpp
cl -nologo -I../../../include -0 -DWIN32 \
WIN32_LEAN_AND_MEAN -D_X86_ /c bar.cpp
if exist bar.exe del bar.exe
cl -aro.exe -nologo -G4 -W2 main.obj \
bar.obj ..//dist/compat.lib msvcrit.lib \
kernel32.lib wsock32.lib -link -nodefaultlib:libc
cd
cd ..
```

到目前为止，一切看起来良好。我们进入`compat`，构建了一个名为`COMPAT.dll`的库，它被复制到项目根目录下的`dist\bin`目录，然后进入`app`并构建应用程序，将其链接到兼容库。现在剩下的是将

## 事项 10：使用跨平台 Make 系统

`bar`应用程序安装到`dist\bin`目录。可以通过输入`nmake install`完成：

```
C:\src-makefile install
```

Microsoft (R) Program Maintenance Utility \

Version 7.10.3077

Copyright (C) Microsoft Corporation. All rights \

reserved.

```
cd lib
"installing" all in ./lib...
nmake -nologo DESTDIR= install
cd compat
"installing" all in ../lib/compat...
nmake -nologo -L DESTDIR=..\..\dist\lib
..\..\configmkdir ..\..\dist\lib
copy COMPAT.lib ..\..\dist\lib\\"
```

```
1 file(s) copied.
..\..\configmkdir ..\..\dist\bin
copy COMPAT.dll ..\..\dist\bin\\
COMPAT.dll
```

```
1 file(s) copied.
"installing" in ../lib/compat done"
cd
..
cd
..
cd app
"installing" all in ../app/...
nmake -nologo DESTDIR= install
cd bar
"installing" all in ../app/bar/...
nmake -nologo -L DESTDIR=..\..\dist\bin
..\..\configmkdir ..\..\dist\bin
copy bar.exe ..\..\dist\bin\bar.exe
1 file(s) copied.
```

```
"installing" in ../app/bar done"
cd
..
```

如你所示，Imake 访问了`lib\compat`和`app\bar`，在这些目录中每一个运行了`nmake install`。在`compat`中进行的 make 是多的，因为 dll 和 lib 文件在之前构建它们时已经安装了。

# 130 第2章 构建系统/工具链

在安装阶段执行的重要工作发生在访问 app\bar 时，此时`nmake install`会将`bar.exe`文件复制到 dist。如果你访问 dist 并输入`dir`，你将看到以下内容：

```
C:\src>cd dist\bin
C:\src\dist\bin>dir
Volume in drive C is PRESARIO
Volume Serial Number is ECA4-3E20
```

Directory of C:\src\dist\bin

+   01/17/2004 09:36 PM    <DIR>

01/17/2004 09:36 PM    <DIR>

01/17/2004 09:36 PM            3,584 bar.exe

                              11,776 COMPAT.dll

                          2 File(s)         15,360 bytes

                          2 Dir(s)    86,027,062 bytes

## 构建 Debug 版本
