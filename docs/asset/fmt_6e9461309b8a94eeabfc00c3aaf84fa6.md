
```cpp
cout << "Directory opened successfully!";

closedir(dir);

} else

cout << "Couldn't open directory\n";

}
```

该程序演示了一个基于 STL (`iostream`) 和 POSIX 功能 (`dirent.2`) 的 MinGW 程序接受路径名作为参数。在这种情况下，我们传递了 `.`，它代表可执行文件的当前目录。返回值是一个指向 `DIR` 类型变量的指针，可以传递另一个名为 `readdir()` 的 POSIX 函数以遍历目录内容。在 Linux 或 Mac OS X 的终端窗口中输入 `opendir` 以获取这些函数的更多信息。

要进行编译，只需打开 MS-DOS 命令窗口并输入：

```cmd
c:> g++ -o mingtest mingtest.cpp
```

如果一切顺利（理应该是这样的），输入以下：

```cmd
c:\ .\mingwtest

Directory opened successfully!

c:\
```

如果你无法编译或执行示例程序，请确保已按照之前的说明设置了路径变量。

## 验证 MinGW 使用的库

MinGW 许可协议规定，使用 MinGW 创建的应用程序可以无限制地发布，无论是商业用途还是其他。这是因为 MinGW 运行时库属于公共领域。在包含 Cygwin 和 MinGW 的系统中，重要的是验证你的二进制文件没有链接到 `Cygwin.dll` 库（在本节描述）。为了验证这一点，可以使用免费提供的工具 `ListDLL` 来检查应用程序加载的动态链接库 (`DLLs`)。Cygwin 随附的一个名为 `dump` 的工具也可以使用。`listdll` 应用程序可以在 `www.microsoft.com` 下载。下载此工具后，启动你的应用程序并从命令行运行 `listdll`，将输出重定向到文件如下：

当 `listdll` 完成后，打开文件（在这种情况下为 `out.txt`）并按名称搜索。这里是执行 `listdll` 执行 `mingwtest` 的输出：

```text
| 名称 (Name) | 大小 (Size) | 路径 (Path) |
|---|---|---|
| mingwtest.exe | 0x0040000 | 2476 | c:\ |
| ntdll.dll | 0x0770000 | 5000 | 0.01.2600 | c:\ |
| kernel32.dll | 0x077e000 | 5300 | 0.01.2600 | c:\ |
| user32.dll | 0x077f000 | a7000 | 0.01.2600 | c:\ |
| msvcrt.dll | 0x07d6000 | e6000 | 0.01.2600 | c:\ |
| shell32.dll | 0x0771000 | d1000 | 0.01.2600 | c:\ |
| advapi32.dll | 0x077c000 | f0000 | 0.01.2600 | c:\ |
| version32.dll | 0x077b000 | 60000 | 0.01.2600 | c:\ |
| gdi32.dll | 0x077d000 | 70000 | 0.01.2600 | c:\ |
| comat32.dll | 0x077a000 | 80000 | 0.01.2600 | c:\ |
| item32.dll | 0x0772000 | 90000 | 0.01.2600 | c:\ |
| ole32.dll | 0x0775000 | 40000 | 0.01.2600 | c:\ |
| olectl32.dll | 0x0774000 | 50000 | 0.01.2600 | c:\ |
| wimg32.dll | 0x0773000 | 60000 | 0.01.2600 | c:\ |
| win32.dll | 0x0776000 | 70000 | 0.01.2600 | c:\ |
| winbase.dll | 0x077e000 | 80000 | 0.01.2600 | c:\ |
| dwhelp.dll | 0x0778000 | 90000 | 0.01.2600 | c:\ |
| uxtheme32.dll | 0x0779000 | a00000 | 0.01.2600 | c:\ |
| crypt32.dll | 0x077a000 | b00000 | 0.01.2600 | c:\ |
| dcrypt32.dll | 0x077b000 | c00000 | 0.01.2600 | c:\ |
| wininet32.dll | 0x077c000 | d00000 | 0.01.2600 | c:\ |
| winmm32.dll | 0x077d000 | e00000 | 0.01.2600 | c:\ |
| dwmapi32.dll | 0x077e000 | f00000 | 0.01.2600 | c:\ |
| apphelp32.dll | 0x077f000 | 100000 | 0.01.2600 | c:\ |
| shlw32.dll | 0x0770000 | 200000 | 0.01.2600 | c:\ |
| expapi32.dll | 0x0771000 | 300000 | 0.01.2600 | c:\ |
| softheap32.dll | 0x0772000 | 400000 | 0.01.2600 | c:\ |
| unisrv32.dll | 0x0773000 | 500000 | 0.01.2600 | c:\ |
| imm332.dll | 0x0774000 | 600000 | 0.01.2600 | c:\ |
| dbhelp32.dll | 0x0775000 | 700000 | 0.01.2600 | c:\ |
| msimg32.dll | 0x0776000 | 800000 | 0.01.2600 | c:\ |
| setupapi32.dll | 0x0777000 | 900000 | 0.01.2600 | c:\ |
```

# Cygwin

Cygwin 是一个由红帽（Red Hat）托管的项目，旨在促进开源应用程序向 Windows 平台的移植性。它的目标比 MinGW 要野心得多。它对世界的主要贡献除了提供了一套相当完整的 Linux/GNU 工具（根据我在 Windows 系统上安装的发行版中找到的可执行文件的正式统计，多于 450 个，而在我的 Mac OS 系统上可能有 650 个）之外，还有一个名为 `Cygwin.dll` 的库，它作为一个仿真层，为应用程序提供 Linux/POSIX API。对于非商业性使用，使用 `Cygwin.dll` 是免费的。然而，商业软件的开发者必须向红帽公司支付许可费用，才能将 Cygwin DLL 链接到其应用程序并随其软件一起分发。关于下载和安装 Cygwin 以及链接到 Cygwin DLL 的详细说明可以在 `www.cygwin.com/` 处找到。不过，以下说明足够让你开始使用并运行 Cygwin。

## 下载和安装 Cygwin

要下载并安装 Cygwin，请按照以下步骤操作：

- 1. 将网络浏览器指向 `www.cygwin.com`。
- 2. 在主页上，有多个“立即安装 Cygwin”图标。点击其中一个来下载 Cygwin 安装程序 `setup.exe`。
- 3. 下载完成后，双击 `setup.exe` 程序。
- 4. 按照 `setup.exe` 提供的指令和提示在你的系统上安装 Cygwin。在提示时，选择 UNIX 作为默认文本文件，并选择 `c:\cygwin` 为安装目录。
- 5. 将以下条目添加到你的路径（`path`）环境变量中：

```
c:\cygwin\bin;c:\cygwin\usr;c:\cygwin\lib
```

如果你已经在你的系统上安装了 MinGW，我建议执行以下操作。

- 1. 从路径变量中删除任何和所有的 MinGW 组件。
- 2. 创建一个名为 `minenv.bat` 的批处理文件（`.bat` 扩展），其中包含以下内容：

```
set PATH=c:\mingw\bin;c:\mingw\lib;%PATH%;
```

## 第 16 项：使用基于标准的 API（例如 POSIX）

在使用 MinGW 运行时，你可以从命令行窗口执行此批处理文件，以确保你的构建使用随 MinGW 分发的 GCC 工具链，并且你的应用程序链接到 MinGW 运行时。

## 测试 Cygwin

我们可以用测试 MinGW 的相同方式测试 Cygwin。使用你喜欢的文本编辑器在名为 `Cygwin.cpp` 的文件中输入以下内容（或者如果你手头有，可以从上面的 `mingwet.cpp` 复制一份）：

```cpp
#include <iostream>
```
