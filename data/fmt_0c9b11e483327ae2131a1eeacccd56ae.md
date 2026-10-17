
要开始构建，选择“构建 -> 库”（`Build -> Library`），或点击工具栏上的“构建库”图标。在过程中，配置工具会在状态栏上显示“正在构建”（`Building`）消息。输出窗口随着构建进行显示消息。构建完成后，输出窗口显示“完成”（`finished`）。

如果发生构建错误，构建过程将停止并在输出窗口中显示特定的错误消息。修正错误后，选择“构建 -> 库”将继续构建过程。

我们下一个应用程序所需的文件位于 `ecos_install` 目录。构建应用程序时所需的头文件位于此处。eCos 库文件和链接器脚本位于 `ecos_build` 目录下。

我们现在准备好构建应用程序了。

> **注意** 如果在构建后需要对配置进行修改，可以使用配置工具删除文件。这是通过选择“构建 -> 清理”（`Build -> Clean`）实现的。为了安全，最好删除构建和安装树。在示例中，这些目录是 `ecos_install` 和 `ecos_build`。保存配置会导致配置工具重新生成目录。

## 12.5 应用程序

我们现在处于可以构建应用程序并整合之前阶段构建的 eCos 库阶段。一旦有了应用程序镜像，可以使用 RedBoot 将加载到 RAM 中运行。在本节中，我们还将介绍使用 GDB 调试应用程序。

应用程序构建的主要目标是生成二进制文件，其中包含了 eCos 库。应用程序构建过程的流程图如图12.8 所示。

![](img/185e30b232edb8183f2482fa0071447a_317.png)

如图 12.8 所示，我们从 C 语言文件 `basic1.c` 开始。在本示例中，我们使用 Makefile 和 GNU make 进行构建。首先，调用 GNU 交叉编译器——在我们的例子中是 `i386-elf-gcc`。

接下来，运行 GNU 链接器 `i386-elf-ld`，它链接我们的应用程序对象文件和 eCos 库 `libtarget.a`。其他必要的 eCos 库在此期间也被链接。在 eCos 构建过程中生成的链接文件 `target.ld` 在链接过程中使用。

输出是一个 ELF 可执行文件 `basic1.exe`。我们使用 GNU 二进制工具之一的 `i386-elf-objcopy` 将 ELF 格式文件翻译为 S-record 文件。RedBoot 用于下载 S-record 文件中的应用程序镜像。

### 12.5.1 构建应用程序

此示例应用程序的源代码位于 CD-ROM 的 `examples\application` 子目录下，其中包含了源代码文件 `basic1.c` 和构建 Makefile。`examples\application\bin` 目录下还包含了用于基础应用程序构建的 ELF (`basic1.exe`)、S-record (`basic1.srec`) 和 map 文件。

让我们来看看此示例中使用的应用程序。该程序中有两个线程，A 和 B 在运行。线程 A 使用信号量通知线程 B。两个线程在运行时都会传递并打印一个值。

## 第 1 步

我们需要为应用程序代码创建一个目录。在我们的 `workdir` 目录下，我们创建一个 `application` 子目录。现在，我们从光盘的 `examples\application` 子目录拷贝应用程序源文件。我们复制的文件是 `basic.c` 和 `makefile`。

## 第 2 步

如果 Cygwin Bash Shell 尚未打开，可以通过双击 Cygwin 桌面图标，或在“开始 -> 程序 -> Cygnus Solutions -> Cygnus Solutions”下选择 Cygwin Bash Shell 来打开。

在 bash shell 中，使用以下命令切换到工作目录：

```bash
$ cd d:/workdir/application
```

## 第 3 步

接下来，我们可以构建应用程序。在构建镜像之前，让我们花一点时间理解我们用于构建应用程序的 `makefile`。构建此应用程序的 `makefile`（部分内容见代码列表 12.3）是基于 eCOS 源代码仓库中 `examples` 子目录下的 eCOS 源代码示例所包含的 `makefile`。关于 `make` 工具和 `makefile` 的更多信息可以在网上找到：

`www.gnu.org/manual`

也可以在命令行传递命令和选项来构建应用程序镜像；然而，`makefile` 避免了我们重复输入命令。在构建多个文件大型项目中，`makefile` 也非常有用。

```makefile
## eCOS 安装目录
PKG_INSTALL_DIR = /cygdrive/d/workdir/ecos/ecos_install

## 这将编译器设置为 i386 PC。
XCC = i386-elf-gcc

## 构建标志。
CFLAGS = -g -Wall -I$(PKG_INSTALL_DIR)/include \
    -function-sections -fdata-sections
LDFLAGS = -nostartfiles -L$(PKG_INSTALL_DIR)/lib \
    -Wl,-gc-sections -Wl,-Map,basic.map
LIBS = -T.ld -nostdlib
LD = $(XCC)

## 构建规则。
```

### 301

```makefile
16  all: basicl
17
18  basicl.o: basicl.c
19      $(CC) -c $*.o $(CFLAGS)
20
21  basicl: basicl.o
22      $(LD) $(LDFLAGS) -o $@ $@ $(LIBS)
```

### 代码列表 12.3 makefile 示例

在代码 12.3 中，`makefile` 的第一部分设置了一些我们之后可以使用的变量，这样 `makefile` 更易于理解，并允许重复使用变量，而无需重新输入整个字符串。当我们想要使用变量时，我们使用语法 `$(VARIABLE_NAME)`。无论 `VARIABLE_NAME` 声明了什么，它都会在变量的地方被替换。

在第 2 行，我们将变量 `PKG_INSTALL_DIR` 设置为我们在示例上一个阶段构建的 ecos 库的位置。在第 5 行，我们将变量 `XCC` 设置为我们正在使用的编译器；在这种情况下，它是 i386 ELF 编译器 (`i386-elf-gcc`)。

接下来，我们将标志设置为不同的变量。使用变量代替长字符串是为了提高清晰度，并在 `makefile` 的多个位置使用。

第一个变量是 `CFLAGS`，如第 8 行和第 9 行所示，包含了我们传递给 GCC 编译器的标志。下一个变量是 `LDFLAGS`，如第 10 行和第 11 行所示，包含了链接器 `LD` 的选项。`CFLAGS` 和 `LDFLAGS` 变量在实际的 `makefile` 中位于同一行；但在这里它们被分开了，以便显示所有选项。

第 12 行的变量 `LIBS` 包含了也传递给链接器的库。最后，在第 13 行定义了 `LD` 用于链接器命令。在这种情况下，链接器被构建在编译器可执行文件 `i386-elf-gcc` 中，因此我们使用 `XCC` 变量来调用链接器。

`makefile` 的下部分包含规则或目标。目标（targets）是 `makefile` 更新的内容。首先是第 16 行的 `all`。这是要构建的目标，即 ELF 文件 `basicl`。

第 18 行和第 19 行包含了构建目标 `basicl.o` 的信息。正如我们在第 19 行看到的，使用变量 `XCC` 调用编译器并传递了随后的标志，包括来自变量 `CFLAGS` 的字符串。

第 21 行和第 22 行包含了构建目标 `basicl` 的信息。`basicl` 目标是 ELF 镜像，使用第 22 行所示的链接器和链接器选项生成。

`makefile` 中包含了编译器链接链接标志的简要描述。关于各种编译器标志的更多信息，可以在 bash 提示符下输入命令：

```bash
$ i386-elf-gcc --help -v
```

`makefile` 还包含一个规则 `clean`，它会移除构建过程中创建的文件（作为对象文件）。这允许我们重新编译所有文件，而不仅仅是自上次构建以来的文件。要清理构建的文件，请在 bash shell 提示符处使用命令 `make clean`。

在继续构建之前，让我们确切查看

- `all: basicl`
- `basicl.o: basicl.c`
- `$(CC) -c $*.o $(CFLAGS)`
- `basicl: basicl.o`
- `$(LD) $(LDFLAGS) -o $@ $(LIBS)`

# 发送文件

![](img/185e30b232edb8183f2482fa0071447a_322_0.png)

图 12.9 HyperTerminal 发送文件对话框。

用于 RedBoot 的 Ymodem 文件发送
